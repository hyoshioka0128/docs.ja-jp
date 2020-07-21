---
title: <trackingProfile>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 154830ff-ddd3-4397-a3b5-5b334907777f
ms.openlocfilehash: 8985da7e1223ac117cf1b68227140634f9c85d3a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79151890"
---
# \<trackingProfile>
追跡参加要素内でワークフロー追跡レコードのサブスクリプションを作成するための、構成セクションを表します。 追跡プロファイルには、実行時にワークフロー インスタンスの状態が変化したときに生成されるワークフロー イベントを追跡参加要素が定期受信できるようにする、追跡クエリが含まれています。 追跡プロファイル セクション内で定義されたクエリでは、サブスクリプションによって返されるイベントの種類が定義されます。  
  
 ワークフロー追跡とその構成の詳細については、「[ワークフローの追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)」と「[追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<trackingProfile>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.serviceModel>
  <tracking>
    <profiles>
      <participants>
        <add name="String"
             profileName="String"
             type="String" />
      </participants>
      <trackingProfile name="String">
        <workflow activityDefinitionId="String">
          <activityScheduledQueries>
            <activityScheduledQuery activityName="String"
                                    childActivityName="String"/>
          </activityScheduledQueries>
          <activityStateQueries>
            <activityStateQuery activityName="String" />
            <arguments>
              <argument name="String" />
            </arguments>
            <states>
              <state name="String"  />
            </states>
            <variables>
              <variable name="String" />
            </variables>
          </activityStateQueries>
          <bookmarkResumptionQueries>
            <bookmarkResumptionQuery name="String" />
          </bookmarkResumptionQueries>
          <cancelRequestQueries>
            <cancelRequestQuery activityName="String"
                                childActivityName="String"/>
          </cancelRequestQueries>
          <customTrackingQueries>
            <customTrackingQuery activityName="String"
                                 name="String"/>
          </customTrackingQueries>
          <faultPropagationQueries>
            <faultPropagationQuery activityName="String"
                                   faultHandlerActivityName="String" />
          </faultPropagationQueries>
          <workflowInstanceQueries>
            <workflowInstanceQuery>
              <states>
                <state name="String" />
              </states>
            </workflowInstanceQuery>
          </workflowInstanceQueries>
        </workflow>
      </trackingProfile>
    </profiles>
  </tracking>
</system.serviceModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|name|追跡プロファイルの名前を指定する文字列。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<participants>](participants.md)|<xref:System.ServiceModel.Activities.Tracking.Configuration.ProfileWorkflowElement.ActivityDefinitionId%2A?displayProperty=nameWithType> プロパティによって識別される特定のワークフローのすべてのクエリを格納する構成要素。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<tracking>](tracking.md)|ワークフロー サービスの追跡設定を定義する構成セクションを表します。|  
  
## <a name="remarks"></a>解説  
 追跡プロファイルには、実行時にワークフロー インスタンスの状態が変化したときに生成されるワークフロー イベントを追跡参加要素が定期受信できるようにする、追跡クエリが含まれています。 監視の要件に応じて、ワークフローの主な状態変化の少数のセットを定期受信する、大まかなプロファイルを作成できます。 それとは反対に、結果として得られるイベントが、後で詳細な実行フローを十分に再構築できるほど豊富な、詳細なプロファイルを作成することもできます。  
  
 追跡プロファイルは、特定の追跡レコードを対象としてワークフロー ランタイムを照会できる、追跡レコード用の宣言型のサブスクリプションとして構築されます。 オブジェクトのさまざまなクラスをサブスクライブできるクエリの種類がいくつかあり <xref:System.Activities.Tracking.TrackingRecord> ます。 クエリの完全な一覧については、「」 [\<participants>](participants.md) および「[追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)」を参照してください。  
  
 次の例は、追跡参加要素がワークフローイベントとワークフローイベントをサブスクライブできるようにする、構成ファイル内の追跡プロファイルを示して `Started` `Completed` います。  
  
```xml  
<system.serviceModel>  
  <tracking>
    <trackingProfile name="Sample Tracking Profile">  
      <workflow activityDefinitionId="*">  
         <workflowInstanceQueries>  
            <workflowInstanceQuery>  
            <states>  
              <state name="Started"/>  
              <state name="Completed"/>  
            </states>  
          </workflowInstanceQuery>  
        </workflowInstanceQueries>  
      </workflow>  
    </trackingProfile>
   </profiles>  
  </tracking>  
</system.serviceModel>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ProfileElement>
- <xref:System.Activities.Tracking.TrackingProfile>
- [ワークフロー追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)
