---
title: データの並べ替え
ms.date: 07/20/2015
ms.assetid: 6f81065c-0c89-4bf3-a6d8-442273f8810e
ms.openlocfilehash: a5ccff745995ed7f41731cf98fb7c49d3247d994
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406795"
---
# <a name="sorting-data-visual-basic"></a>データの並べ替え (Visual Basic)

並べ替え操作では、1 つ以上の属性に基づいてシーケンスの要素を並べ替えます。 並べ替えの第 1 条件で、要素に対して一回目の並べ替えが実行されます。 第 2 条件を指定すると、第 1 条件で並べ替えられた各グループ内の要素を並べ替えることができます。

次の図は、文字のシーケンスに対してアルファベット順の並べ替え操作を実行した結果を示しています。

![アルファベット順の並べ替え操作を示している図。](./media/sorting-data/alphabetical-sort-operation.png)

次のセクションでは、データの並べ替えを実行する標準クエリ演算子のメソッドの一覧を示します。

## <a name="methods"></a>メソッド

|メソッド名|説明|Visual Basic のクエリ式の構文|説明|
|-----------------|-----------------|------------------------------------------|----------------------|
|OrderBy|値を昇順に並べ替えます。|`Order By`|<xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderBy%2A?displayProperty=nameWithType>|
|OrderByDescending|値を降順に並べ替えます。|`Order By … Descending`|<xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderByDescending%2A?displayProperty=nameWithType>|
|ThenBy|2 番目の並べ替えを昇順で実行します。|`Order By …, …`|<xref:System.Linq.Enumerable.ThenBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenBy%2A?displayProperty=nameWithType>|
|ThenByDescending|2 番目の並べ替えを降順で実行します。|`Order By …, … Descending`|<xref:System.Linq.Enumerable.ThenByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenByDescending%2A?displayProperty=nameWithType>|
|Reverse|コレクションの要素の順序を反転させます。|該当なし。|<xref:System.Linq.Enumerable.Reverse%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Reverse%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-examples"></a>クエリ式の構文例

### <a name="primary-sort-examples"></a>1 番目の並べ替えの例

#### <a name="primary-ascending-sort"></a>1 番目の並べ替え (昇順)

次の例は、LINQ クエリで `Order By` 句を使用して、配列内の文字列を文字列長に従って昇順に並べ替える方法を示しています。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' fox
' quick
' brown
' jumps
```

#### <a name="primary-descending-sort"></a>1 番目の並べ替え (降順)

次の例は、LINQ クエリで `Order By Descending` 句を使用して、文字列を最初の文字に従って降順に並べ替える方法を示しています。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Substring(0, 1) Descending
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' quick
' jumps
' fox
' brown
```

### <a name="secondary-sort-examples"></a>2 番目の並べ替えの例

#### <a name="secondary-ascending-sort"></a>2 番目の並べ替え (昇順)

次の例は、LINQ クエリで `Order By` 句を使用して、配列内の文字列に対して 1 番目および 2 番目の並べ替えを実行する方法を示しています。 文字列は、最初に文字列長を基準として、次に文字列の最初の文字を基準として、どちらも昇順に並べ替えられます。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length, word.Substring(0, 1)
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' fox
' the
' brown
' jumps
' quick
```

#### <a name="secondary-descending-sort"></a>2 番目の並べ替え (降順)

次の例は、LINQ クエリで `Order By Descending` 句を使用して、1 番目の並べ替えを昇順で実行し、2 番目の並べ替えを降順で実行する方法を示しています。 各文字列は、最初に文字列長を基準として、次に文字列の最初の文字を基準として並べ替えられます。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length, word.Substring(0, 1) Descending
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' fox
' the
' quick
' jumps
' brown
```

## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [Order By 句](../../../language-reference/queries/order-by-clause.md)
- [方法: クエリ結果を並べ替える](../../language-features/linq/how-to-sort-query-results-by-using-linq.md)
- [方法: 任意の単語またはフィールドを基準にテキスト データの並べ替えまたはフィルター処理を実行する (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
