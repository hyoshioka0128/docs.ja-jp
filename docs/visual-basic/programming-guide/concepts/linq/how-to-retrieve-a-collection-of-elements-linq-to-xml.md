---
title: '方法: 要素のコレクションを取得する (LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 2269f9de-8fb9-4666-b8a1-a4e754fa6a81
ms.openlocfilehash: 13aa9ce10df1e23ba5191b523db0272aa52ea581
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397870"
---
# <a name="how-to-retrieve-a-collection-of-elements-linq-to-xml-visual-basic"></a>方法: 要素のコレクションを取得する (LINQ to XML) (Visual Basic)
このトピックでは、<xref:System.Xml.Linq.XContainer.Elements%2A> メソッドについて説明します。 このメソッドは、要素の子要素のコレクションを取得します。  
  
## <a name="example"></a>例  
 この例では、`purchaseOrder` 要素の子要素を反復処理します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:一般的な購買発注書 (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md) を使用します。  
  
```vb  
Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
Dim childElements As IEnumerable(Of XElement)  
childElements = _  
    From el In po.Elements() _  
    Select el  
For Each el As XElement In childElements  
    Console.WriteLine("Name: " & el.Name.ToString())  
Next  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```console  
Name: Address  
Name: Address  
Name: DeliveryNotes  
Name: Items  
```  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (Visual Basic)](linq-to-xml-axes.md)
