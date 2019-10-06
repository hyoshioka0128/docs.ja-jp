---
title: WIF 3.5 でビルドされたアプリケーションを WIF 4.5 に移行するためのガイドライン
ms.date: 03/30/2017
ms.assetid: 7a32fe6e-5f68-4693-9371-19411fa8063c
author: BrucePerlerMS
ms.openlocfilehash: 645fd09de91d8190384faea9df2ef18511162c2f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834519"
---
# <a name="guidelines-for-migrating-an-application-built-using-wif-35-to-wif-45"></a>WIF 3.5 でビルドされたアプリケーションを WIF 4.5 に移行するためのガイドライン

## <a name="applies-to"></a>対象

- Microsoft® Windows® Identity Foundation (WIF) 3.5 および 4.5。

## <a name="overview"></a>概要

Windows Identity Foundation (WIF) は、もともと .NET 3.5 SP1 タイム フレームでリリースされました。 その WIF のバージョンは WIF 3.5 と呼ばれています。 WIF は個別のランタイムおよび SDK としてリリースされました。つまりこれは、WIF 対応アプリケーションを実行しているすべてコンピューターには WIF のランタイムがインストールされている必要があり、開発者は WIF 対応アプリケーションを開発できる Visual Studio のテンプレートとツールを取得するため WIF SDK をダウンロードしてインストールする必要があることを意味します。 .NET 4.5 以降では、WIF は .NET Framework に完全に統合されています。 個別のランタイムが不要になり、WIF のツールは、Visual Studio Extensions Manager を使用して Visual Studio 2012 にインストールできます。 この WIF のバージョンは WIF 4.5 と呼ばれています。

.NET への WIF の統合には WIF API サーフェイスの複数の変更が必要でした。 WIF 4.5 には、Visual Studio 用の新しい名前空間、構成要素の変更、および新しいツールが含まれます。 このトピックでは、WIF 3.5 から WIF 4.5 を使用してビルドされたアプリケーションを移行するうえでのガイダンスを示します。 Windows 8 または Windows Server 2012 を実行するコンピューターで WIF 3.5 を使用してビルドされたレガシ アプリケーションを実行する必要がある場合があります。 またこのトピックでは、これらのオペレーティング システム向けに WIF 3.5 を有効にする方法についてのガイダンスも示します。

## <a name="changes-required-for-wif-45"></a>WIF 4.5 に必要な変更

ここでは、WIF 3.5 アプリケーションを WIF 4.5 に移行するために必要な変更について説明します。

### <a name="assembly-and-namespace-changes"></a>アセンブリおよび名前空間の変更

WIF 3.5 では、WIF クラスはすべて `Microsoft.IdentityModel` アセンブリ (microsoft.identitymicrosoft.identitymodel.dll) に含まれています。 WIF 4.5 では、WIF クラスは、`mscorlib` (mscorlib.dll)、`System.IdentityModel` (System.IdentityModel.dll)、`System.IdentityModel.Services` (System.IdentityModel.Services.dll)、および `System.ServiceModel` (System.ServiceModel.dll) というアセンブリに分割されています。

