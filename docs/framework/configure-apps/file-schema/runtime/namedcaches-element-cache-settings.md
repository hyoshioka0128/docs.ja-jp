---
title: <namedCaches> 要素 (キャッシュ設定)
ms.date: 03/30/2017
helpviewer_keywords:
- namedCaches element
- caching [.NET Framework], configuration
- <namedCaches> element
ms.assetid: 6bd4fbc5-55a6-4dc4-998b-cdcc7e023330
ms.openlocfilehash: e0640ca18d386141f3c03135019eb4fe959b5bf8
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153959"
---
# <a name="namedcaches-element-cache-settings"></a>\<namedCaches> 要素 (キャッシュ設定)
名前付きインスタンスの構成設定のコレクションを指定し <xref:System.Runtime.Caching.MemoryCache> ます。 プロパティは、構成 <xref:System.Runtime.Caching.Configuration.MemoryCacheSection.NamedCaches%2A> ファイルの1つ以上の要素から構成設定のコレクションを参照し `namedCaches` ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.caching>**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<memoryCache>**](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<namedCaches>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<namedCaches>  
  <add name="default"/>
</namedCaches>  
```  
  
## <a name="type"></a>Type  
 `None`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`cacheMemoryLimitMegabytes`|のインスタンスを拡張できる最大許容サイズを mb 単位で指定する整数値 <xref:System.Runtime.Caching.MemoryCache> 。 既定値は0です。これは、クラスの自動サイズ調整ヒューリスティックが <xref:System.Runtime.Caching.MemoryCache> 既定で使用されることを意味します。|  
|`name`|キャッシュの名前。|  
|`physicalMemoryLimitPercentage`|物理的にインストールされたコンピューターメモリのうち、キャッシュで使用できる最大パーセンテージを指定する 0 ~ 100 の整数値。 既定値は0です。これは、クラスの自動サイズ調整ヒューリスティックが <xref:System.Runtime.Caching.MemoryCache> 既定で使用されることを意味します。|  
|`pollingInterval`|時間間隔を示す値。この値を超えると、キャッシュの実装によりキャッシュ インスタンスに設定されている絶対およびパーセントのメモリ制限と現在のメモリ負荷が比較されます。 この値は、"HH: MM: SS" 形式で入力します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<add>](add-element-for-namedcaches.md)|名前付きキャッシュを、メモリ キャッシュの `namedCaches` コレクションに追加します。|  
|[\<clear>](clear-element-for-namedcaches.md)|メモリ キャッシュの `namedCaches` コレクションを消去します。|  
|[\<remove>](remove-element-for-namedcaches.md)|名前付きキャッシュ エントリを、メモリ キャッシュの `namedCaches` コレクションから削除します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素を指定します。|  
|[\<memoryCache>](memorycache-element-cache-settings.md)|<xref:System.Runtime.Caching.MemoryCache> クラスに基づくキャッシュを構成するために使用される要素を定義します。|  
|[\<system.runtime.caching>](system-runtime-caching-element-cache-settings.md)|.NET Framework に組み込まれているアプリケーションに出力キャッシュを実装できる型が含まれています。|  
  
## <a name="remarks"></a>解説  
 Web.config ファイルのメモリキャッシュ構成セクションには `add` 、コレクションの、、の各属性を含めることができ `remove` `clear` `namedCaches` ます。 各 `namedCaches` エントリは、属性によって一意に識別され `name` ます。  
  
 メモリキャッシュエントリのインスタンスを取得するには、アプリケーション構成ファイル内の情報を参照します。 既定では、構成ファイルにエントリが存在するのは既定のキャッシュインスタンスだけです。 既定のキャッシュインスタンスは、プロパティから返されるインスタンスです <xref:System.Runtime.Caching.MemoryCache.Default%2A> 。  
  
 Name 属性を "default" に設定した場合、要素は既定のメモリキャッシュインスタンスを使用します。  
  
## <a name="example"></a>例  
 次の例は、属性を "default" に設定することによって、キャッシュの名前を既定のキャッシュエントリ名に設定する方法を示して `name` います。  
  
 `cacheMemoryLimitMegabytes` 属性および `physicalMemoryPercentage` 属性はゼロに設定されます。 これらの属性を0に設定すると、クラスの自動サイズ調整ヒューリスティックが <xref:System.Runtime.Caching.MemoryCache> 使用されます。 キャッシュの実装では、現在のメモリ負荷と、絶対値および割合に基づくメモリ制限を2分ごとに比較します。  
  
```xml  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="default"
               cacheMemoryLimitMegabytes="0"
               physicalMemoryLimitPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [\<memoryCache>要素 (キャッシュ設定)](memorycache-element-cache-settings.md)
