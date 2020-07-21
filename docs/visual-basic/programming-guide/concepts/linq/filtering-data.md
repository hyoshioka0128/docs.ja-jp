---
title: データのフィルター処理
ms.date: 07/20/2015
ms.assetid: 7749519a-7edc-49fe-aef9-6a353864af6c
ms.openlocfilehash: f7a1aa76dc93cc03952e55f5f8fc3f75176a3f9f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84383418"
---
# <a name="filtering-data-visual-basic"></a>データのフィルター処理 (Visual Basic)

フィルター処理とは、特定の条件を満たす要素のみが含まれるように結果セットを限定する操作のことです。 選択とも呼ばれます。

次の図は、文字のシーケンスをフィルター処理した結果を示したものです。 フィルター処理操作の述語では、文字が "A" でなければならないことが指定されています。

![LINQ のフィルター操作を示す図。](./media/filtering-data/linq-filter-operation.png)

次のセクションでは、選択を実行する標準クエリ演算子メソッドの一覧を示します。

## <a name="methods"></a>メソッド

|メソッド名|説明|Visual Basic のクエリ式の構文|説明|
|-----------------|-----------------|------------------------------------------|----------------------|
|OfType|指定した型にキャストできるかどうかにより、値を選択します。|該当なし。|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|
|Where|述語関数に基づいて値を選択します。|`Where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-example"></a>クエリ式の構文例

次の例では、`Where` を使って、配列から特定の長さを持つ文字列をフィルター処理します。

```vb
Dim words() As String = {"the", "quick", "brown", "fox", "jumps"}

Dim query = From word In words
            Where word.Length = 3
            Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In query
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' fox
```

## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [WHERE 句](../../../language-reference/queries/where-clause.md)
- [方法: クエリ結果をフィルター処理する](../../language-features/linq/how-to-filter-query-results-by-using-linq.md)
- [方法: リフレクションを使用してアセンブリのメタデータにクエリを実行する (LINQ) (Visual Basic)](how-to-query-an-assembly-s-metadata-with-reflection-linq.md)
- [方法: 指定された属性または名前のファイルを照会する (Visual Basic)](how-to-query-for-files-with-a-specified-attribute-or-name.md)
- [方法: 任意の単語またはフィールドを基準にテキスト データの並べ替えまたはフィルター処理を実行する (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
