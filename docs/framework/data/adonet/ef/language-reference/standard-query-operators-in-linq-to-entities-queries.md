---
title: LINQ to Entities クエリの標準クエリ演算子
ms.date: 08/21/2018
ms.assetid: 7fa55a9b-6219-473d-b1e5-2884a32dcdff
ms.openlocfilehash: 76d32db5c81d88db28194da19e722b1a80c1a870
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249141"
---
# <a name="standard-query-operators-in-linq-to-entities-queries"></a>LINQ to Entities クエリの標準クエリ演算子
クエリでは、データ ソースから取得する情報を指定できます。 また、並べ替え、グループ化、整形方法を指定して情報を取得することもできます。 LINQ には、クエリで使用できる一連の標準クエリ メソッドが用意されています。 これらのメソッドの大部分はシーケンスに対して機能します。この文脈でのシーケンスとは、<xref:System.Collections.Generic.IEnumerable%601> インターフェイスまたは <xref:System.Linq.IQueryable%601> インターフェイスを実装している型のオブジェクトのことです。 標準クエリ演算子のクエリ機能には、フィルター処理、投影、集計、並べ替え、グループ化、ページングなどがあります。 よく使用される標準クエリ演算子の中には、クエリ式構文を使用することで呼び出しが可能になるように、専用のキーワード構文のあるものもあります。 クエリ式はメソッド ベースの方法とは異なり、読み取りやすくクエリを表現できます。 クエリ式の句は、コンパイル時にクエリ メソッドへの呼び出しに変換されます。 同等なクエリ式の句がある標準クエリ演算子の一覧については、「[標準クエリ演算子の概要](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397896(v=vs.120))」を参照してください。  
  
 標準クエリ演算子のすべてが LINQ to Entities クエリでサポートされるわけではありません。 詳細については、「[サポート対象の LINQ メソッドとサポート非対象の LINQ メソッド (LINQ to Entities)](supported-and-unsupported-linq-methods-linq-to-entities.md)」を参照してください。 このトピックでは、LINQ to Entities に固有の標準クエリ演算子について説明します。 LINQ to Entities クエリの既知の問題の詳細については、「[LINQ to Entities の既知の問題および注意点](known-issues-and-considerations-in-linq-to-entities.md)」を参照してください。  
  
## <a name="projection-and-filtering-methods"></a>投影およびフィルター処理メソッド  
 "*投影*" とは、結果セットの要素を目的の形式に変換することです。 たとえば、結果セットの各オブジェクトから必要なプロパティのサブセットを投影したり、特定のプロパティを投影してそのプロパティで数学演算を実行したり、結果セットの全オブジェクトを投影したりすることが可能です。 投影メソッドは、`Select` と `SelectMany` です。  
  
 "*フィルター処理*" とは、特定の条件に一致する要素のみが含まれるように結果セットを限定する操作のことです。 フィルター処理メソッドは、`Where` です。  
  
 投影およびフィルター処理メソッドのオーバーロードの大部分は、位置引数を受け入れるオーバーロードを例外として、LINQ to Entities でサポートされます。  
  
## <a name="join-methods"></a>結合メソッド  
 結合は、互いにナビゲート可能なリレーションシップを持たないデータ ソースをターゲットとするクエリにおいて重要な操作です。 2 つのデータ ソースを結合する操作とは、あるデータ ソース内のオブジェクトを、他方のデータ ソース内で共通の属性またはプロパティを持つオブジェクトと関連付けることです。 結合メソッドは、`Join` と `GroupJoin` です。  
  
 <xref:System.Collections.Generic.IEqualityComparer%601> を使用するオーバーロードを例外として、結合メソッドの大部分のオーバーロードがサポートされます。 これは、Comparer をデータ ソースに変換できないためです。  
  
## <a name="set-methods"></a>メソッドの設定  
 LINQ のセット操作は、同一または別のコレクション (またはセット) 内に同等の要素があるかどうかによって結果セットが変化するクエリ操作です。 セット メソッドは、`All`、`Any`、`Concat`、`Contains`、`DefaultIfEmpty`、`Distinct`、`EqualAll`、`Except`、`Intersect`、および `Union` です。  
  
 LINQ to Objects と比較すれば動作に多少の違いがありますが、セット メソッドの大部分のオーバーロードは LINQ to Entities でサポートされます。 ただし、<xref:System.Collections.Generic.IEqualityComparer%601> を使用するセット メソッドは、Comparer をデータ ソースに変換することができないためサポートされません。  
  
## <a name="ordering-methods"></a>並べ替えメソッド  
 並べ替えとは、1 つまたは複数の属性に基づいて結果セットの要素を並べ替えることです。 複数の基準を指定すると、グループ内での結び付きが壊れることがあります。  
  
 <xref:System.Collections.Generic.IComparer%601> を使用するオーバーロードを例外として、並べ替えメソッドの大部分のオーバーロードがサポートされます。 これは、Comparer をデータ ソースに変換できないためです。 並べ替えメソッドは、`OrderBy`、`OrderByDescending`、`ThenBy`、`ThenByDescending`、および `Reverse` です。  
  
 クエリはデータ ソースで実行されるため、並べ替えの動作が CLR で実行されるクエリとは異なる場合があります。 これは、大文字と小文字の並べ替え、漢字の並べ替え、null の並べ替えなど、並べ替えのオプションをデータ ソースで設定できることが原因です。 データ ソースによっては、これらの並べ替えオプションを使用すると、CLR の結果とは異なる結果が返される場合があります。  
  
 複数の並べ替え操作で同一のキー セレクターを指定すると、並べ替えが重複します。 これは無効であり、例外がスローされます。  
  
