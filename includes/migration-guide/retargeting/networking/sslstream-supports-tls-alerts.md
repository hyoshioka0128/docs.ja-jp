---
ms.openlocfilehash: 0024b2a53444319788b8cdd312d537f994070b5e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614757"
---
### <a name="sslstream-supports-tls-alerts"></a>SslStream で TLS アラートに対応

#### <a name="details"></a>説明

TLS ハンドシェイクに失敗すると、最初の I/O 読み取り/書き込み操作によって <xref:System.IO.IOException?displayProperty=fullName> と内部例外 <xref:System.ComponentModel.Win32Exception?displayProperty=fullName> がスローされます。 [TLS および SSL アラートの Schannel エラー コード](https://docs.microsoft.com/windows/desktop/SecAuthN/schannel-error-codes-for-tls-and-ssl-alerts)を使用して、<xref:System.ComponentModel.Win32Exception?displayProperty=fullName> の <xref:System.ComponentModel.Win32Exception.NativeErrorCode?displayProperty=fullName> コードをリモート パーティからの TLS アラートにマップすることができます。詳しくは、[RFC 2246: セクション 7.2.2「Error alerts (エラー アラート)」](https://tools.ietf.org/html/rfc2246#section-7.2.2)を参照してください。 <br/>.NET Framework 4.6.2 およびそれより前のバージョンでの動作では、他のパーティがハンドシェイクに失敗してそのすぐ後に接続を拒否した場合、トランスポート チャネル (通常は TCP 接続) は書き込みまたは読み取り中にタイムアウトします。

#### <a name="suggestion"></a>提案される解決策

<xref:System.IO.Stream.Read(System.Byte[],System.Int32,System.Int32)>/<xref:System.IO.Stream.Write(System.Byte[],System.Int32,System.Int32)> などのネットワーク I/O API を呼び出すアプリケーションは、<xref:System.IO.IOException> または <xref:System.TimeoutException?displayProperty=fullName> を処理する必要があります。<br/>TLS アラート機能は、.NET Framework 4.7 以降では既定で有効になります。 .NET Framework 4.7 またはそれより後のシステムで動作する 4.0 から 4.6.2 のバージョンの .NET Framework を対象とするアプリケーションは、互換性を維持するためにこの機能を無効にします。 <br/>.NET Framework 4.7 以降で動作する .NET Framework 4.6 以降のアプリケーションでこの機能を有効または無効にするには、次の構成 API を使います。

- プログラムによる: ServicePointManager は 1 回のみ初期化するため、アプリケーションで行われる一番最初の動作にする必要があります。

    ```csharp
    AppContext.SetSwitch("TestSwitch.LocalAppContext.DisableCaching", true);

    // Set to 'false' to enable the feature in .NET Framework 4.6 - 4.6.2.
    AppContext.SetSwitch("Switch.System.Net.DontEnableTlsAlerts", true);
    ```

- AppConfig:

    ```xml
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Net.DontEnableTlsAlerts=true"/>
      <!-- Set to 'false' to enable the feature in .NET Framework 4.6 - 4.6.2. -->
    </runtime>
    ```

- レジストリ キー (マシン グローバル): .NET Framework 4.6 - 4.6.2 でこの機能を有効にするには、Value を `false` に設定します。

    ```ini
    Key: HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\AppContext\Switch.System.Net.DontEnableTlsAlerts
    - Type: String
    - Value: "true"
    ```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.Security.SslStream?displayProperty=nameWithType>
- <xref:System.Net.WebRequest?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>
- <xref:System.Net.FtpWebRequest?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.Http?displayProperty=nameWithType>
