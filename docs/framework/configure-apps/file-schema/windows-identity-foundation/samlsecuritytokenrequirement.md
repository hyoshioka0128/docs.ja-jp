---
title: <samlSecurityTokenRequirement>
ms.date: 03/30/2017
ms.assetid: 09202d12-88d3-49cc-953b-703bcc1690eb
author: BrucePerlerMS
ms.openlocfilehash: b27f337189a7d0b66ffd38e032b5eb864e5094a1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152633"
---
# \<samlSecurityTokenRequirement>
クラス、クラス、 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> またはこれらのクラスの派生クラスの構成を提供します。 クラスによって表さ <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> れます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<samlSecurityTokenRequirement>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement
            issuerCertificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
            issuerCertificateRevocationMode="NoCheck||Offline||Online"  
            issuerCertificateTrustedStoreLocation="CurrentLocation||LocalMachine"  
            issuerCertificateValidator="Namespace.Class Assembly"  
            mapToWindows=xs:boolean  
          <nameClaimType value=xs:string />  
          <roleClaimType value=xs:string />  
        </samlSecurityTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|mapToWindows|受信 UPN 要求を使用して、トークンハンドラーが検証トークンを Windows アカウントにマップする必要があるかどうかを指定します。 既定値は "false" です。|  
|issuerCertificateRevocationMode|<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>X.509 証明書に使用する失効モードを指定する値。 既定値は "Online" です。|  
|issuerCertificateValidationMode|<xref:System.ServiceModel.Security.X509CertificateValidationMode>X.509 証明書に使用する検証モードを指定する値。 既定値は "PeerOrChainTrust" です。|  
|issuerCertificateTrustedStoreLocation|<xref:System.Security.Cryptography.X509Certificates.StoreLocation>X.509 証明書ストアを示す値です。 既定値は "LocalMachine" です。|  
|issuerCertificateValidator|から派生するカスタム型 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 。 `issuerCertificateValidationMode`属性が "Custom" の場合、この型のインスタンスは発行者の証明書の検証に使用されます。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<nameClaimType>](nameclaimtype.md)|プロパティを指定するクレームの種類を設定し <xref:System.Security.Principal.IIdentity.Name%2A> ます。|  
|[\<roleClaimType>](roleclaimtype.md)|<xref:System.Security.Claims.ClaimsIdentity>トークンハンドラーのメソッドによって返されるオブジェクトのコレクション内でのロールの種類の要求を定義する要求の種類を指定し <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> ます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<add>](add.md)|指定されたセキュリティトークンハンドラーをトークンハンドラーコレクションに追加します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `<samlSecurityTokenRequirement>` オブジェクトモデルのクラスによって表され、 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> `SamlSecurityTokenRequirement` またはでプロパティを構成するために使用され <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> ます。  
  
## <a name="example"></a>例  
  
```xml  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement issuerCertificateValidationMode="PeerOrChainTrust"  
                                  issuerCertificateRevocationMode="Online"  
                                  issuerCertificateTrustedStoreLocation="LocalMachine"  
                                  mapToWindows="false">  
  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
        <roleClaimType value="schemas.microsoft.com/ws/2006/04/identity/claims/role" />  
    </samlSecurityTokenRequirement>  
</add>  
```
