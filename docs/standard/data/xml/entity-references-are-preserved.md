---
title: 保持されるエンティティ参照
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 000a6cae-5972-40d6-bd6c-a9b7d9649b3c
ms.openlocfilehash: e4c902df1b0cd2bd9e97b49c0ec1d10df91ef1c7
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290345"
---
# <a name="entity-references-are-preserved"></a>保持されるエンティティ参照
エンティティ参照を展開せずに保持する場合、XML ドキュメント オブジェクト モデル (DOM) は、エンティティ参照を検出すると **XmlEntityReference** ノードを構築します。  
  
 たとえば、次の XML を使用します。  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 DOM は、`&publisher;` 参照を検出すると **XmlEntityReference** ノードを構築します。 **XmlEntityReference** には、エンティティ宣言のコンテンツからコピーされた子ノードが格納されます。 上記のコード サンプルでは、エンティティ宣言にテキストが含まれているため、エンティティ参照ノードの子ノードとして **XmlText** ノードが作成されます。  
  
 ![保持されているエンティティ参照のツリー構造](media/xmlentityref-notexpanded-nodes.gif "xmlentityref_notexpanded_nodes")  
エンティティ参照が保持される場合のツリー構造  
  
 **XmlEntityReference** の子ノードは、エンティティ宣言が検出されたときに **XmlEntity** ノードから作成されたすべての子ノードのコピーです。  
  
> [!NOTE]
> **XmlEntity** からコピーされたノードは、エンティティ参照ノードの下に配置されると、必ずしも元のノードの完全なコピーにはなりません。 エンティティ参照ノードが現れた位置のスコープに名前空間が適用されていると、それが子ノードの最終的な構成に影響する可能性があります。  
  
 既定では、`&abc;` のような一般エンティティは保持され、常に **XmlEntityReference** ノードが作成されます。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
