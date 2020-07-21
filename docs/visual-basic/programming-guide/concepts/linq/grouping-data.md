---
title: データのグループ化
ms.date: 07/20/2015
ms.assetid: 8f3a0871-6958-4aef-8f6f-493e189fd57d
ms.openlocfilehash: 8996eee748489c596bc5adc32f53b6b39dbfc6ac
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398384"
---
# <a name="grouping-data-visual-basic"></a>データのグループ化 (Visual Basic)
グループ化とは、各グループの要素が共通の属性を持つようにデータをグループに分ける操作を指します。  
  
 次の図は、文字のシーケンスをグループ化した結果を示しています。 各グループのキーは文字です。  
  
 ![LINQ グループ化操作を示す図。](./media/grouping-data/linq-group-operation.png)  
  
 次のセクションでは、データ要素をグループ化する標準クエリ演算子メソッドの一覧を示します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド名|説明|Visual Basic のクエリ式の構文|説明|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|GroupBy|共通の属性を共有する要素をグループ化します。 各グループは <xref:System.Linq.IGrouping%602> オブジェクトによって表されます。|`Group … By … Into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|キー セレクター関数に基づいて、<xref:System.Linq.Lookup%602> (一対多の辞書) に要素を挿入します。|該当なし。|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>クエリ式の構文例  
 次のコード例では、`Group By` 句を使用して、偶数か奇数かによってリスト内の整数をグループ化します。  
  
```vb  
Dim numbers As New System.Collections.Generic.List(Of Integer)(  
     New Integer() {35, 44, 200, 84, 3987, 4, 199, 329, 446, 208})  
  
Dim query = From number In numbers
            Group By Remainder = (number Mod 2) Into Group  
  
Dim sb As New System.Text.StringBuilder()  
For Each group In query  
    sb.AppendLine(If(group.Remainder = 0, vbCrLf & "Even numbers:", vbCrLf & "Odd numbers:"))  
    For Each num In group.Group  
        sb.AppendLine(num)  
    Next  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' Odd numbers:  
' 35  
' 3987  
' 199  
' 329  
  
' Even numbers:  
' 44  
' 200  
' 84  
' 4  
' 446  
' 208  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [Group By 句](../../../language-reference/queries/group-by-clause.md)
- [方法: 拡張機能でファイルをグループ化する (LINQ) (Visual Basic)](how-to-group-files-by-extension-linq.md)
- [方法: グループを使用してファイルを複数のファイルに分割する (LINQ) (Visual Basic)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
