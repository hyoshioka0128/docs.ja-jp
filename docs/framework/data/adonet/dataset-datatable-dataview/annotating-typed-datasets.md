---
title: 型指定された DataSet の注釈
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
ms.openlocfilehash: 757a87f92d8dc6049de1844fed892d95dc57c990
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151521"
---
# <a name="annotating-typed-datasets"></a>型指定された DataSet の注釈
注釈を使用すると、基になるスキーマを変更せずに型指定された <xref:System.Data.DataSet> の要素の名前を変更できます。 基になるスキーマの要素の名前を変更すると、データ ソースにあるオブジェクトへの参照が失われるだけでなく、型指定された **DataSet** がデータ ソースにないオブジェクトを参照することになります。  
  
 注釈を使用すると、基になるスキーマを変更せずに、型指定された **DataSet** のオブジェクトをわかりやすい名前にカスタマイズできるため、コードが読みやすくなり、型指定された **DataSet** がクライアントで使用しやすくなります。 たとえば、次の **Northwind** データベースの **Customers** テーブルのスキーマ要素は、**CustomersRow** という名前の **DataRow** オブジェクト名および **Customers** という名前の <xref:System.Data.DataRowCollection> となります。  
  
```xml  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 **Customers** という **DataRowCollection** 名は、クライアント コードでは意味がありますが、**CustomersRow** という **DataRow** 名は単一のオブジェクトであるため、誤解が生じます。 また、一般的なシナリオでは、オブジェクトは **Row** ID を指定せずに参照されるため、単に **Customer** オブジェクトとして参照されます。 この問題を解決するには、スキーマに注釈を付け、**DataRow** オブジェクトと **DataRowCollection** オブジェクトに新しい名前を指定します。 上記のスキーマに注釈を付けたスキーマを次に示します。  
  
```xml  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 **Customer** という **typedName** 値を指定すると、**Customer** という **DataRow** オブジェクト名になります。 **Customers** という **typedPlural** 値を指定すると、**Customers** という **DataRowCollection** 名が保存されます。  
  
 使用できる注釈を次の表に示します。  
  
|注釈|説明|  
|----------------|-----------------|  
|**typedName**|オブジェクト名。|  
|**typedPlural**|オブジェクトのコレクション名。|  
|**typedParent**|親のリレーションシップで参照される場合のオブジェクト名。|  
|**typedChildren**|子のリレーションシップからオブジェクトを返すメソッド名。|  
|**nullValue**|基になる値が **DBNull** の場合の値。 **nullValue** の注釈については、次の表を参照してください。 既定値は **_throw** です。|  
  
 **nullValue** 注釈に指定できる値を次の表に示します。  
  
|nullValue の値|説明|  
|---------------------|-----------------|  
|*置換値*|返される値を指定します。 返された値は要素の型と一致する必要があります。 たとえば、整数型フィールドが null の場合に 0 を返すために `nullValue="0"` を使用します。|  
|**_throw**|例外をスローします。 既定値です。|  
|**_null**|プリミティブ型が見つかった場合は、null 参照を返すか、例外をスローします。|  
|**_empty**|文字列の場合は **String.Empty** を、それ以外の場合は空のコンストラクターから作成されたオブジェクトを返します。 プリミティブ型が見つかった場合、例外をスローします。|  
  
 型指定された **DataSet** のオブジェクトの既定値と使用できる注釈を次の表に示します。  
  
|オブジェクト/メソッド/イベント|Default|注釈|  
|---------------------------|-------------|----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** のメソッド|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Property**|PropertyName|typedName|  
|**Child** アクセサー|GetChildTableNameRows|typedChildren|  
|**Parent** アクセサー|TableNameRow|typedParent|  
|**DataSet** イベント|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 型指定された **DataSet** の注釈を使用するには、XML スキーマ定義言語 (XSD) スキーマに次の **xmlns** 参照をインクルードする必要があります。 データベース テーブルから xsd を作成するには、<xref:System.Data.DataSet.WriteXmlSchema%2A> に関するトピック、または「[Visual Studio でのデータセットの操作](/visualstudio/data-tools/dataset-tools-in-visual-studio)」を参照してください。  
  
```xml  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 **Orders** テーブルとのリレーションを持つ **Northwind** データベースの **Customers** テーブルを公開する、注釈の付いたスキーマのサンプルを次に示します。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""
      xmlns:xs="http://www.w3.org/2001/XMLSchema"
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone" codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order" codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"                  codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter" codegen:nullValue="1980-01-01T00:00:00"
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 サンプル スキーマから作成された厳密に型指定された **DataSet** を次のコード サンプルで使用します。 また、一方の <xref:System.Data.SqlClient.SqlDataAdapter> を使用して **Customers** テーブルを、他方の <xref:System.Data.SqlClient.SqlDataAdapter> を使用して **Orders** テーブルを作成します。 厳密に型指定された **DataSet** により、**DataRelations** が定義されます。  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =
    customers.Customers.NewCustomer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [型指定されたデータセット](typed-datasets.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
