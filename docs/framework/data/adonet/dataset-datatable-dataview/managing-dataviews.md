---
title: DataViews の管理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b67fab5-1722-4d2b-bfc1-247a75f0f1ee
ms.openlocfilehash: 5e85fccddf6359791ea702667a36b44f611815dc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784507"
---
# <a name="managing-dataviews"></a>DataViews の管理
<xref:System.Data.DataViewManager> のすべてのテーブルのビュー設定を管理するには、<xref:System.Data.DataView> を使用します。 リレーションシップを移動するグリッドなどのように、1 つのコントロールを複数のテーブルに連結する場合は、**DataViewManager** が適しています。  
  
 **DataViewManager** には、<xref:System.Data.DataSet> のテーブルのビュー設定に使用される <xref:System.Data.DataViewSetting> オブジェクトのコレクションが含まれています。 <xref:System.Data.DataViewSettingCollection> には、**DataSet** の各テーブルに対応する <xref:System.Data.DataViewSetting> オブジェクトが 1 つずつ含まれています。 **DataViewSetting** を使用することで、参照テーブルの既定の **ApplyDefaultSort**、**Sort**、**RowFilter**、**RowStateFilter** の各プロパティを設定できます。 名前または序数参照によって、または参照をその特定のテーブル オブジェクトに渡すことによって、特定のテーブルの **DataViewSetting** を参照できます。 **DataViewSettings** プロパティを使用することで、**DataViewManager** の **DataViewSetting** オブジェクトのコレクションにアクセスできます。  
  
 次のコード例では、**DataSet** に、SQL Server の **Northwind** データベースの **Customers**、**Orders**、**Order Details** の各テーブルを格納し、テーブル間のリレーションシップを作成し、**DataViewManager** を使用して既定の **DataView** の設定を指定し、**DataGrid** を **DataViewManager** にバインドします。 この例では、**DataSet** のすべてのテーブルに対して、テーブルの主キーによって並べ替えるように (**ApplyDefaultSort** = **true**) **DataView** の既定の設定を指定した後、**Customers** テーブルの並べ替え順序を **CompanyName** で並べ替えるように変更します。  
  
```vb  
' Assumes connection is a valid SqlConnection to Northwind.  
' Create a Connection, DataAdapters, and a DataSet.  
Dim custDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
Dim orderDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, CustomerID FROM Orders", connection)  
Dim ordDetDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, ProductID, Quantity FROM [Order Details]", connection)  
  
Dim custDS As DataSet = New DataSet()  
  
' Open the Connection.  
connection.Open()  
  
    ' Fill the DataSet with schema information and data.  
    custDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
    orderDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
    ordDetDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
  
    custDA.Fill(custDS, "Customers")  
    orderDA.Fill(custDS, "Orders")  
    ordDetDA.Fill(custDS, "OrderDetails")  
  
    ' Close the Connection.  
    connection.Close()  
  
    ' Create relationships.  
    custDS.Relations.Add("CustomerOrders", _  
          custDS.Tables("Customers").Columns("CustomerID"), _  
          custDS.Tables("Orders").Columns("CustomerID"))  
  
    custDS.Relations.Add("OrderDetails", _  
          custDS.Tables("Orders").Columns("OrderID"), _  
          custDS.Tables("OrderDetails").Columns("OrderID"))  
  
' Create default DataView settings.  
Dim viewManager As DataViewManager = New DataViewManager(custDS)  
  
Dim viewSetting As DataViewSetting  
For Each viewSetting In viewManager.DataViewSettings  
  viewSetting.ApplyDefaultSort = True  
Next  
  
viewManager.DataViewSettings("Customers").Sort = "CompanyName"  
  
' Bind to a DataGrid.  
Dim grid As System.Windows.Forms.DataGrid = New System.Windows.Forms.DataGrid()  
grid.SetDataBinding(viewManager, "Customers")  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection to Northwind.  
// Create a Connection, DataAdapters, and a DataSet.  
SqlDataAdapter custDA = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
SqlDataAdapter orderDA = new SqlDataAdapter(  
  "SELECT OrderID, CustomerID FROM Orders", connection);  
SqlDataAdapter ordDetDA = new SqlDataAdapter(  
  "SELECT OrderID, ProductID, Quantity FROM [Order Details]", connection);  
  
DataSet custDS = new DataSet();  
  
// Open the Connection.  
connection.Open();  
  
    // Fill the DataSet with schema information and data.  
    custDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
    orderDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
    ordDetDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
  
    custDA.Fill(custDS, "Customers");  
    orderDA.Fill(custDS, "Orders");  
    ordDetDA.Fill(custDS, "OrderDetails");  
  
    // Close the Connection.  
    connection.Close();  
  
    // Create relationships.  
    custDS.Relations.Add("CustomerOrders",  
          custDS.Tables["Customers"].Columns["CustomerID"],  
          custDS.Tables["Orders"].Columns["CustomerID"]);  
  
    custDS.Relations.Add("OrderDetails",  
          custDS.Tables["Orders"].Columns["OrderID"],  
          custDS.Tables["OrderDetails"].Columns["OrderID"]);  
  
// Create default DataView settings.  
DataViewManager viewManager = new DataViewManager(custDS);  
  
foreach (DataViewSetting viewSetting in viewManager.DataViewSettings)  
  viewSetting.ApplyDefaultSort = true;  
  
viewManager.DataViewSettings["Customers"].Sort = "CompanyName";  
  
// Bind to a DataGrid.  
System.Windows.Forms.DataGrid grid = new System.Windows.Forms.DataGrid();  
grid.SetDataBinding(viewManager, "Customers");  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataSet>
- <xref:System.Data.DataViewManager>
- <xref:System.Data.DataViewSetting>
- <xref:System.Data.DataViewSettingCollection>
- [DataViews](dataviews.md)
- [ADO.NET の概要](../ado-net-overview.md)
