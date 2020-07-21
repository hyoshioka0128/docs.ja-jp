---
ms.openlocfilehash: d00b8ecaa61b358e062d85a2b68ca8a95cada442
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803261"
---
### <a name="kestrel-configuration-changes-at-run-time-detected-by-default"></a>Kestrel: 実行時に構成変更が既定で検出される

Kestrel では実行時に、プロジェクトの `IConfiguration` インスタンス (*appsettings.json* など) の `Kestrel` セクションに対する変更に対応するようになりました。 *appsettings.json* を使用して Kestrel を構成する方法の詳細については、[エンドポイント構成](/aspnet/core/fundamentals/servers/kestrel#endpoint-configuration)の *appsettings.json* 例を参照してください。

Kestrel では、こうした構成変更に対応する目的で必要であれば、エンドポイントをバインド、バインド解除、再バインドします。

ディスカッションについては、イシュー [dotnet/aspnetcore#22807](https://github.com/dotnet/aspnetcore/issues/22807) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 7

#### <a name="old-behavior"></a>以前の動作

ASP.NET Core 5.0 Preview 6 より前は、Kestrel では、実行時に構成を変更できませんでした。

ASP.NET Core 5.0 Preview 6 では、実行時に構成変更に対応するという新しい既定の動作を選択できます。 選択では、Kestrel の構成を手動でバインドする必要がありました。

```csharp
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
                webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                {
                    kestrelOptions.Configure(
                        builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: true);
                });

                webBuilder.UseStartup<Startup>();
            });
}
```

#### <a name="new-behavior"></a>新しい動作

Kestrel では既定で、実行時に構成変更に対応します。 この変更をサポートする目的で、<xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A> では既定で `reloadOnChange: true` を指定して `KestrelServerOptions.Configure(IConfiguration, bool)` が呼び出されます。

#### <a name="reason-for-change"></a>変更理由

サーバーを完全に再起動しなくても実行時のエンドポイント再構成がサポートされるように変更が行われました。 サーバーの完全再起動の場合とは異なり、変更のないエンドポイントは一時的でもバインド解除されません。

#### <a name="recommended-action"></a>推奨アクション

* Kestrel の既定の構成セクションが実行時に変更されない大抵のシナリオはこの変更の影響を受けず、何の措置も必要ありません。
* Kestrel の既定の構成セクションが実行時に変更され、Kestrel がそれに対応しなければならないシナリオでは、これが既定の動作になります。
* Kestrel の既定の構成セクションが実行時に変更されるが、Kestrel はそれに対応する必要がないシナリオでは、次のようにオプトアウトできます。

    ```csharp
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
                    webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                    {
                        kestrelOptions.Configure(
                            builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: false);
                    });

                    webBuilder.UseStartup<Startup>();
                });
    }
    ```

**注:**

依然として `reloadOnChange: false` 動作の既定である `KestrelServerOptions.Configure(IConfiguration)` オーバーロードの動作がこの変更によって修正されることはありません。

構成ソースで再読み込みがサポートされることを確認することも重要です。 JSON ソースの場合、再読み込みは `AddJsonFile(path, reloadOnChange: true)` を呼び出すことで構成されます。 *appsettings.json* と *appsettings.{Environment}.json* については、再読み込みが既定で構成されています。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

`Overload:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults`

-->
