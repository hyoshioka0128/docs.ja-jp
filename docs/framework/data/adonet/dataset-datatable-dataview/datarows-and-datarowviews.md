---
title: DataRow および DataRowView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8f5eec26-b809-4aca-8778-7e202356d856
ms.openlocfilehash: 14e7e1ccb051410c351e49afee9f2d6809264833
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151300"
---
# <a name="datarows-and-datarowviews"></a>DataRow および DataRowView
<xref:System.Data.DataView> は、<xref:System.Data.DataRowView> オブジェクトの列挙可能なコレクションを公開します。 **DataRowView** オブジェクトは、基になるテーブルの列の名前または列の序数参照によってインデックスが設定されているオブジェクトの配列として値を公開します。 **DataRowView** の <xref:System.Data.DataRowView.Row%2A> プロパティを使用することによって、**DataRowView** で公開されている <xref:System.Data.DataRow> にアクセスできます。  
  
 **DataRowView** を使用して値を表示している場合は、**DataView** の <xref:System.Data.DataView.RowStateFilter%2A> プロパティによって、基になる **DataRow** から公開される行バージョンが決まります。 **DataRow** を使用してさまざまな行バージョンにアクセスする方法については、「[行の状態とバージョン](row-states-and-row-versions.md)」をご覧ください。  
  
 テーブルの現在の値と元の値をすべて表示するコード サンプルを次に示します。  
  
```vb  
Dim catView As DataView = New DataView(catDS.Tables("Categories"))  
Console.WriteLine("Current Values:")  
WriteView(catView)  
Console.WriteLine("Original Values:")  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal  
WriteView(catView)
  
Public Shared Sub WriteView(thisDataView As DataView)  
  Dim rowView As DataRowView  
  Dim i As Integer  
  
  For Each rowView In thisDataView  
    For i = 0 To thisDataView.Table.Columns.Count - 1  
      Console.Write(rowView(i) & vbTab)  
    Next  
    Console.WriteLine()  
  Next  
End Sub  
```  
  
```csharp  
DataView catView = new DataView(catDS.Tables["Categories"]);  
Console.WriteLine("Current Values:");  
WriteView(catView);  
Console.WriteLine("Original Values:");  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal;  
WriteView(catView);  
  
public static void WriteView(DataView thisDataView)  
{  
  foreach (DataRowView rowView in thisDataView)  
  {  
    for (int i = 0; i < thisDataView.Table.Columns.Count; i++)  
      Console.Write(rowView[i] + "\t");  
    Console.WriteLine();  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataRowVersion>
- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataView>
- <xref:System.Data.DataRowView>
- [DataViews](dataviews.md)
- [ADO.NET の概要](../ado-net-overview.md)
