---
title: <certificateValidation>
ms.date: 03/30/2017
ms.assetid: 6c54c704-b55e-4631-88ff-4d4a5621554c
author: BrucePerlerMS
ms.openlocfilehash: c2d1a5d36cb5616ef06eedc093dd70a68a164a81
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252133"
---
# \<certificateValidation>
トークンハンドラーが証明書を検証するために使用する設定を制御します。 特定のハンドラーが独自の検証コントロールを使用して構成されている場合、これらの設定はオーバーライドされます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateValidation>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation  
      certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
      revocationMode="NoCheck||Offline||Online"  
      trustedStoreLocation="CurrentLocation||LocalMachine" >  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|certificateValidationMode|<xref:System.ServiceModel.Security.X509CertificateValidationMode>X.509 証明書に使用する検証モードを指定する値。 既定値は "PeerOrChainTrust" です。 カスタム検証を指定するには、この属性を "Custom" に設定し、要素を使用して検証コントロールを指定し [\<certificateValidator>](certificatevalidator.md) ます。 省略可能。|  
|revocationMode|<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>X.509 証明書に使用する失効モードを指定する値。 既定値は "Online" です。 省略可能。|  
|trustedStoreLocation|<xref:System.Security.Cryptography.X509Certificates.StoreLocation>X.509 証明書ストアを示す値です。 既定値は "LocalMachine" です。 省略可能。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<certificateValidator>](certificatevalidator.md)|証明書の検証に使用するカスタムの種類を指定します。 この型は `certificateValidationMode` 、要素の属性 [\<certificateValidation>](certificatevalidation.md) が "Custom" に設定されている場合にのみ使用されます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|サービスレベルの id 設定を指定します。|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|セキュリティトークンハンドラーのコレクションの構成を提供します。|  
  
## <a name="remarks"></a>解説  
 要素は `<certificateValidation>` 、要素の下のサービスレベルで指定することも、 `<identityConfiguration>` 要素の下のセキュリティトークンハンドラーコレクションレベルで指定することもでき `<securityTokenHandlerConfiguration>` ます。 トークンハンドラーコレクションの設定は、サービスで指定された設定よりも優先されます。 一部のトークンハンドラーでは、構成で証明書の検証設定を指定できます。 個々のトークンハンドラーの設定は、サービスレベルとセキュリティトークンハンドラーコレクションの両方で指定された設定よりも優先されます。  
  
## <a name="example"></a>例  
  
```xml  
<certificateValidation certificateValidationMode="PeerOrChainTrust"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine" />  
```
