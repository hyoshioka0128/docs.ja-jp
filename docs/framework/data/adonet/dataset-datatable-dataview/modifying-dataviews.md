---
title: DataView の変更
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 697a3991-b660-4a5a-8a54-1a2304ff158e
ms.openlocfilehash: 3e811410ea9fdd4be0cbd84b895483f69f58b0d0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786046"
---
# <a name="modifying-dataviews"></a>DataView の変更
<xref:System.Data.DataView> を使用して、データ行を基になるテーブルに追加、削除、または変更できます。 基になるテーブルのデータを **DataView** で変更できるかどうかは、**DataView** の 3 つのブール値プロパティで制御されます。 この 3 つのプロパティとは、<xref:System.Data.DataView.AllowNew%2A>、<xref:System.Data.DataView.AllowEdit%2A> および <xref:System.Data.DataView.AllowDelete%2A> です。 これらのプロパティの既定値は **true** です。  
  
 **AllowNew** が **true** の場合は、**DataView** の <xref:System.Data.DataView.AddNew%2A> メソッドを使用して新しい <xref:System.Data.DataRowView> を作成できます。 **DataRowView** の <xref:System.Data.DataRowView.EndEdit%2A> メソッドが呼び出されるまで、基になる <xref:System.Data.DataTable> に新しい行が実際に追加されることはないことに注意してください。 **DataRowView** の <xref:System.Data.DataRowView.CancelEdit%2A> メソッドが呼び出されると、新しい行は破棄されます。 また、一度に編集できる **DataRowView** は 1 つだけであることにも注意してください。 保留中の行がある間に、**DataRowView** の **AddNew** メソッドまたは **BeginEdit** メソッドを呼び出すと、保留中の行に対して **EndEdit** が暗黙的に呼び出されます。 **EndEdit** が呼び出されると、基になる **DataTable** に対して変更が適用されます。適用された変更をコミットするには **DataTable**、**DataSet**、または**DataRow** オブジェクトの **AcceptChanges** メソッドを使用し、拒否するにはこれらのオブジェクトの **RejectChanges** メソッドを使用します。 **AllowNew** が **false** の場合は、**DataRowView** の **AddNew** メソッドを呼び出すと例外がスローされます。  
  
 **AllowEdit** が **true** の場合は、**DataRowView** を使用して **DataRow** の内容を変更できます。 基になる行の変更内容を確定するには **DataRowView.EndEdit** を使用し、変更内容を取り消すには **DataRowView.CancelEdit** を使用します。 一度に編集できるのは 1 行だけです。 保留中の行がある間に、**DataRowView** の **AddNew** メソッドまたは **BeginEdit** メソッドを呼び出すと、保留中の行に対して **EndEdit** が暗黙的に呼び出されます。 **EndEdit** が呼び出されると、基になる **DataRow** の **Current** 行バージョンに対して変更が適用されます。適用された変更をコミットするには **DataTable**、**DataSet**、または **DataRow** オブジェクトの **AcceptChanges** メソッドを使用し、拒否するにはこれらのオブジェクトの **RejectChanges** メソッドを使用します。 **AllowEdit** が **false** の場合、**DataView** の値を変更しようとすると、例外がスローされます。  
  
 既存の **DataRowView** の編集中でも、まだ確定されていない変更に関して、基になる **DataTable** のイベントが発生する場合があります。 **DataRowView** に対して **EndEdit** と **CancelEdit** のどちらが呼び出されているかに関係なく、基になる **DataRow** に対して **EndEdit** を呼び出すと、確定されていない変更が適用され、**CancelEdit** を呼び出すと、確定されていない変更が取り消されます。  
  
 **AllowDelete** が **true** の場合は、**DataView** オブジェクトまたは **DataRowView** オブジェクトの **Delete** メソッドを使用して **DataView** から行を削除することができ、基になる **DataTable** から行が削除されます。 後でこの削除操作をコミットするには **AcceptChanges** を使用し、拒否するには **RejectChanges** を使用します。 **AllowDelete** が **false** の場合は、**DataView** または **DataRowView** の **Delete** メソッドを呼び出すと例外がスローされます。  
  
 次のコード例では、**DataView** を使用して行を削除する機能を無効にし、**DataView** を使用して基になるテーブルに新しい行を追加します。  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custView As DataView = custTable.DefaultView  
custView.Sort = "CompanyName"  
  
custView.AllowDelete = False  
  
Dim newDRV As DataRowView = custView.AddNew()  
newDRV("CustomerID") = "ABCDE"  
newDRV("CompanyName") = "ABC Products"  
newDRV.EndEdit()  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
DataView custView = custTable.DefaultView;  
custView.Sort = "CompanyName";  
  
custView.AllowDelete = false;  
  
DataRowView newDRV = custView.AddNew();  
newDRV["CustomerID"] = "ABCDE";  
newDRV["CompanyName"] = "ABC Products";  
newDRV.EndEdit();  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- <xref:System.Data.DataRowView>
- [DataViews](dataviews.md)
- [ADO.NET の概要](../ado-net-overview.md)
