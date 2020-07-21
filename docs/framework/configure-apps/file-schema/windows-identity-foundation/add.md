---
title: <add>
ms.date: 03/30/2017
ms.assetid: 4712a888-f154-4395-8887-ef14a88a6497
author: BrucePerlerMS
ms.openlocfilehash: 83ba51cbbd5100bf7412f9914a270cac88f7faa1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73973802"
---
# \<add>
指定されたセキュリティトークンハンドラーをトークンハンドラーコレクションに追加します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type=xs:string>  
        <optionalConfigurationElement>  
        </optionalConfigurationElement>  
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
|type|追加するトークンハンドラーの CLR 型名。 属性を指定する方法の詳細については `type` 、「[カスタム型参照](https://docs.microsoft.com/previous-versions/windows-identity-foundation/gg638728(v=msdn.10)#custom-type-references)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<samlSecurityTokenRequirement>](samlsecuritytokenrequirement.md)|クラス、クラス、 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> またはこれらのクラスの派生クラスの構成を提供します。|  
|[\<sessionTokenRequirement>](sessiontokenrequirement.md)|<xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>クラスまたは派生クラスの構成を提供します。|  
|[\<userNameSecurityTokenHandlerRequirement>](usernamesecuritytokenhandlerrequirement.md)|<xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler>クラスまたは派生クラスの構成を提供します。|  
|[\<x509SecurityTokenHandlerRequirement>](x509securitytokenhandlerrequirement.md)|クラスまたは派生クラスのオプションの構成を提供 <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlers>](securitytokenhandlers.md)|エンドポイントに登録されているセキュリティトークンハンドラーのコレクションを指定します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `<add>` トークンハンドラーの構成を指定する1つの子要素を受け取ることができます。 これは、要素の属性を通じて参照されるハンドラークラスが `type` この機能をサポートするかどうかによって異なり `<add>` ます。 この機能を提供するトークンハンドラークラスは、オブジェクトを受け取るコンストラクターを公開する必要があり <xref:System.Xml.XmlElement> ます。  

```csharp  
public class CustomTokenHandler : Microsoft.IdentityModel.Tokens.SecurityTokenHandler  
{  
    public CustomTokenHandler( XmlElement customConfig )  
    {  
    }  
}  
```  
  
 いくつかの組み込みセキュリティトークンハンドラークラスは、この機能を提供します。 これらのクラスは、、、、 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler> <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> 、および <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> です。  
  
> [!IMPORTANT]
> トークンハンドラーコレクションには、指定された任意の型の1つのハンドラーのみを含めることができます。 これは、たとえば、クラスから派生したハンドラーをコレクションに追加する場合は、 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> 最初にコレクションから既定で存在するを削除する必要があることを意味し <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> ます。 要素を使用して、 [\<remove>](remove.md) コレクションから1つのハンドラーを削除することも、要素を使用してコレクションからすべてのハンドラーを削除することもでき [\<clear>](clear.md) ます。  
  
 ハンドラーに指定された設定は、要素の下のトークンハンドラーコレクションで指定された同等 [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) の設定をオーバーライドし、要素の下のサービスレベルで指定され [\<identityConfiguration>](identityconfiguration.md) ます。  
  
## <a name="example"></a>例  
 次の XML は、および要素を使用して、 `<add>` `<remove>` 既定のセッショントークンハンドラーをカスタムセッショントークンハンドラーに置き換える方法を示しています。 XML は、「」のサンプルから抜粋したものです `ClaimsAwareWebFarm` 。  
  
```xml  
<securityTokenHandlers>  
  <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
</securityTokenHandlers>  
```
