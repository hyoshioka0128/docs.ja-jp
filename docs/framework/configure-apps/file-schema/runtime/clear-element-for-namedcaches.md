---
title: <namedCaches> の <clear> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- <clear> element for <namedCaches>
- clear element for <namedCaches>
ms.assetid: ea01a858-65da-4348-800f-5e3df59d4d79
ms.openlocfilehash: bcc0e23f0c47ad3a98430e36da31d39612caa3c9
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252756"
---
# <a name="clear-element-for-namedcaches"></a>\<namedCaches> の \<clear> 要素
`namedCache`メモリキャッシュのコレクション内のすべてのエントリをクリア `namedCaches` します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.caching>**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<memoryCache>**](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<namedCaches>**](namedcaches-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<namedCaches>  
    <clear name="Default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## <a name="type"></a>Type  
 `Type`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 `None`  
  
### <a name="child-elements"></a>子要素  
 `None`  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<namedCaches>](namedcaches-element-cache-settings.md)|名前付きインスタンスの構成設定のコレクションを格納 <xref:System.Runtime.Caching.MemoryCache> します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `clear` `namedCache` メモリキャッシュの名前付きキャッシュコレクション内のすべてのエントリをクリアします。 要素を使用して、 `clear` `add` コレクション内に他の名前付きキャッシュが存在しないことを特定するために、要素を使用して新しい名前付きキャッシュエントリを追加することができます。  
  
## <a name="see-also"></a>関連項目

- [\<namedCaches>要素 (キャッシュ設定)](namedcaches-element-cache-settings.md)
