---
title: <certificate><clientCertificate>要素の
ms.date: 03/30/2017
ms.assetid: 00297efb-a7f2-4e03-bc2b-943d545610fc
ms.openlocfilehash: d0c4ef9d3657d2dfa787feb3576beda09d1997a3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400543"
---
# <a name="certificate-of-clientcertificate-element"></a>\<certificate>\<clientCertificate>要素の
メッセージの署名と暗号化に使用される X.509 証明書を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCertificate>**](clientcertificate-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificate>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<certificate findValue="String"
             storeLocation = "CurrentUser/LocalMachine"
             storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
             X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`findValue`|X.509 証明書ストアで検索する値を含む文字列。 属性に含まれている型は、指定された X509FindType の要件を満たしている必要があります。 既定値は空の文字列です。|  
|`storeLocation`|クライアントがサーバーの証明書の検証に使用する X.509 証明書ストアの場所を指定します。 有効な値は次のとおりです。<br /><br /> -LocalMachine: ローカルコンピューターに割り当てられた証明書ストア。<br />-CurrentUser: 現在のユーザーに割り当てられている証明書ストア。<br /><br /> 既定値は LocalMachine です。|  
|`storeName`|開く X.509 証明書ストアの名前を指定します。 有効な値は次のとおりです。<br /><br /> -アドレス帳: 他のユーザーの証明書ストア。<br />-AuthRoot: サードパーティ証明機関 (Ca) の証明書ストア。<br />-Microsoft-windows-certificationauthority: 中間証明機関 (Ca) の証明書ストア。<br />-許可されていません: 失効した証明書の証明書ストア。<br />-My: 個人証明書の証明書ストア。<br />-Root: 信頼されたルート証明機関 (Ca) の証明書ストア。<br />-TrustedPeople: 直接信頼されている人間とリソースの証明書ストア。<br />-TrustedPublisher: 直接信頼された発行元の証明書ストア。<br /><br /> 既定値は My です。|  
|`X509FindType`|実行する X.509 検索の種類を定義します。 有効な値は次のとおりです。<br /><br /> -FindByThumbPrint<br />-FindBySubjectName<br />-Findbysubjectdistinguishedname です<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />-FindBySerialNumber<br />- FindByTimeValid<br />- FindByTimeNotYetValid<br />- FindByTemplateName<br />- FindByApplicationPolicy<br />- FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />- FindBySubjectKeyIdentifier<br /><br /> `findValue` 属性に含まれている型は、指定された X509FindType の要件を満たしている必要があります。<br /><br /> 既定値は FindBySubjectDistinguishedName です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-servicecredentials.md)||  
  
## <a name="remarks"></a>解説  
 `<certificate>` 要素は、サービスがクライアントと安全に通信するために、サービスが前もってクライアントの証明書を持っている必要がある場合に使用します。 このような状況は、双方向通信パターンを使用する場合に生じます。 より一般的な要求/応答パターンでは、クライアントは自身の証明書を要求に含め、サービスはそれを使用してクライアントへの応答を暗号化し、署名します。 一方、双方向通信パターンでは、サービスにはクライアントからの要求が来ないので、クライアントの証明書をあらかじめ取得することで、クライアント宛のメッセージのセキュリティを保護する必要があります。 このため、クライアントの証明書を帯域外のネゴシエーションで取得し、この要素を使用して証明書を指定する必要があります。 双方向サービスの詳細については、「[方法: 双方向コントラクトを作成](../../../wcf/feature-details/how-to-create-a-duplex-contract.md)する」を参照してください。  
  
## <a name="example"></a>例  
 次のコードは、`<authentication>` 要素の適切な X.509 証明書とカスタム検証タイプの検索方法を指定します。  
  
```xml  
<serviceBehaviors>
  <behavior name="myServiceBehavior">
    <clientCertificate>
      <certificate findValue="www.cohowinery.com"
                   storeLocation="CurrentUser"
                   storeName="TrustedPeople"
                   x509FindType="FindByIssuerName" />
      <authentication customCertificateValidatorType="MyTypes.Coho"
                      certificateValidationMode="Custom"
                      revocationMode="Offline"
                      includeWindowsGroups="false"
                      mapClientCertificateToWindowsAccount="true" />
    </clientCertificate>
  </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Certificate%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Certificate%2A>
- <xref:System.ServiceModel.Configuration.X509ClientCertificateCredentialsElement>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [方法: カスタム証明書検証を使用するサービスを作成する](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
