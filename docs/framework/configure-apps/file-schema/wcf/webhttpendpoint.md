---
title: <webHttpEndpoint>
ms.date: 03/30/2017
ms.assetid: ecaaeb6f-ebd0-411d-8b53-92477cd45347
ms.openlocfilehash: 8d4f55fd5b51ea77839b7fdbb930e937f5700417
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70854801"
---
# \<webHttpEndpoint>
この構成要素は、 [\<webHttpBinding>](webhttpbinding.md) 動作を自動的に追加する固定バインドを持つ標準エンドポイントを定義し [\<webHttp>](webhttp.md) ます。 このエンドポイントは、REST サービスを作成する場合に使用します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<standardEndpoints>**](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<webHttpEndpoint>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <webHttpEndpoint>
      <standardEndpoint automaticFormatSelectionEnabled="String"
                        defaultOutgoingResponseFormat="Xml/Json"
                        helpEnabled="Boolean"
                        webEndpointType="String" />
    </webHttpEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|形式の自動選択が有効かどうかを示すブール値。<br /><br /> 形式の自動選択が有効な場合、インフラストラクチャが要求メッセージの `Accept` ヘッダーを解析し、最適な応答形式を判断します。 適切な応答形式が `Accept` ヘッダーに指定されていなかった場合は、要求メッセージの `Content-Type` または操作の既定の応答形式がインフラストラクチャによって使用されます。|  
|defaultOutgoingResponseFormat|既定の送信応答形式を指定する属性。 この属性は <xref:System.ServiceModel.Web.WebMessageFormat> 型です。|  
|helpEnabled|エンドポイントに対して HTTP ヘルプ ページが有効になっているかどうかを示すブール値。|  
|webEndpointType|エンドポイントの種類を指定する文字列。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<standardEndpoints>](standardendpoints.md)|1 つ以上のプロパティ (アドレス、バインディング、コントラクト) が固定されている、あらかじめ定義されたエンドポイントである標準エンドポイントのコレクション。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Description.WebHttpEndpoint>
- <xref:System.ServiceModel.Configuration.WebHttpEndpointElement>
