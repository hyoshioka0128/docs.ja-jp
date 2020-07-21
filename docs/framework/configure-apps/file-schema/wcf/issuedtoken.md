---
title: <issuedToken>
ms.date: 03/30/2017
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
ms.openlocfilehash: 56439748926ada642018f48a5787634a50d0f180
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "72846858"
---
# \<issuedToken>
サービスに対するクライアントの認証に使用されるカスタム トークンを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<issuedToken>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<issuedToken cacheIssuedTokens="Boolean"
             defaultKeyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
             issuedTokenRenewalThresholdPercentage = "0 to 100"
             issuerChannelBehaviors="String"
             localIssuerChannelBehaviors="String"
             maxIssuedTokenCachingTime="TimeSpan">
</issuedToken>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`cacheIssuedTokens`|トークンがキャッシュされるかどうかを指定する省略可能なブール属性。 既定値は、`true` です。|  
|`defaultKeyEntropyMode`|ハンドシェイク操作に使用されるランダム値 (エントロピ) を指定する省略可能な文字列属性。 値には、`ClientEntropy`、`ServerEntropy`、および `CombinedEntropy` があります。既定値は `CombinedEntropy` です。 この属性は <xref:System.ServiceModel.Security.SecurityKeyEntropyMode> 型です。|  
|`issuedTokenRenewalThresholdPercentage`|トークンが更新されるまでに待機できる有効な期間 (トークン発行者によって提供される) のパーセンテージを指定する省略可能な整数属性。 値は 0 ～ 100 の範囲です。 既定値は 60 で、更新の実行までに待機できる期間の 60% を示します。|  
|`issuerChannelBehaviors`|発行者との通信時に使用するチャネル動作を指定する省略可能な属性。|  
|`localIssuerChannelBehaviors`|ローカル発行者との通信時に使用するチャネル動作を指定する省略可能な属性。|  
|`maxIssuedTokenCachingTime`|トークン発行者 (STS) が期間を指定しない場合に、発行済みトークンがキャッシュされる期間を指定する省略可能な Timespan 属性。 既定値は "10675199.02:48: 05.4775807" です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<localIssuer>](localissuer.md)|トークンのローカル発行者のアドレスと、エンドポイントとの通信に使用されるバインディングを指定します。|  
|[\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)|ローカル発行者に接続するときに使用するエンドポイント動作を指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|サービスに対するクライアントの認証に使用される資格情報を指定します。|  
  
## <a name="remarks"></a>解説  
 発行済みトークンは、フェデレーション シナリオでセキュリティ トークン サービス (STS) を使用して認証するときに使用されるカスタム資格情報の種類です。 既定ではトークンは、SAML トークンです。 詳細については、「[フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)」、および「[フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)」を参照してください。  
  
 このセクションには、トークンのローカル発行者やセキュリティ トークン サービスで使用する動作の構成に使用する要素が含まれます。 ローカル発行者を使用するようにクライアントを構成する方法については、「[方法: ローカル発行者を構成](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)する」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>
- <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [方法: フェデレーション クライアントを作成する](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [方法: ローカル発行者を設定する](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