WIF 3.5 クラスはすべて `Microsoft.IdentityModel` 名前空間 (`Microsoft.IdentityModel`、`Microsoft.IdentityModel.Tokens`、`Microsoft.IdentityModel.Web` など) の 1 つに含まれていました。 WIF 4.5 では、WIF クラスは [System.IdentityModel](https://go.microsoft.com/fwlink/?LinkId=272004) 名前空間、<xref:System.Security.Claims?displayProperty=nameWithType> 名前空間、および <xref:System.ServiceModel.Security?displayProperty=nameWithType> 名前空間に分散されています。 この再編成に加えて、一部の WIF 3.5 クラスは WIF 4.5 では削除されました。

次の表に、より重要な WIF 4.5 の名前空間とそれに含まれるクラスの種類を示します。 WIF 3.5 および WIF 4.5 間で名前空間を対応付ける方法および WIF 4.5 で削除された名前空間とクラスの詳細については、「[Namespace Mapping between WIF 3.5 and WIF 4.5](namespace-mapping-between-wif-3-5-and-wif-4-5.md)」(WIF 3.5 と WIF 4.5 間での名前空間マッピング) を参照してください。

|WIF 4.5 名前空間|説明|
|-----------------------|-----------------|
|<xref:System.IdentityModel?displayProperty=nameWithType>|クッキーの変換、セキュリティ トークン サービス、および特殊な XML ディクショナリ リーダーを表すクラスが含まれます。 `Microsoft.IdentityModel`、`Microsoft.IdentityModel.SecurityTokenService`、および `Microsoft.IdentityModel.Threading` という WIF 3.5 名前空間のクラスが含まれます。|
|<xref:System.Security.Claims?displayProperty=nameWithType>|クレーム、クレーム ベースの ID、クレーム ベースの原則、およびその他のクレーム ベースの ID モデル成果物を表すクラスが含まれます。 `Microsoft.IdentityModel.Claims` 名前空間のクラスが含まれます。|
|<xref:System.IdentityModel.Tokens?displayProperty=nameWithType>|セキュリティ トークン、セキュリティ トークン ハンドラー、およびその他のセキュリティ トークンの成果物を表すクラスが含まれます。 `Microsoft.IdentityModel.Tokens`、`Microsoft.IdentityModel.Tokens.Saml11`、および `Microsoft.IdentityModel.Tokens.Saml2` という WIF 3.5 名前空間のクラスが含まれます。|
|<xref:System.IdentityModel.Services?displayProperty=nameWithType>|受動的な (WS-Federation) シナリオで使用されるクラスが含まれます。 `Microsoft.IdentityModel.Web` 名前空間のクラスが含まれます。|
|<xref:System.ServiceModel.Security?displayProperty=nameWithType>|アクティブな (WS-Trust) シナリオで使用される WCF のコントラクト、チャネル、サービス ホスト、およびその他の成果物を表すクラスは、現在はこの名前空間にあります。 WIF 3.5 では、これらのクラスは `Microsoft.IdentityModel.Protocols.WSTrust` 名前空間にありました。|

> [!IMPORTANT]
> `System.IdentityModel`、<xref:System.IdentityModel.Claims?displayProperty=nameWithType>、および <xref:System.IdentityModel.Policy?displayProperty=nameWithType> という <xref:System.IdentityModel.Selectors?displayProperty=nameWithType> 名前空間には、WCF クレーム ベースの ID モデルを実装するクラスが含まれます。 WCF クレーム ベース ID モデルは WIF に置き換えられています。 WIF に基づいてソリューションをビルドする際は、これら 3 つの名前空間でクラスを使用しないでください。

### <a name="changes-due-to-net-integration"></a>.NET の統合による変更

WIF は現在、.NET Framework に統合されています。 ほとんどの .NET の ID とプリンシパル クラスは、<xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType> と <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> から派生します。 WIF 4.5 での次の変更による結果:

- クレーム、ID、およびプリンシパルを表す WIF クラスは、現在は <xref:System.Security.Claims?displayProperty=nameWithType> 名前空間にあります。

    > [!IMPORTANT]
    > <xref:System.IdentityModel.Claims?displayProperty=nameWithType> 名前空間には、WCF クレーム ベースの ID モデルで成果物を表すクラスが含まれます。 これらのクラスの多くは、WIF クラスと同じ名前を持ちます (`Claims` など)。 WIF に基づいてソリューションをビルドする場合は、これらのクラスは使用しないでください。

- .NET の ID およびプリンシパル クラスは、直接 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType> と <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> から派生します。 したがって、WIF 3.5 インターフェイス `IClaimsIdentity` と `IClaimsPrincipal` は不要になり、WIF 4.5 では使用できません。

- <xref:System.Security.Principal.WindowsIdentity?displayProperty=nameWithType> および <xref:System.Security.Principal.WindowsPrincipal?displayProperty=nameWithType> などの .NET の ID およびプリンシパル クラスは、<xref:System.Security.Claims.ClaimsIdentity> および <xref:System.Security.Claims.ClaimsPrincipal> から派生し、組み込みのクレーム機能を備えています。 したがって、WIF 3.5 にあった `WindowsClaimsIdentity` と `WindowsClaimsPrincipal` などのクレーム固有の ID およびプリンシパル クラスは不要になり、WIF 4.5 には存在しません。

### <a name="other-changes-to-wif-functionality"></a>WIF 機能のその他の変更

名前空間の変更と.NET との統合による変更に加えて、WIF 4.5 では WIF 機能に対する次の一般的な変更が行われています。

- 特定の SOAP エラーに例外を対応付ける機能を備えていた `Microsoft.IdentityModel.ExceptionMapper` クラスは削除されます。

- 例外のサーフェイスは大幅に削減されました。

- プロトコルまたは WS-* 固有の定数を定義したクラスの多く (たとえば、WS-Addressing 1.0 に関連する定数を定義した `Microsoft.IdentityModel.WSAddressing10Constants` クラスなど) は削除されます。

- `Microsoft.IdentityModel.WindowsTokenService` 名前空間の Claims to Windows Token Service (c2wts) とその関連クラスが削除されます。

### <a name="wif-configuration-changes"></a>WIF 構成の変更

構成ファイルの変更の多くは WIF 4.5 での名前空間の更新により発生しました。 たとえば、WS-Federation Authentication Manager をアプリケーションに追加するため、`<httpModules>` セクションの次の WIF 3.5 エントリについて考えます。

```xml
<add name="WSFederationAuthenticationModule" type="Microsoft.IdentityModel.Web.WSFederationAuthenticationModule, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=abcd … 5678" />
```

このエントリは WIF 4.5 で新しい名前空間とアセンブリのバージョンを含むように更新されています。

```xml
<add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcd … 5678"/>
```

次の一覧に、WIF 4.5 用の構成ファイルへの主要な変更を示します。

- `<microsoft.identityModel>` セクションは、[\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) セクションになっています。

- `<service>` 要素は、[\<identityConfiguration>](../configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 要素になっています。

- 新しいセクション [\<system.identityModel.services>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) は、受動的な (WS-Federation) シナリオで動作を制御する設定を指定するために追加されました。

- [\<federationConfiguration>](../configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 要素とその子要素は、WIF 3.5 の `<service>` 要素から新しい `<system.identityModel.services>` 要素に移動されました。

- WIF 3.5 では `<service>` 要素の直下のサービスレベルで指定できた複数の要素が、[\<securityTokenHandlerConfiguration>](../configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) 要素での指定に制限されました (WIF 4.5 では、下位互換性を維持するため、これらは [\<identityConfiguration>](../configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 要素で指定できます)。

WIF 4.5 の構成要素の詳細な一覧については、「[WIF Configuration Schema](../configure-apps/file-schema/windows-identity-foundation/index.md)」(WIF 構成スキーマ) を参照してください。

### <a name="visual-studio-tooling-changes"></a>Visual Studio ツールの変更

WIF 3.5 SDK では、スタンドアロンのフェデレーション ユーティリティである FedUtil.exe (FedUtil) が用意されており、これを使用して WIF 対応アプリケーションでの ID 管理をセキュリティ トークン サービス (STS) に外部委託できました。 このツールにより、WIF の設定がアプリケーション構成ファイルに追加され、アプリケーションは 1 つ以上の STS からセキュリティ トークンを取得できました。また **[STS サービス参照の追加]** ボタンによって Visual Studio に表示されました。 FedUtil は WIF 4.5 には付属していません。 代わりに、WIF 4.5 は Identity and Access Tool for Visual Studio 2012 という名前の新しい Visual Studio の拡張ツールをサポートします。これを使用することで、ID 管理を STS に外部委託するために必要な WIF の設定を備えたアプリケーションの構成ファイルを変更できます。 また Identity and Access Tool は、WIF 対応アプリケーションのテストに使用できる Local STS と呼ばれる STS を実装しています。 多くの場合、この機能により、開発中のソリューションをテストするのに WIF 3.5 で頻繁に必要とされたカスタム STS をビルドする必要がなくなりました。 したがって、STS のテンプレートは、Visual Studio 2012 でサポートされなくなりました。ただし、STS の開発をサポートするクラスは WIF 4.5 でも使用できます。

Visual Studio の Extensions and Updates Manager から Identity and Access Tool をインストールすることも、コードギャラリーの次のページからダウンロードすることもできます。[コードギャラリーの Visual Studio 2012 用 id およびアクセスツール](https://go.microsoft.com/fwlink/?LinkID=245849)。 Visual Studio ツールの変更を次のリストにまとめます。

- [STS サービス参照の追加] 機能は削除されています。 その代わりとなるのが Identity and Access Tool です。

- Visual Studio STS のテンプレートは削除されています。 Identity and Access Tool で入手可能な Local STS を使用でき、WIF を使用して開発した ID ソリューションをテストできます。 Local STS 構成を変更して、クレームをカスタマイズできます。

- スタンドアロンのフェデレーション ユーティリティ (FedUtil) は WIF 4.5 では使用できません。 Identity and Access Tool を使用して、構成ファイルを変更し、ID 管理を STS に外部委託できます。

Id およびアクセスツールの詳細については、「 [Visual Studio 2012 用 id およびアクセスツール](identity-and-access-tool-for-vs.md)」を参照してください。

<a name="BKMK_ToolingChanges"></a>

### <a name="passive-ws-federation-scenarios"></a>受動的な (WS-Federation) シナリオ:

- 受動的なシナリオをサポートするクラスが <xref:System.IdentityModel.Services?displayProperty=nameWithType> 名前空間に移動されました。 WIF 3.5 では、これらのクラスは `Microsoft.IdentityModel.Web` 名前空間にありました。

- `Microsoft.IdentityModel.Web.Configuration` 名前空間のクラスは <xref:System.IdentityModel.Services.Configuration?displayProperty=nameWithType>に移動されました。 これらのクラスは、受動的なシナリオの構成に固有のオブジェクトを表します。

- `FederatedPassiveSignInControl` はサポートされていません。`Microsoft.IdentityModel.Web.Controls` 名前空間のすべてのクラスは、WIF 4.5 から削除されました。

- WS-Federation 認証モジュール (<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>) のサインアウト機能は WIF 3.5 とは異なります。 WIF 4.5 でのサインアウトの機能の詳細については、<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> クラスのトピックを参照してください。

### <a name="active-wcfws-trust-scenarios"></a>アクティブな (WCF/WS-Trust) シナリオ:

- `Microsoft.IdentityModel.Protocols.WSTrust` 名前空間は、WIF 4.5 の主に 2 つの名前空間に分割されています。 WS-Trust プロトコル固有の成果物を表すクラスは <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType> にあります。 これには <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken> などのクラスが含まれます。 WCF アプリケーションで WS-Trust を使用して、含まれているサービス コントラクト、チャネル、サービス ホスト、およびその他の成果物を表すクラスは、<xref:System.ServiceModel.Security?displayProperty=nameWithType> に移動されました (<xref:System.ServiceModel.Security.IWSTrust13AsyncContract> インターフェイスなど)。

- WIF を使用するための WCF アプリケーションの構成は、大幅に単純化されました。 以前は `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` は動作拡張として追加する必要があり、`<federatedServiceHostConfiguration>` 要素を指定することで、この機能を使用して WIF をサービス動作に追加していました。 WIF 4.5 は WCF とより密接に統合されました。 これで、次の XML に示すように `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>` 要素で `useIdentityConfiguration` 属性を指定することで WCF サービス上で WIF を有効にできます。

    ```xml
    <serviceCredentials useIdentityConfiguration="true">
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />
    </serviceCredentials>
    ```

- WIF 4.5 では、アクティブな (WCF) サービスが使用するサービス証明書はサービス ホストで指定する必要があります。 構成では、前の例に示すように `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>`/`<serviceCertificate>` 要素でこれを指定できます。 WIF 3.5 では、サービス証明書は WIF の `<serviceCertificate>` 要素の `<service>` 子要素により指定できます。 この機能は WIF 4.5 にはないため、代わりに `<serviceCertificate>` 要素の `<serviceCredentials>` 要素を指定します。

- WCF に WIF 3.5 を追加するために使用されていたクラスは存在しません。 これには `Microsoft.IdentityModel.Tokens` 名前空間の `FederatedSecurityTokenManager`、`FederatedServiceCredentials`、`IdentityModelServiceAuthorizationManager`、および `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` クラスが含まれています。

## <a name="enabling-wif-35-in-windows-8"></a>Windows 8 で WIF 3.5 を有効にする

WIF 4.5 は .NET 4.5 の一部であるため、Windows 8 および Windows Server 2012 を実行するコンピューターで自動的に有効になり、WIF 4.5 を使用して作成されたアプリケーションは、既定では Windows 8 または Windows Server 2012 で実行されます。 ただし、WIF 3.5 を使用して作成されたアプリケーションは、Windows 8 または Windows Server 2012 を実行しているコンピューター上で実行することが必要になる場合があります。 この場合、ターゲット コンピューターで WIF 3.5 を有効にする必要があります。 これは、Windows 8 を実行するコンピューター上で、展開イメージのサービスと管理 (DISM) ツールを使用して行うことができます。 Windows Server 2012 を実行するコンピューターで、DISM ツールを使用するか、または Windows PowerShell の `Add-WindowsFeature` コマンドレットを使用できます。 どちらの場合も、適切なコマンドは、コマンド ラインまたは Windows PowerShell の環境内から呼び出すことができます。

次のコマンドは、DISM ツールをコマンド ラインまたは Windows PowerShell の環境内から使用する方法を示します。 既定では、DISM PowerShell モジュールは Windows 8 および Windows Server 2012 に含まれるので、インポートする必要はありません。 Windows PowerShell を使用した DISM の使い方の詳細については、「[Windows PowerShell の DISM の使用方法](https://go.microsoft.com/fwlink/?LinkId=254419)」を参照してください。

DISM を使用して WIF 3.5 を有効にするには:

```console
dism /online /enable-feature:windows-identity-foundation
```

DISM を使用して WIF 3.5 を無効にするには:

```console
dism /online /disable-feature:windows-identity-foundation
```

DISM を使用して有効または無効にする機能を確認するには:

```console
dism /online /get-features
```

または、Windows Server 2012 を実行するコンピューターで Windows PowerShell コマンドレット `Add-WindowsFeature` を使用して WIF 3.5 を有効にすることができます。 コマンド ラインから実行するには、次のコマンドを入力します。

```console
powershell "add-windowsfeature windows-identity-foundation"
```

 Windows PowerShell の環境内から、直接コマンドを入力できます。

```powershell
Add-WindowsFeature windows-identity-foundation
```

> [!NOTE]
> WIF 3.5 および WIF 4.5 では多くのクラスが同じ名前を持つため、WIF 3.5 と WIF 4.5 の両方を使用している場合は、完全修飾クラス名、または WIF 3.5 および WIF 4.5 でクラスを区別するための名前空間エイリアスを必ず使用してください。

## <a name="see-also"></a>関連項目

- [WIF 構成スキーマ](../configure-apps/file-schema/windows-identity-foundation/index.md)
- [WIF 3.5 と WIF 4.5 間での名前空間マッピング](namespace-mapping-between-wif-3-5-and-wif-4-5.md)
- [Windows Identity Foundation 4.5 の新機能](whats-new-in-wif.md)
- [Visual Studio 2012 の ID およびアクセス ツール](identity-and-access-tool-for-vs.md)
