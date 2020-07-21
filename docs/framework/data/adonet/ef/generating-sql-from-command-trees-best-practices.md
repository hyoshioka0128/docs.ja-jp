---
title: 'コマンド ツリーからの SQL の生成: ベスト プラクティス'
ms.date: 03/30/2017
ms.assetid: 71ef6a24-4c4f-4254-af3a-ffc0d855b0a8
ms.openlocfilehash: 869722b91550855a184a74e706271c3e2d417b84
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039997"
---
# <a name="generating-sql-from-command-trees---best-practices"></a>コマンド ツリーからの SQL の生成: ベスト プラクティス

出力クエリ コマンド ツリーは、SQL で表現できるクエリに厳密に従って作成されます。 ただし、出力コマンド ツリーから SQL を生成する際にプロバイダーの作成者が直面する、一般的な問題がいくつかあります。 このトピックでは、これらの問題について説明します。 これらの問題への対処方法については、次のトピックでサンプル プロバイダーを介して紹介します。

## <a name="group-dbexpression-nodes-in-a-sql-select-statement"></a>SQL SELECT ステートメントでの DbExpression ノードのグループ化

一般的な SQL ステートメントは、次の形状の入れ子の構造を持ちます。

```sql
SELECT …
FROM …
WHERE …
GROUP BY …
ORDER BY …
```

1 つ以上の句が空でもかまいません。  入れ子の SELECT ステートメントは、どの行にも出現する可能性があります。

クエリ コマンド ツリーを SQL SELECT ステートメントに変換すると、すべての関係演算子に対応する 1 つのサブクエリが生成されます。 ただしその結果、入れ子になった不要なサブクエリが生成され、読み取りが困難になります。  一部のデータ ストアでは、クエリは十分なパフォーマンスを発揮しません。

例として、次のクエリ コマンド ツリーについて考えます。

```csharp
Project (
a.x,
   a = Filter(
      b.y = 5,
      b = Scan("TableA")
   )
)
```

非効率な変換を行った場合、次のような SQL が生成されます。

```sql
SELECT a.x
FROM (   SELECT *
         FROM TableA as b
         WHERE b.y = 5) as a
```

すべての関係式ノードが新しい SQL SELECT ステートメントになっていることに注目してください。

そのため、正確性を維持しながら、可能な限り多くの式ノードを 1 つの SQL SELECT ステートメントに集約することが重要になります。

このような集約を上の例に適用した場合、結果は次のようになります。

```sql
SELECT b.x
FROM TableA as b
WHERE b.y = 5
```

## <a name="flatten-joins-in-a-sql-select-statement"></a>SQL SELECT ステートメントでの結合のフラット化

複数のノードを 1 つの SQL SELECT ステートメントに集約する処理の 1 つに、1 つの SQL SELECT ステートメントへの複数の結合式の集約があります。 DbJoinExpression は、2 つの入力の間の 1 つの結合を表します。 ただし、1 つの SQL SELECT ステートメントの一部として、複数の結合を指定できます。 その場合、結合は指定の順序で実行されます。

左辺スパイン結合 (別の結合の左辺の子として表示される結合) は、1 つの SQL SELECT ステートメントに簡単にフラット化できます。 たとえば、次のクエリ コマンド ツリーについて考えます。

```csharp
InnerJoin(
   a = LeftOuterJoin(
   b = Extent("TableA")
   c = Extent("TableB")
   ON b.y = c.x ),
   d = Extent("TableC")
   ON a.b.y = d.z
)
```

これは、次のように適切に変換できます。

```sql
SELECT *
FROM TableA as b
LEFT OUTER JOIN TableB as c ON b.y = c.x
INNER JOIN TableC as d ON b.y = d.z
```

ただし、左辺スパイン結合以外の結合のフラット化は容易ではないので、実行しないでください。 たとえば、次のクエリ コマンド ツリーの結合について考えます。

```csharp
InnerJoin(
   a = Extent("TableA")
   b = LeftOuterJoin(
   c = Extent("TableB")
   d = Extent("TableC")
   ON c.y = d.x),
   ON a.z = b.c.y
)
```

