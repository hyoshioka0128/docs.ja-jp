---
ms.openlocfilehash: 3244a36808fb687663241e704d08775ea5c96720
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803246"
---
### <a name="kestrel-default-supported-tls-protocol-versions-changed"></a>Kestrel: 既定でサポートされている TLS プロトコル バージョンの変更

Kestrel では現在、以前のように TLS 1.1 プロトコルと TLS 1.2 プロトコルへの接続を制限するのではなく、システム既定の TLS プロトコル バージョンを使用します。

この変更で可能になること:

* それをサポートする環境で TLS 1.3 を既定で使用できます。
* TLS 1.0 を一部の環境 (既定の Windows Server 2016 など) で使用できます。通常、これは[望ましくありません](/security/engineering/solving-tls1-problem)。

ディスカッションについては、イシュー [dotnet/aspnetcore#22563](https://github.com/dotnet/aspnetcore/issues/22563) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 6

#### <a name="old-behavior"></a>以前の動作

Kestrel では既定で、TLS 1.1 または TLS 1.2 を接続に使用する必要がありました。

#### <a name="new-behavior"></a>新しい動作

Kestrel では、使用に最適なプロトコルを選択し、セキュリティに保護されていないプロトコルをブロックすることがオペレーティング システムに許可されます。 <xref:Microsoft.AspNetCore.Server.Kestrel.Https.HttpsConnectionAdapterOptions.SslProtocols%2A?displayProperty=nameWithType> は既定で `SslProtocols.Tls12 | SslProtocols.Tls11` ではなく `SslProtocols.None` になりました。

#### <a name="reason-for-change"></a>変更理由

TLS 1.3 と、将来の TLS バージョンが利用できるようになったときにそれをサポートする目的で変更が行われました。

#### <a name="recommended-action"></a>推奨アクション

アプリケーション側に特別な理由がある場合を除き、新しい既定値を使用してください。 セキュリティで保護されているプロトコルのみを許可するようにシステムが構成されていることを確認してください。

以前のプロトコルを無効にするには、次のいずれかのアクションを行います。

* [Windows の指示に従い](/dotnet/framework/network-programming/tls#configuring-schannel-protocols-in-the-windows-registry)、TLS 1.0 など、古いプロトコルをシステム全体で無効にします。 現在のところ、すべての Windows バージョンで既定で有効になっています。
* コードでサポートするプロトコルを次のように手動で選択します。

    ```csharp
    using System.Security.Authentication;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.Extensions.Hosting;

    public class Program
    {
        public static void Main(string[] args) =>
            CreateHostBuilder(args).Build().Run();

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseKestrel(kestrelOptions =>
                    {
                        kestrelOptions.ConfigureHttpsDefaults(httpsOptions =>
                        {
                            httpsOptions.SslProtocols = SslProtocols.Tls12 | SslProtocols.Tls13;
                        });
                    });

                    webBuilder.UseStartup<Startup>();
                });
    }
    ```

残念ながら、特定のプロトコルを除外する API はありません。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.Server.Kestrel.Https.HttpsConnectionAdapterOptions.SslProtocols%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

`P:Microsoft.AspNetCore.Server.Kestrel.Https.HttpsConnectionAdapterOptions.SslProtocols`

-->
