---
title: <serviceCertificate> の <serviceCredentials>
ms.date: 03/30/2017
ms.assetid: 597ae6d5-4938-4950-9f5e-b2280e816182
ms.openlocfilehash: 513dcad7f4325d653df87fe9cc27572c25e153c5
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399669"
---
# <a name="servicecertificate-of-servicecredentials"></a>\<serviceCertificate> の \<serviceCredentials>
メッセージ セキュリティ モードを使用しているクライアントへのサービスの認証に使用する X.509 証明書を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceCertificate>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<serviceCertificate findValue="String"
                    storeLocation="LocalMachine/CurrentUser"
                    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                    x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`findValue`|X.509 証明書ストアで検索する値を含む文字列。 属性に含まれている型は、指定された X509FindType の要件を満たしている必要があります。 既定値は空の文字列です。|  
|`storeLocation`|クライアントがサーバーの証明書の検証に使用する X.509 証明書ストアの場所を指定します。 有効な値は次のとおりです。<br /><br /> -LocalMachine: ローカルコンピューターに割り当てられた証明書ストア。<br />-CurrentUser: 現在のユーザーに割り当てられている証明書ストア。<br /><br /> 既定値は LocalMachine です。|  
|`storeName`|開く X.509 証明書ストアの名前を指定します。 有効な値は次のとおりです。<br /><br /> -アドレス帳: 他のユーザーの証明書ストア。<br />-AuthRoot: サードパーティ証明機関 (Ca) の証明書ストア。<br />-証明機関: 中間証明機関 (Ca) の証明書ストア。<br />-許可されていません: 失効した証明書の証明書ストア。<br />-My: 個人証明書の証明書ストア。<br />-Root: 信頼されたルート証明機関 (Ca) の証明書ストア。<br />-TrustedPeople: 直接信頼されている人間とリソースの証明書ストア。<br />-TrustedPublisher: 直接信頼された発行元の証明書ストア。<br /><br /> 既定値は My です。|  
|`x509FindType`|実行する X.509 検索の種類を定義します。 有効な値は次のとおりです。<br /><br /> -FindByThumbprint<br />-FindBySubjectName<br />-Findbysubjectdistinguishedname です<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />-FindBySerialNumber<br />- FindByTimeValid<br />- FindByTimeNotYetValid<br />- FindByTemplateName<br />- FindByApplicationPolicy<br />- FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />- FindBySubjectKeyIdentifier<br /><br /> `findValue` 属性に含まれている型は、指定された X509FindType の要件を満たしている必要があります。<br /><br /> 既定値は FindBySubjectDistinguishedName です。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|サービスの認証に使用される資格情報と、クライアントの資格情報検証関連の設定を指定します。|  
  
## <a name="remarks"></a>解説  
 メッセージ セキュリティ モードを使用しているクライアントへのサービスの認証に使用する X.509 証明書を指定するには、この要素を使用します。 定期的に更新される証明書を使用している場合は、証明書のサムプリントが変更されます。 その場合、証明書を同じサブジェクト名で再発行できるため、`x509FindType` としてサブジェクト名を使用します。  
  
 要素の使用方法の詳細については、「[方法: クライアント資格情報の値を指定する](../../../wcf/how-to-specify-client-credential-values.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateServiceElement>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.ServiceCertificate%2A>
- <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>
- <xref:System.ServiceModel.Description.ServiceCredentials.ServiceCertificate%2A>
- [方法: クライアントの資格情報の値を指定する](../../../wcf/how-to-specify-client-credential-values.md)
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
