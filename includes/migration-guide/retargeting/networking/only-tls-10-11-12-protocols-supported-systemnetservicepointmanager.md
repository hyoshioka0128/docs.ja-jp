---
ms.openlocfilehash: 87dc93ece10eaedbfbabddb5f857d0bcd12e05c4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615695"
---
### <a name="only-tls-10-11-and-12-protocols-supported-in-systemnetservicepointmanager-and-systemnetsecuritysslstream"></a>System.Net.ServicePointManager と System.Net.Security.SslStream で TLS 1.0、1.1、1.2 プロトコルのみサポート

#### <a name="details"></a>説明

.NET Framework 4.6 から、<xref:System.Net.ServicePointManager> クラスと <xref:System.Net.Security.SslStream> クラスには、Tls1.0、Tls1.1、Tls 1.2 という 3 つのプロトコルのいずれかを使用することのみが許可されます。 SSL3.0 プロトコルと RC4 の暗号化はサポートされていません。

#### <a name="suggestion"></a>提案される解決策

推奨される軽減策はサーバー側のアプリを Tls1.0、Tls1.1、または Tls1.2 にアップグレードすることです。 これが現実的でない場合、またはクライアント アプリが破損している場合は、次の 2 つの方法のいずれかにより、<xref:System.AppContext?displayProperty=fullName> クラスを使用してこの機能を除外できます。

- プログラムで <xref:System.AppContext?displayProperty=fullName> の互換性スイッチを設定する (説明は[こちら](https://devblogs.microsoft.com/dotnet/net-announcements-at-build-2015/#dotnet46)にあります)。
- app.config ファイルの `<runtime>` セクションに以下の行を追加する。

```xml
<AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchUseStrongCrypto=true"/>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.SecurityProtocolType.Ssl3?displayProperty=nameWithType>
- <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>
- <xref:System.Security.Authentication.SslProtocols.Ssl2?displayProperty=nameWithType>
- <xref:System.Security.Authentication.SslProtocols.Ssl3?displayProperty=nameWithType>
