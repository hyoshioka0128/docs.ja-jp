---
title: <Directives>要素 (.NET ネイティブ)
ms.date: 03/30/2017
ms.assetid: 444846f3-48d5-4341-a43e-69f7221389eb
ms.openlocfilehash: 0c6ebb8954e80f3f6dc6733f0e9d76094477689b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84202379"
---
# <a name="directives-element-net-native"></a>\<Directives>要素 (.NET ネイティブ)
.NET ネイティブのすべてのランタイムディレクティブファイルのルート要素。  
  
 `<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">`
  
## <a name="syntax"></a>構文  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <!-- child elements -->
</Directives>  
```  
  
## <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`xmlns`|XML 名前空間。 値は常に `http://schemas.microsoft.com/netfx/2013/01/metadata` です。|  
  
## <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|リフレクションで使用可能なメタデータを持つアプリケーション全体の型と型のメンバーのコンテナーとして機能します。|  
|[\<Library>](library-element-net-native.md)|実行時にメタデータを必要とする子型と型のメンバーを持つアセンブリを定義します。|  
  
## <a name="remarks"></a>解説  
 各ランタイム ディレクティブ ファイルには、`<Directives>` 要素を 1 つのみ含めることができます。  
  
 要素には、 `<Directives>` 0 個または1個の要素と、0個以上の要素を含めることができ [\<Application>](application-element-net-native.md) [\<Library>](library-element-net-native.md) ます。  
  
## <a name="see-also"></a>関連項目

- [ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス](runtime-directives-rd-xml-configuration-file-reference.md)
- [ランタイム ディレクティブ要素](runtime-directive-elements.md)
