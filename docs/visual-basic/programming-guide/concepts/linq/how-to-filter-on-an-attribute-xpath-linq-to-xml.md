---
title: '方法: 属性をフィルター処理する (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: ffefb9d6-45ec-4677-a396-dd9c2b36298f
ms.openlocfilehash: 5bc0a621f0d3bb8e22701440383cdac54c7be51b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394506"
---
# <a name="how-to-filter-on-an-attribute-xpath-linq-to-xml-visual-basic"></a>方法: 属性をフィルター処理する (XPath-LINQ to XML) (Visual Basic)
このトピックでは、指定した名前を持ち、かつ指定した値の属性を持つ子孫要素を取得する方法について説明します。  
  
 XPath 式を次に示します。  
  
 `.//Address[@Type='Shipping']`  
  
## <a name="example"></a>例  
 この例では、`Address` という名前を持ち、かつ "Shipping" という値の `Type` 属性を持つ子孫要素をすべて検索します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:複数の購買発注書 (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    From el In po...<Address> _  
    Where el.@Type = "Shipping" _  
    Select el  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = _  
    po.XPathSelectElements(".//Address[@Type='Shipping']")  
  
If (list1.Count = list2.Count And _  
        list1.Intersect(list2).Count() = list1.Count()) Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
For Each el As XElement In list1  
    Console.WriteLine(el)  
Next  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```console
Results are identical  
<Address Type="Shipping">  
  <Name>Ellen Adams</Name>  
  <Street>123 Maple Street</Street>  
  <City>Mill Valley</City>  
  <State>CA</State>  
  <Zip>10999</Zip>  
  <Country>USA</Country>  
</Address>  
<Address Type="Shipping">  
  <Name>Cristian Osorio</Name>  
  <Street>456 Main Street</Street>  
  <City>Buffalo</City>  
  <State>NY</State>  
  <Zip>98112</Zip>  
  <Country>USA</Country>  
</Address>  
<Address Type="Shipping">  
  <Name>Jessica Arnold</Name>  
  <Street>4055 Madison Ave</Street>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98112</Zip>  
  <Country>USA</Country>  
</Address>  
```  
  
## <a name="see-also"></a>関連項目

- [XPath ユーザー向けの LINQ to XML (Visual Basic)](linq-to-xml-for-xpath-users.md)
