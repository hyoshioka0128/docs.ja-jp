---
ms.openlocfilehash: 92210f6becb5a5a43893ee0fd51ef51e2ddd7f8d
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325239"
---
### <a name="kestrel-http2-disabled-over-tls-on-incompatible-windows-versions"></a>Kestrel: 互換性のない Windows バージョンでの TLS 経由の HTTP/2 の無効化

Windows で HTTP/2 over TLS (トランスポート層セキュリティ) を有効にするには、次の 2 つの要件を満たす必要があります。

- アプリケーション層プロトコル ネゴシエーション (ALPN) のサポート。これは、Windows 8.1 および Windows Server 2012 R2 以降で使用できます。
- HTTP/2 と互換性のある暗号のセット。これは、Windows 10 および Windows Server 2016 以降で使用できます。

そのため、HTTP/2 over TLS が構成されている場合の Kestrel の動作は、次のように変更されました。

- `Http1` にダウングレードし、[ListenOptions.HttpProtocols](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.httpprotocols) が `Http1AndHttp2` に設定されている場合は、`Information` レベルでメッセージをログに記録します。 `ListenOptions.HttpProtocols` の既定値は `Http1AndHttp2` です。
- `ListenOptions.HttpProtocols` が `Http2` に設定されている場合は、`NotSupportedException` をスローします。

ディスカッションについては、イシュー [dotnet/aspnetcore#23068](https://github.com/dotnet/aspnetcore/issues/23068) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

ASP.NET Core 5.0 Preview 7

#### <a name="old-behavior"></a>以前の動作

次の表には、HTTP/2 over TLS が構成されている場合の動作の概要が示されています。

| プロトコル | Windows 7、<br />Windows Server 2008 R2、<br />またはそれ以前 | Windows 8、<br />Windows Server 2012 | Windows 8.1、<br />Windows Server 2012 R2 | Windows 10、<br />Windows Server 2016、<br />またはそれ以降 |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | `NotSupportedException` をスローする                   | TLS ハンドシェイク中にエラーが発生する     | TLS ハンドシェイク中にエラーが発生する &ast;     | エラーなし |
| `Http1AndHttp2` | `Http1` にダウングレードする                    | `Http1` にダウングレードする     | TLS ハンドシェイク中にエラーが発生する &ast;     | エラーなし |

&ast; 互換性のある暗号スイートを構成して、これらのシナリオを有効にします。

#### <a name="new-behavior"></a>新しい動作

次の表には、HTTP/2 over TLS が構成されている場合の動作の概要が示されています。

| プロトコル | Windows 7、<br />Windows Server 2008 R2、<br />またはそれ以前 | Windows 8、<br />Windows Server 2012 | Windows 8.1、<br />Windows Server 2012 R2 | Windows 10、<br />Windows Server 2016、<br />またはそれ以降 |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | `NotSupportedException` をスローする                   | `NotSupportedException` をスローする     | `NotSupportedException` をスローする &ast;&ast;     | エラーなし |
| `Http1AndHttp2` | `Http1` にダウングレードする                    | `Http1` にダウングレードする     | `Http1` にダウングレードする &ast;&ast;     | エラーなし |

&ast;&ast; 互換性のある暗号スイートを構成し、アプリ コンテキスト スイッチ `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` を `true` に設定して、これらのシナリオを有効にします。

#### <a name="reason-for-change"></a>変更理由

この変更によって、以前の Windows バージョンでの HTTP/2 TLS over TLS の互換性エラーができるだけ早い段階で明確に示されるようになります。

#### <a name="recommended-action"></a>推奨アクション

互換性のない Windows バージョンで HTTP/2 over TLS が無効になるようにします。 Windows 8.1 および Windows Server 2012 R2 は、既定で必要な暗号がないため、互換性はありません。 しかし、HTTP/2 と互換性のある暗号を使用するように、コンピューターの構成設定を更新することは可能です。 詳細については、「[Windows 8.1 の TLS 暗号スイート](/windows/win32/secauthn/tls-cipher-suites-in-windows-8-1)」を参照してください。 構成が完了したら、アプリ コンテキスト スイッチ `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` を設定し、Kestrel で HTTP/2 over TLS を有効にする必要があります。 次に例を示します。

```csharp
AppContext.SetSwitch("Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2", true);
```

基になるサポートは変更されていません。 たとえば、Windows 8 や Windows Server 2012 で HTTP/2 over TLS が動作したことはありません。 この変更により、これらのサポートされていないシナリオでのエラーの表示方法が変わります。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

None

<!--

#### Affected APIs

Not detectable via API analysis

-->
