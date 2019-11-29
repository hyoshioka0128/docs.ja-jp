---
title: 資格情報の呼び出し-WCF 開発者向けの gRPC
description: ASP.NET Core 3.0 で gRPC 通話資格情報を実装して使用する方法。
ms.date: 09/02/2019
ms.openlocfilehash: 2588fe3590a63ea6071b85ff29b3685efbfa25db
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967999"
---
# <a name="call-credentials"></a>資格情報を呼び出す

呼び出し資格情報は、すべての要求に対してメタデータで渡される何らかの種類のトークンに基づいています。

## <a name="ws-federation"></a>WS-Federation

ASP.NET Core は、 [wsfederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) NuGet パッケージを使用した ws-federation をサポートしています。 WS フェデレーションは、HTTP/2 でサポートされていない Windows 認証の代替として使用できる最も近いものです。 ユーザーは Active Directory フェデレーションサービス (AD FS) (ADFS) を使用して認証されます。 ADFS は、ASP.NET Core での認証に使用できるトークンを提供します。

この認証方法の使用を開始する方法の詳細については、 [ASP.NET Core にある ws-federation を使用したユーザーの認証に](https://docs.microsoft.com/aspnet/core/security/authentication/ws-federation?view=aspnetcore-3.0)関する記事を参照してください。

## <a name="jwt-bearer-tokens"></a>JWT ベアラートークン

[JSON Web Token](https://jwt.io) standard には、エンコードされた文字列でユーザーとそのクレームに関する情報をエンコードし、コンシューマーが公開キー暗号化を使用してトークンの整合性を検証できるように、そのトークンに署名する方法が用意されています。 IdentityServer4 などのさまざまなサービスを使用して、ユーザーを認証し、gRPC と HTTP Api で使用する OpenID Connect (OIDC) トークンを生成することができます。

ASP.NET Core 3.0 では、JWT ベアラーパッケージを使用して JSON Web トークンを処理できます。 GRPC アプリケーションの構成は、ASP.NET Core MVC アプリケーションとまったく同じです。

この章では、WS-FEDERATION を使用した開発が簡単であるため、JWT ベアラートークンに焦点を当てています。

## <a name="adding-authentication-and-authorization-to-the-server"></a>サーバーへの認証と承認の追加

JWT ベアラーパッケージは、既定では ASP.NET Core 3.0 には含まれていません。 アプリに[AspNetCore JwtBearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer) NuGet パッケージをインストールします。

Startup クラスに認証サービスを追加し、JWT ベアラーハンドラーを構成します。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddGrpc();

    var signingKey = ObtainSigningKeySomehow();

    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters =
                new TokenValidationParameters
                {
                    ValidateAudience = false,
                    ValidateIssuer = false,
                    ValidateActor = false,
                    ValidateLifetime = true,
                    IssuerSigningKey = signingKey
                };
        });

}
```

`IssuerSigningKey` プロパティには、署名されたトークンを検証するために必要な暗号化データと共に `Microsoft.IdentityModels.Tokens.SecurityKey` の実装が必要です。 このトークンは、Azure KeyVault などの*シークレットサーバー*に安全に格納されている必要があります。

次に、承認サービスを追加します。これにより、システムへのアクセスが制御されます。

```csharp
    services.AddAuthorization(options =>
    {
        options.AddPolicy(JwtBearerDefaults.AuthenticationScheme, policy =>
        {
            policy.AddAuthenticationSchemes(JwtBearerDefaults.AuthenticationScheme);
            policy.RequireClaim(ClaimTypes.Name);
        });
    });

```

> [!TIP]
> 認証と承認は、2つの別個の手順です。 認証は、ユーザーの id を決定するために使用されます。 承認は、システムのさまざまな部分へのアクセスがユーザーに許可されているかどうかを判断します。

次に、認証と承認のミドルウェアを `Configure` メソッドの ASP.NET Core パイプラインに追加します。

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    // Authenticate, then Authorize
    app.UseAuthentication();
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapGrpcService<PortfolioService>();
    });
}
```

最後に、`[Authorize]` 属性をセキュリティで保護するすべてのサービスまたはメソッドに適用し、基になる `HttpContext` の `User` プロパティを使用してアクセス許可を確認します。

```csharp
[Authorize]
public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!TryValidateUser(request.TraderId, context.GetHttpContext().User))
    {
        throw new RpcException(new Status(StatusCode.PermissionDenied, "Denied."));
    }

    var portfolio = await _repository.GetAsync(traderId, request.PortfolioId);

    return new GetResponse
    {
        Portfolio = Portfolio.FromRepositoryModel(portfolio)
    };
}
```

## <a name="providing-call-credentials-in-the-client-application"></a>クライアントアプリケーションでの呼び出し資格情報の提供

Id サーバーから JWT トークンを取得したら、それを使用してクライアントからの gRPC 呼び出しを認証できます。そのためには、次のように呼び出しのメタデータヘッダーとして追加します。

```csharp
public async Task ShowPortfolioAsync(int portfolioId)
{
    var headers = new Grpc.Core.Metadata
    {
        { "Authorization", $"Bearer {_userToken}" }
    };
    var request = new GetRequest
    {
        TraderId = _userId,
        PortfolioId = portfolioId
    };
    var response = await _portfoliosClient.GetAsync(request, headers);

    // Display portfolio
}
```

これで、JWT ベアラートークンを呼び出し資格情報として使用して gRPC サービスがセキュリティで保護されました。 [認証と承認を追加したポートフォリオサンプル gRPC アプリケーション](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/PortfoliosSample/grpc/TraderSysAuth)のバージョンは、GitHub にあります。

>[!div class="step-by-step"]
>[前へ](security.md)
>[次へ](channel-credentials.md)
