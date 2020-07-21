---
title: '方法: 関連要素を検索する (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 6b0ef058-d704-48a5-98cd-33f00d088af9
ms.openlocfilehash: 5819ef216f767367aa16b20f818b2bbc537d54b7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364657"
---
# <a name="how-to-find-related-elements-xpath-linq-to-xml-visual-basic"></a>方法: 関連要素を検索する (XPath-LINQ to XML) (Visual Basic)
このトピックでは、別の要素の値によって参照される属性に基づいて要素を取得する方法について説明します。  
  
 XPath 式を次に示します。  
  
 `.//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]`  
  
## <a name="example"></a>例  
 この例では、12 番目の `Order` 要素を検索し、その注文に対応する顧客を検索します。  
  
 .NET でのリストのインデックスは '0' から始まることに注意してください。 XPath 述語のノード コレクションのインデックスは '1' から始まります。 両者の違いを次の例で示します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:顧客と注文 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)。  
  
```vb  
Dim co As XDocument = XDocument.Load("CustomersOrders.xml")  
  
' LINQ to XML query  
Dim customer1 As XElement = ( _  
    From el In co...<Customer> _  
    Where el.@CustomerID = co.<Root>.<Orders>.<Order>. _  
        ToList()(11).<CustomerID>(0).Value _  
    Select el).First()  
  
' An alternate way to write the query that avoids creation  
' of a System.Collections.Generic.List:  
Dim customer2 As XElement = ( _  
    From el In co...<Customer> _  
    Where el.@CustomerID = co.<Root>.<Orders>.<Order>. _  
        Skip(11).First().<CustomerID>(0).Value _  
    Select el).First()  
  
' XPath expression  
Dim customer3 As XElement = co.XPathSelectElement _  
    (".//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]")  
  
If customer1 Is customer2 And customer1 Is customer3 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(customer1)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```console
Results are identical  
<Customer CustomerID="HUNGC">  
  <CompanyName>Hungry Coyote Import Store</CompanyName>  
  <ContactName>Yoshi Latimer</ContactName>  
  <ContactTitle>Sales Representative</ContactTitle>  
  <Phone>(503) 555-6874</Phone>  
  <Fax>(503) 555-2376</Fax>  
  <FullAddress>  
    <Address>City Center Plaza 516 Main St.</Address>  
    <City>Elgin</City>  
    <Region>OR</Region>  
    <PostalCode>97827</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
</Customer>  
```  
  
## <a name="see-also"></a>関連項目

- [XPath ユーザー向けの LINQ to XML (Visual Basic)](linq-to-xml-for-xpath-users.md)
