---
title: <certificateValidator>
ms.date: 03/30/2017
ms.assetid: 86161897-c20f-4ad8-9d7f-050c247251bf
author: BrucePerlerMS
ms.openlocfilehash: 3f3d79d3567c1714a79423b7767ce3f454b9d52d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152789"
---
# \<certificateValidator>
証明書の検証に使用するカスタムの種類を指定します。 この型は `certificateValidationMode` 、要素の属性 [\<certificateValidation>](certificatevalidation.md) が "Custom" に設定されている場合にのみ使用されます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<certificateValidation>**](certificatevalidation.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateValidator>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation>  
      <certificateValidator type=xs:string>  
      </certificateValidator>  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|クラスから派生するカスタム型を指定し <xref:System.IdentityModel.Selectors.X509CertificateValidator> ます。 `certificateValidationMode` [\<certificateValidation>](certificatevalidation.md) この型を使用するには、要素の属性を "Custom" に設定します。 属性を指定する方法の詳細については `type` 、「[カスタム型参照](../windows-workflow-foundation/index.md)」を参照してください。 省略可能。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<certificateValidation>](certificatevalidation.md)|トークンハンドラーが証明書を検証するために使用する設定を制御します。|  
  
## <a name="example"></a>例  
  
```xml  
<certificateValidation certificateValidationMode="Custom"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine">  
    <certificateValidator type="MyNamespace.CustomValidator, MyAssembly" />
</certificateValidation>
```
