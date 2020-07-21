---
title: <issuedTokenParameters>
ms.date: 03/30/2017
ms.assetid: 120b3f37-7331-4816-b712-d6aab39655a4
ms.openlocfilehash: 8432463ff62e4b5e54a491b574cc6a5285efe220
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70397953"
---
# \<issuedTokenParameters>
フェデレーション セキュリティのシナリオで発行されるセキュリティ トークンのパラメーターを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<issuedTokenParameters>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<issuedTokenParameters defaultMessageSecurityVersion="System.ServiceModel.MessageSecurityVersion"
                       inclusionMode="AlwaysToInitiator/AlwaysToRecipient/Never/Once"
                       keySize="Integer"
                       keyType="AsymmetricKey/BearerKey/SymmetricKey"
                       tokenType="String">
  <additionalRequestParameters />
  <claimTypeRequirements>
    <add claimType="URI"
         isOptional="Boolean" />
  </claimTypeRequirements>
  <issuer address="String"
          binding="" />
  <issuerMetadata address="String" />
</issuedTokenParameters>
```  
  
## <a name="type"></a>Type  
 `Type`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|defaultMessageSecurityVersion|バインドでサポートする必要があるセキュリティ仕様 (WS-Security、WS-Trust、WS-Secure Conversation、および WS-Security Policy) のバージョンを指定します。 この値は、<xref:System.ServiceModel.MessageSecurityVersion> 型です。|  
|inclusionMode|トークン包含要件を指定します。 この属性は <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode> 型です。|  
|keySize|トークン キー サイズを指定する整数。 既定値は 256 です。|  
|keyType|キーの型を指定する <xref:System.IdentityModel.Tokens.SecurityKeyType> の有効な値。 既定値は、`SymmetricKey` です。|  
|tokenType|トークンの種類を指定する文字列。 既定値は "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAML" です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<additionalRequestParameters>](additionalrequestparameters-element.md)|追加の要求パラメーターを指定する構成要素のコレクション。|  
|[\<claimTypeRequirements>](claimtyperequirements-element.md)|必須のクレームの種類のコレクションを指定します。<br /><br /> フェデレーション シナリオでは、サービスが受信資格情報についての要件を記述します。 たとえば、受信資格情報は、特定のクレーム タイプのセットを処理する必要があります。 このコレクションの要素はそれぞれ、フェデレーション資格情報に表示されると予想される必須の要求および省略可能な要求の種類を指定します。|  
|[\<issuer>](issuer-of-issuedtokenparameters.md)|現在のトークンを発行するエンドポイントを指定する構成要素。|  
|[\<issuerMetadata>](issuermetadata-of-issuedtokenparameters.md)|トークン発行者のメタデータのエンドポイント アドレスを指定する構成要素。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|セキュリティで保護されたメッセージ交換サービスの開始に使用される既定値を指定します。|  
|[\<security>](security-of-custombinding.md)|カスタム バインドのセキュリティ オプションを指定します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [カスタム バインディング セキュリティ](../../../wcf/samples/custom-binding-security.md)
- [サービス ID と認証](../../../wcf/feature-details/service-identity-and-authentication.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [カスタム バインディングを使用したセキュリティ機能](../../../wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
