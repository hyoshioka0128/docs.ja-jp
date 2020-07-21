---
title: Entity SQL と Transact-SQL の相違点
ms.date: 03/30/2017
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
ms.openlocfilehash: 96e2283074b6c69e51bb7fee4d4f257cdb58d615
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615632"
---
# <a name="how-entity-sql-differs-from-transact-sql"></a>Entity SQL と Transact-SQL の相違点

この記事では、Entity SQL と Transact-SQL の相違点について説明します。  
  
## <a name="inheritance-and-relationships-support"></a>継承とリレーションシップのサポート  
 Entity SQL では、エンティティの概念スキーマが直接操作され、継承やリレーションシップなどの概念モデル機能がサポートされます。  
  
 継承を操作するときは、スーパータイプ インスタンスのコレクションからサブタイプのインスタンスを選択すると便利である場合がよくあります。 Entity SQL 内の [oftype](oftype-entity-sql.md) 演算子 (C# シーケンスの `oftype` に相当) によってこの機能が提供されます。  
  
## <a name="support-for-collections"></a>コレクションのサポート  
 Entity SQL では、コレクションがファーストクラスのエンティティとして扱われます。 次に例を示します。  
  
- コレクションの式は、`from` 句内で有効です。  
  
- `in` サブクエリと `exists` サブクエリは任意のコレクションを使用できるように一般化されています。  
  
     サブクエリは一種のコレクションです。 `e1 in e2` および `exists(e)` は、これらの演算を実行する Entity SQL 構造です。  
  
- `union`、`intersect`、`except` などの集合演算は、現在ではコレクションに対して実行されます。  
  
- 結合はコレクションに対して実行されます。  
  
## <a name="support-for-expressions"></a>式のサポート  
 Transact-SQL にはサブクエリ (テーブル) と式 (行と列) があります。  
  
 コレクションおよび入れ子になったコレクションをサポートするために、Entity SQL ではすべてが式として扱われます。 Entity SQL は Transact-SQL よりコンポーザブルであり、すべての式をどこにでも使用できます。 クエリ式は常に投射型のコレクションとなり、コレクション式が許可されている任意の場所で使用できます。 Entity SQL でサポートされていない Transact-SQL の式について詳しくは、「[サポートされていない式](unsupported-expressions-entity-sql.md)」をご覧ください。  
  
 次の Entity SQL クエリはすべて有効です。  
  
```sql  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}
e1 union all e2  
set(e1)  
```  
  
## <a name="uniform-treatment-of-subqueries"></a>サブクエリの一貫した処理  
 Transact-SQL では、テーブルに重点を置いてサブクエリのコンテキストが解釈されます。 たとえば、`from` 句内のサブクエリは、マルチセット (テーブル) と見なされます。 ただし、`select` 句で使用される同じサブクエリは、スカラー サブクエリと見なされます。 同様に、`in` 演算子の左側で使用されるサブクエリはスカラー サブクエリと見なされますが、右側で使用されるサブクエリはマルチセット サブクエリと見なされます。  
  
 Entity SQL ではこれらの違いが排除されます。 式は、使用するコンテキストに依存しない、一貫した方法で解釈されます。 Entity SQL では、すべてのサブクエリがマルチセット サブクエリと見なされます。 サブクエリでスカラー値が必要な場合のために、Entity SQL には `anyelement` 演算子が用意されています。この演算子はコレクション (この場合はサブクエリ) に対して演算を行い、コレクションからシングルトン値を抽出します。  
  
### <a name="avoiding-implicit-coercions-for-subqueries"></a>サブクエリの暗黙の強制型変換の回避  
 サブクエリの一貫した処理に伴う二次的作用として、スカラー値へのサブクエリの暗黙的な変換があります。 具体的には、Transact-SQL では、単一フィールドの行のマルチセットはそのフィールドのデータ型を持つスカラー値に暗黙的に変換されます。  
  
 Entity SQL では、この暗黙の強制型変換をサポートしていません。 Entity SQL では、コレクションからシングルトン値を抽出するための `ANYELEMENT` 演算子と、クエリ式の実行中に row ラッパーの作成を回避するための `select value` 句が提供されています。  
  
## <a name="select-value-avoiding-the-implicit-row-wrapper"></a>SELECT VALUE: 暗黙の row ラッパーの回避  
 Transact-SQL サブクエリ内の SELECT 句では、句内の項目に row ラッパーが暗黙的に作成されます。 これは、スカラーやオブジェクトのコレクションを作成できないことを意味します。 Transact-SQL では、1 つのフィールドの `rowtype` と、同じデータ型のシングルトン値との間の暗黙の強制型変換が許可されています。  
  
 Entity SQL には、暗黙の行の構築をスキップする `select value` 句が用意されています。 `select value` 句には 1 つの項目のみを指定できます。 このような句を使用した場合、`select` 句内の項目には row ラッパーは構築されず、目的の構造を持つコレクションを作成できます (例: `select value a`)。  
  
 Entity SQL には、任意の行を構築するための行コンストラクターも用意されています。 `select` は、プロジェクションの 1 つ以上の要素を受け取り、フィールドを持つデータ レコードを生成します。  
  
 `select a, b, c`  
  
## <a name="left-correlation-and-aliasing"></a>左の相関関係と別名定義  
 Transact-SQL では、1 つのスコープ内の式 (`select` や `from` のような単一句) は同じスコープ内で先に定義された式を参照できません。 一部の SQL 言語仕様 (Transact-SQL を含む) では、`from` 句でこれらが制限付きでサポートされています。  
  
 Entity SQL では `from` 句における左の相関関係が一般化され、一貫した方法でこれらが扱われます。 `from` 句内の式は、追加の構文を使用せずに、同じ句内で先に作成された定義 (左側の定義) を参照できます。  
  
 Entity SQL では、`group by` 句を伴うクエリにも追加の制限が課されます。 このようなクエリの `select` 句および `having` 句内の式では、別名を使用した場合にのみ `group by` キーを参照できます。 次の構造は Transact-SQL では有効ですが、Entity SQL では無効です。  
  
```sql  
SELECT t.x + t.y FROM T AS t group BY t.x + t.y
```  
  
 Entity SQL でこれを行うには、次のようにします。  
  
```sql  
SELET k FROM T AS t GROUP BY (t.x + t.y) AS k
```  
  
## <a name="referencing-columns-properties-of-tables-collections"></a>テーブル (コレクション) の列 (プロパティ) の参照  
 Entity SQL 内の列の参照は、すべてテーブルの別名を使用して修飾する必要があります。 次のコンストラクトは Transact-SQL では有効ですが、Entity SQL では無効です (`a` がテーブル `T` の有効な列である場合)。  
  
```sql  
SELECT a FROM T
```  
  
 Entity SQL の形式は次のようになります  
  
```sql  
SELECT t.a AS A FROM T AS t
```  
  
 テーブルの別名は `from` 句では省略できます。 テーブル名は暗黙的な別名として使用されます。 Entity SQL では次の形式も使用できます。  
  
```sql  
SELET Tab.a FROM Tab
```  
  
## <a name="navigation-through-objects"></a>オブジェクト間の移動  
 Transact-SQL では、テーブルの列または行の参照に "." 表記が使用されます。 Entity SQL では (プログラミング言語に由来する) この表記が拡張され、オブジェクトのプロパティ間の移動がサポートされています。  
  
 たとえば、`p` が Person 型の式である場合、この人の住所の市区町村を参照するには次の Entity SQL 構文が使用されます。  
  
```sql  
p.Address.City
```  
  
## <a name="no-support-for-"></a>\* のサポートなし  
 Transact-SQL では、修飾されていない \* 構文は行全体の別名としてサポートされており、修飾された \* 構文 (t.\*) はそのテーブルのフィールドのショートカットとしてサポートされています。 また、Transact-SQL では NULL を含む特殊な count(\*) 集計も使用できます。  
  
 Entity SQL では、* 構造がサポートされていません。 `select * from T` および `select T1.* from T1, T2...` の形式の Transact-SQL クエリは、Entity SQL ではそれぞれ `select value t from T as t` および `select value t1 from T1 as t1, T2 as t2...` として表すことができます。 また、これらの構造は継承 (値の置換可能性) に対応していますが、`select *` Variant 型では宣言された型の最上位レベルのプロパティに限定されています。  
  
 Entity SQL では、`count(*)` 集約がサポートされていません。 代わりに、`count(0)` を使用してください。  
  
## <a name="changes-to-group-by"></a>Group By への変更  
 Entity SQL では `group by` キーの別名定義がサポートされています。 `select` 句および `having` 句内の式では、これらの別名を使用して `group by` キーを参照する必要があります。 たとえば、次の Entity SQL 構文です。  
  
```sql  
SELECT k1, count(t.a), sum(t.a)
FROM T AS t
GROUP BY t.b + t.c AS k1
```  
  
 これは、次の Transact-SQL と同じです。  
  
```sql  
SELECT b + c, count(*), sum(a)
FROM T
GROUP BY b + c
```  
  
## <a name="collection-based-aggregates"></a>コレクションベースの集計  
 Entity SQL では、2 種類の集約がサポートされています。  
  
 コレクションベースの集計は、コレクションに対して演算を行い、集計結果を生成します。 これらはクエリ内の任意の場所で使用でき、`group by` 句を必要としません。 次に例を示します。  
  
```sql  
SELECT t.a AS a, count({1,2,3}) AS b FROM T AS t
```  
  
 Entity SQL では、SQL スタイルの集約もサポートされています。 次に例を示します。  
  
```sql  
SELECT a, sum(t.b) FROM T AS t GROUP BY t.a AS a
```  
  
## <a name="order-by-clause-usage"></a>ORDER BY 句の使用法  
Transact-SQL では、`ORDER BY` 句は最上位の `SELECT .. FROM .. WHERE` ブロック内でのみ指定できます。 Entity SQL では、入れ子になった `ORDER BY` 式を使用でき、それをクエリ内の任意の場所に配置できますが、入れ子になったクエリ内の順序は保持されません。  
  
```sql  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact AS C1
        ORDER BY C1.LastName  
```  
  
```sql  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="identifiers"></a>識別子  
 Transact-SQL では、識別子の比較は現在のデータベースの照合順序に基づきます。 Entity SQL の識別子では、常に大文字と小文字は区別されず、アクセントは区別されます (つまり、Entity SQL ではアクセントのある文字とアクセントのない文字が区別されます。たとえば、'a' と 'ấ' は等しくありません)。 Entity SQL では、外観が同じでも別のコード ページに由来している複数の文字のバージョンが別々の文字として扱われます。 詳しくは、「[入力文字セット](input-character-set-entity-sql.md)」をご覧ください。  
  
## <a name="transact-sql-functionality-not-available-in-entity-sql"></a>Entity SQL では使用できない Transact-SQL 機能  
 Transact-SQL の次の機能は、Entity SQL では使用できません。  
  
 DML  
 Entity SQL では現在、DML ステートメント (insert、update、delete) はサポートされていません。  
  
 DDL  
 Entity SQL の現在のバージョンでは DDL はサポートされていません。  
  
 命令型プログラミング  
 Transact-SQL とは異なり、Entity SQL では、命令型プログラミングはサポートされていません。 代わりにプログラミング言語を使用します。  
  
 グループ化関数  
 Entity SQL では、グループ化関数 (CUBE、ROLLUP、GROUPING_SET など) はまだサポートされていません。  
  
 分析関数  
 Entity SQL では、分析関数は (まだ) サポートされていません。  
  
 組み込み関数、演算子  
 Entity SQL では、Transact-SQL の組み込み関数と演算子のサブセットがサポートされています。 これらの演算子と関数の多くは、主要なストア プロバイダーによりサポートされています。 Entity SQL では、プロバイダー マニフェストで宣言されたストア固有の関数が使用されます。 また、Entity Framework では、Entity SQL で使用される既存の組み込みストア関数とユーザー定義ストア関数を宣言できます。  
  
 ヒント  
 Entity SQL には、クエリ ヒントのメカニズムが用意されていません。  
  
 クエリ結果のバッチ処理  
 Entity SQL では、クエリ結果のバッチ処理がサポートされていません。 たとえば、次の Transact-SQL は有効です (バッチとして送信)。  
  
```sql  
SELECT * FROM products;
SELECT * FROM catagories;
```  
  
 ただし、同等の Entity SQL はサポートされていません。  
  
```sql  
SELECT value p FROM Products AS p;
SELECT value c FROM Categories AS c;
```  
  
 Entity SQL では、コマンドごとに 1 つの結果生成クエリ ステートメントのみがサポートされます。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
- [サポートされていない式](unsupported-expressions-entity-sql.md)
