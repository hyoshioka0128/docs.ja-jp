---
title: <cookieHandler>
ms.date: 03/30/2017
ms.assetid: bfdc127f-8d94-4566-8bef-f583c6ae7398
author: BrucePerlerMS
ms.openlocfilehash: 853dc9817d080e59ac7a792576eda862bd0b1f1d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252025"
---
# \<cookieHandler>
<xref:System.IdentityModel.Services.CookieHandler> <xref:System.IdentityModel.Services.SessionAuthenticationModule> (SAM) が cookie の読み取りと書き込みに使用するを構成します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<cookieHandler>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler name=xs:string  
        path=Path  
        mode="Chunked||Custom||Default"  
        persistentSessionLifetime=xs:string  
        hideFromScript=xs:boolean  
        requireSSL=xs:boolean  
        domain=xs:string  
      <chunkedCookieHandler size=xs:int />  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|name|書き込まれたすべてのクッキーの基本名を指定します。 既定値は "FedAuth" です。|  
|path|書き込まれたすべてのクッキーのパス値を指定します。 既定値は "HttpRuntime. AppDomainAppVirtualPath" です。|  
|mode|<xref:System.IdentityModel.Services.CookieHandlerMode>SAM によって使用されるクッキーハンドラーの種類を指定する値の1つ。 次の値を使用できます。<br /><br /> -"Default"-"Chunked" と同じです。<br />-"Chunked" —クラスのインスタンスを使用 <xref:System.IdentityModel.Services.ChunkedCookieHandler> します。 この cookie ハンドラーによって、個々の cookie が設定された最大サイズを超えないようにします。 これを実現するには、1つの論理クッキーをネットワーク上の多数の cookie に "チャンキング" します。<br />-"Custom" —は、から派生したカスタムクラスのインスタンスを使用 <xref:System.IdentityModel.Services.CookieHandler> します。 派生クラスは、子要素によって参照され `<customCookieHandler>` ます。<br /><br /> 既定値は "Default" です。|  
|persistentSessionLifetime|永続的なセッションの有効期間を指定します。 ゼロの場合は、一時的なセッションが常に使用されます。 既定値は "0:0:0" で、一時的なセッションを指定します。 最大値は "365:0:0" で、これは365日のセッションを指定します。 値は、次の制限に従って指定する必要があります。つまり、左端の値には日を指定し、中央の値 `<xs:pattern value="([0-9.]+:){0,1}([0-9]+:){0,1}[0-9.]+" />` (存在する場合) は時間を指定し、右端の値 (存在する場合) は分を指定します。|  
|requireSsl|書き込まれたすべてのクッキーに対して "Secure" フラグを出力するかどうかを指定します。 この値が設定されている場合、サインインセッションの cookie は HTTPS 経由でのみ使用できます。 既定値は "true" です。|  
|hideFromScript|書き込まれたクッキーに対して "HttpOnly" フラグを出力するかどうかを制御します。 一部の web ブラウザーでは、クライアント側のスクリプトに cookie 値へのアクセスを保持することで、このフラグが適用されます。 既定値は "true" です。|  
|domain|書き込まれたすべてのクッキーのドメイン値。 既定値は "" です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<chunkedCookieHandler>](chunkedcookiehandler.md)|を構成 <xref:System.IdentityModel.Services.ChunkedCookieHandler> します。 この要素は `mode` 、要素の属性 `<cookieHandler>` が "Default" または "Chunked" の場合にのみ存在する可能性があります。|  
|[\<customCookieHandler>](customcookiehandler.md)|カスタムクッキーハンドラーの種類を設定します。 `mode`要素の属性 `<cookieHandler>` が "Custom" の場合、この要素は存在する必要があります。 属性の他の値には存在できません `mode` 。 カスタム型は、クラスから派生する必要があり <xref:System.IdentityModel.Services.CookieHandler> ます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>(Wsfam) と (SAM) を構成する設定が含まれてい <xref:System.IdentityModel.Services.SessionAuthenticationModule> ます。|  
  
## <a name="remarks"></a>解説  
 <xref:System.IdentityModel.Services.CookieHandler>は、HTTP プロトコルレベルでの未加工の cookie の読み取りと書き込みを行います。 <xref:System.IdentityModel.Services.ChunkedCookieHandler>またはクラスから派生したカスタム cookie ハンドラーを構成でき <xref:System.IdentityModel.Services.CookieHandler> ます。  
  
 チャンク cookie ハンドラーを構成するには、mode 属性を "Chunked" または "Default" に設定します。 既定のチャンクサイズは2000バイトですが、必要に応じて、子要素を含めることによって別のチャンクサイズを指定することもでき `<chunkedCookieHandler>` ます。  
  
 カスタム cookie ハンドラーを構成するには、mode 属性を "Custom" に設定します。 また、 `<customCookieHandler>` カスタムハンドラーの型を参照する子要素も指定する必要があります。  
  
 `<cookieHandler>`要素は、クラスによって表され <xref:System.IdentityModel.Services.CookieHandlerElement> ます。 構成で指定されたクッキーハンドラーは、プロパティに設定されている <xref:System.IdentityModel.Services.Configuration.FederationConfiguration.CookieHandler%2A> オブジェクトのプロパティから取得でき <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> ます。  
  
## <a name="example"></a>例  
 次の XML は、要素を示して `<cookieHandler>` います。 この例では、 `mode` 属性が指定されていないため、既定の cookie ハンドラーが SAM によって使用されます。 これはクラスのインスタンスです <xref:System.IdentityModel.Services.ChunkedCookieHandler> 。 `<chunkedCookieHandler>`子要素が指定されていないため、既定のチャンクサイズが使用されます。 属性が設定されているため、HTTPS は必要ありません `requireSsl` `false` 。  
  
> [!WARNING]
> この例では、セッション cookie を書き込むために HTTPS は必要ありません。 これは、 `requireSsl` 要素の属性 `<cookieHandler>` がに設定されているためです `false` 。 ほとんどの運用環境では、セキュリティ上のリスクが生じる可能性があるため、この設定は推奨されません。  
  
```xml  
<cookieHandler requireSsl="false" />  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Services.CookieHandler>
- <xref:System.IdentityModel.Services.ChunkedCookieHandler>
- <xref:System.IdentityModel.Services.SessionAuthenticationModule>
