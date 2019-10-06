---
title: <defaultHttpCachePolicy> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultHttpCachePolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultHttpCachePolicy
helpviewer_keywords:
- defaultHttpCachePolicy element
- <defaultHttpCachePolicy> element
ms.assetid: 2c1247d0-39b0-4c12-919a-a925ce075c79
ms.openlocfilehash: f3b029e8b931e976bee85c98dd926e020c5b8743
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698277"
---
# <a name="defaulthttpcachepolicy-element-network-settings"></a>\<defaultHttpCachePolicy> 要素 (ネットワーク設定)
HTTP キャッシュがアクティブかどうか、および既定のキャッシュポリシーについて説明します。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t 47 >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t @ no__t-2 @ no__t-3[ **\<requestcaching >** ](requestcaching-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 **\<defaultHttpCachePolicy >** を行います。  
  
## <a name="syntax"></a>構文  
  
```xml  
<defaultHttpCachePolicy  
  policyLevel="BypassCache|Default"  
  minimumFresh="d.hh:mm:ss|minValue|maxValue"  
  maximumAge="d.hh:mm:ss|minValue|maxValue"  
  maximumStale="d.hh:mm:ss|minValue|maxValue"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`maximumAge`|キャッシュされたオブジェクトを期限切れとしてマークするまでの最大時間間隔を指定します。|  
|`maximumStale`|キャッシュされたオブジェクトを期限切れとしてマークするまでの、計算された鮮度時間を超える最大時間を指定します。|  
|`minimumFresh`|キャッシュされたオブジェクトが最新であると見なされるための最小時間を指定します。|  
|`policyLevel`|キャッシュポリシーが自動であるかどうか、またはキャッシュをバイパスするかどうかを指定します。 既定値は `BypassCache` です。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[requestCaching](requestcaching-element-network-settings.md)|ネットワーク要求のキャッシュメカニズムを制御します。|  
  
## <a name="remarks"></a>コメント  
 @No__t-0 属性の値は、`BypassCache` または `Default` のいずれかです。  
  
 @No__t-0、`maximumStale`、`minimumFresh` の各要素の値は、明示的な時間間隔であり、形式は*d*です。*hh*:*mm*:*ss* (日数、時間、分、秒)、または必要に応じて `minValue` または `maxValue` の定数。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、6時間、最長有効期間、および最大4時間の最長時間を指定する方法を示します。  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultHttpCachePolicy  
        minimumFresh="0.06:00:00"  
        maximumAge="2.00:00:00"  
        maximumStale="0.04:00:00"
      />  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Cache>
- <xref:System.Net.WebRequest>
- <xref:System.Net.Cache.RequestCacheLevel>
- [ネットワーク設定スキーマ](index.md)
