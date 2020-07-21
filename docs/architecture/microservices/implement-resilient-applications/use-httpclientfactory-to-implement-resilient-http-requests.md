---
title: IHttpClientFactory を使用して回復力の高い HTTP 要求を実装する
description: .NET Core 2.1 以降で使用できる IHttpClientFactory を使用して、`HttpClient` インスタンスを作成し、それをアプリケーションで簡単に使用できるようにする方法について説明します。
ms.date: 03/03/2020
ms.openlocfilehash: ade26208a931faa456c8e267def2caef7a3f32de
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82507300"
---
# <a name="use-ihttpclientfactory-to-implement-resilient-http-requests"></a>IHttpClientFactory を使用して回復力の高い HTTP 要求を実装する

<xref:System.Net.Http.IHttpClientFactory> はコントラクトであり、ご利用のアプリケーションで使用する <xref:System.Net.Http.HttpClient> インスタンスを作成するために .NET Core 2.1 以降で使用できる自己主張の強いファクトリ `DefaultHttpClientFactory` によって実装されます。

## <a name="issues-with-the-original-httpclient-class-available-in-net-core"></a>.NET Core で使用可能な元の HttpClient クラスに関する問題

よく知られている元の <xref:System.Net.Http.HttpClient> クラスは、簡単に使用できますが、場合によっては、多くの開発者が適切に使用していません。

このクラスでは `IDisposable` が実装されますが、これを `using` ステートメント内で宣言およびインスタンス化することはお勧めできません。その理由は、`HttpClient` オブジェクトが破棄されても、基になるソケットがすぐに解放されず、_ソケットの枯渇_の問題が発生する可能性があるということにあります。 この問題の詳細については、ブログ記事「[HttpClient の誤った使い方がソフトウェアを不安定にする](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)」を参照してください。

そのため、`HttpClient` は一度インスタンス化されたら、アプリケーションの有効期間にわたって再利用されることを目的としています。 すべての要求に対して `HttpClient` クラスをインスタンス化すると、高負荷の下で使用可能なソケットの数が枯渇してしまいます。 この問題により、`SocketException` エラーが発生します。 この問題を解決するために可能なアプローチは、HttpClient クライアントの使用に関するこの [Microsoft の記事](../../../csharp/tutorials/console-webapiclient.md)で説明されているように、`HttpClient` オブジェクトをシングルトンまたは静的として作成することに基づいています。 これは、1 日に数回実行される有効期間の短いコンソールアプリまたは類似のものに適したソリューションとなります。

