---
ms.openlocfilehash: 44d33fb28e66e590e4604c6dd2c73616e4c5e943
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728299"
---
### <a name="http-httpclient-instances-created-by-ihttpclientfactory-log-integer-status-codes"></a>HTTP:IHttpClientFactory ログの整数状態コードによって作成された HttpClient インスタンス

<xref:System.Net.Http.IHttpClientFactory> によって作成された <xref:System.Net.Http.HttpClient> インスタンスでは、HTTP 状態コードが、状態コード名を付加するのではなく、整数としてログに記録されます。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="old-behavior"></a>以前の動作

ログの HTTP 状態コードに説明テキストが使用されます。 次にログ メッセージの例を示します。

```
Received HTTP response after 56.0044ms - OK
End processing HTTP request after 70.0862ms - OK
```

#### <a name="new-behavior"></a>新しい動作

ログの HTTP 状態コードに整数値が使用されます。 次にログ メッセージの例を示します。

```
Received HTTP response after 56.0044ms - 200
End processing HTTP request after 70.0862ms - 200
```

#### <a name="reason-for-change"></a>変更理由

このログの元の動作では、常に整数値が使用されている ASP.NET Core の他の部分と一貫性がありません。 一貫性がないため、[Elasticsearch](https://www.elastic.co/elasticsearch/) などの構造化ログ システムを使用したログのクエリが難しくなります。 詳細については、[dotnet/extensions#1549](https://github.com/dotnet/extensions/issues/1549) を参照してください。

整数値を使用すると、値の範囲に対してクエリを実行できるようになるため、テキストよりも柔軟性が向上します。

整数の状態コードを取得するログ値を別に追加することが検討されました。 残念ながら、これを行うと、ASP.NET Core の残りの部分にさらに不整合が生じます。 HttpClient ログと HTTP サーバー/ホスト ログで既に同じ `StatusCode` キー名が使用されています。

#### <a name="recommended-action"></a>推奨アクション

最適なオプションは、状態コードの整数値を使用するようにログ クエリを更新することです。 このオプションを選択すると、複数の ASP.NET Core バージョンに対するクエリの作成が難しくなる場合があります。 しかしながら、整数をこの目的に使用すると、ログのクエリの柔軟性が大きく向上します。

以前の動作との互換性を維持し、テキスト形式の状態コードを使用する必要がある場合は、`IHttpClientFactory` ログを独自のものに置き換えます。

1. 次のクラスの .NET Core 3.1 バージョンをプロジェクトにコピーします。

    * [LoggingHttpMessageHandlerBuilderFilter](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandlerBuilderFilter.cs)
    * [LoggingHttpMessageHandler](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandler.cs)
    * [LoggingScopeHttpMessageHandler](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingScopeHttpMessageHandler.cs)
    * [HttpHeadersLogValue](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/HttpHeadersLogValue.cs)

1. [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http) NuGet パッケージでパブリック型との競合を避けるために、クラスの名前を変更します。

1. プロジェクトの `Startup.ConfigureServices` メソッドで、`LoggingHttpMessageHandlerBuilderFilter` の組み込みの実装を独自のものに置き換えます。 次に例を示します。

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        // Other service registrations go first. Code omitted for brevity.

        // Place the following after all AddHttpClient registrations.
        var descriptors = services.Where(
            s => s.ServiceType == typeof(IHttpMessageHandlerBuilderFilter));
        foreach (var descriptor in descriptors)
        {
            services.Remove(descriptor);
        }

        services.AddSingleton<IHttpMessageHandlerBuilderFilter,
                              MyLoggingHttpMessageHandlerBuilderFilter>();
    }
    ```

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:System.Net.Http.HttpClient?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:System.Net.Http.HttpClient`

-->
