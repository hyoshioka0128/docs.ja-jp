---
title: '方法: 2 つのコレクションを結合する (LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 5a5758d4-906b-4285-908d-5b930db192e6
ms.openlocfilehash: dc3cfd19d990fa81e00f4781cb15bf07eb9a80ea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398052"
---
# <a name="how-to-join-two-collections-linq-to-xml-visual-basic"></a>方法: 2 つのコレクションを結合する (LINQ to XML) (Visual Basic)
XML ドキュメント内の要素または属性は、別の要素または属性を参照することがあります。 たとえば、「[サンプル XML ファイル: 顧客と注文 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)」の XML ドキュメントには、顧客の一覧と注文の一覧が含まれています。 各 `Customer` 要素には、`CustomerID` 属性が含まれています。 各 `Order` 要素には、`CustomerID` 要素が含まれています。 各注文の `CustomerID` 要素は、顧客の `CustomerID` 属性を参照します。  
  
 「[サンプル XSD ファイル: 顧客と注文](sample-xsd-file-customers-and-orders.md)」のトピックには、このドキュメントの検証に使用できる XSD が含まれています。 この XSD は、XSD の `xs:key` 機能と `xs:keyref` 機能を使用して、`CustomerID` 要素の `Customer` 属性がキーであることを確立し、各 `CustomerID` 要素の `Order` 要素と各 `CustomerID` 要素の `Customer` 属性の間にリレーションシップを確立します。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] では、`Join` 句を使用することで、このリレーションシップを利用できます。  
  
 使用できるインデックスがないため、このような結合では実行時のパフォーマンスが低下することに注意してください。  
  
 `Join` の詳細については、「[結合操作 (Visual Basic)](join-operations.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Customer` 要素を `Order` 要素に結合し、注文に `CompanyName` 要素が含まれている新しい XML ドキュメントを生成します。  
  
 クエリを実行する前に、この例では、ドキュメントが「[サンプル XSD ファイル: 顧客と注文](sample-xsd-file-customers-and-orders.md)」のスキーマに準拠しているかどうかを検証します。 これにより、結合句が常に機能するようになります。  
  
 このクエリでは、まずすべての `Customer` 要素を取得し、次にそれらを `Order` 要素に結合します。 クエリでは、"K" より大きい `CustomerID` を持つ顧客の注文のみを選択します。 次に、各注文内に顧客情報を含む新しい `Order` 要素を射影します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:顧客と注文 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)」。  
  
 この例では、XSD スキーマ、[サンプル XSD ファイル: 顧客と注文](sample-xsd-file-customers-and-orders.md)」の XSD スキーマを使用しています。  
  
 この方式の結合ではパフォーマンスが低下することに注意してください。 結合は線形探索によって実行されます。 パフォーマンスを向上させるハッシュ テーブルまたはインデックスはありません。  
  
```vb  
Public Class Program  
    Public Shared errors As Boolean = False  
  
    Public Shared Function LamValidEvent(ByVal o As Object, _  
                 ByVal e As ValidationEventArgs) As Boolean  
        Console.WriteLine("{0}", e.Message)  
        errors = True  
    End Function  
  
    Shared Sub Main()  
        Dim schemas As New XmlSchemaSet()  
        schemas.Add("", "CustomersOrders.xsd")  
  
        Console.Write("Attempting to validate, ")  
        Dim custOrdDoc As XDocument = XDocument.Load("CustomersOrders.xml")  
  
        custOrdDoc.Validate(schemas, Function(o, e) LamValidEvent(0, e))  
        If errors Then  
            Console.WriteLine("custOrdDoc did not validate")  
        Else  
            Console.WriteLine("custOrdDoc validated")  
        End If  
  
        If Not errors Then  
            'Join customers and orders, and create a new XML document with  
            ' a different shape.  
            'The new document contains orders only for customers with a  
            ' CustomerID > 'K'.  
            Dim custOrd As XElement = custOrdDoc.<Root>.FirstOrDefault  
            Dim newCustOrd As XElement = _  
                <Root>  
                    <%= From c In custOrd.<Customers>.<Customer> _  
                        Join o In custOrd.<Orders>.<Order> _  
                        On c.@CustomerID Equals o.<CustomerID>.Value _  
                        Where c.@CustomerID.CompareTo("K") > 0 _  
                        Select _  
                        <Order>  
                            <CustomerID><%= c.@CustomerID %></CustomerID>  
                            <%= c.<CompanyName> %>  
                            <%= c.<ContactName> %>  
                            <%= o.<EmployeeID> %>  
                            <%= o.<OrderDate> %>  
                        </Order> _  
                    %>  
                </Root>  
            Console.WriteLine(newCustOrd)  
        End If  
    End Sub  
End Class  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console
Attempting to validate, custOrdDoc validated  
<Root>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-03-21T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-05-22T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-06-25T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-10-27T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>6</EmployeeID>  
    <OrderDate>1997-11-10T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>4</EmployeeID>  
    <OrderDate>1998-02-12T00:00:00</OrderDate>  
  </Order>  
</Root>  
```  
  
## <a name="see-also"></a>関連項目

- [高度なクエリ手法 (LINQ to XML) (Visual Basic)](advanced-query-techniques-linq-to-xml.md)