## <a name="grouping-methods"></a>グループ化メソッド  
 グループ化とは、各グループの要素が共通の属性を持てるようにデータをグループに配置することです。 グループ化メソッドは `GroupBy` です。  
  
 <xref:System.Collections.Generic.IEqualityComparer%601> を使用するオーバーロードを例外として、グループ化メソッドの大部分のオーバーロードがサポートされます。 これは、Comparer をデータ ソースに変換できないためです。  
  
 グループ化メソッドは、キー セレクターの個別のサブクエリを使用してデータ ソースにマップされます。 キー セレクターの比較サブクエリは、`null` 値の比較に関する問題など、データ ソースのセマンティクスを使用することによって実行されます。  
  
## <a name="aggregate-methods"></a>集計メソッド  
 集計の操作では、値の集合体から単一の値が計算されます。 たとえば、1 か月分の毎日の気温値から 1 日あたりの平均の気温値を計算することが集計操作です。 集計メソッドは、`Aggregate`、`Average`、`Count`、`LongCount`、`Max`、`Min`、および `Sum` です。  
  
 集計メソッドの大部分のオーバーロードはサポートされています。 null 値に関連する動作では、集計メソッドでデータ ソース セマンティクスが使用されます。 null 値が関係する集計メソッドの動作は、使用するバックエンド データ ソースに応じて異なる可能性があります。 データ ソースのセマンティクスを使用する集計メソッドの動作でも、CLR のメソッドから見込まれる動作とは異なる場合があります。 たとえば、SQL Server での `Sum` メソッドの既定動作では、例外がスローされずに null 値が無視されます。  
  
 `Sum` 関数のオーバーフローなど、集計によって生じるあらゆる例外は、クエリ結果の具体化の最中にデータ ソースの例外または Entity Framework の例外としてスローされます。  
  
 `Sum`、`Average` など、シーケンス全体の計算にかかわるメソッドの場合、実際の計算はサーバーで行われます。 結果として、サーバー上での型変換や有効桁の消失が発生する場合があり、CLR セマンティクスを使用した際に見込まれる結果とは異なる結果が返される可能性があります。  
  
 次の表に、null および非 null 値に対する集計メソッドの既定の動作を示します。  
  
|メソッド|データなし|すべての null 値|いくつかの null 値|null 値なし|  
|------------|-------------|---------------------|----------------------|--------------------|  
|`Average`|null を返します。|null を返します。|シーケンス内の null 値以外の値の平均を返します。|数値のシーケンスの平均を計算します。|  
|`Count`|0 を返します。|シーケンス内の null 値の数を返します。|シーケンス内の null 値と非 null 値の数を返します。|シーケンス内の要素の数を返します。|  
|`Max`|null を返します。|null を返します。|シーケンス内の null 以外の値の最大値を返します。|シーケンス内の最大値を返します。|  
|`Min`|null を返します。|null を返します。|シーケンス内の null 以外の値の最小値を返します。|シーケンス内の最小値を返します。|  
|`Sum`|null を返します。|null を返します。|シーケンス内の null 以外の値の合計を返します。|数値のシーケンスの合計を計算します。|  
  
## <a name="type-methods"></a>型メソッド  
 Entity Framework のコンテキストでは、型変換と判定を処理する 2 つの LINQ メソッドがサポートされます。 つまり、サポートされる型は、適切な Entity Framework 型にマップされる型のみです。 これらの型の一覧については、「[概念モデルの型 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)」を参照してください。 型メソッドは、`Convert` と `OfType` です。  
  
 エンティティ型では、`OfType` がサポートされます。 概念モデル プリミティブ型では、`Convert` がサポートされます。  C# の `is` および `as` メソッドもサポートされます。  
  
## <a name="paging-methods"></a>ページング メソッド  
 ページング操作では、シーケンスから単一の要素または複数の要素が返されます。 サポートされているページング メソッドは、`First`、`FirstOrDefault`、`Single`、`SingleOrDefault`、`Skip`、および `Take` です。  
  
 多くのページング メソッドはサポートされていません。これは、関数をデータ ソースにマップできないことと、データ ソースでのセットの明示的な順序付けが不足していることのいずれかが理由です。 既定値を返すメソッドは、null 既定値を持つ概念モデル プリミティブ型および参照型に限定されます。 空シーケンスで実行されるページング メソッドは null を返します。  
  
## <a name="see-also"></a>関連項目

- [サポート対象の LINQ メソッドとサポート非対象の LINQ メソッド (LINQ to Entities) ](supported-and-unsupported-linq-methods-linq-to-entities.md)
- [標準クエリ演算子の概要](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397896(v=vs.120))
