---
title: DataView の作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b1cc02d1-23b1-4439-a998-0da1899f3442
ms.openlocfilehash: 9d21b17068ff3ce5b0bd3990144383d7f9ded2f9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151339"
---
# <a name="creating-a-dataview"></a>DataView の作成
<xref:System.Data.DataView> は 2 とおりの方法で作成できます。 **DataView** コンストラクターを使用するか、または <xref:System.Data.DataTable> の <xref:System.Data.DataTable.DefaultView%2A> プロパティへの参照を作成します。 空の **DataView** コンストラクターを使用できます。また、DataView コンストラクターでは、**DataTable** を 1 つの引数としてとるか、またはフィルター条件、並べ替え条件、および行状態フィルターと共に **DataTable** を使用します。 **DataView** で使用できるその他の引数については、「[データの並べ替えとフィルター処理](sorting-and-filtering-data.md)」を参照してください。  
  
 **DataView** のインデックスが作成されるのは、**DataView** が作成される時点と、**Sort**、**RowFilter**、または **RowStateFilter** の各プロパティが変更される時点であるため、**DataView** の作成時に初期の並べ替え順序または初期フィルター条件をコンストラクター引数として指定すると、パフォーマンスを最大限に引き出すことができます。 並べ替え条件やフィルター条件を指定せずに **DataView** を作成してから、**Sort**、**RowFilter**、または **RowStateFilter** の各プロパティを設定すると、インデックスが少なくとも 2 回作成されます。これは、**DataView** の作成時点と、並べ替えプロパティまたはフィルター プロパティの変更時です。  
  
 引数のないコンストラクターを使用して **DataView** を作成すると、**Table** プロパティを設定するまで、**DataView** を使用できないことに注意してください。  
  
 次のコード例では、**DataView** コンストラクターを使用して **DataView** を作成する方法を示します。 **DataTable** と共に **RowFilter**、**Sort** 列、および **DataViewRowState** が指定されています。  
  
```vb  
Dim custDV As DataView = New DataView(custDS.Tables("Customers"), _  
    "Country = 'USA'", _  
    "ContactName", _  
    DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView custDV = new DataView(custDS.Tables["Customers"],
    "Country = 'USA'",
    "ContactName",
    DataViewRowState.CurrentRows);  
```  
  
 テーブルの **DefaultView** プロパティを使用して **DataTable** の既定の **DataView** への参照を取得するコード サンプルを次に示します。  
  
```vb  
Dim custDV As DataView = custDS.Tables("Customers").DefaultView  
```  
  
```csharp  
DataView custDV = custDS.Tables["Customers"].DefaultView;  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataViews](dataviews.md)
- [データの並べ替えとフィルター処理](sorting-and-filtering-data.md)
- [DataTables](datatables.md)
- [ADO.NET の概要](../ado-net-overview.md)
