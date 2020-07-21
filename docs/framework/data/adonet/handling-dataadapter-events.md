---
title: DataAdapter のイベント処理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.openlocfilehash: d01198d158c4e1c64f12e8a0756c3d4e599fce74
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149545"
---
# <a name="handling-dataadapter-events"></a>DataAdapter のイベント処理
ADO.NET <xref:System.Data.Common.DataAdapter> は、データ ソースのデータに対して行われた変更に応答するときに使用できる 3 つのイベントを公開します。 `DataAdapter` のイベントを次の表に示します。  
  
|event|説明|  
|-----------|-----------------|  
|`RowUpdating`|行に対する UPDATE、INSERT、または DELETE の各操作が (`Update` メソッドの 1 つの呼び出しによって) 開始しようとしています。|  
|`RowUpdated`|行に対する UPDATE、INSERT、DELETE の各操作が (`Update` メソッドの 1 つの呼び出しによって) 完了しました。|  
|`FillError`|`Fill` 操作中にエラーが発生しました。|  
  
## <a name="rowupdating-and-rowupdated"></a>RowUpdating と RowUpdated  
 `RowUpdating` は、<xref:System.Data.DataSet> 側で生じた行に対する更新が、データ ソース側で処理される前に発生します。 `RowUpdated` は、`DataSet` 側で生じた行に対する更新が、データ ソース側で処理された後で発生します。 したがって、更新が始まる前に `RowUpdating` を使用して更新の動作を変更することで、更新発生時に行う追加の処理の提供、更新行への参照の保存、現在の更新のキャンセル、後で処理するバッチ処理のための更新スケジュールなどを提供できます。 `RowUpdated` は、更新中に発生するエラーや例外の応答に便利です。 `DataSet` にエラー情報や再試行ロジックなどを追加できます。  
  
 `RowUpdating` イベントおよび `RowUpdated` イベントに渡される <xref:System.Data.Common.RowUpdatingEventArgs> 引数および <xref:System.Data.Common.RowUpdatedEventArgs> 引数には、更新を実行するために使用される `Command` オブジェクトを参照する `Command` プロパティ、更新情報を格納する `DataRow` オブジェクトを参照する `Row` プロパティ、どのタイプの更新を実行するかを示す `StatementType` プロパティ、適用可能な場合は `TableMapping`、および、操作の `Status` などがあります。  
  
 `Status` プロパティを使用すると、操作中にエラーが発生したかどうかを確認したり、必要に応じて現在の行および結果行に対するアクションを制御したりできます。 イベントが発生すると、`Status` プロパティは `Continue` または `ErrorsOccurred` のいずれかになります。 次の表では、更新の後続のアクションを制御するために `Status` プロパティに設定できる値を示しています。  
  
|Status|説明|  
|------------|-----------------|  
|`Continue`|更新操作を続行します。|  
|`ErrorsOccurred`|更新操作を中止し、例外をスローします。|  
|`SkipCurrentRow`|現在の行を無視し、更新操作を続行します。|  
|`SkipAllRemainingRows`|更新操作を中止しますが、例外はスローしません。|  
  
 `Status` プロパティを `ErrorsOccurred` に設定すると、例外がスローされます。 `Errors` プロパティを例外として設定することで、どの例外をスローするかを制御できます。 `Status` に他の値を使用すると、例外はスローされません。  
  
 `ContinueUpdateOnError` プロパティを使用して更新行に関するエラーを処理することもできます。 `DataAdapter.ContinueUpdateOnError` を `true` に設定すると、行を更新した結果、例外がスローされようとしているときに、例外のテキストをその行の `RowError` 情報の中に格納し、例外をスローせずに処理を続行できます。 これにより、`Update` が完了した時点でエラーに応答できるようになります。これに対して `RowUpdated` イベントを使用すると、エラーが発生した時点でエラーに応答できます。  
  
 イベント ハンドラーを追加および削除する方法を次のコード サンプルに示します。 `RowUpdating` イベント ハンドラーは、削除されたすべてのレコードのログをタイムスタンプと共に記録します。 `RowUpdated` イベント ハンドラーでは、`DataSet` の行の `RowError` プロパティにエラー情報を追加し、例外をスローせずに処理を続行します (`ContinueUpdateOnError` = `true` の場合と同等の動作です)。  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
' Add handlers.  
AddHandler custAdapter.RowUpdating, New SqlRowUpdatingEventHandler( _  
  AddressOf OnRowUpdating)  
AddHandler custAdapter.RowUpdated, New SqlRowUpdatedEventHandler(  
  AddressOf OnRowUpdated)  
  
' Set DataAdapter command properties, fill DataSet, and modify DataSet.  
  
custAdapter.Update(custDS, "Customers")  
  
' Remove handlers.  
RemoveHandler custAdapter.RowUpdating, _  
  New SqlRowUpdatingEventHandler(AddressOf OnRowUpdating)  
RemoveHandler custAdapter.RowUpdated, _  
  New SqlRowUpdatedEventHandler(AddressOf OnRowUpdated)  
  
