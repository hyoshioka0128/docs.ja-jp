---
title: <namedCaches> の <add> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- add element for <namedCaches>
- <add> element for <namedCaches>
ms.assetid: ce2a63a8-c829-4742-a6ea-72ee5d89f169
ms.openlocfilehash: c1345022b79df371ad9c89a39a0a8b625e26608c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154506"
---
# <a name="add-element-for-namedcaches"></a>\<namedCaches> の \<add> 要素
`namedCache`メモリキャッシュのコレクションにエントリを追加し `namedCaches` ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.caching>**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<memoryCache>**](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<namedCaches>**](namedcaches-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<namedCaches>  
    <add name="Default" />  
      <!-- child elements -->  
 </namedCaches>  
```  
  
## <a name="type"></a>Type  
 `None`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|-|-|  
|`CacheMemoryLimitMegabytes`|のインスタンスを拡張できる最大許容サイズ (メガバイト単位) を指定する整数値 <xref:System.Runtime.Caching.MemoryCache> 。 既定値は0です。これは、 <xref:System.Runtime.Caching.MemoryCache> クラスの自動サイズ調整ヒューリスティックが既定で使用されることを意味します。|  
|`Name`|キャッシュの名前。|  
|`PhysicalMemoryLimitPercentage`|物理的にインストールされたコンピューターメモリのうち、キャッシュで使用できる最大パーセンテージを指定する 0 ~ 100 の整数値。 既定値は0です。これは、 <xref:System.Runtime.Caching.MemoryCache> クラスの自動サイズ調整ヒューリスティックが既定で使用されることを意味します。|  
|`PollingInterval`|時間間隔を示す値。この値を超えると、キャッシュの実装によりキャッシュ インスタンスに設定されている絶対およびパーセントのメモリ制限と現在のメモリ負荷が比較されます。 この値は、"HH: MM: SS" 形式で入力します。|  
  
### <a name="child-elements"></a>子要素  
 `None`  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<namedCaches>](namedcaches-element-cache-settings.md)|名前付きインスタンスの構成設定のコレクションを格納 <xref:System.Runtime.Caching.MemoryCache> します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `add` メモリキャッシュのコレクションにエントリを追加し `namedCaches` ます。 要素を使用する前に[clear](clear-element-for-namedcaches.md)要素を使用して、 `add` コレクション内に他の名前付きキャッシュが存在しないことを確認できます。 この要素は、machine.config ファイルと web.config ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、 `namedCache` メモリキャッシュのコレクションに対する既定のエントリの設定を定義する方法を示して `namedCaches` います。  
  
```xml  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="Default"
               cacheMemoryLimitMegabytes="0"
               physicalMemoryPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [\<namedCaches>要素 (キャッシュ設定)](namedcaches-element-cache-settings.md)