これは、サブクエリを持つ SQL SELECT ステートメントに変換されます。

```sql
SELECT *
FROM TableA as a
INNER JOIN (SELECT *
   FROM TableB as c
   LEFT OUTER JOIN TableC as d
   ON c.y = d.x) as b
ON b.y = d.z
```

## <a name="input-alias-redirecting"></a>入力の別名のリダイレクト

入力の別名のリダイレクトについて理解するために、DbFilterExpression、DbProjectExpression、DbCrossJoinExpression、DbJoinExpression、DbSortExpression、DbGroupByExpression、DbApplyExpression、DbSkipExpression などの関係式の構造について考えてみましょう。

これらの型はそれぞれ、入力コレクションを示す 1 つ以上の入力プロパティを持ちます。各入力に対応するバインディング変数は、コレクションのトラバース時にその入力の各要素を表すために使用されます。 バインディング変数は、DbFilterExpression の Predicate プロパティや DbProjectExpression の Projection プロパティなどにおいて、入力要素を参照するときに使用されます。

多数の関係式ノードを 1 つの SQL SELECT ステートメントに集約し、関係式の一部 (たとえば、DbProjectExpression の Projection プロパティの一部) である式を評価する場合、複数の式のバインディングを 1 つのエクステントにリダイレクトする必要があるため、使用されるバインディング変数が入力の別名と異なる可能性があります。  この問題は、別名の名前変更と呼ばれます。

このトピックの最初の例について考えてみてください。 単純な変換を実行して Projection a.x (DbPropertyExpression(a, x)) を変換する場合、バインディング変数に合わせて入力に "a" という別名を設定しているため、`a.x` に変換するのが適切な処理です。  ただし、両方のノードを 1 つの SQL SELECT ステートメントに集約する場合は、入力に "b" という別名が設定されているため、同じ DbPropertyExpression を `b.x` に変換する必要があります。

## <a name="join-alias-flattening"></a>結合の別名のフラット化

出力コマンド ツリーの他の関係式とは異なり、DbJoinExpression は 2 つの列から成る行として結果の型を出力します。この 2 つの列のそれぞれが、いずれか 1 つの入力に対応しています。 結合から生じたスカラー プロパティにアクセスするために作成された DbPropertyExpression は、別の DbPropertyExpression に基づいています。

例として、例 2 の "a.b.y" と例 3 の "b.c.y" が挙げられます。 ただし、対応する SQL ステートメントでは、これらは "b.y" になります。 この別名の再設定は、結合の別名のフラット化と呼ばれます。

## <a name="column-name-and-extent-alias-renaming"></a>列名およびエクステントの別名の名前変更

結合を持つ SQL SELECT クエリを射影を使用して完成させる必要がある場合、関与するすべての列を入力から列挙する際に、名前の競合が発生することがあります。これは、複数の入力が同じ列名を持っている場合です。 競合を避けるには、列に異なる名前を使用してください。

また、結合のフラット化の際にも、関与するテーブル (またはサブクエリ) の別名が競合することがあります。この場合にも名前の変更が必要です。

## <a name="avoid-select-"></a>SELECT * の回避

ベース テーブルから選択する際には `SELECT *` を使用しないでください。 Entity Framework アプリケーションのストレージ モデルでは、データベース テーブル内の列のサブセットのみを含めることができます。 この場合、`SELECT *` によって正しくない結果が生成される可能性があります。 代わりに、関与する式の結果の型の列名を使用して、関与するすべての列を指定してください。

## <a name="reuse-of-expressions"></a>式の再利用

式は、Entity Framework によって渡されたクエリ コマンド ツリーで再利用できます。 各式は、クエリ コマンド ツリーで 1 回しか使用できないわけではありません。

## <a name="mapping-primitive-types"></a>プリミティブ型のマッピング

概念 (EDM) 型をプロバイダー型にマップする場合は、さまざまな値に対応できるように、最も幅の広い型 (Int32) にマップする必要があります。 また、BLOB 型のような、多様な操作に使用できない型 (SQL Server の `ntext` など) にマップすることは避けてください。

## <a name="see-also"></a>関連項目

- [SQL 生成](sql-generation.md)
