---
ms.openlocfilehash: 5c86be598ab6196ecf4da05451c7f22d2be52c12
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614697"
---
### <a name="default-value-of-servicepointmanagersecurityprotocol-is-securityprotocoltypesystemdefault"></a>ServicePointManager.SecurityProtocol の既定値は SecurityProtocolType.System.Default

#### <a name="details"></a>説明

.NET Framework 4.7 を対象とするアプリから、<xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> プロパティの既定値が <xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType> になります。 この変更により、SslStream をベースとする NET Framework ネットワーク API (FTP、HTTPS、SMTP など) は、.NET Framework によって定義されるハード コーディングされた値を使用する代わりに、オペレーティング システムから既定のセキュリティ プロトコルを継承できます。 既定値はオペレーティング システムと、システム管理者が実行するカスタム構成によって異なります。 Windows オペレーティング システムの各バージョンにおける既定の SChannel プロトコルについては、「[Protocols in TLS/SSL (Schannel SSP)](https://docs.microsoft.com/windows/desktop/SecAuthN/protocols-in-tls-ssl--schannel-ssp-)」 (TLS/SSL のプロトコル (Schannel SSP)) を参照してください。</p>以前のバージョンの .NET Framework を対象とするアプリケーションの場合、<xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> プロパティの既定値は、対象となる .NET Framework のバージョンに依存します。 詳細については、「.NET Framework 4.5.2 から 4.6 への移行に関する変更の再ターゲット」の「[ネットワーキング](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#networking)」セクションを参照してください。

#### <a name="suggestion"></a>提案される解決策

この変更は、.NET Framework 4.7 以降のバージョンを対象とするアプリケーションに影響します。 システム初期設定に依存せず、はっきり定められたプロトコルを使用する場合、<xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> プロパティの値を明示的に設定できます。 この変更が望ましくない場合、アプリケーション構成ファイルの [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに構成設定を追加して、無効にすることができます。 次の例では、`<runtime>` セクションと無効に切り替える処理 `Switch.System.Net.DontEnableSystemDefaultTlsVersions` の両方を確認できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSystemDefaultTlsVersions=true" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType>
