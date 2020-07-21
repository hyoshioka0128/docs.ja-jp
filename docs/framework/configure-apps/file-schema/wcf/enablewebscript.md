---
title: <enableWebScript>
ms.date: 03/30/2017
ms.assetid: 9c7e96e1-af70-4e6e-ac5c-d67929dddbaa
ms.openlocfilehash: 20c0057c80b668df97379d0168bb7c005d9927ce
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400384"
---
# \<enableWebScript>
この要素は、ASP.NET AJAX Web ページからサービスを使用できるようにするエンドポイントの動作を有効にします。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<enableWebScript>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<enableWebScript />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 [なし] :  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|エンドポイントの動作のセットを指定します。|  
  
## <a name="remarks"></a>解説  
 この動作は、 [\<webHttpBinding>](webhttpbinding.md) 標準バインディングまたはバインディング要素と組み合わせて使用する必要があり [\<webMessageEncoding>](webmessageencoding.md) ます。  この動作の詳細については、「<xref:System.ServiceModel.Description.WebScriptEnablingBehavior>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.WebScriptEnablingElement>
- <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>
- [AJAX の統合と JSON のサポート](../../../wcf/feature-details/ajax-integration-and-json-support.md)
- [\<webHttp>](webhttp.md)
