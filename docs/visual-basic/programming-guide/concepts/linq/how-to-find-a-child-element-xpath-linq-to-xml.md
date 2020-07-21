---
title: '方法: 子要素を検索する (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: adb46c98-a650-42e2-b62d-835920fe8421
ms.openlocfilehash: 1b0a3af5a1679643d73649f9de6b1dc3c44cbb0d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357168"
---
# <a name="how-to-find-a-child-element-xpath-linq-to-xml-visual-basic"></a>方法: 子要素を検索する (XPath-LINQ to XML) (Visual Basic)
このトピックでは、XPath の子要素軸と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<xref:System.Xml.Linq.XContainer.Element%2A> メソッドを比較します。  
  
 XPath 式は `DeliveryNotes` です。  
  
## <a name="example"></a>例  
 この例では、`DeliveryNotes` 子要素を検索します。  
  
 この例では、次の XML ドキュメントを使用します。「[サンプル XML ファイル:複数の購買発注書 (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。  
  
```vb  
Dim cpo As XDocument = XDocument.Load("PurchaseOrders.xml")  
Dim po As XElement = cpo.Root.<PurchaseOrder>.FirstOrDefault  
  
'LINQ to XML query  
Dim el1 As XElement = po.<DeliveryNotes>.FirstOrDefault  
  
' XPath expression  
Dim el2 As XElement = po.XPathSelectElement("DeliveryNotes")  
' same as "child::DeliveryNotes"  
' same as "./DeliveryNotes"  
  
If el1 Is el2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(el1)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```console
Results are identical  
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>  
```  
  
## <a name="see-also"></a>関連項目

- [XPath ユーザー向けの LINQ to XML (Visual Basic)](linq-to-xml-for-xpath-users.md)
