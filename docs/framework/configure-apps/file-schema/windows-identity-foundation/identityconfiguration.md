---
title: <identityConfiguration>
ms.date: 03/30/2017
ms.assetid: 1db76253-07da-447b-9e7a-3705c7228cf4
author: BrucePerlerMS
ms.openlocfilehash: 0fa8c574fd5663606cf081f1000a24884306edfe
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70251996"
---
# \<identityConfiguration>

サービスレベルの id 設定を指定します。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<identityConfiguration>**  

## <a name="syntax"></a>構文

```xml
<system.identityModel>
  <identityConfiguration
      name=xs:string
      saveBootstrapContext=xs:boolean>
      maximumClockSkew=TimeSpan >
  </identityConfiguration>
</system.identityModel>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|Id 構成セクションの名前。 この名前を使用して、特定の構成セクションを参照することができます。 属性が指定されていない場合、セクションでは `name` 既定の構成を定義します。 既定の構成は、パッシブフェデレーションシナリオでは常に使用されます。 詳細については、要素を参照してください [\<federationConfiguration>](federationconfiguration.md) 。|
|saveBootstrapContext|ブートストラップトークンをセッショントークンに含める必要があるかどうかを指定します。 また、要素の属性を設定することによって、トークンハンドラーコレクションに値を設定することもでき `saveBootstrapContext` [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) ます。 トークンハンドラーコレクションに設定された値は、サービスで設定された値よりも優先されます。|
|maximumClockSkew|<xref:System.TimeSpan>許容される最大のクロックスキューを指定する。 サインインセッションの有効期限の検証など、時間を区別する操作を実行するときに許容される最大のクロックスキューを制御します。 既定値は5分 "00:05:00" です。 値を指定する方法の詳細について <xref:System.TimeSpan> は、「 [Timespan values](../windows-workflow-foundation/index.md)」を参照してください。 また、要素の属性を設定することによって、トークンハンドラーコレクションに最大クロックスキューを設定することもでき `maximumClockSkew` [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) ます。 トークンハンドラーコレクションに設定された値は、サービスで設定された値よりも優先されます。|

### <a name="child-elements"></a>子要素

|要素|Description|
|-------------|-----------------|
|[\<caches>](caches.md)|セッショントークンとトークンリプレイ検出に使用されるキャッシュを登録します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 省略可能。|
|[\<certificateValidation>](certificatevalidation.md)|トークンハンドラーが証明書を検証するために使用する設定を制御します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 省略可能。|
|[\<claimsAuthenticationManager>](claimsauthenticationmanager.md)|入力方向の要求に対して要求認証マネージャーを登録します。 省略可能。|
|[\<claimsAuthorizationManager>](claimsauthorizationmanager.md)|入力方向の要求に対して要求承認マネージャーを登録します。 省略可能。|
|[\<claimTypeRequired>](claimtyperequired.md)|受信セキュリティトークンに必要な要求のセットを指定します。 省略可能。|
|[\<securityTokenHandlers>](securitytokenhandlers.md)|セキュリティトークンハンドラーのコレクションを指定します。 セキュリティトークンハンドラーの0個以上のコレクションを指定できます。 省略可能。|
|[\<tokenReplayDetection>](tokenreplaydetection.md)|トークンリプレイ検出を有効にし、トークンの有効期限を指定します。 は、サービスレベルまたはセキュリティトークンハンドラーコレクションで指定できます。 省略可能。|

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|[\<system.identityModel>](system-identitymodel.md)|アプリケーションで Windows Identity Foundation (WIF) オプションを有効にするための構成を提供します。|

## <a name="remarks"></a>解説

複数の id 構成を定義し、それぞれに一意の名前を指定できます。 動作は次のとおりです。

1. 要素が指定されていない場合は `<identityConfiguration>` 。 既定の id 構成は、実行時に作成され、既定値が設定されます。

2. 1つの `<identityConfiguration>` 要素が指定されている場合。 これは既定の id 構成です。 名前が付けられているか名前が付いていないかは関係ありません。

3. 複数の要素が指定されている場合 `<identityConfiguration>` 。 無名の要素は、既定の id 構成を指定します。 複数の要素を指定する場合は `<identityConfiguration>` 、そのうちの1つを名前のないものにすることをお勧めします。

> [!WARNING]
> 複数の要素を指定する場合は `<identityConfiguration>` 、そのうちの1つを名前なしにする必要があります。 名前のない要素が既定の id 構成になります。

 要素で指定された設定の一部 `<identityConfiguration>` は、セキュリティトークンハンドラーコレクションの設定、または個々のセキュリティトークンハンドラーの設定によって上書きできます。

> [!IMPORTANT]
> クラスまたはクラスを使用して、 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> コード内にクレームベースのアクセス制御を提供する場合、要素によって参照される id 構成によって、 `<federationConfiguration>` 承認の決定に使用される要求承認マネージャーとポリシーが構成されます。 これは、Windows Communication Foundation (WCF) アプリケーションや Web ベースではないアプリケーションなど、パッシブな Web シナリオではないシナリオでも当てはまります。 アプリケーションがパッシブな Web アプリケーションでない場合は、 [\<claimsAuthorizationManager>](claimsauthorizationmanager.md) 参照される id 構成の要素 (およびその子ポリシー要素が存在する場合) が適用される唯一の設定です。 その他すべての設定は無視されます。 詳細については、要素を参照してください [\<federationConfiguration>](federationconfiguration.md) 。

`<identityConfiguration>`要素は、クラスによって表され <xref:System.IdentityModel.Configuration.IdentityConfigurationElement> ます。 Id 構成セクションは、クラスによって表され <xref:System.IdentityModel.Configuration.IdentityConfiguration> ます。

> [!IMPORTANT]
> 要素の子要素として次の要素を指定することは `<identityConfiguration>` 非推奨とされますが、旧バージョンとの互換性のために動作は引き続きサポートされています。 これらの要素は、代わりに要素で指定する必要があり [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) ます。
>
> - [\<audienceUris>](audienceuris.md)
> - [\<issuerNameRegistry>](issuernameregistry.md)
> - [\<issuerTokenResolver>](issuertokenresolver.md)
> - [\<serviceTokenResolver>](servicetokenresolver.md)

## <a name="example"></a>例

次の例では、"alternateConfiguration" という名前の id 構成を作成します。 Id 構成では、既定の設定を指定します。

```xml
<system.identityModel>
    <identityConfiguration name="alternateConfiguration"/>
</system.identityModel>
```

## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Configuration.IdentityConfiguration>
- <xref:System.IdentityModel.Configuration.IdentityConfigurationElement>
