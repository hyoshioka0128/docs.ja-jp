---
title: <memoryCache> 要素 (キャッシュ設定)
ms.date: 03/30/2017
helpviewer_keywords:
- <memoryCache> element
- caching [.NET Framework], configuration
- memoryCache element
ms.assetid: 182a622f-f7cf-472d-9d0b-451d2fd94525
ms.openlocfilehash: 94c21e0408b7616bf0c8a24267b72bfa7cc3aaa0
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153985"
---
# <a name="memorycache-element-cache-settings"></a>\<memoryCache> 要素 (キャッシュ設定)
<xref:System.Runtime.Caching.MemoryCache> クラスに基づくキャッシュを構成するために使用される要素を定義します。 <xref:System.Runtime.Caching.Configuration.MemoryCacheElement> クラスは、キャッシュの構成に使用できる [memoryCache](memorycache-element-cache-settings.md) 要素を定義します。 <xref:System.Runtime.Caching.MemoryCache> クラスの複数のインスタンスを、単一のアプリケーションで使用できます。 構成ファイル内の各 `memoryCache` 要素には、指定した <xref:System.Runtime.Caching.MemoryCache> インスタンスの設定を含むことができます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.caching>**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<memoryCache>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<memoryCache>
    <namedCaches>  
        <!-- child elements -->  
    </namedCaches>
</memoryCache>  
```  
  
## <a name="type"></a>Type  
 <xref:System.Runtime.Caching.MemoryCache> クラス。  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`CacheMemoryLimitMegabytes`|<xref:System.Runtime.Caching.MemoryCache> オブジェクトのインスタンスを拡張できる最大メモリ サイズ (メガバイト)。 既定値は 0 であり、これは <xref:System.Runtime.Caching.MemoryCache> クラスの自動サイズ調整ヒューリスティックが既定で使用されることを意味します。|  
|`Name`|キャッシュ構成の名前。|  
|`PhysicalMemoryLimitPercentage`|キャッシュが使用できる物理メモリの割合。 既定値は 0 であり、これは <xref:System.Runtime.Caching.MemoryCache> クラスの自動サイズ調整ヒューリスティックが既定で使用されることを意味します。|  
|`PollingInterval`|時間間隔を示す値。この値を超えると、キャッシュの実装によりキャッシュ インスタンスに設定されている絶対およびパーセントのメモリ制限と現在のメモリ負荷が比較されます。 値は "HH:MM:SS" 形式で入力します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<namedCaches>](namedcaches-element-cache-settings.md)|`namedCache` インスタンスの構成設定のコレクションが含まれます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素を指定します。|  
|[\<system.runtime.caching>](system-runtime-caching-element-cache-settings.md)|.NET Framework に組み込まれているアプリケーションに出力キャッシュを実装できる型が含まれています。|  
  
## <a name="remarks"></a>解説  
 <xref:System.Runtime.Caching.MemoryCache> クラスは、抽象 <xref:System.Runtime.Caching.ObjectCache> クラスの具象実装です。 <xref:System.Runtime.Caching.MemoryCache> クラスのインスタンスには、アプリケーション構成ファイルの構成情報を指定することができます。 [memoryCache](memorycache-element-cache-settings.md) 構成セクションには、 `namedCaches` の構成コレクションが含まれます。  
  
 メモリ ベースのキャッシュ オブジェクトが初期化されると、まず、メモリ キャッシュ コンストラクターに渡されるパラメーターの名前と一致する `namedCaches` のエントリの検索が試行されます。 `namedCaches` のエントリが見つかると、ポーリングとメモリ管理の情報が構成ファイルから取得されます。  
  
 次に、初期化プロセスで、コンストラクターの構成情報にある名前/値ペアの任意のコレクションを使用して、構成エントリがオーバーライドされているかどうかが確認されます。 名前/値ペアのコレクションの、次の値のいずれかを渡すと、構成ファイルから取得した情報をその値がオーバーライドします。  
  
- <xref:System.Runtime.Caching.Configuration.MemoryCacheElement.CacheMemoryLimitMegabytes%2A>  
  
- <xref:System.Runtime.Caching.Configuration.MemoryCacheElement.PhysicalMemoryLimitPercentage%2A>  
  
- <xref:System.Runtime.Caching.MemoryCache.PollingInterval%2A>  
  
## <a name="example"></a>例  
 次の例は、 <xref:System.Runtime.Caching.MemoryCache> 属性を "default" に設定することによって、オブジェクトの名前を既定のキャッシュオブジェクト名に設定する方法を示して `name` います。  
  
 `cacheMemoryLimitMegabytes` 属性および `physicalMemoryLimitPercentage` 属性はゼロに設定されます。 これらの属性をゼロに設定すると、 <xref:System.Runtime.Caching.MemoryCache> の自動サイズ調整ヒューリスティックが既定で使用されることになります。 キャッシュの実装では、現在のメモリ負荷と絶対およびパーセントのメモリ制限を 2 分ごとに比較する必要があります。  
  
```xml  
<configuration>  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="Default"
               cacheMemoryLimitMegabytes="0"
               physicalMemoryLimitPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Caching.MemoryCache>
- [\<system.runtime.caching>要素 (キャッシュ設定)](system-runtime-caching-element-cache-settings.md)
- [\<namedCaches>要素 (キャッシュ設定)](namedcaches-element-cache-settings.md)
