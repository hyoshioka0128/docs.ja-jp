---
title: Load メソッド
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
ms.openlocfilehash: f1c819333225c22efb85946001a1fc8340d57989
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150728"
---
# <a name="the-load-method"></a>Load メソッド
<xref:System.Data.DataTable.Load%2A> メソッドを使用して、データ ソースの行を <xref:System.Data.DataTable> に読み込むことができます。 これはオーバーロードされたメソッドで、最も単純な形式で単一の **DataReader** パラメーターを受け取ります。 この形式により、このメソッドでは **DataTable** に対する行の読み込みのみが行われます。 または、**LoadOption** パラメーターを指定して **DataTable** へのデータの追加方法を制御することもできます。  
  
 **LoadOption** パラメーターは、データ ソースからの受信データをテーブルに既に格納されているデータと組み合わせる方法が記述されているため、**DataTable** に既にデータ行が含まれている場合に特に便利です。 たとえば、**PreserveCurrentValues** (既定値) は、**DataTable** の行が **Added** としてマークされ、データ ソースの行に一致する内容に対して **Original** 値または各列が設定されている場合に指定します。 **Current** 値は、行が追加されたときに割り当てられた値が保持され、その行の **RowState** は **Changed** に設定されます。  
  
 <xref:System.Data.LoadOption> 列挙値の簡単な説明を次の表に示します。  
  
|LoadOption の値|説明|  
|----------------------|-----------------|  
|**OverwriteRow**|読み込まれる行と **DataTable** に既に存在する行で **PrimaryKey** 値が同じ場合、各列の **Original** 値と **Current** 値は読み込まれる行の値に置き換えられ、**RowState** プロパティは **Unchanged** に設定されます。<br /><br /> **DataTable** に存在していなかった行がデータ ソースから読み込まれ、その行の **RowState** 値は **Unchanged** に設定されます。<br /><br /> このオプションは **DataTable** の内容を更新して、データ ソースの内容と一致するようにします。|  
|**PreserveCurrentValues (既定値)**|読み込まれる行と **DataTable** に既に存在する行の **PrimaryKey** 値が同じ場合、**Original** 値には読み込まれる行の内容が設定されますが、**Current** 値は変更されません。<br /><br /> **RowState** が **Added** または **Modified** の場合、この値は **Modified** に設定されます。<br /><br /> **RowState** が **Deleted** であった場合、この値は **Deleted** のままとなります。<br /><br /> **DataTable** に存在していなかった行がデータ ソースから読み込まれ、その行の **RowState** は **Unchanged** に設定されます。|  
|**UpdateCurrentValues**|読み込まれる行と **DataTable** に既に存在する行の **PrimaryKey** 値が同じ場合、**Current** 値が **Original** 値にコピーされ、**Current** 値には読み込まれる行の内容が設定されます。<br /><br /> **DataTable** の **RowState** が **Added** の場合、**RowState** は **Added** のままとなります。 **Modified** または **Deleted** としてマークされた行の **RowState** は **Modified** になります。<br /><br /> **DataTable** に存在していなかった行がデータ ソースから読み込まれ、その行の **RowState** は **Added** に設定されます。|  
  
 **Load** メソッドを使用して **Northwind** データベースに従業員の誕生日リストを表示する例を次に示します。  
  
```vb  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## <a name="see-also"></a>関連項目

- [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)
- [ADO.NET の概要](../ado-net-overview.md)
