---
title: <system.identityModel.services>
ms.date: 03/30/2017
ms.assetid: fa1624dd-2d74-4ae3-942e-498cee261ac5
author: BrucePerlerMS
ms.openlocfilehash: 57757aaec39bc5c552e7ba12c9779cb3a92a9025
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152505"
---
# \<system.identityModel.services>
WS-FEDERATION プロトコルを使用した認証の構成セクション。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<system.identityModel.services>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration name=xs:string identityConfigurationName=xs:string>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>(Wsfam) および <xref:System.IdentityModel.Services.SessionAuthenticationModule> (SAM) HTTP モジュールを構成する設定が含まれています。|  
  
### <a name="parent-elements"></a>親要素  
 なし  
  
## <a name="remarks"></a>解説  
 `<system.identityModel.services>`アプリケーションの構成ファイルにセクションを追加して、SAM と WSFAM の設定を指定します。  
  
> [!IMPORTANT]
> クラスまたはクラスを使用して、 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> コード内にクレームベースのアクセス制御を提供する場合、承認の決定に使用される要求承認マネージャー ( <xref:System.Security.Claims.ClaimsAuthorizationManager> ) とポリシーは、 `<identityConfiguration>` `<federationConfiguration>` このセクションの要素から暗黙的または明示的に参照される要素によって構成されます。 詳細については、要素の「**解説**」を参照してください [\<federationConfiguration>](federationconfiguration.md) 。  
  
 `<system.identityModel.services>`セクションは、クラスによって表され <xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection> ます。 `<federationConfiguration>`セクションで構成された子要素のコレクションは、クラスによって表され <xref:System.IdentityModel.Services.Configuration.FederationConfigurationElementCollection> ます。  
  
## <a name="example"></a>例  
 次の XML は、構成ファイルにセクションを追加する方法を示して `<system.identityModel.services>` います。 まず、セクションとセクションの両方にセクション宣言を追加する必要があり `<system.identityModel.services>` `<system.identityModel>` ます。 (セクションを追加する場合は、必要に応じ `<system.identityModel.services>` `<system.identityModel>` て、ランタイムが既定のセクションを作成できるように、セクションの宣言も追加する必要があり `<identityConfiguration>` ます)。セクション宣言を追加した後、要素の下にフェデレーション認証設定を構成でき `<system.identityModel.services>` ます。  
  
```xml  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  <!-- Additional elements (not shown) -->  
  
  <system.identityModel.services>  
    <federationConfiguration>  
      <wsFederation passiveRedirectEnabled="true"
        issuer="http://localhost:15839/wsFederationSTS/Issue"
        realm="http://localhost:50969/" reply="http://localhost:50969/"
        requireHttps="false"
        signOutReply="http://localhost:50969/SignedOutPage.html"
        signOutQueryString="Param1=value2&Param2=value2"
        persistentCookiesOnPassiveRedirects="true" />  
      <cookieHandler requireSsl="false" />  
    </federationConfiguration>  
  </system.identityModel.services>  
  
</configuration>  
```
