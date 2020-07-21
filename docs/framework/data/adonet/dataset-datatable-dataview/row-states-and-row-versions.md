---
title: 行の状態とバージョン
ms.date: 07/19/2018
dev_langs:
- csharp
- vb
ms.assetid: 2e6642c9-bfc6-425c-b3a7-e4912ffa6c1f
ms.openlocfilehash: 70596d6acb62fa01092e5e55dd3b6c84eb162b5d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784328"
---
# <a name="row-states-and-row-versions"></a>行の状態とバージョン
ADO.NET は、行の状態とバージョンを使用してテーブル内の行を管理します。 行状態は、1 つの行のステータスを示します。行バージョンは、1 つの行の値が変更されるときに、変更に応じてその行に格納される現在の値、元の値、既定値などを維持します。 たとえば、ある行の 1 つの列を変更すると、この行の状態は `Modified` になり、次の 2 つの行バージョンが存在することになります。`Current` には現在の行値が格納され、`Original` にはその列が変更される前の行値が格納されます。  
  
 各 <xref:System.Data.DataRow> オブジェクトにある <xref:System.Data.DataRow.RowState%2A> プロパティを調べると、行の現在の状態を確認できます。 `RowState` 列挙値ごとの簡単な説明を次の表に示します。  
  
|RowState の値|説明|  
|--------------------|-----------------|  
|<xref:System.Data.DataRowState.Unchanged>|`AcceptChanges` が最後に呼び出されてから、または `DataAdapter.Fill` によって行が作成されてから変更は行われていません。|  
|<xref:System.Data.DataRowState.Added>|行がテーブルに追加されましたが、`AcceptChanges` が呼び出されていません。|  
|<xref:System.Data.DataRowState.Modified>|行のいくつかの要素が変更されました。|  
|<xref:System.Data.DataRowState.Deleted>|行がテーブルから削除されましたが、`AcceptChanges` が呼び出されていません。|  
|<xref:System.Data.DataRowState.Detached>|行がどの `DataRowCollection` にも属していません。 新しく作成された行の `RowState` は `Detached` に設定されます。 `DataRow` メソッドを呼び出して新しい `DataRowCollection` を `Add` に追加すると、`RowState` プロパティの値は `Added` に設定されます。<br /><br /> `Detached` は、`DataRowCollection` メソッドを使用するか、または `Remove` メソッドに続いて `Delete` メソッドを使用して `AcceptChanges` から削除された行に対しても設定されます。|  
  
 `AcceptChanges`、<xref:System.Data.DataSet>、または <xref:System.Data.DataTable> の <xref:System.Data.DataRow> が呼び出されると、`Deleted` の行状態を持つすべての行が削除されます。 残りの行の行状態は `Unchanged` になり、`Original` 行バージョンの値は `Current` 行バージョンの値で上書きされます。 `RejectChanges` が呼び出されると、`Added` の行状態を持つすべての行が削除されます。 残りの行の行状態は `Unchanged` になり、`Current` 行バージョンの値は `Original` 行バージョンの値で上書きされます。  
  
 <xref:System.Data.DataRowVersion> パラメーターと列参照を渡すことにより、ある行の行バージョンを表示する例を次に示します。  
  
```vb  
Dim custRow As DataRow = custTable.Rows(0)  
Dim custID As String = custRow("CustomerID", DataRowVersion.Original).ToString()  
```  
  
```csharp  
DataRow custRow = custTable.Rows[0];  
string custID = custRow["CustomerID", DataRowVersion.Original].ToString();  
```  
  
 `DataRowVersion` 列挙値ごとの簡単な説明を次の表に示します。  
  
|DataRowVersion の値|説明|  
|--------------------------|-----------------|  
|<xref:System.Data.DataRowVersion.Current>|行の現在の値。 この行バージョンは、`RowState` の `Deleted` を持つ行については存在しません。|  
|<xref:System.Data.DataRowVersion.Default>|特定の行の既定の行バージョン。 `Added`、`Modified`、または `Deleted` 行の既定の行バージョンは、`Current` です。 `Detached` 行の既定の行バージョンは、`Proposed` です。|  
|<xref:System.Data.DataRowVersion.Original>|行の元の値。 この行バージョンは、`RowState` の `Added` を持つ行については存在しません。|  
|<xref:System.Data.DataRowVersion.Proposed>|行に対して提示された値。 この行バージョンは、行、つまり `DataRowCollection` の一部ではない行に対する編集操作の間存在します。|  
  
 `DataRow` メソッドを呼び出して <xref:System.Data.DataRow.HasVersion%2A> を引数として渡すことにより、`DataRowVersion` が特定の行バージョンを持っているかどうかを確認できます。 たとえば、`DataRow.HasVersion(DataRowVersion.Original)` は、新しく追加された行に対して `false` が呼び出されていない場合に `AcceptChanges` を返します。  
  
 テーブルから削除されたすべての行の値を表示するコード サンプルを次に示します。 `Deleted` 行には `Current` 行バージョンがないため、列値にアクセスするときに `DataRowVersion.Original` を渡す必要があります。  
  
```vb  
Dim catTable As DataTable = catDS.Tables("Categories")  
  
Dim delRows() As DataRow = catTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
Console.WriteLine("Deleted rows:" & vbCrLf)  
  
Dim catCol As DataColumn  
Dim delRow As DataRow  
  
For Each catCol In catTable.Columns  
  Console.Write(catCol.ColumnName & vbTab)  
Next  
Console.WriteLine()  
  
For Each delRow In delRows  
  For Each catCol In catTable.Columns  
    Console.Write(delRow(catCol, DataRowVersion.Original) & vbTab)  
  Next  
  Console.WriteLine()  
Next  
```  
  
```csharp  
DataTable catTable = catDS.Tables["Categories"];  
  
DataRow[] delRows = catTable.Select(null, null, DataViewRowState.Deleted);  
  
Console.WriteLine("Deleted rows:\n");  
  
foreach (DataColumn catCol in catTable.Columns)  
  Console.Write(catCol.ColumnName + "\t");  
Console.WriteLine();  
  
foreach (DataRow delRow in delRows)  
{  
  foreach (DataColumn catCol in catTable.Columns)  
    Console.Write(delRow[catCol, DataRowVersion.Original] + "\t");  
  Console.WriteLine();  
}  
```  
  
## <a name="see-also"></a>関連項目

- [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)
- [DataSet、DataTable、および DataView](index.md)
- [DataAdapter と DataReader](../dataadapters-and-datareaders.md)
- [ADO.NET の概要](../ado-net-overview.md)
