---
title: <tracking>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: fd9b50ed-98a1-4518-836d-e4e02c670822
ms.openlocfilehash: 968cfa8e5402458afd6f13545ed999a472adf2e0
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79151911"
---
# \<tracking>
ワークフロー サービスの追跡設定を定義する構成セクションを表します。  
  
 ワークフロー追跡とその構成の詳細については、「ワークフローの[追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)」と「ワークフロー[の追跡の構成](../../../windows-workflow-foundation/configuring-tracking-for-a-workflow.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<tracking>**  
  
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
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<participants>](participants.md)|追跡レコードを定期受信する参加要素を定義する、構成要素のコレクション。 追跡参加要素には、追跡レコードからペイロードを処理するロジックが含まれています (たとえば、ファイルへの書き込みを選択できるなど)。|  
|[\<trackingProfile>](trackingprofile.md)|ワークフロー インスタンスで発生した追跡レコードをフィルター処理するための追跡プロファイル。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|system.ServiceModel|すべてのワークフロー構成要素のルート要素。|  
  
## <a name="remarks"></a>解説  
 追跡には、ワークフローの実行を検証する機能が用意されています。 ワークフロー追跡インフラストラクチャはワークフローをインストルメント化し、実行中の主要イベントを反映してレコードを生成します。 たとえば、ワークフロー インスタンスが開始または完了すると、追跡レコードが生成されます。 また、追跡によって、ワークフロー変数に関連付けられたビジネス関連データを抽出することもできます。 たとえば、ワークフローが注文処理システムを表している場合は、注文 ID と共に追跡レコードを抽出できます。 一般的に、WF 追跡機能を有効にすると、ワークフロー実行の診断またはビジネス分析が容易になります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection?displayProperty=nameWithType>
- [ワークフロー追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
