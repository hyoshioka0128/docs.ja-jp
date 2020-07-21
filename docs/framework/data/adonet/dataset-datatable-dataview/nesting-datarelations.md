---
title: DataRelation の入れ子化
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9530f9c9-dd98-4b93-8cdb-40d7f1e8d0ab
ms.openlocfilehash: 971a1bddc40521dc7381ecb2e39709c0fed282ed
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785987"
---
# <a name="nesting-datarelations"></a>DataRelation の入れ子化
データのリレーショナル表現では、各テーブルに含まれている行が、列または列セットを使用して相互に関連付けられています。 ADO.NET の <xref:System.Data.DataSet> では、テーブル間のリレーションシップは <xref:System.Data.DataRelation> を使用して実装されます。 **DataRelation** を作成すると、列の親子リレーションシップはこのリレーションだけをとおして管理されます。 テーブルと列はそれぞれ別個のエンティティです。 XML のデータ階層表現では、子要素が入れ子の状態で含まれている親要素によって親子のリレーションシップが表現されます。  
  
 **DataSet** が <xref:System.Xml.XmlDataDocument> と同期されているとき、または **WriteXml** を使用して XML データとして書き込まれるときに、子オブジェクトの入れ子を容易にするため、**DataRelation** では **Nested** プロパティが公開されています。 **DataRelation** の **Nested** プロパティを **true** に設定すると、XML データとして書き込まれるとき、または **XmlDataDocument** と同期されるときに、リレーションの子の行が親の列に入れ子にされます。 **DataRelation** の **Nested** プロパティは、既定では **false** に設定されます。  
  
 たとえば、次のような **DataSet** があるとします。  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection)  
  
connection.Open()  
  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
customerAdapter.Fill(dataSet, "Customers")  
orderAdapter.Fill(dataSet, "Orders")  
  
connection.Close()  
  
Dim customerOrders As DataRelation = dataSet.Relations.Add( _  
  "CustOrders", dataSet.Tables("Customers").Columns("CustomerID"), _  
  dataSet.Tables("Orders").Columns("CustomerID"))  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection);  
  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
customerAdapter.Fill(dataSet, "Customers");  
orderAdapter.Fill(dataSet, "Orders");  
  
connection.Close();  
  
DataRelation customerOrders = dataSet.Relations.Add(  
  "CustOrders", dataSet.Tables["Customers"].Columns["CustomerID"],  
  dataSet.Tables["Orders"].Columns["CustomerID"]);  
```  
  
 この **DataSet** では **DataRelation** オブジェクトの **Nested** プロパティが **true** に設定されていないため、この **DataSet** が XML データとして表されるときに、子オブジェクトは親要素内に入れ子にされません。 データ リレーションが入れ子になっていない関連 **DataSet** が含まれる **DataSet** の XML 表現を変換すると、パフォーマンスが低下する場合があります。 データ リレーションシップは入れ子にすることをお勧めします。 そのためには、**Nested** プロパティを **true** に設定します。 次に、トップダウン階層形式の XPath クエリ式を使用してデータを検索、変換するコードを XSLT スタイル シートに記述します。  
  
 次のコード例では、**DataSet** に対して **WriteXml** を呼び出した結果を示します。  
  
```xml  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
  <Orders>  
    <OrderID>10643</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-08-25T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10692</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-10-03T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10308</OrderID>  
    <CustomerID>ANATR</CustomerID>  
    <OrderDate>1996-09-18T00:00:00</OrderDate>  
  </Orders>  
</CustomerOrders>  
```  
  
 **Customers** 要素と **Orders** 要素が兄弟要素として示されていることに注意してください。 **Orders** 要素が該当する親要素の子として示されるようにするには、**DataRelation** の **Nested** プロパティを **true** に設定する必要があり、次のコードを追加します。  
  
```vb  
customerOrders.Nested = True  
```  
  
```csharp  
customerOrders.Nested = true;  
```  
  
 上記のコードを追加した結果の出力を次のコードに示します。この例では、**Orders** 要素がそれぞれ該当する親要素の中で入れ子になっています。  
  
```xml  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <Orders>  
      <OrderID>10643</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-08-25T00:00:00</OrderDate>  
    </Orders>  
    <Orders>  
      <OrderID>10692</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-10-03T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <Orders>  
      <OrderID>10308</OrderID>  
      <CustomerID>ANATR</CustomerID>  
      <OrderDate>1996-09-18T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
</CustomerOrders>  
```  
  
## <a name="see-also"></a>関連項目

- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataRelation の追加](adding-datarelations.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
