---
title: <serviceDiscovery>
ms.date: 03/30/2017
ms.assetid: a3c68a4a-fc95-43c5-aacb-785936c0cf39
ms.openlocfilehash: 7ac067e84f2a4d2724e3d8f2d0af9b220fd15538
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399648"
---
# \<serviceDiscovery>
サービス エンドポイントの探索可能性を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceDiscovery>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <serviceDiscovery>
        <announcementEndpoints>
          <endpoint name="String"
                    kind="Type" />
        </announcementEndpoints>
        <discoveryEndpoints>
          <endpoint name="String"
                    kind="Type" />
        </discoveryEndpoints>
      </serviceDiscovery>
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<announcementEndpoint>](announcementendpoint.md)|アナウンス エンドポイントのコレクション。 このセクションを使用して、アナウンス メッセージの送信に使用するエンドポイントを指定します。|  
|[\<discoveryEndpoint>](discoveryendpoint.md)|探索エンドポイントのコレクション。 このセクションを使用して、探索メッセージをリッスンするエンドポイントを指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|動作の要素を指定します。|  
  
## <a name="remarks"></a>解説  
 サービスの動作構成に追加すると、この構成要素により、サービスの探索可能性はすべてのエンドポイントで有効になります。 または子要素を使用して、このようなエンドポイントの探索機能をさらに構成でき [\<discoveryEndpoint>](discoveryendpoint.md) [\<announcementEndpoint>](announcementendpoint.md) ます。 [\<announcementEndpoint>](announcementendpoint.md)サービスのお知らせを送信するために使用するエンドポイント構成 (オンライン/Hello およびオフライン/Bye) を指定することにより、セクションを使用してアナウンスを構成します。 [\<discoveryEndpoint>](discoveryendpoint.md)探索メッセージをリッスンするエンドポイントを手動で指定するには、「」セクションを使用します。  
  
## <a name="example"></a>例  
 次の構成例では、CalculatorService を探索可能に指定しています。また、オプションで、使用するアナウンス エンドポイントを指定しています。  
  
```xml  
<services>
  <service name="CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    ...
  </service>
</services>
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <serviceDiscovery>
        <announcementEndpoints>
          <endpoint name="udpEndpoint"
                    kind="udpAnnouncementEndpoint" />
        </announcementEndpoints>
      </serviceDiscovery>
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>
