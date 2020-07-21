---
title: <webHttp>
ms.date: 03/30/2017
ms.assetid: 1f9d0754-d41e-44ce-a298-e51cb3096c64
ms.openlocfilehash: 00644d248e6fb85d7cf712620e6ac74405e6b0c3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399158"
---
# \<webHttp>
この要素は、構成によってエンドポイントに <xref:System.ServiceModel.Description.WebHttpBehavior> を指定します。 この動作を標準のバインディングと組み合わせて使用すると [\<webHttpBinding>](webhttpbinding.md) 、Windows Communication Foundation (WCF) サービスの Web プログラミングモデルが有効になります。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<webHttp>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<webHttp />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|このプロパティが `true` に設定されている場合は、使用する最適な形式が WCF インフラストラクチャで決定されます。 形式の自動選択は、既定で、下位互換性のために無効になっています。 形式の自動選択は、プログラムで有効にすることも、構成ファイルを使用して有効にすることもできます。|  
|defaultBodyStyle|返されたメッセージの既定の本文のスタイルを指定します。 詳細については、「」 <xref:System.ServiceModel.Web.WebMessageBodyStyle> および「 [WCF Web HTTP 書式設定](../../../wcf/feature-details/wcf-web-http-formatting.md)」を参照してください。|  
|defaultOutgoingResponseFormat|メッセージの既定の送信応答形式を指定します。 詳細については、「 [WCF WEB HTTP 書式設定](../../../wcf/feature-details/wcf-web-http-formatting.md)」を参照してください。|  
|faultExceptionEnabled|内部サーバー エラー (HTTP ステータス コード: 500) が発生したときに FaultException が生成されるかどうかを指定するフラグを取得または設定します。|  
|helpEnabled| ヘルプ ページが有効かどうかを示す値を取得または設定します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|エンドポイントの動作のセットを指定します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.WebHttpElement>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [AJAX の統合と JSON のサポート](../../../wcf/feature-details/ajax-integration-and-json-support.md)
- [\<webHttpBinding>](webhttpbinding.md)
