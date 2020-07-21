---
title: <federationConfiguration>
ms.date: 03/30/2017
ms.assetid: 8b14054c-6d07-46ab-ab58-03f14beac0f2
author: BrucePerlerMS
ms.openlocfilehash: bcd8e00b770517e3faff011b4acee08ebdc5a0df
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152737"
---
# \<federationConfiguration>
<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> <xref:System.IdentityModel.Services.SessionAuthenticationModule> Ws-federation プロトコルを介してフェデレーション認証を使用する場合、(wsfam) と (SAM) を構成します。 <xref:System.Security.Claims.ClaimsAuthorizationManager> <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> またはクラスを使用して <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> クレームベースのアクセス制御を提供するときに、を構成します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<federationConfiguration>**  
  
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
  
|属性|説明|  
|---------------|-----------------|  
|name|フェデレーション構成要素の名前。 この属性は、主に将来のプロトコルの機能拡張ポイントを提供します。 省略可能。|  
|identity Configurationname|使用する要素で指定されている id 構成セクションの名前 [\<identityConfiguration>](identityconfiguration.md) 。 この属性が指定されていない場合は、既定の id 構成セクションが使用されます。 省略可能。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<cookieHandler>](cookiehandler.md)|SAM によって使用されるクッキーハンドラーを構成します。 省略可能。|  
|[\<serviceCertificate>](servicecertificate.md)|トークンの暗号化と復号化に使用される証明書を構成します。 省略可能。|  
|[\<wsFederation>](wsfederation.md)|WS-FEDERATION 認証モジュール (WSFAM) を構成します。 省略可能。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<system.identityModel.services>](system-identitymodel-services.md)|WS-FEDERATION プロトコルを使用した認証の構成セクション。|  
  
## <a name="remarks"></a>解説  
 要素は、 \<federationConfiguration> 2 つの異なるシナリオで設定を提供します。  
  
- パッシブ Web アプリケーションで WS-FEDERATION を使用する場合、要素には、 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (wsfam) と (SAM) を構成する設定が含まれ <xref:System.IdentityModel.Services.SessionAuthenticationModule> ます。 また、セキュリティトークンハンドラーと証明書の構成に使用される id 構成と、要求承認マネージャーや要求認証マネージャーなどのコンポーネントも参照しています。  
  
- クラスまたはクラスを使用して、 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> コード内にクレームベースのアクセス制御を提供する場合、要素は、承認の決定に使用されるクレーム承認マネージャーとポリシーを構成する id 構成を参照します。 これは、パッシブな Web シナリオではないシナリオでも当てはまります。たとえば、Windows Communication Foundation (WCF) アプリケーションや、Web ベースではないアプリケーションなどです。 アプリケーションがパッシブな Web アプリケーションでない場合は、要素 [\<claimsAuthorizationManager>](claimsauthorizationmanager.md) (およびその子ポリシー要素が存在する場合) は、要素によって参照される id 構成に適用される `<federationConfiguration>` 唯一の設定です。 他の属性はすべて無視されます。  
  
 シナリオに関係なく、ランタイムは既定のフェデレーション構成を読み込みます。 動作は次のように定義されています。  
  
1. 要素が存在しない場合 `<federationConfiguration>` 、ランタイムはフェデレーション構成を作成し、既定値を設定します。 この既定のフェデレーション構成では、既定の id 構成が参照されます。  
  
2. 1つの `<federationConfiguration>` 要素が存在する場合は、名前が付けられているか名前が付いていないかに関係なく、既定のフェデレーション構成になります。 `identityConfiguration`属性が指定されている場合は、名前付き id 構成が参照されます。それ以外の場合は、既定の id 構成が参照されます。  
  
3. 名前のない `<federationConfiguration>` 要素が存在する場合は、既定のフェデレーション構成になります。 `identityConfiguration`属性が指定されている場合は、名前付き id 構成が参照されます。それ以外の場合は、既定の id 構成が参照されます。  
  
4. 複数の名前付き `<federationConfiguration>` 要素が存在し、名前のない要素が存在しない場合は `<federationConfiguration>` 、例外がスローされます。  
  
 通常、1つの `<federationConfiguration>` セクションのみが定義されます。 このセクションは、既定のフェデレーション構成です。 一意の名前を持つ複数の要素を指定することもできます `<federationConfiguration>` 。ただし、この場合は、名前のないフェデレーション構成を読み込む場合は、のハンドラーを指定する必要があります。 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated>イベントを発生さ <xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=nameWithType> せると共に、ハンドラー内のプロパティを、 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 構成ファイル内の適切な要素の値で初期化されたオブジェクトに設定し `<federationConfiguration>` ます。  
  
 `<federationConfiguration>`要素は、クラスによって表され <xref:System.IdentityModel.Services.Configuration.FederationConfigurationElement> ます。 構成オブジェクト自体は、クラスによって表され <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> ます。 1つの <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> インスタンスがプロパティに設定され、 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> アプリケーションのフェデレーション構成が提供されます。  
  
## <a name="example"></a>例  
 次の XML は、 `<federationConfiguration>` WSFAM の設定を指定する要素を示し、既定の cookie ハンドラー (クラスのインスタンス <xref:System.IdentityModel.Services.ChunkedCookieHandler> ) が SAM によって使用されることを指定します。  
  
> [!WARNING]
> この例では、cookie ハンドラーも WSFAM も HTTPS を使用する必要はありません。 これは、 `requireHttps` 要素の属性 `<wsFederation>` と `requireSsl` の属性 `<cookieHandlerElement>` が `false` であるためです。 ほとんどの運用環境では、セキュリティ上のリスクが生じる可能性があるため、これらの設定は推奨されません。  
  
```xml  
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
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- <xref:System.IdentityModel.Services.SessionAuthenticationModule>
- <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>
- [\<identityConfiguration>](identityconfiguration.md)
