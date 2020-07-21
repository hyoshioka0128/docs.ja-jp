---
title: <identity>
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: 15c9e38a141fc294c47863b1a932711444ac079a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855156"
---
# \<identity>
ID 要素を使用すると、クライアント開発者は予想されるサービスの ID をデザイン時に指定できます。 クライアントとサービスの間のハンドシェイクプロセスでは、Windows Communication Foundation (WCF) インフラストラクチャによって、予期されるサービスの id がこの要素の値と一致することが保証されるため、認証することができます。 詳細については、「[サービス id と認証](../../../wcf/feature-details/service-identity-and-authentication.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<identity>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<identity>
  <certificate encodedValue="String" />
  <certificateReference findValue="String"
                        isChainIncluded="Boolean"
                        storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                        storeLocation="LocalMachine/CurrentUser"
                        X509FindType="Enumeration" />
  <dns value="String" />
  <rsa value="String" />
  <servicePrincipalName value="String" />
  <userPrincipalName value="String" />
</identity>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|証明書 (certificate)|X.509 証明書の設定を指定します。 この要素は <xref:System.ServiceModel.Configuration.CertificateElement> 型です。 この要素には、この証明書でエンコードされる値を指定する文字列の `encodedValue` 属性が含まれています。|  
|certificateReference|X.509 証明書検証の設定を指定します。 この要素は <xref:System.ServiceModel.Configuration.CertificateReferenceElement> 型です。|  
|dns|サービスの認証に使用される X.509 証明書の DNS を指定します。 この要素には、実際の ID を含む文字列の `value` 属性が含まれています。|  
|rsa|クライアントに対するサービスの認証に使用される X.509 証明書の RSA フィールドの値を指定します。 この要素には、実際の ID を含む文字列の `value` 属性が含まれています|  
|servicePrincipalName|サーバー プリンシパル名 (SPN) ID を指定します。これは、サービスのインスタンスを一意に識別するために、クライアントにより使用されるプリンシパル名です。 この要素には、実際のプリンシパル名が文字列で含まれている `value` 属性が含まれています。 この要素は <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement> 型です。|  
|userPrincipalName|ユーザー プリンシパル名 (UPN) ID を指定します。これは、ネットワーク上のユーザーのログオン名の種類です。 ユーザープリンシパル名は、Active Directory で使用されるユーザーオブジェクト名の後にアットマーク () が続き、 \@ 通常はドメイン名システムの親ドメインで構成されます。 たとえば、Fabrikam.com ドメインツリーの Jeff には、ユーザープリンシパル名が含まれている場合があり [jeff@fabrikam.com](mailto:jeffsmith@fabrikam.com) ます。  この要素には、実際のプリンシパル名が文字列で含まれている `value` 属性が含まれています。 この要素は <xref:System.ServiceModel.Configuration.UserPrincipalNameElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<custom>](custom.md)|netPeerTcpBinding のカスタム ピア リゾルバーを指定します。|  
|[\<endpoint>](endpoint-element.md)|サービスエンドポイントを構成します。|  
|[\<endpoint>の\<client>](endpoint-of-client.md)|チャネルエンドポイントを構成します。|  
|[\<issuer>](issuer.md)|フェデレーション サービスのセキュリティ トークン サービス (STS) を指定します。|  
|[\<issuerMetadata>](issuermetadata.md)|フェデレーション サービスのセキュリティ トークン サービス (STS) のメタデータ エンドポイントを指定します。|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|カスタム バインドで発行済みトークンのパラメーターを定義します。|  
|[\<localIssuer>](localissuer.md)|ローカル セキュリティ トークン サービス (STS) を指定します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- [サービス ID と認証](../../../wcf/feature-details/service-identity-and-authentication.md)
- [エンドポイント:アドレス、バインディング、およびコントラクト](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
