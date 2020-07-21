---
title: <authentication><clientCertificate>要素の
ms.date: 03/30/2017
ms.assetid: 4a55eea2-1826-4026-b911-b7cc9e9c8bfe
ms.openlocfilehash: 99084f6b7afbdd8586ee706cd6ec44b349d81ff2
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398264"
---
# <a name="authentication-of-clientcertificate-element"></a>\<authentication>\<clientCertificate>要素の
サービスによって使用されるクライアント証明書の認証動作を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCertificate>**](clientcertificate-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<authentication>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<authentication customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                includeWindowsGroups="Boolean"
                mapClientCertificateToWindowsAccount="Boolean"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|customCertificateValidatorType|省略可能な文字列。 カスタム型の検証に使用される型およびアセンブリです。 `certificateValidationMode` が `Custom` に設定されている場合は、この属性を設定する必要があります。|  
|certificateValidationMode|省略可能な列挙体です。 資格情報の検証に使用されるモードのいずれかを指定します。 この属性は <xref:System.ServiceModel.Security.X509CertificateValidationMode> 型です。 <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom?displayProperty=nameWithType> に設定されている場合、`customCertificateValidator` も指定する必要があります。 既定値は、<xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust?displayProperty=nameWithType> です。|  
|includeWindowsGroups|省略可能なブール。 セキュリティ コンテキストに Windows グループが含まれているかどうかを指定します。 この属性を `true` に設定すると、グループ全体が拡張されるため、パフォーマンスに影響が及びます。 ユーザーが属するグループの一覧を生成する必要がない場合は、この属性を `false` に設定します。|  
|mapClientCertificateToWindowsAccount|Boolean です。 証明書を使用してクライアントを Windows ID にマップできるかどうかを指定します。 これを行うには、Active Directory が有効である必要があります。|  
|revocationMode|省略可能な列挙体です。 証明書失効リスト (RCL) のチェックに使用されるモードのいずれかです。 既定値は、`Online` です。 この値は、HTTP トランスポート セキュリティを使用する場合は無視されます。|  
|trustedStoreLocation|省略可能な列挙体です。 2 つのシステム格納場所 (`LocalMachine` または `CurrentUser`) のいずれかです。 この値は、サービス証明書がクライアントにネゴシエートされるときに使用されます。 指定されたストアの場所にある**信頼さ**れた People ストアに対して検証が実行されます。 既定値は、`CurrentUser` です。|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType 属性  
  
|値|説明|  
|-----------|-----------------|  
|String|タイプ名およびアセンブリと、タイプの検索に使用される他のデータを指定します。|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode 属性  
  
|値|Description|  
|-----------|-----------------|  
|Enumeration|None、PeerTrust、ChainTrust、PeerOrChainTrust、Custom のいずれかの値にします。<br /><br /> 詳細については、「[証明書の使用](../../../wcf/feature-details/working-with-certificates.md)」を参照してください。|  
  
## <a name="revocationmode-attribute"></a>revocationMode 属性  
  
|値|Description|  
|-----------|-----------------|  
|Enumeration|NoCheck、Online、Offline のいずれかの値にします。 詳細については、「[証明書の使用](../../../wcf/feature-details/working-with-certificates.md)」を参照してください。|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation 属性  
  
|値|Description|  
|-----------|-----------------|  
|Enumeration|次のいずれかの値を指定できます。`LocalMachine` または `CurrentUser`。 既定値は、`CurrentUser` です。 クライアント アプリケーションがシステム アカウントで実行されている場合、証明書は通常 `LocalMachine` の下にあります。 クライアント アプリケーションがユーザー アカウントで実行されている場合、証明書は通常 `CurrentUser` の下にあります。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-servicecredentials.md)|サービスに対するクライアントの認証に使用する X.509 証明書を定義します。|  
  
## <a name="remarks"></a>解説  
 `<authentication>` 要素は、<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> クラスに対応します。 この要素を使用すると、クライアントを認証する方法をカスタマイズできます。 `certificateValidationMode` 属性は、`None`、`ChainTrust`、`PeerOrChainTrust`、`PeerTrust`、または `Custom` に設定できます。 既定では、レベルはに設定されています `ChainTrust` 。これは、チェーンの最上位にあるルート証明*機関*で終了する証明書の階層構造で各証明書を検索する必要があることを指定します。 これは最もセキュリティで保護されているモードです。 また、値を `PeerOrChainTrust` に設定することもできます。これは、信頼されたチェーン内の証明書と共に、自己発行された証明書 (ピア信頼) も受け入れるよう指定します。 自己発行の資格情報は信頼された証明機関から購入したものである必要はないため、この値はクライアントとサービスの開発およびデバッグに使用されます。 クライアントを展開するときは、代わりに `ChainTrust` 値を使用します。  
  
 また、値を `Custom` に設定することもできます。 `Custom` 値に設定する場合は、`customCertificateValidatorType` 属性を、証明書の検証に使用するアセンブリと型に設定する必要もあります。 独自のカスタム検証を作成するには、抽象 <xref:System.IdentityModel.Selectors.X509CertificateValidator> クラスを継承する必要があります。 詳細については、「[方法: カスタム証明書検証を使用するサービスを作成](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)する」を参照してください。  
  
## <a name="example"></a>例  
 次のコードは、`<authentication>` 要素の X.509 証明書とカスタム検証タイプを指定します。  
  
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

- <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>
- <xref:System.ServiceModel.Security.X509CertificateValidationMode>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509ClientCertificateAuthenticationElement>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [方法: カスタム証明書検証を使用するサービスを作成する](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
