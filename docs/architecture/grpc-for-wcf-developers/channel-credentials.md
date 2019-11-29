---
title: チャネル資格情報-WCF 開発者向け gRPC
description: ASP.NET Core 3.0 で gRPC チャネル資格情報を実装して使用する方法について説明します。
ms.date: 09/02/2019
ms.openlocfilehash: b424db49337a2dc6e3d0245d36349e3f408cdf6c
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967959"
---
# <a name="channel-credentials"></a>チャンネルの資格情報

名前が示すように、チャネルの資格情報は、基になる gRPC チャネルにアタッチされます。 標準形式のチャネル資格情報では、クライアント証明書認証が使用されます。この場合、クライアントは、接続時に TLS 証明書を提供します。これは、サーバーによって検証されてから、呼び出しを行うことができます。

チャネル資格情報を呼び出し資格情報と組み合わせて、gRPC サービスに包括的なセキュリティを提供することができます。 チャネル資格情報は、クライアントアプリケーションがサービスへのアクセスを許可されていることを証明し、呼び出し資格情報は、クライアントアプリケーションを使用しているユーザーに関する情報を提供します。

クライアント証明書の認証は、ASP.NET Core と同じように、gRPC に対して機能します。 ここでは構成プロセスについて概要を説明しますが、詳細については、「 [ASP.NET Core での証明書認証の構成](https://docs.microsoft.com/aspnet/core/security/authentication/certauth?view=aspnetcore-3.0)」を参照してください。

開発目的では自己署名証明書を使用できますが、運用環境では、信頼された機関によって署名された適切な HTTPS 証明書を使用する必要があります。

## <a name="adding-certificate-authentication-to-the-server"></a>サーバーに証明書認証を追加する

証明書認証は、Kestrel サーバーや ASP.NET Core パイプラインなど、ホストレベルで構成する必要があります。

### <a name="configuring-certificate-validation-on-kestrel"></a>Kestrel での証明書の検証の構成

クライアント証明書を要求するように Kestrel (ASP.NET Core HTTP サーバー) を構成し、必要に応じて、受信接続を受け入れる前に指定された証明書の検証を実行することができます。 この構成は、`Startup`ではなく、`Program` クラスの `CreateWebHostBuilder` メソッドで実行されます。

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            var serverCert = ObtainServerCertificate();
            webBuilder.UseStartup<Startup>()
                .ConfigureKestrel(kestrelServerOptions => {
                    kestrelServerOptions.ConfigureHttpsDefaults(opt =>
                    {
                        opt.ClientCertificateMode = ClientCertificateMode.RequireCertificate;

                        // Verify that client certificate was issued by same CA as server certificate
                        opt.ClientCertificateValidation = (certificate, chain, errors) =>
                            certificate.Issuer == serverCert.Issuer;
                    });
                });
        });

```

`ClientCertificateMode.RequireCertificate` 設定を使用すると、Kestrel がクライアント証明書を提供していない接続要求を直ちに拒否しますが、証明書は検証されません。 `ClientCertificateValidation` コールバックを追加すると、Kestrel は、接続が確立される時点でクライアント証明書 (この場合はサーバー証明書と同じ*証明機関*によって発行されたものであること) を検証することができます。この場合、ASP.NET Core パイプラインが使用されます。

### <a name="adding-aspnet-core-certificate-authentication"></a>ASP.NET Core 証明書認証の追加

証明書の認証は、 [AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) NuGet パッケージによって提供されます。

`ConfigureServices` メソッドに証明書認証サービスを追加し、`Configure` メソッドで ASP.NET Core パイプラインに認証と承認を追加します。

```csharp
public class Startup
{
    private readonly bool _isDevelopment;

    public Startup(IWebHostEnvironment env)
    {
        _isDevelopment = env.IsDevelopment();
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(CertificateAuthenticationDefaults.AuthenticationScheme)
            .AddCertificate(options =>
            {
                if (_isDevelopment)
                {
                    // DO NOT DO THIS IN PRODUCTION!
                    options.RevocationMode = X509RevocationMode.NoCheck;
                }
            });
        services.AddAuthorization();
        services.AddGrpc();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseRouting();

        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints => { endpoints.MapGrpcService<GreeterService>(); });
    }
}
```

## <a name="providing-channel-credentials-in-the-client-application"></a>クライアントアプリケーションでのチャネル資格情報の提供

`Grpc.Net.Client` パッケージでは、接続に使用される `GrpcChannel` に提供される <xref:System.Net.Http.HttpClient> インスタンスで証明書が構成されます。

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        // Assume path to a client .pfx file and password are passed from command line
        // On Windows this would probably be a reference to the Certificate Store
        var cert = new X509Certificate2(args[0], args[1]);

        var handler = new HttpClientHandler();
        handler.ClientCertificates.Add(cert);
        var httpClient = new HttpClient(handler);

        var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
        {
            HttpClient = httpClient
        });

        var grpc = new Greeter.GreeterClient(channel);
        var response = await grpc.SayHelloAsync(new HelloRequest { Name = "Bob" });
        System.Console.WriteLine(response.Message);
    }
}
```

## <a name="combining-channelcredentials-and-callcredentials"></a>ChannelCredentials と CallCredentials を組み合わせる

証明書の変更を Kestrel サーバーに適用し、ASP.NET Core で JWT ベアラーミドルウェアを使用することによって、証明書とトークン認証の両方を使用するようにサーバーを構成できます。

ChannelCredentials と CallCredentials の両方をクライアントに提供するには、`ChannelCredentials.Create` メソッドを使用して呼び出し資格情報を適用します。 証明書の認証は <xref:System.Net.Http.HttpClient> インスタンスを使用して適用する必要があります。 `SslCredentials` コンストラクターに引数を渡すと、内部クライアントコードが例外をスローします。 `SslCredentials` パラメーターは、`Grpc.Core` パッケージとの互換性を維持するために、`Grpc.Net.Client` パッケージの `Create` メソッドにのみ含まれています。

```csharp
var handler = new HttpClientHandler();
handler.ClientCertificates.Add(cert);

var httpClient = new HttpClient(handler);

var callCredentials = CallCredentials.FromInterceptor(((context, metadata) =>
    {
        metadata.Add("Authorization", $"Bearer {_token}");
    }));

var channelCredentials = ChannelCredentials.Create(new SslCredentials(), callCredentials);

var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
{
    HttpClient = httpClient,
    Credentials = channelCredentials
});

var grpc = new Portfolios.PortfoliosClient(channel);
```

> [!TIP]
> チャネルに対して行われたすべての呼び出しにトークン資格情報を渡す便利な方法として、証明書認証を使用しないクライアントには `ChannelCredentials.Create` メソッドを使用できます。

[証明書認証が追加された Fullstockticker サンプル gRPC アプリケーション](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker)のバージョンは、GitHub にあります。

>[!div class="step-by-step"]
>[前へ](call-credentials.md)
>[次へ](encryption.md)
