---
ms.openlocfilehash: 9a747d8fc15ca8fa2b915f89291f118d7344d172
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325211"
---
### <a name="httpsys-client-certificate-renegotiation-disabled-by-default"></a>HttpSys:既定で無効になっているクライアント証明書の再ネゴシエーション

接続を再ネゴシエートし、クライアント証明書を要求するオプションは既定で無効になっています。 ディスカッションについては、イシュー [dotnet/aspnetcore#23181](https://github.com/dotnet/aspnetcore/issues/23181) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

ASP.NET Core 5.0

#### <a name="old-behavior"></a>以前の動作

接続を再ネゴシエートし、クライアント証明書を要求できます。

#### <a name="new-behavior"></a>新しい動作

クライアント証明書は、初回接続ハンドシェイク中にのみ要求できます。 詳細については、pull request [dotnet/aspnetcore#23162](https://github.com/dotnet/aspnetcore/pull/23162) を参照してください。

#### <a name="reason-for-change"></a>変更理由

再ネゴシエーションによって、パフォーマンスとデッドロックのさまざまな問題が発生しました。 また、HTTP/2 でサポートされていません。 この動作を制御するオプションが ASP.NET Core 3.1 で導入されて以降の追加コンテキストについては、イシュー [dotnet/aspnetcore#14806](https://github.com/dotnet/aspnetcore/issues/14806) を参照してください。

#### <a name="recommended-action"></a>推奨アクション

クライアント証明書を必要とするアプリでは *netsh.exe* を使用し、`clientcertnegotiation` オプションを `enabled` に設定する必要があります。 詳細については、「[netsh http コマンド](/windows-server/networking/technologies/netsh/netsh-http)」を参照してください。

クライアント証明書をアプリの一部のみで有効にする場合、「[オプションのクライアント証明書](/aspnet/core/security/authentication/certauth?view=aspnetcore-3.1#optional-client-certificates)」にあるガイダンスをご覧ください。

以前の再ネゴシエート動作が必要な場合、以前の値である `ClientCertificateMethod.AllowRenegotiate` に `HttpSysOptions.ClientCertificateMethod` を設定してください。 これは上述の理由から推奨されておらず、リンク先のガイダンスで推奨されていません。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.AspNetCore.Http.ConnectionInfo.ClientCertificate%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.ConnectionInfo.GetClientCertificateAsync%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ClientCertificateMethod%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:Microsoft.AspNetCore.Http.ConnectionInfo.ClientCertificate`
- `Overload:Microsoft.AspNetCore.Http.ConnectionInfo.GetClientCertificateAsync`
- `Overload:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ClientCertificateMethod`

-->