開発者が遭遇するもう 1 つの問題は、長時間実行されるプロセスで `HttpClient` の共有インスタンスを使用するタイミングです。 HttpClient がシングルトンまたは静的オブジェクトとしてインスタンス化される状況では、dotnet/runtime GitHub リポジトリのこちらの[問題](https://github.com/dotnet/runtime/issues/18348)で説明されているように、DNS の変更を処理できません。

ただし、この問題は実際には `HttpClient` にあるのではなく、[HttpClient の既定のコンストラクター](https://docs.microsoft.com/dotnet/api/system.net.http.httpclient.-ctor?view=netcore-3.1#System_Net_Http_HttpClient__ctor)にあります。理由として、それによって、前述の "*ソケット枯渇*" および DNS 変更の問題を抱える、<xref:System.Net.Http.HttpMessageHandler> の新しい具象インスタンスが作成されるということが挙げられます。

上記の問題に対処し、`HttpClient` インスタンスを管理しやすくするために、.NET Core 2.1 では、<xref:System.Net.Http.IHttpClientFactory> インターフェイスが導入されました。これを使用すれば、依存関係の挿入 (DI) を介してアプリ内で `HttpClient` インスタンスを構成および作成することができます。 HttpClient でのハンドラーのデリゲートを利用するために、Polly ベースのミドルウェアに対する拡張機能も提供されます。

[Polly](http://www.thepollyproject.org/) は、事前に定義されたポリシーを緩やかでスレッドセーフな方法で使用することにより、開発者がアプリケーションに回復性を追加できるようにするための一時的な障害処理ライブラリです。

## <a name="benefits-of-using-ihttpclientfactory"></a>IHttpClientFactory を使用する利点

<xref:System.Net.Http.IHttpClientFactory> の現在の実装 (これによって <xref:System.Net.Http.IHttpMessageHandlerFactory> も実装される) には、次のような利点があります。

- 論理 `HttpClient` オブジェクトの名前付けと構成を行うために、中央の場所が提供されます。 たとえば、特定のマイクロサービスにアクセスするために事前に構成されているクライアント (サービス エージェント) を構成できます。
- `HttpClient` でのハンドラーのデリゲートにより送信ミドルウェアの概念を体系化し、Polly ベースのミドルウェアを実装して、回復性のための Polly のポリシーを利用します。
- `HttpClient` は既に、送信 HTTP 要求用にリンクできるハンドラーのデリゲートの概念を備えています。 ファクトリに HTTP クライアントを登録できるほか、Polly ハンドラーを使用して、再試行、サーキット ブレーカーなどに Polly ポリシーを使用することができます。
- <xref:System.Net.Http.HttpMessageHandler> の有効期間を管理して、`HttpClient` の有効期間を自分で管理する際に発生する可能性がある上記の問題を回避します。

> [!TIP]
> DI によって挿入された `HttpClient` インスタンスは、関連付けられた `HttpMessageHandler` がファクトリによって管理されるため、安全に破棄できます。 実際、挿入された `HttpClient` インスタンスは、DI パースペクティブから "*範囲指定*" されます。

> [!NOTE]
> `IHttpClientFactory` の実装 (`DefaultHttpClientFactory`) は、`Microsoft.Extensions.DependencyInjection` NuGet パッケージ内の DI の実装に緊密に関連付けられています。 その他の DI コンテナーの使用に関する詳細については、こちらの [GitHub のディスカッション](https://github.com/dotnet/extensions/issues/1345)を参照してください。

## <a name="multiple-ways-to-use-ihttpclientfactory"></a>IHttpClientFactory を使用する複数の方法

アプリケーションで `IHttpClientFactory` を使用するには、複数の方法があります。

- 基本的な使用方法
- 名前付きクライアントを使用する
- 型指定されたクライアントを使用する
- 生成されたクライアントを使用する

簡潔にするために、このガイダンスでは、型指定されたクライアント (サービス エージェント パターン) を使用する、`IHttpClientFactory` を使用するための最も構造化された方法を示します。 しかし、オプションはすべてドキュメント化されており、現在、[`IHttpClientFactory` の使用方法が記載されたこちらの記事](/aspnet/core/fundamentals/http-requests#consumption-patterns)で一覧表示されています。

## <a name="how-to-use-typed-clients-with-ihttpclientfactory"></a>IHttpClientFactory で型指定されたクライアントを使用する方法

それでは、"型指定されたクライアント" とは何でしょうか。 これは、特定の用途に合わせて事前に構成された `HttpClient` にすぎません。 この構成には、ベース サーバー、HTTP ヘッダー、またはタイムアウトなどの特定の値を含めることができます。

次の図は、`IHttpClientFactory` で型指定されたクライアントを使用する方法を示しています。

![IHttpClientFactory で型指定されたクライアントを使用する方法を示している図。](./media/use-httpclientfactory-to-implement-resilient-http-requests/client-application-code.png)

**図 8-4** 型指定されたクライアント クラスで `IHttpClientFactory` を使用する

上の図では、(コントローラーまたはクライアント コードによって使用される) `ClientService` によって、登録済みの `IHttpClientFactory` によって作成された `HttpClient` が使用されます。 このファクトリでは、プールからの `HttpClient` が `HttpMessageHandler` に割り当てられます。 拡張メソッド <xref:Microsoft.Extensions.DependencyInjection.HttpClientFactoryServiceCollectionExtensions.AddHttpClient*> を使用して `IHttpClientFactory` を DI コンテナーに登録するときに、Polly のポリシーを使用して `HttpClient` を構成できます。

上の構造を構成するには、<xref:Microsoft.Extensions.DependencyInjection.IServiceCollection> に対する <xref:Microsoft.Extensions.DependencyInjection.HttpClientFactoryServiceCollectionExtensions.AddHttpClient*> 拡張メソッドを含む `Microsoft.Extensions.Http` NuGet パッケージをインストールすることで、アプリケーションに <xref:System.Net.Http.IHttpClientFactory> を追加します。 この拡張メソッドでは、インターフェイス `IHttpClientFactory` のシングルトンとして使用される内部 `DefaultHttpClientFactory` クラスが登録されます。 これは <xref:Microsoft.Extensions.Http.HttpMessageHandlerBuilder> の一時的な構成を定義します。 プールから取得されたこのメッセージ ハンドラー (<xref:System.Net.Http.HttpMessageHandler> オブジェクト) は、ファクトリから返された `HttpClient` によって使用されます。

次のコードで、`AddHttpClient()` を使用して、`HttpClient` を使用する必要がある型指定されたクライアント (エージェント サービス) を登録する方法を確認できます。

```csharp
// Startup.cs
//Add http client services at ConfigureServices(IServiceCollection services)
services.AddHttpClient<ICatalogService, CatalogService>();
services.AddHttpClient<IBasketService, BasketService>();
services.AddHttpClient<IOrderingService, OrderingService>();
```

前のコードに示されているように、クライアント サービスを登録すると、`DefaultClientFactory` によって、サービスごとに標準の `HttpClient` が作成されるようになります。

また、次のコードに示すように、登録にインスタンス固有の構成を追加し、ベース アドレスの構成や回復性ポリシーの追加などを行うこともできます。

```csharp
services.AddHttpClient<ICatalogService, CatalogService>(client =>
{
    client.BaseAddress = new Uri(Configuration["BaseUrl"]);
})
    .AddPolicyHandler(GetRetryPolicy())
    .AddPolicyHandler(GetCircuitBreakerPolicy());
```

例として、次のコードで上記のポリシーの 1 つを確認できます。

```csharp
static IAsyncPolicy<HttpResponseMessage> GetRetryPolicy()
{
    return HttpPolicyExtensions
        .HandleTransientHttpError()
        .OrResult(msg => msg.StatusCode == System.Net.HttpStatusCode.NotFound)
        .WaitAndRetryAsync(6, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
}
```

[次の記事](implement-http-call-retries-exponential-backoff-polly.md)では、Polly の使用に関する詳細を確認できます。

### <a name="httpclient-lifetimes"></a>HttpClient の有効期間

`IHttpClientFactory` から `HttpClient` オブジェクトを取得するたび、新しいインスタンスが返されます。 ただし、各 `HttpClient` では、`HttpMessageHandler` の有効期間が切れていない限り、リソースの消費量を減らすために `IHttpClientFactory` によってプールおよび再利用されている `HttpMessageHandler` を使用します。

通常各ハンドラーは基になる HTTP 接続を独自に管理しており、必要以上に多くのハンドラーを作成すると接続が遅延する可能性があるため、ハンドラーをプールするのは望ましい方法です。 また、一部のハンドラーは接続を無期限に開いており、DNS の変更にハンドラーが対応できないことがあります。

プール内の `HttpMessageHandler` オブジェクトには、有効期間があります。この有効期間は、プール内の `HttpMessageHandler` インスタンスを再利用できる期間です。 既定値は 2 分ですが、型指定されたクライアントごとにオーバーライドできます。 オーバーライドするには、次のコードに示すように、クライアント作成時に返された <xref:Microsoft.Extensions.DependencyInjection.IHttpClientBuilder> で `SetHandlerLifetime()` を呼び出します。

```csharp
//Set 5 min as the lifetime for the HttpMessageHandler objects in the pool used for the Catalog Typed Client
services.AddHttpClient<ICatalogService, CatalogService>()
    .SetHandlerLifetime(TimeSpan.FromMinutes(5));
```

型指定された各クライアントには、独自の構成済みハンドラーの有効期間の値を設定できます。 ハンドラーの有効期限を無効にするには、有効期間を `InfiniteTimeSpan` に設定します。

### <a name="implement-your-typed-client-classes-that-use-the-injected-and-configured-httpclient"></a>挿入された構成済みの HttpClient を使用する、型指定されたクライアント クラスを実装する

前の手順では、型指定されたクライアント クラス (サンプル コードにある、'BasketService'、'CatalogService'、'OrderingService' のようなクラスなど) が定義されている必要がありました。型指定されたクライアントは、(そのコンストラクターを通じて挿入された) `HttpClient` オブジェクトを受け取り、それを使用していくつかのリモート HTTP サービスを呼び出すクラスです。 次に例を示します。

```csharp
public class CatalogService : ICatalogService
{
    private readonly HttpClient _httpClient;
    private readonly string _remoteServiceBaseUrl;

    public CatalogService(HttpClient httpClient)
    {
        _httpClient = httpClient;
    }

    public async Task<Catalog> GetCatalogItems(int page, int take,
                                               int? brand, int? type)
    {
        var uri = API.Catalog.GetAllCatalogItems(_remoteServiceBaseUrl,
                                                 page, take, brand, type);

        var responseString = await _httpClient.GetStringAsync(uri);

        var catalog = JsonConvert.DeserializeObject<Catalog>(responseString);
        return catalog;
    }
}
```

型指定されたクライアント (この例では `CatalogService`) は、依存関係の挿入 (DI) によってアクティブ化されます。つまり `HttpClient` だけでなく、そのコンストラクター内に登録されている任意のサービスを受け取ることができます。

型指定されたクライアントは、実際には、一時的なオブジェクトです。つまり、新しいインスタンスは必要になるたびに作成され、新しい `HttpClient` インスタンスが構築されるたびにそれを受け取ります。 ただし、プール内の `HttpMessageHandler` オブジェクトは、複数の `HttpClient` 要求で再利用されるオブジェクトです。

### <a name="use-your-typed-client-classes"></a>型指定されたクライアント クラスを使用する

最後に、型指定されたクラスを実装し、`AddHttpClient()` に登録して構成したら、DI によってサービスを挿入できる場所であればどこでもそれらを使用できます。 たとえば、次の eShopOnContainers のコードのように、Razor ページ コード、または MVC Web アプリのコントローラーなどがあります。

```csharp
namespace Microsoft.eShopOnContainers.WebMVC.Controllers
{
    public class CatalogController : Controller
    {
        private ICatalogService _catalogSvc;

        public CatalogController(ICatalogService catalogSvc) =>
                                                           _catalogSvc = catalogSvc;

        public async Task<IActionResult> Index(int? BrandFilterApplied,
                                               int? TypesFilterApplied,
                                               int? page,
                                               [FromQuery]string errorMsg)
        {
            var itemsPage = 10;
            var catalog = await _catalogSvc.GetCatalogItems(page ?? 0,
                                                            itemsPage,
                                                            BrandFilterApplied,
                                                            TypesFilterApplied);
            //… Additional code
        }

        }
}
```

この時点までは、示されているコードは、通常の Http 要求を実行するだけですが、次のセクションでは、"不思議なこと" が起こります。ポリシーを追加して、ハンドラーを登録済みの型指定されているクライアントにデリゲートするだけで、`HttpClient` によって実行されるすべての HTTP 要求が、指数バックオフを含む再試行、サーキット ブレーカー、またはその他の任意のカスタム デリゲート ハンドラーなど、回復力のあるポリシーを考慮して、追加のセキュリティ機能 (認証トークンの使用など) やその他のカスタム機能を実装するようになります。

## <a name="additional-resources"></a>その他の技術情報

- **.NET Core で HttpClientFactory を使用する**  
  [https://docs.microsoft.com/aspnet/core/fundamentals/http-requests](/aspnet/core/fundamentals/http-requests)

- **`dotnet/extensions` GitHub リポジトリ内の HttpClientFactory ソース コード**  
  <https://github.com/dotnet/extensions/tree/master/src/HttpClientFactory>

- **Polly (.NET の復元および一時的な障害処理ライブラリ)**  
  <http://www.thepollyproject.org/>
  
- **依存関係挿入なしで IHttpClientFactory を使用する (GitHub の問題)**  
  <https://github.com/dotnet/extensions/issues/1345>

>[!div class="step-by-step"]
>[前へ](implement-resilient-entity-framework-core-sql-connections.md)
>[次へ](implement-http-call-retries-exponential-backoff-polly.md)
