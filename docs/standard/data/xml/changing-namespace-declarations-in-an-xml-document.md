---
title: XML ドキュメントの名前空間宣言の変更
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
ms.openlocfilehash: e55486feeb427c95a9394ac83758e6052603921e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291579"
---
# <a name="changing-namespace-declarations-in-an-xml-document"></a>XML ドキュメントの名前空間宣言の変更
**XmlDocument** は、名前空間宣言と **xmlns** 属性をドキュメント オブジェクト モデルの一部として公開します。 名前空間宣言と xmlns 属性は **XmlDocument** に格納されるため、ドキュメントの保存時にはこれらの属性の場所を保持できます。 これらの属性を変更しても、ツリーに既に存在する別のノードの **Name**、**NamespaceURI**、**Prefix** プロパティは影響を受けません。 たとえば、次のドキュメントを読み込むと、`test` 要素の **NamespaceURI** は `123.` になります。  
  
```xml  
<test xmlns="123"/>  
```  
  
 その後、次のように `xmlns` 要素を削除しても、`test` 要素の **NamespaceURI** は `123` のまま変わりません。  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 同様に、次のように別の `xmlns` 属性を `doc` 要素に追加しても、`test` 要素の **NamespaceURI** は `123` のまま変わりません。  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456")
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 つまり、`xmlns` 属性を変更しても、**XmlDocument** オブジェクトを保存して再び読み込むまで、プロパティは影響を受けません。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
