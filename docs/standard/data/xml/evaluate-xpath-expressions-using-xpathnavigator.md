---
title: XPathNavigator による Xpath 式の評価
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 2913ccf3-f932-4363-8028-9e2d22ce6093
ms.openlocfilehash: b6e18fe02a828ae307ac7ade15650d3303f2600c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287806"
---
# <a name="evaluate-xpath-expressions-using-xpathnavigator"></a>XPathNavigator による Xpath 式の評価
<xref:System.Xml.XPath.XPathNavigator> クラスは、XPath 式を評価する <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドを提供します。 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドは XPath 式を受け取って評価し、XPath 式の結果に基づいて W3C XPath 型のブール値、数字、文字列、またはノード セットを返します。  
  
## <a name="the-evaluate-method"></a>Evaluate メソッド  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドは XPath 式を受け取って評価し、XPath 式の結果に基づいて W3C XPath 型のブール値 (<xref:System.Boolean>)、数字 (<xref:System.Double>)、文字列 (<xref:System.String>)、またはノード セット (<xref:System.Xml.XPath.XPathNodeIterator>) を返します。 たとえば、<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドは数値演算メソッドで使用できます。 次のサンプル コードは、`books.xml` ファイル内の本すべての総額を計算します。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Dim query As XPathExpression = navigator.Compile("sum(//price/text())")  
Dim total As Double = CType(navigator.Evaluate(query), Double)  
Console.WriteLine(total)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
XPathExpression query = navigator.Compile("sum(//price/text())");  
Double total = (Double)navigator.Evaluate(query);  
Console.WriteLine(total);  
```  
  
 この例は、`books.xml` ファイルを入力として使用します。  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="position-and-last-functions"></a>position 関数と last 関数  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドはオーバーロードされます。 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドの 1 つは、パラメーターとして <xref:System.Xml.XPath.XPathNodeIterator> オブジェクトを受け取ります。 この特定の <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> メソッドは、現在の評価対象コンテキストを指定するノード セット引数を許可することを除き、パラメーターとして <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> オブジェクトだけを受け取る <xref:System.Xml.XPath.XPathExpression> メソッドと同じです。 XPath の `position()` 関数および `last()` 関数は現在のコンテキスト ノードに相対的であるため、これらの関数ではコンテキストが必須です。 ロケーション ステップで述語として使用される場合を除き、XPath の `position()` 関数および `last()` 関数では、ノード セットへの参照が評価のために必須です。ノード セットへの参照がない場合、`position` 関数および `last` 関数は `0` を返します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath データ モデルを使用した XML データの処理](process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator を使用した XML データの選択](select-xml-data-using-xpathnavigator.md)
- [XPathNavigator によるノードの一致](matching-nodes-using-xpathnavigator.md)
- [XPath クエリで認識されるノード型](node-types-recognized-with-xpath-queries.md)
- [XPath クエリおよび名前空間](xpath-queries-and-namespaces.md)
- [コンパイルされた XPath 式](compiled-xpath-expressions.md)
