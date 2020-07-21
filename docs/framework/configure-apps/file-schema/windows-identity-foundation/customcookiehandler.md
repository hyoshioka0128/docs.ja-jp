---
title: <customCookieHandler>
ms.date: 03/30/2017
ms.assetid: a03b153d-5ec6-4915-9031-6f0c3fd348be
author: BrucePerlerMS
ms.openlocfilehash: e1f32e17cf0da5e948d778e8b61aca6053eff4ef
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252019"
---
# \<customCookieHandler>
カスタムクッキーハンドラーの種類を設定します。 この要素は `mode` 、要素の属性が "Custom" の場合にのみ存在する可能性があり `<cookieHandler>` ます。 カスタム型は、クラスから派生する必要があり <xref:System.IdentityModel.Services.CookieHandler> ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<cookieHandler>**](cookiehandler.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<customCookieHandler>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Custom">  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" >  
      </customCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|クラスから派生するカスタム型を指定し <xref:System.IdentityModel.Services.CookieHandler> ます。 属性を指定する方法の詳細については `type` 、「[カスタム型参照](../windows-workflow-foundation/index.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<cookieHandler>](cookiehandler.md)|<xref:System.IdentityModel.Services.CookieHandler>が <xref:System.IdentityModel.Services.SessionAuthenticationModule> cookie の読み取りと書き込みに使用するを構成します。|  
  
## <a name="remarks"></a>解説  
 要素の属性を "Custom" に設定してカスタム cookie ハンドラーを指定する場合は、 `mode` `<cookieHandler>` `<customCookieHandler>` クッキーハンドラーの型を参照する子要素を含めることによって、カスタム cookie ハンドラーの型を指定する必要があります。 `mode`属性が "Chunked" または "Default" に設定されている場合、この要素を指定することはできません。 カスタムクッキーハンドラーは、クラスから派生する必要があり <xref:System.IdentityModel.Services.CookieHandler> ます。  
  
 `<customCookieHandler>`要素は、クラスによって表され <xref:System.IdentityModel.Configuration.CustomTypeElement> ます。  
  
## <a name="example"></a>例  
 次の例では、型のカスタム cookie ハンドラーを使用するように SAM を構成し `MyNamespace.MyCustomCookieHandler` ます。  
  
```xml  
<cookieHandler mode="Custom">  
    <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
</cookieHandler>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Services.CookieHandler>
