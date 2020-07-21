---
title: DataRow の削除
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c34f531d-4b9b-4071-b2d7-342c402aa586
ms.openlocfilehash: 3f48339539f08bbc1c2c15035741375bd9ade553
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784725"
---
# <a name="datarow-deletion"></a>DataRow の削除
<xref:System.Data.DataTable> オブジェクトから <xref:System.Data.DataRow> オブジェクトを削除するには、<xref:System.Data.DataRowCollection> オブジェクトの **Remove** メソッドと **DataRow** オブジェクトの <xref:System.Data.DataRow.Delete%2A> メソッドの、2 つのメソッドを使用できます。 <xref:System.Data.DataRowCollection.Remove%2A> メソッドでは **DataRowCollection** から **DataRow** が削除されるのに対し、<xref:System.Data.DataRow.Delete%2A> メソッドでは削除対象の行がマークされるだけです。 実際の削除は、アプリケーションで **AcceptChanges** メソッドを呼び出すと実行されます。 <xref:System.Data.DataRow.Delete%2A> を使用すると、行を実際に削除する前に、削除対象としてどの行がマークされているかをプログラムによってチェックできます。 削除対象としてマークされている行の <xref:System.Data.DataRow.RowState%2A> プロパティは、<xref:System.Data.DataRow.Delete%2A> に設定されています。  
  
 <xref:System.Data.DataRow.Delete%2A> オブジェクトを反復処理している間は、foreach ループで <xref:System.Data.DataRowCollection.Remove%2A> も <xref:System.Data.DataRowCollection> も呼び出すことはできません。 <xref:System.Data.DataRow.Delete%2A> または <xref:System.Data.DataRowCollection.Remove%2A> はコレクションの状態を変更します。  
  
 **DataAdapter** およびリレーショナル データ ソースに関連して <xref:System.Data.DataSet> または **DataTable** を使用するときは、**DataRow** の **Delete** メソッドを使用して行を削除します。 **Delete** メソッドでは、**DataSet** または **DataTable** の行が **Deleted** としてマークされますが、その行は削除されません。 代わりに、**DataAdapter** で **Deleted** としてマークされた行が検出されたときに、**DeleteCommand** メソッドが実行されて、データ ソースの該当する行が削除されます。 その後、**AcceptChanges** メソッドを使用して、その行を永続的に削除できます。 **Remove** を使用して行を削除すると、行はテーブルから完全に削除されますが、**DataAdapter** ではデータ ソースの行は削除されません。  
  
 次の例で示すように、**DataRowCollection** の **Remove** メソッドに引数として **DataRow** を渡すと、その行がコレクションから削除されます。  
  
```vb  
workTable.Rows.Remove(workRow)  
```  
  
```csharp  
workTable.Rows.Remove(workRow);  
```  
  
 これに対して、次の例では、**DataRow** で **Delete** メソッドを呼び出して、その **RowState** を **Deleted** に変更する方法を示します。  
  
```vb  
workRow.Delete  
```  
  
```csharp  
workRow.Delete();  
```  
  
 行を削除対象としてマークしてから **DataTable** オブジェクトの **AcceptChanges** メソッドを呼び出すと、その行が **DataTable** から削除されます。 これに対して、**RejectChanges** を呼び出すと、行の **RowState** はその行が **Deleted** としてマークされる前の状態に戻ります。  
  
> [!NOTE]
> **DataRow** の **RowState** が **Added** である場合、つまりテーブルに行が追加された直後の状態の場合に、その行を **Deleted** としてマークすると、その行はテーブルから削除されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)
- [ADO.NET の概要](../ado-net-overview.md)
