---
title: データ型の変換
ms.date: 07/20/2015
ms.assetid: 9b0cf1ab-de48-4c6e-9f00-05b40fade46e
ms.openlocfilehash: 1394f53923ba850ae11fbc326a25c279589c3be1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410852"
---
# <a name="converting-data-types-visual-basic"></a>データ型の変換 (Visual Basic)

変換メソッドは、入力オブジェクトの型を変更します。

 LINQ クエリの変換操作は、さまざまなアプリケーションで役に立ちます。 次はその例の一部です。

- <xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=nameWithType> メソッドを使用すると、標準クエリ演算子の型のカスタム実装を非表示することができます。

- <xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType> メソッドを使用すると、LINQ クエリのパラメーター化されていないコレクションを有効にすることができます。

- <xref:System.Linq.Enumerable.ToArray%2A?displayProperty=nameWithType>、<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=nameWithType>、<xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType>、および <xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType> メソッドを使用すると、クエリが列挙されるまで延期させるのではなく、即時のクエリ実行を強制することができます。

## <a name="methods"></a>メソッド

次の表には、データ型の変換を実行する標準クエリ演算子メソッドの一覧が示されています。

名前が "As" で始まるこの表の変換メソッドは、ソース コレクションの静的型を変更しますが、ソース コレクションを列挙しません。 名前が "To" で始まるメソッドは、ソース コレクションを列挙し、各項目を対応するコレクション型に変換します。

|メソッド名|説明|Visual Basic のクエリ式の構文|説明|
|-----------------|-----------------|------------------------------------------|----------------------|
|AsEnumerable|<xref:System.Collections.Generic.IEnumerable%601> として型指定された入力を返します。|該当なし。|<xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=nameWithType>|
|AsQueryable|(ジェネリック) <xref:System.Collections.IEnumerable> を (ジェネリック) <xref:System.Linq.IQueryable> に変換します。|該当なし。|<xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=nameWithType>|
|Cast|コレクションの要素を指定した型にキャストします。|`From … As …`|<xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Cast%2A?displayProperty=nameWithType>|
|OfType|指定した型にキャストできるかどうかに応じて値をフィルター処理します。|該当なし。|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|
|ToArray|コレクションを配列に変換します。 このメソッドはクエリの実行を強制します。|該当なし。|<xref:System.Linq.Enumerable.ToArray%2A?displayProperty=nameWithType>|
|ToDictionary|キー セレクター関数に基づいて、<xref:System.Collections.Generic.Dictionary%602> に要素を変換します。 このメソッドはクエリの実行を強制します。|該当なし。|<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=nameWithType>|
|ToList|コレクションを <xref:System.Collections.Generic.List%601> に変換します。 このメソッドはクエリの実行を強制します。|該当なし。|<xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType>|
|ToLookup|キー セレクター関数に基づいて、<xref:System.Linq.Lookup%602> (一対多の辞書) に要素を変換します。 このメソッドはクエリの実行を強制します。|該当なし。|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-example"></a>クエリ式の構文例

次のコード例では、サブタイプでのみ使用できるメンバーにアクセスする前に、`From As` 句を使用して、型をそのサブタイプにキャストしています。

```vb
Class Plant
    Public Property Name As String
End Class

Class CarnivorousPlant
    Inherits Plant
    Public Property TrapType As String
End Class

Sub Cast()

    Dim plants() As Plant = {
        New CarnivorousPlant With {.Name = "Venus Fly Trap", .TrapType = "Snap Trap"},
        New CarnivorousPlant With {.Name = "Pitcher Plant", .TrapType = "Pitfall Trap"},
        New CarnivorousPlant With {.Name = "Sundew", .TrapType = "Flypaper Trap"},
        New CarnivorousPlant With {.Name = "Waterwheel Plant", .TrapType = "Snap Trap"}}

    Dim query = From plant As CarnivorousPlant In plants
                Where plant.TrapType = "Snap Trap"
                Select plant

    Dim sb As New System.Text.StringBuilder()
    For Each plant In query
        sb.AppendLine(plant.Name)
    Next

    ' Display the results.
    MsgBox(sb.ToString())

    ' This code produces the following output:

    ' Venus Fly Trap
    ' Waterwheel Plant

End Sub
```

## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [From 句](../../../language-reference/queries/from-clause.md)
- [方法: LINQ を使用して ArrayList を照会する (Visual Basic)](how-to-query-an-arraylist-with-linq.md)
