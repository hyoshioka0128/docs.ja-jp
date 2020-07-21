---
title: DOM への新しいノードの作成
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
ms.openlocfilehash: d99a3c68c7554ab266d71a4cbf2e676bc6db8cbc
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289578"
---
# <a name="create-new-nodes-in-the-dom"></a>DOM への新しいノードの作成
<xref:System.Xml.XmlDocument> には、すべてのノード型に対応する Create メソッドがあります。 このメソッドに、名前が必要な場合は名前を渡し、コンテンツを持つノードではコンテンツやその他のパラメーターを指定すると、そのノードが作成されます。コンテンツを持つノードには、たとえばテキスト ノードがあります。 次のメソッドは、ノードを適切に作成するために、名前といくつかのパラメーターの指定が必要なメソッドです。  
  
- <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
- <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
- <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
- <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
- <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 その他のノード型では、パラメーターにデータを与えるだけでなく、他の要件を満たす必要もあります。  
  
 属性の詳細については、「[DOM の要素に対する新しい属性の作成](creating-new-attributes-for-elements-in-the-dom.md)」を参照してください。 要素名と属性名の検証については、「[新しいノードの作成時における XML 要素名および属性名の検証](xml-element-and-attribute-name-verification-when-creating-new-nodes.md)」を参照してください。 エンティティ参照の作成については、「[新しいエンティティ参照の作成](creating-new-entity-references.md)」を参照してください。 エンティティ参照の展開における名前空間の影響については、「[要素と属性を含む新しいノードでのエンティティ参照の展開に対する名前空間の影響](namespace-affect-on-entity-ref-expansion-for-new-nodes.md)」を参照してください。  
  
 新しく作成したノードをツリーに挿入するには、いくつかのメソッドを使用できます。 使用できるメソッドと、そのメソッドによって DOM のどこに新しいノードが作成されるかの説明を次の表に示します。  
  
|メソッド|ノードの位置|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|参照ノードの前に挿入されます。 たとえば、5 番目の位置に新しいノードを挿入するには、次のようにします。<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> 詳細については、<xref:System.Xml.XmlNode.InsertBefore%2A> メソッドを参照してください。|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|参照ノードの後に挿入されます。 次に例を示します。<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> 詳細については、<xref:System.Xml.XmlNode.InsertAfter%2A> メソッドを参照してください。|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|当該ノードの子ノードのリストの末尾にノードを追加します。 追加するノードが <xref:System.Xml.XmlDocumentFragment> の場合は、ドキュメント フラグメントの内容全体がこのノードの子リストに移動されます。 詳細については、<xref:System.Xml.XmlNode.AppendChild%2A> メソッドを参照してください。|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|当該ノードの子ノードのリストの先頭にノードを追加します。 追加するノードが <xref:System.Xml.XmlDocumentFragment> の場合は、ドキュメント フラグメントの内容全体がこのノードの子リストに移動されます。 詳細については、<xref:System.Xml.XmlNode.PrependChild%2A> メソッドを参照してください。|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|要素に関連付けられている属性コレクションの末尾に <xref:System.Xml.XmlAttribute> ノードを追加します。 詳細については、<xref:System.Xml.XmlAttributeCollection.Append%2A> メソッドを参照してください。|  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
