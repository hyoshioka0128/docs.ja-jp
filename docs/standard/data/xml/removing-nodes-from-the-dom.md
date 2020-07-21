---
title: DOM からのノードの削除
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 0a98e0ca-0555-45c1-ab69-0d8d20ca1abd
ms.openlocfilehash: 5df95700bb1e84aa5f3adcc752b2314dc964477b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288642"
---
# <a name="removing-nodes-from-the-dom"></a>DOM からのノードの削除
XML ドキュメント オブジェクト モデル (DOM) からノードを削除するには、<xref:System.Xml.XmlNode.RemoveChild%2A> メソッドを使用して特定のノードを削除します。 ノードを削除すると、削除しようとしたノードがリーフ ノードでない場合は、そのノードに含まれるサブツリーも削除されます。  
  
 DOM から複数のノードを削除するには、<xref:System.Xml.XmlNode.RemoveAll%2A> メソッドを使用します。現在のノードに子や属性があれば、それらがすべて削除されます。  
  
 <xref:System.Xml.XmlNamedNodeMap> を使用している場合は、<xref:System.Xml.XmlNamedNodeMap.RemoveNamedItem%2A> メソッドを使用してノードを削除できます。  
  
 属性を削除するには、「[DOM の要素ノードからの属性の削除](removing-attributes-from-an-element-node-in-the-dom.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
