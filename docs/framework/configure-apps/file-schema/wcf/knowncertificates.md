---
title: <knownCertificates>
ms.date: 03/30/2017
ms.assetid: 678e21b4-6493-47c3-8359-fcf0d37e2138
ms.openlocfilehash: 23fe19258e09e9e8a5e05a94ccef0e40ee1cb5fd
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400332"
---
# \<knownCertificates>
セキュリティ トークン サービス (STS) から発行されるセキュリティ資格情報を認証するために提供される X.509 証明書のコレクションを表します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenAuthentication>**](issuedtokenauthentication-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<knownCertificates>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<knownCertificates>
  <add findValue="String"
       storeLocation="CurrentUser/LocalMachine"
       storeName=" CurrentUser/LocalMachine"
       x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
</knownCertificates>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<add>](add-of-knowncertificates.md)|コレクションに X.509 証明書を追加します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)|サービス資格情報として発行されるトークンを指定します。|  
  
## <a name="remarks"></a>解説  
 発行されるトークンのシナリオには、3 つの段階があります。 最初の段階では、サービスにアクセスしようとしているクライアントは、*セキュリティで保護されたトークンサービス*と呼ばれます。 次に、セキュリティ トークン サービスがクライアントを認証し、その後、クライアントにトークン (通常は、SAML (Security Assertions Markup Language) トークン) を発行します。 最後に、クライアントがトークンを持ってサービスに戻ります。 サービスはトークンを調べ、トークンを認証することでクライアントの認証を可能にするデータを確認します。 トークンを認証するには、セキュリティ トークン サービスで使用される証明書がサービスによって認識されている必要があります。  
  
 要素は、 [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md) このようなセキュリティトークンサービス証明書のリポジトリです。 証明書を追加するには、 [ \<knownCertificates> 要素](knowncertificates.md)を使用します。 次の [\<add>](add-of-knowncertificates.md) 例に示すように、各証明書のを挿入します。  
  
```xml  
<issuedTokenAuthentication>
  <knownCertificates>
    <add findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="My"
         X509FindType="FindBySubjectName" />
  </knownCertificates>
</issuedTokenAuthentication>
```  
  
 既定では、証明書はセキュリティ トークン サービスから取得する必要があります。 このような "既知" の証明書により、正当なクライアントのみがサービスにアクセスできるようになります。  
  
 フェデレーションサービスによってクライアントが認証されるために必要な条件を確認するには、「[方法: フェデレーションサービスで資格情報を構成](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)する」を参照してください。 フェデレーションシナリオの詳細については、「[フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)」を参照してください。  
  
 構成のコレクションにデータを設定する方法を示す例については、「」を参照してください [\<add>](add-of-knowncertificates.md) 。  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.KnownCertificates%2A>
- <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElementCollection>
- <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>
- [\<add>](add-of-knowncertificates.md)
- [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [方法: フェデレーション サービスで資格情報を設定する](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
- [フェデレーションと発行済みトークン](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [\<add>](add-of-knowncertificates.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
