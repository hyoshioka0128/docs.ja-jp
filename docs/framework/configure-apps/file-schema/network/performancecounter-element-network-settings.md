---
title: <performanceCounter> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounter element
- <performanceCounter> element
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
ms.openlocfilehash: 58a2bf5118a3a2cd9c33301eca5dcc751c2351bf
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "74283092"
---
# <a name="performancecounter-element-network-settings"></a>\<performanceCounter> 要素 (ネットワーク設定)
ネットワークパフォーマンスカウンターを有効または無効にします。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<performanceCounters>**

## <a name="syntax"></a>構文  
  
```xml  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|ネットワークパフォーマンスカウンターを有効にするかどうかを指定します。 既定値は `false` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[設定](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
 ネットワーク パフォーマンス カウンターは、使用される構成ファイルで有効になっている必要があります。 すべてのネットワーク パフォーマンス カウンターは、構成ファイル内の 1 つの設定で有効または無効にされます。 ネットワーク パフォーマンス カウンターを個別に有効または無効にすることはできません。 特定のネットワークパフォーマンスカウンターの詳細については、「[ネットワークパフォーマンスカウンター](../../../debug-trace-profile/performance-counters.md#networking-performance-counters)」を参照してください。  
  
 既定値は、ネットワークパフォーマンスカウンターが無効になっていることを示します。  
  
 プロパティは、 <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType> 適用可能**な**構成ファイルから enabled 属性の現在の値を取得するために使用できます。  
  
## <a name="example"></a>例  
 次の例では、および関連する名前空間を構成して、ネットワークパフォーマンスカウンターを有効にする方法を示し <xref:System.Net> ます。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
- [ネットワークパフォーマンスカウンター](../../../debug-trace-profile/performance-counters.md#networking-performance-counters)
