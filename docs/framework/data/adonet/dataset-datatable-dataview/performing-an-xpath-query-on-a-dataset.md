---
title: DataSet に対する XPath クエリの実行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e828566-fffe-4d38-abb2-4d68fd73f663
ms.openlocfilehash: 5e9a00ab78a57c3c1686d7c87ed8b45d9b2649af
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150832"
---
# <a name="performing-an-xpath-query-on-a-dataset"></a>DataSet に対する XPath クエリの実行
同期された <xref:System.Data.DataSet> と <xref:System.Xml.XmlDataDocument> との間のリレーションシップによって、XPath (XML Path Language) クエリなどの XML サービスが使用できます。XML サービスは **XmlDataDocument** にアクセスし、**DataSet** に直接アクセスするよりも、特定の機能を効率的に実行できます。 たとえば、<xref:System.Data.DataTable> の **Select** メソッドを使用して **DataSet** の他のテーブルとのリレーションシップをナビゲートする代わりに、**DataSet** と同期化された **XmlDataDocument** に対して XPath クエリを実行すると、<xref:System.Xml.XmlNodeList> 形式で XML 要素のリストを取得できます。 <xref:System.Xml.XmlElement> ノードとしてキャストされた **XmlNodeList** のノードを **XmlDataDocument** の **GetRowFromElement** メソッドに渡すと、同期化された **DataSet** のテーブルの行に一致する <xref:System.Data.DataRow> 参照が返されます。  
  
 たとえば、次に示すコード サンプルでは孫 XPath クエリが実行されます。 **DataSet** には、次の 3 つのテーブルが格納されます: **Customers**、**Orders**、**OrderDetails**。 このサンプルでは、**Customers** テーブルと **Orders** テーブルの間に親子のリレーションが作成され、次に **Orders** テーブルと **OrderDetails** テーブルの間に親子のリレーションが作成されます。 XPath クエリが実行され、値 43 の **ProductID** ノードを持つ孫 **OrderDetails** ノードのある **Customers** ノードの **XmlNodeList** リストが返されます。 つまり、このサンプルでは、XPath クエリを使用して **ProductID** が 43 の製品を注文した顧客を確認します。  
  
```vb  
' Assumes that connection is a valid SqlConnection.  
connection.Open()  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
Dim detailAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM [Order Details]", connection)  
detailAdapter.Fill(dataSet, "OrderDetails")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
dataSet.Relations.Add("OrderDetail", _  
  dataSet.Tables("Orders").Columns("OrderID"), _  
dataSet.Tables("OrderDetails").Columns("OrderID"), false).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)
  
Dim nodeList As XmlNodeList = xmlDoc.DocumentElement.SelectNodes( _  
  "descendant::Customers[*/OrderDetails/ProductID=43]")  
  
Dim dataRow As DataRow  
Dim xmlNode As XmlNode  
  
For Each xmlNode In nodeList  
  dataRow = xmlDoc.GetRowFromElement(CType(xmlNode, XmlElement))  
  
  If Not dataRow Is Nothing then Console.WriteLine(xmlRow(0).ToString())  
Next  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection.  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(dataSet, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(dataSet, "Orders");  
  
SqlDataAdapter detailAdapter = new SqlDataAdapter(  
  "SELECT * FROM [Order Details]", connection);  
detailAdapter.Fill(dataSet, "OrderDetails");  
  
connection.Close();  
  
dataSet.Relations.Add("CustOrders",  
  dataSet.Tables["Customers"].Columns["CustomerID"],  
 dataSet.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
dataSet.Relations.Add("OrderDetail",  
  dataSet.Tables["Orders"].Columns["OrderID"],  
  dataSet.Tables["OrderDetails"].Columns["OrderID"],
  false).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);
  
XmlNodeList nodeList = xmlDoc.DocumentElement.SelectNodes(  
  "descendant::Customers[*/OrderDetails/ProductID=43]");  
  
DataRow dataRow;  
foreach (XmlNode xmlNode in nodeList)  
{  
  dataRow = xmlDoc.GetRowFromElement((XmlElement)xmlNode);  
  if (dataRow != null)  
    Console.WriteLine(dataRow[0]);  
}  
```  
  
## <a name="see-also"></a>関連項目

- [DataSet と XmlDataDocument の同期](dataset-and-xmldatadocument-synchronization.md)
- [ADO.NET の概要](../ado-net-overview.md)
