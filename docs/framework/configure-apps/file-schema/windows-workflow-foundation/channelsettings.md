---
title: <channelSettings>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 94a4457f-f43f-458d-a47e-2d11103ee75e
ms.openlocfilehash: f6a57e2cc1e7c5e114fd38ee3534ab7c4e629b36
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152275"
---
# \<channelSettings>
チャネル キャッシュの設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<sendMessageChannelCache>**](sendmessagechannelcache.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<channelSettings>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <sendMessageChannelCache allowUnsafeCaching="Boolean">
        <channelSettings idleTimeout="TimeSpan"
                         leaseTimeout="TimeSpan"
                         maxItemsInCache="Integer" />
      </sendMessageChannelCache>
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|idleTimeout|オブジェクトが破棄されるまでにキャッシュ内でアイドル状態を維持できる最大時間を指定する TimeSpan 値。|  
|leaseTimeout|オブジェクトがキャッシュから削除されるまでの時間間隔を指定する TimeSpan 値。|  
|maxItemsInCache|キャッシュに置くことができるオブジェクトの最大数を指定する整数。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<sendMessageChannelCache>](sendmessagechannelcache.md)|キャッシュの共有レベルのカスタマイズや、チャネル ファクトリ キャッシュの設定を可能にするほか、Send メッセージング アクティビティを使用してサービス エンドポイントにメッセージを送信するワークフローのチャネル キャッシュの設定も可能にするサービス動作。|  
  
## <a name="remarks"></a>解説  
 このサービス動作は、サービス エンドポイントにメッセージを送信するワークフローを対象としています。 これらのワークフローは、通常はクライアント ワークフローですが、<xref:System.ServiceModel.WorkflowServiceHost> でホストされるワークフロー サービスである場合もあります。  
  
 既定では、<xref:System.ServiceModel.WorkflowServiceHost> によってホストされるワークフローでは、<xref:System.ServiceModel.Activities.Send> メッセージング アクティビティが使用するキャッシュは <xref:System.ServiceModel.WorkflowServiceHost> のすべてのワークフロー インスタンス間で共有されます (ホストレベルのキャッシュ)。 <xref:System.ServiceModel.WorkflowServiceHost> によってホストされないクライアント ワークフローの場合、キャッシュを使用できるのはワークフロー インスタンスだけです (インスタンスレベルのキャッシュ)。 構成でエンドポイントが定義されているワークフローに送信アクティビティがある場合、キャッシュは既定で無効になります。  
  
 チャネルファクトリおよびチャネルキャッシュの既定のキャッシュ共有レベルとキャッシュ設定を変更する方法の詳細については、「 [Send アクティビティのキャッシュ共有レベルの変更](../../../wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md)」を参照してください。  
  
## <a name="example"></a>例  
 ホストされたワークフロー サービスでは、ファクトリ キャッシュとチャネル キャッシュの設定をアプリケーション構成ファイルで指定できます。 これを行うには、ファクトリ キャッシュおよびチャネル キャッシュのキャッシュ設定を含むサービス動作を追加し、そのサービス動作をサービスに追加します。 次の例は、 `MyChannelCacheBehavior` カスタムファクトリキャッシュとチャネルキャッシュ設定を使用したサービス動作を含む構成ファイルの内容を示しています。 このサービス動作は、属性を通じてサービスに追加され `behaviorConfiguration` ます。  
  
```xml  
<configuration>
  <system.serviceModel>  
    <!-- List of other config sections here -->
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.SendMessageChannelCache>
- <xref:System.ServiceModel.Activities.Configuration.SendMessageChannelCacheElement>
- <xref:System.ServiceModel.Activities.Send>
- <xref:System.ServiceModel.Activities.ChannelCacheSettings>
- [Send アクティビティのキャッシュ共有レベルの変更](../../../wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md)
