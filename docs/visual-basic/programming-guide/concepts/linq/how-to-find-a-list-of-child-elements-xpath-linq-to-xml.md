---
title: '方法: 子要素の一覧を検索する (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 2868abfd-9f7b-412a-9cb5-f643f0fed146
ms.openlocfilehash: d03b89f93fede3abd2d482c01979e93876d60c0b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410774"
---
# <a name="how-to-find-a-list-of-child-elements-xpath-linq-to-xml-visual-basic"></a>方法: 子要素の一覧を検索する (XPath-LINQ to XML) (Visual Basic)
このトピックでは、XPath の子要素軸と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<xref:System.Xml.Linq.XContainer.Elements%2A> 軸を比較します。  
  
 XPath 式は `./*` です。  
  
## <a name="example"></a>例  
 この例では、`Address` 要素の子要素をすべて検索します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:複数の購買発注書 (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。  
  
```vb  
Dim cpo As XDocument = XDocument.Load("PurchaseOrders.xml")  
Dim po As XElement = cpo.Root.<PurchaseOrder>.<Address>.FirstOrDefault  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = po.Elements()  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = po.XPathSelectElements("./*")  
  
If (list1.Count() = list2.Count()) AndAlso _  
    (list1.Intersect(list2).Count() = list1.Count()) Then  
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
<Name>Ellen Adams</Name>  
<Street>123 Maple Street</Street>  
<City>Mill Valley</City>  
<State>CA</State>  
<Zip>10999</Zip>  
<Country>USA</Country>  
```  
  
## <a name="see-also"></a>関連項目

- [XPath ユーザー向けの LINQ to XML (Visual Basic)](linq-to-xml-for-xpath-users.md)
