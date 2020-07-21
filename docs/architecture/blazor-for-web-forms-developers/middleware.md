---
title: モジュール、ハンドラー、ミドルウェア
description: モジュール、ハンドラー、およびミドルウェアを使用した HTTP 要求の処理について説明します。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 10/11/2019
ms.openlocfilehash: ff2b3fd41316a1c8c20a0eed9a585e5fd2733af3
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173186"
---
# <a name="modules-handlers-and-middleware"></a>モジュール、ハンドラー、ミドルウェア

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

ASP.NET Core アプリは一連の*ミドルウェア*に基づいて構築されています。 ミドルウェアは、要求と応答を処理するためにパイプラインに配置されるハンドラーです。 Web フォームアプリでは、HTTP ハンドラーとモジュールは同様の問題を解決します。 ASP.NET Core では、モジュール、ハンドラー、 *Global.asax.cs*、およびアプリのライフサイクルはミドルウェアに置き換えられます。 この章では、アプリのコンテキストにおけるミドルウェアについて説明し Blazor ます。

## <a name="overview"></a>概要

ASP.NET Core 要求パイプラインは、順番に呼び出される一連の要求デリゲートで構成されています。 次の図は、その概念を示しています。 実行のスレッドは黒い矢印をたどります。

![pipeline](media/middleware/request-delegate-pipeline.png)

上の図には、ライフサイクルイベントの概念がありません。 この概念は、ASP.NET Web フォーム要求がどのように処理されるかについての基礎となります。 このシステムにより、どのようなプロセスが発生しているかがわかりやすくなり、ミドルウェアをいつでも挿入できるようになります。 ミドルウェアは、要求パイプラインに追加された順序で実行されます。 また、構成ファイルではなくコードに追加されています (通常は*Startup.cs*)。

## <a name="katana"></a>Katana

Katana に慣れている読者は、ASP.NET Core に慣れることができます。 実際、Katana は、ASP.NET Core が派生するフレームワークです。 ASP.NET 4.x 用の同様のミドルウェアとパイプラインパターンが導入されました。 Katana 向けに設計されたミドルウェアは、ASP.NET Core パイプラインで動作するように調整できます。

## <a name="common-middleware"></a>共通ミドルウェア

ASP.NET 4.x には多数のモジュールが含まれています。 同様に、ASP.NET Core にも多くのミドルウェアコンポーネントが用意されています。 IIS モジュールは、ASP.NET Core がある場合に使用できます。 それ以外の場合は、ネイティブ ASP.NET Core ミドルウェアを使用できます。

次の表に、ASP.NET Core の代替ミドルウェアとコンポーネントの一覧を示します。

|モジュール                 |ASP.NET 4.x モジュール           |ASP.NET Core オプション|
|-----------------------|-----------------------------|-------------------|
|HTTP エラー            |`CustomErrorModule`          |[状態コード ページ ミドルウェア](/aspnet/core/fundamentals/error-handling#usestatuscodepages)|
|既定のドキュメント       |`DefaultDocumentModule`      |[既定のファイル ミドルウェア](/aspnet/core/fundamentals/static-files#serve-a-default-document)|
|ディレクトリ参照     |`DirectoryListingModule`     |[ディレクトリ参照ミドルウェア](/aspnet/core/fundamentals/static-files#enable-directory-browsing)|
|動的圧縮    |`DynamicCompressionModule`   |[応答圧縮ミドルウェア](/aspnet/core/performance/response-compression)|
|失敗した要求のトレース|`FailedRequestsTracingModule`|[ASP.NET Core のログ](/aspnet/core/fundamentals/logging/index#tracesource-provider)|
|ファイルのキャッシュ           |`FileCacheModule`            |[応答キャッシュ ミドルウェア](/aspnet/core/performance/caching/middleware)|
|HTTP キャッシュ           |`HttpCacheModule`            |[応答キャッシュ ミドルウェア](/aspnet/core/performance/caching/middleware)|
|HTTP ログ           |`HttpLoggingModule`          |[ASP.NET Core のログ](/aspnet/core/fundamentals/logging/index)|
|HTTP リダイレクト       |`HttpRedirectionModule`      |[URL リライト ミドルウェア](/aspnet/core/fundamentals/url-rewriting)|
|ISAPI フィルター          |`IsapiFilterModule`          |[ミドルウェア](/aspnet/core/fundamentals/middleware/index)|
|ISAPI                  |`IsapiModule`                |[ミドルウェア](/aspnet/core/fundamentals/middleware/index)|
|要求のフィルタリング      |`RequestFilteringModule`     |[URL リライトミドルウェア IRule](/aspnet/core/fundamentals/url-rewriting#irule-based-rule)|
|URL リライト&#8224;   |`RewriteModule`              |[URL リライト ミドルウェア](/aspnet/core/fundamentals/url-rewriting)|
|静的な圧縮     |`StaticCompressionModule`    |[応答圧縮ミドルウェア](/aspnet/core/performance/response-compression)|
|静的コンテンツ         |`StaticFileModule`           |[静的ファイル ミドルウェア](/aspnet/core/fundamentals/static-files)|
|URL 承認      |`UrlAuthorizationModule`     |[ASP.NET Core ID](/aspnet/core/security/authentication/identity)|

このリストは完全なものではありませんが、2つのフレームワーク間にどのようなマッピングが存在するのかを把握する必要があります。 詳細な一覧については、「 [ASP.NET Core を使用した IIS モジュール](/aspnet/core/host-and-deploy/iis/modules)」を参照してください。

## <a name="custom-middleware"></a>カスタムミドルウェア

組み込みのミドルウェアでは、アプリに必要なすべてのシナリオを処理することはできません。 このような場合は、独自のミドルウェアを作成するのが理にかなっています。 ミドルウェアを定義する方法は複数ありますが、最も単純なのは単純なデリゲートです。 クエリ文字列からカルチャ要求を受け取る次のミドルウェアを考えてみます。

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            var cultureQuery = context.Request.Query["culture"];

            if (!string.IsNullOrWhiteSpace(cultureQuery))
            {
                var culture = new CultureInfo(cultureQuery);

                CultureInfo.CurrentCulture = culture;
                CultureInfo.CurrentUICulture = culture;
            }

            // Call the next delegate/middleware in the pipeline
            await next();
        });

        app.Run(async (context) =>
            await context.Response.WriteAsync(
                $"Hello {CultureInfo.CurrentCulture.DisplayName}"));
    }
}
```

ミドルウェアは、インターフェイスを実装するか、 `IMiddleware` 次のミドルウェア規約を使用して、クラスとして定義することもできます。 詳細については、「[カスタム ASP.NET Core ミドルウェアを作成](/aspnet/core/fundamentals/middleware/write)する」を参照してください。

>[!div class="step-by-step"]
>[前へ](data.md)
>[次へ](config.md)
