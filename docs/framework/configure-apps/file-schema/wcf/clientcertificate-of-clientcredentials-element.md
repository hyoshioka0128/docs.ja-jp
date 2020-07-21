---
title: <clientCertificate><clientCredentials>要素の
ms.date: 03/30/2017
ms.assetid: 3b3fa000-3434-4142-a178-11903bdd2c5d
ms.openlocfilehash: fb95ef3168378227e41e55c6fd5e5b772cb7ad0f
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400514"
---
# <a name="clientcertificate-of-clientcredentials-element"></a>\<clientCertificate>\<clientCredentials>要素の
サービスに対するクライアントの認証に使用する X.509 証明書を定義します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clientCertificate>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<clientCertificate findValue="String"
                   storeLocation="LocalMachine/CurrentUser"
                   storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                   X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`findValue`|X.509 証明書ストアで検索する値を含む文字列。 属性に格納されている型は、`X509FindType` 属性値の要件を満たす必要があります。 既定値は空の文字列です。|  
|`storeLocation`|クライアントがサービスに対して自身を認証するために使用する X.509 証明書の場所を指定します。 有効な値は次のとおりです。<br /><br /> -LocalMachine: ローカルコンピューターに割り当てられた証明書ストア。<br />-CurrentUser: 現在のユーザーに割り当てられている証明書ストア。<br /><br /> 既定値は LocalMachine です。 この属性は <xref:System.Security.Cryptography.X509Certificates.StoreLocation> 型です。|  
|`storeName`|検索する X.509 証明書ストアの名前を指定します。 有効な値は次のとおりです。<br /><br /> -アドレス帳: 他のユーザーの証明書ストア。<br />-AuthRoot: サードパーティの証明機関 (Ca) の証明書ストア。<br />-CertificateAuthority: 中間証明機関 (Ca) の証明書ストア。<br />-許可されていません: 失効した証明書の証明書ストア。<br />-My: 個人証明書の証明書ストア。<br />-Root: 信頼されたルート証明機関 (Ca) の証明書ストア。<br />-TrustedPeople: 直接信頼されている人間とリソースの証明書ストア。<br />-TrustedPublisher: 直接信頼された発行元の証明書ストア。<br /><br /> 既定値は My です。 この属性は <xref:System.Security.Cryptography.X509Certificates.StoreName> 型です。|  
|X509FindType|実行する X.509 検索の種類を定義します。 `findValue` 属性に格納されている型は、この属性の要件を満たす必要があります。 有効な値は次のとおりです。<br /><br /> -FindByThumbPrint<br />-FindBySubjectName<br />-Findbysubjectdistinguishedname です<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />-FindBySerialNumber<br />- FindByTimeValid<br />- FindByTimeNotYetValid<br />- FindByTemplateName<br />- FindByApplicationPolicy<br />- FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />- FindBySubjectKeyIdentifier<br /><br /> 既定値は FindBySubjectDistinguishedName です。 この属性は <xref:System.Security.Cryptography.X509Certificates.X509FindType> 型です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|サービスに対するクライアントの認証に使用される資格情報を指定します。|  
  
## <a name="remarks"></a>解説  
 この構成要素は、この要素によるクライアントの認証に使用する証明書を指定します。 詳細については、「[方法: クライアント資格情報の値を指定する](../../../wcf/how-to-specify-client-credential-values.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ClientCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [方法: クライアントの資格情報の値を指定する](../../../wcf/how-to-specify-client-credential-values.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
