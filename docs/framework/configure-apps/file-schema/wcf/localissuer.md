---
title: <localIssuer>
ms.date: 03/30/2017
ms.assetid: 26bdd0df-0e7d-4b9e-bbeb-f28c53769385
ms.openlocfilehash: 055b7b49d1f775d49ac20de18c18ca0433716a23
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70397861"
---
# \<localIssuer>
セキュリティ トークンの取得に使用される、ローカル発行者のアドレスとバインディングを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedToken>**](issuedtoken.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<localIssuer>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<localIssuer address="String"
             binding="String"
             bindingConfiguration="String" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|address|必須の文字列。 ローカル発行者の URI を指定します。|  
|binding|省略可能な文字列。 システム指定のバインディングの 1 つ。 リストについては、「[システム指定のバインディング](../../../wcf/system-provided-bindings.md)」を参照してください。|  
|bindingConfiguration|省略可能な文字列。 構成ファイル内に存在するバインディング構成を指定します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identity>](identity.md)|ローカル発行者の ID 情報を指定します。|  
|[\<headers>](headers-element.md)|ローカル発行者を正しくアドレス指定するために必要なアドレス ヘッダーのコレクション。 `add` キーワードを使用して、このコレクションにヘッダーを追加できます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<issuedToken>](issuedtoken.md)|サービスに対するクライアントの認証に使用されるカスタム トークンを指定します。|  
  
## <a name="remarks"></a>解説  
 発行されたトークンをセキュリティ トークン サービス (STS) から取得する場合は、クライアント アプリケーションに、STS との通信に使用するアドレスとバインディングが構成されている必要があります。 が <xref:System.ServiceModel.WSFederationHttpBinding> Security Token Service の URL を提供しない場合、またはフェデレーションバインディングの発行者アドレスが `http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous` またはの場合 `null` 、クライアントの Windows Communication Foundation (WCF) チャネルは、およびで指定された値を使用して `address` STS と通信し、発行され `binding` たトークンを取得します。 ローカル発行者の構成の詳細については、「[方法: ローカル発行者を構成](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)する」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、`address` 要素の `binding`、`bindingConfiguration`、および `localIssuer` 属性を設定します。  
  
```xml  
<system.serviceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior name="MyEndpointBehavior">
        <clientCredentials>
          <issuedToken cacheIssuedTokens="false"
                       defaultKeyEntropyMode="ClientEntropy">
            <localIssuer address="net.tcp://cohowinery/tokens"
                         binding="netTcpBinding"
                         bindingConfiguration="myTcpBindingConfig" />
          </issuedToken>
        </clientCredentials>
      </behavior>
    </endpointBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.LocalIssuer%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [方法: ローカル発行者を設定する](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [サービス ID と認証](../../../wcf/feature-details/service-identity-and-authentication.md)
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [方法: フェデレーション クライアントを作成する](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
