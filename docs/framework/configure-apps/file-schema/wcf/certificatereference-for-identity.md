---
title: <identity> の <certificateReference>
ms.date: 03/30/2017
ms.assetid: ac359c65-c22d-42d2-97de-db53b77cebdb
ms.openlocfilehash: 93a6290d780ff61756f7315cd0c32f0e199ca00f
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70849983"
---
# <a name="certificatereference-for-identity"></a>\<identity> の \<certificateReference>
X.509 証明書検証の設定を指定します。 この id を持つエンドポイントに接続するセキュリティで保護された Windows Communication Foundation (WCF) クライアントは、サーバーによって提示されるクレームに、この id の構築に使用される id 要求が含まれていることを確認します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<identity>**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateReference>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<certificateReference findValue="String"
                      isChainIncluded="Boolean"
                      storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                      storeLocation="LocalMachine/CurrentUser"
                      X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier">
</certificateReference>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|findValue|X.509 証明書ストアで検索する値を指定します。 この属性に格納されている型は、指定された `X509FindType` 値の要件を満たす必要があります。 既定値は空の文字列です。|  
|isChainIncluded|証明書チェーンを使用して検証を行うかどうかを指定するブール値です。|  
|storeLocation|クライアントがサーバーの証明書の検証に使用できる証明書ストアの場所を指定します。<br /><br /> 有効な値は次のとおりです。<br /><br /> -LocalMachine: ローカルコンピューターに割り当てられた証明書ストア。<br />-CurrentUser: 現在のユーザーに割り当てられている証明書ストア。<br /><br /> 既定値は LocalMachine です。<br /><br /> この属性は <xref:System.Security.Cryptography.X509Certificates.StoreLocation> 型です。|  
|storeName|開く X.509 証明書ストアの名前を指定します。<br /><br /> 有効な値は次のとおりです。<br /><br /> -アドレス帳: 他のユーザーの証明書ストア。<br />-AuthRoot: サードパーティ証明機関 (Ca) の証明書ストア。<br />-CertificateAuthority: 中間 Ca の証明書ストア。<br />-許可されていません: 失効した証明書の証明書ストア。<br />-My: 個人証明書の証明書ストア。<br />-Root: 信頼されたルート Ca の証明書ストア。<br />-TrustedPeople: 直接信頼されている人間とリソースの証明書ストア。<br />-TrustedPublisher: 直接信頼された発行元の証明書ストア。<br /><br /> 既定値は、My です。<br /><br /> この属性は <xref:System.Security.Cryptography.X509Certificates.StoreName> 型です。|  
|X509FindType|実行する X.509 検索の種類を指定します。 `findValue` 属性に含まれている型は、指定された X509FindType の要件を満たしている必要があります。<br /><br /> 有効な値は次のとおりです。<br /><br /> -FindByThumbPrint<br />-FindBySubjectName<br />-Findbysubjectdistinguishedname です<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />-FindBySerialNumber<br />- FindByTimeValid<br />- FindByTimeNotYetValid<br />- FindByTemplateName<br />- FindByApplicationPolicy<br />- FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />- FindBySubjectKeyIdentifier<br /><br /> 既定値は FindBySubjectDistinguishedName です。<br /><br /> この属性は <xref:System.Security.Cryptography.X509Certificates.X509FindType> 型です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identity>](identity.md)|メッセージを交換する他のエンドポイントによるエンドポイントの認証を可能にする設定を指定します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.CertificateReferenceElement>
- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
