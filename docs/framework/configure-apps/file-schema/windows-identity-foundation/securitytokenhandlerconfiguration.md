---
title: <securityTokenHandlerConfiguration>
ms.date: 03/30/2017
ms.assetid: 28724cc6-020c-4a06-9a1f-d7594f315019
author: BrucePerlerMS
ms.openlocfilehash: e3e65820fa4dc341371d4f67689a288cd3f63951
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152568"
---
# \<securityTokenHandlerConfiguration>
トークンハンドラーのコレクションの構成を提供します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<securityTokenHandlerConfiguration>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration saveBootstrapContext=xs:boolean  
          maximumClockSkew=TimeSpan>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|saveBootstrapContext|ブートストラップトークンをセッショントークンに含める必要があるかどうかを指定します。 また、要素の属性を設定することによって、トークンハンドラーコレクションに値を設定することもでき `saveBootstrapContext` [\<identityConfiguration>](identityconfiguration.md) ます。 トークンハンドラーコレクションに設定された値は、サービスで設定された値よりも優先されます。|  
|maximumClockSkew|<xref:System.TimeSpan>許容される最大のクロックスキューを指定する。 サインインセッションの有効期限の検証など、時間を区別する操作を実行するときに許容される最大のクロックスキューを制御します。 既定値は5分 "00:05:00" です。 値を指定する方法の詳細について <xref:System.TimeSpan> は、「 [Timespan values](../windows-workflow-foundation/index.md)」を参照してください。 また、要素の属性を設定することによって、サービスレベルで時刻のずれの最大値を設定することもでき `maximumClockSkew` [\<identityConfiguration>](identityconfiguration.md) ます。 トークンハンドラーコレクションに設定された値は、サービスで設定された値よりも優先されます。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<audienceUris>](audienceuris.md)|この証明書利用者の許容される識別子である Uri のセットを指定します。 省略可能。|  
|[\<caches>](caches.md)|セッショントークンとトークンリプレイ検出に使用されるキャッシュを登録します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 省略可能。|  
|[\<certificateValidation>](certificatevalidation.md)|トークンハンドラーが証明書を検証するために使用する設定を制御します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 特定のハンドラーが独自の検証コントロールを使用して構成されている場合、これらの設定はオーバーライドされます。 省略可能。|  
|[\<issuerNameRegistry>](issuernameregistry.md)|トークンハンドラーコレクションのハンドラーによって使用される発行者名レジストリを構成します。 省略可能。|  
|[\<issuerTokenResolver>](issuertokenresolver.md)|トークンハンドラーコレクションのハンドラーによって使用される発行者トークンリゾルバーを登録します。 発行者トークンリゾルバーは、受信トークンとメッセージの署名トークンを解決するために使用されます。 省略可能。|  
|[\<serviceTokenResolver>](servicetokenresolver.md)|トークンハンドラーコレクションのハンドラーによって使用されるサービストークンリゾルバーを登録します。 サービストークンリゾルバーは、受信トークンとメッセージの暗号化トークンを解決するために使用されます。 省略可能。|  
|[\<tokenReplayDetection>](tokenreplaydetection.md)|トークンリプレイ検出を有効にし、トークンの有効期限を指定します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 省略可能。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlers>](securitytokenhandlers.md)|エンドポイントに登録されているセキュリティトークンハンドラーのコレクションを指定します。|  
  
## <a name="remarks"></a>解説  
 このセクションでは、オブジェクトのプロパティ値を提供 <xref:System.IdentityModel.Tokens.SecurityTokenHandlerConfiguration> します。 このセクションで構成した設定は、サービスで構成されている設定よりも優先されます。 これらの設定の一部は、ハンドラーがセキュリティトークンハンドラーコレクションに追加されたときに指定される設定によってオーバーライドされることがあります。  
  
## <a name="example"></a>例  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>
      <securityTokenHandlerConfiguration>  
  
        <audienceUris>  
          <clear/>  
          <add value="http://www.example.com/myapp/" />  
        </audienceUris>  
  
        <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel">  
          <trustedIssuers>  
            <add thumbprint="97249e1a … 4c9158de" name="contoso.com" />  
          </trustedIssuers>  
        </issuerNameRegistry>  
  
        <issuerTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
        <serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```