Private Shared Sub OnRowUpdating(sender As Object, _  
  args As SqlRowUpdatingEventArgs)  
  If args.StatementType = StatementType.Delete Then  
    Dim tw As System.IO.TextWriter = _  
  System.IO.File.AppendText("Deletes.log")  
    tw.WriteLine( _  
      "{0}: Customer {1} Deleted.", DateTime.Now, args.Row(_  
      "CustomerID", DataRowVersion.Original))  
    tw.Close()  
  End If  
End Sub  
  
Private Shared Sub OnRowUpdated( _  
  sender As Object, args As SqlRowUpdatedEventArgs)  
  If args.Status = UpdateStatus.ErrorsOccurred  
    args.Status = UpdateStatus.SkipCurrentRow  
    args.Row.RowError = args.Errors.Message  
  End If  
End Sub  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
// Add handlers.  
custAdapter.RowUpdating += new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
// Set DataAdapter command properties, fill DataSet, modify DataSet.  
  
custAdapter.Update(custDS, "Customers");  
  
// Remove handlers.  
custAdapter.RowUpdating -= new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated -= new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
protected static void OnRowUpdating(  
  object sender, SqlRowUpdatingEventArgs args)  
{  
  if (args.StatementType == StatementType.Delete)  
  {  
    System.IO.TextWriter tw = System.IO.File.AppendText("Deletes.log");  
    tw.WriteLine(  
      "{0}: Customer {1} Deleted.", DateTime.Now,
       args.Row["CustomerID", DataRowVersion.Original]);  
    tw.Close();  
  }  
}  
  
protected static void OnRowUpdated(  
  object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.Status == UpdateStatus.ErrorsOccurred)  
  {  
    args.Row.RowError = args.Errors.Message;  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## <a name="fillerror"></a>FillError  
 `DataAdapter` は、`FillError` 操作中にエラーが発生すると `Fill` イベントを発行します。 このタイプのエラーは通常、追加する行のデータを .NET Framework 型に変換したときに、有効桁を消失してしまった場合に発生します。  
  
 `Fill` 操作中にエラーが発生した場合、現在の行は `DataTable` に追加されません。 `FillError` イベントを使用すると、エラーを解決してその行を追加するか、または除外された行を無視し、`Fill` 操作を続行できます。  
  
 `FillErrorEventArgs` イベントに渡す `FillError` には、エラーに応答してエラーを解決できるいくつかのプロパティを含めることができます。 `FillErrorEventArgs` オブジェクトのプロパティを次の表に示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`Errors`|発生した `Exception`。|  
|`DataTable`|エラー発生時にデータを格納しようとしていた `DataTable` オブジェクト。|  
|`Values`|エラー発生時に追加しようとしていた行の値を保持しているオブジェクトの配列。 `Values` 配列の序数参照は、追加しようとしていた行の列の序数参照に対応します。 たとえば、`Values[0]` は、行の第 1 列として追加しようとした値です。|  
|`Continue`|例外をスローするかどうかを選択できます。 `Continue` プロパティを `false` に設定すると、エラーが発生したときに現在の `Fill` 操作を停止し、例外をスローします。 `Continue` を `true` に設定すると、エラーに関係なく `Fill` 操作を続行します。|  
  
 次のコード例では、`FillError` の `DataAdapter` イベントにイベント ハンドラーを追加しています。 この `FillError` イベント コードの例は、有効桁の消失が発生したかどうかを確認し、例外に応答する機会を与えます。  
  
```vb  
AddHandler adapter.FillError, New FillErrorEventHandler( _  
  AddressOf FillError)  
  
Dim dataSet As DataSet = New DataSet  
adapter.Fill(dataSet, "ThisTable")  
  
Private Shared Sub FillError(sender As Object, _  
  args As FillErrorEventArgs)  
  If args.Errors.GetType() Is Type.GetType("System.OverflowException") Then  
    ' Code to handle precision loss.  
    ' Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(New Object() _  
      {args.Values(0), args.Values(1), DBNull.Value})  
    ' Set the RowError containing the value for the third column.  
    myRow.RowError = _  
      "OverflowException encountered. Value from data source: " & _  
      args.Values(2)  
    args.Continue = True  
  End If  
End Sub  
```  
  
```csharp  
adapter.FillError += new FillErrorEventHandler(FillError);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "ThisTable");  
  
protected static void FillError(object sender, FillErrorEventArgs args)  
{  
  if (args.Errors.GetType() == typeof(System.OverflowException))  
  {  
    // Code to handle precision loss.  
    //Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(new object[]  
       {args.Values[0], args.Values[1], DBNull.Value});  
    //Set the RowError containing the value for the third column.  
    myRow.RowError =
       "OverflowException Encountered. Value from data source: " +  
       args.Values[2];  
    args.Continue = true;  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [DataSet のイベント処理](./dataset-datatable-dataview/handling-dataset-events.md)
- [DataTable イベントの処理](./dataset-datatable-dataview/handling-datatable-events.md)
- [イベント](../../../standard/events/index.md)
- [ADO.NET の概要](ado-net-overview.md)
