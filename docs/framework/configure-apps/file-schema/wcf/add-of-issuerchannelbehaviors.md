---
title: <add> の <issuerChannelBehaviors>
ms.date: 03/30/2017
ms.assetid: 50710506-e28f-45dd-ab7e-bff6f44173db
ms.openlocfilehash: cf7ac2691ad1c641352a8047373ced538b19e983
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398331"
---
# <a name="add-of-issuerchannelbehaviors"></a>\<add> の \<issuerChannelBehaviors>

STS と通信するときに使用されるエンドポイントの動作を追加します。

> [!NOTE]
> いずれかのエンドポイント動作に要素が含まれている場合は [\<clientCredentials>](clientcredentials.md) 、例外がスローされます。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedToken>**](issuedtoken.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuerChannelBehaviors>**](issuerchannelbehaviors-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  

## <a name="syntax"></a>構文

```xml
<add issuerAddress="string"
     behaviorConfiguration="string" />
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|issuerAddress|通信するためのセキュリティ トークン発行者の URI。|
|behaviorConfiguration|同じ構成ファイルに定義されたエンドポイントの動作の名前。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|[\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)|指定されたサービストークンサービスと通信するときに使用される Windows Communication Foundation (WCF) クライアントエンドポイントの動作のコレクションを格納します。|

## <a name="remarks"></a>解説

`issuerAddress` には、クライアントの通信相手となるセキュリティ トークン サービスの URI が含まれます。 `behaviorConfiguration`セキュリティトークンサービスから発行済みトークンを取得するために Windows Communication Foundation (WCF) によって作成されたチャネルでアプリケーションが使用するエンドポイント動作を指します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.IssuerChannelBehaviors%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElement>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElementCollection>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuerChannelBehaviors%2A>
- [サービス ID と認証](../../../wcf/feature-details/service-identity-and-authentication.md)
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [方法: フェデレーション クライアントを作成する](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [方法: ローカル発行者を設定する](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)
