---
title: <appDomainResourceMonitoring> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- appDomainResourceMonitoring element
- <appDomainResourceMonitoring> element
ms.assetid: 02119ab6-1e91-448e-97ad-e7b2e5c4bbbd
ms.openlocfilehash: 3c6092b6c34bb13c0ad0e66df2d3b7e65ac3de7e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154377"
---
# <a name="appdomainresourcemonitoring-element"></a>\<appDomainResourceMonitoring> 要素
プロセスのライフサイクルにおいて、プロセスのすべてのアプリケーション ドメインの統計を収集するようにランタイムに指示します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<appDomainResourceMonitoring>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<appDomainResourceMonitoring
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> アプリケーションドメインのリソース監視の統計情報をランタイムが収集するかどうかを指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|Description|  
|-----------|-----------------|  
|`true`|アプリケーションドメインのリソース監視の統計情報が収集されます。|  
|`false`|アプリケーションドメインのリソース監視の統計情報は収集されません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>解説  
 アプリケーションドメインのリソース監視は、マネージアプリケーションドメインクラス、ホスティング[ICLRAppDomainResourceMonitor](../../../unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)インターフェイス、および Windows イベントトレーシング (ETW) を介して使用できます。 監視が有効になっている場合、プロセス内のすべてのアプリケーションドメインについて、プロセスの実行中に統計が収集されます。  
  
 マネージコードからの監視を有効にするには、プロパティを使用し <xref:System.AppDomain.MonitoringIsEnabled%2A> ます。  
  
 この構成要素は、.NET Framework 4 以降でのみ使用できます。  
  
## <a name="example"></a>例  
 次の例は、アプリケーションドメインのリソース監視を有効にする方法を示しています。  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainResourceMonitoring enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>
- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
