---
title: アプリのプロジェクト構造 Blazor
description: ASP.NET Web フォームおよびプロジェクトのプロジェクト構造を比較する方法について説明 Blazor します。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 09/11/2019
ms.openlocfilehash: 473b708a9b58fa88844bc6f79a898943d5a7db71
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173043"
---
# <a name="project-structure-for-blazor-apps"></a>アプリのプロジェクト構造 Blazor

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

大きなプロジェクト構造の違いにもかかわらず、ASP.NET の Web フォームは、 Blazor さまざまな概念を共有しています。 ここでは、プロジェクトの構造を見 Blazor て、それを ASP.NET の Web フォームプロジェクトと比較します。

最初のアプリを作成するには、 Blazor 「 [ Blazor 作業の開始](/aspnet/core/blazor/get-started)」の手順に従ってください。 指示に従って、 Blazor ASP.NET Core でホストされているサーバーアプリまたはアプリを作成でき Blazor WebAssembly ます。 ホスティングモデル固有のロジックを除き、両方のプロジェクトのコードのほとんどは同じです。

## <a name="project-file"></a>プロジェクト ファイル

Blazorサーバーアプリは .NET Core プロジェクトです。 サーバーアプリのプロジェクトファイル Blazor は、次のように簡単に取得できます。

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>
```

アプリのプロジェクトファイルは Blazor WebAssembly 少し複雑になります (正確なバージョン番号は異なる場合があります)。

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <RazorLangVersion>3.0</RazorLangVersion>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Blazor" Version="3.1.0" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.Build" Version="3.1.0" PrivateAssets="all" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.HttpClient" Version="3.1.0" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.DevServer" Version="3.1.0" PrivateAssets="all" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\Shared\BlazorWebAssemblyApp1.Shared.csproj" />
  </ItemGroup>

</Project>
```

BlazorWebAssemblyプロジェクトは、ベースの .net ランタイムでブラウザーで実行されるため、.Net Core ではなく .NET Standard を対象と WebAssembly します。 サーバーや開発者のコンピューターで使用できるように、web ブラウザーに .NET をインストールすることはできません。 その結果、プロジェクトは Blazor 個別のパッケージ参照を使用してフレームワークを参照します。

これに対し、既定の ASP.NET Web フォームプロジェクトでは、 *.csproj*ファイルに約300行の XML が含まれています。そのほとんどは、プロジェクト内のさまざまなコードおよびコンテンツファイルを明示的に一覧表示します。 .NET Core および .NET Standard ベースのプロジェクトの単純化の多くは、sdk を参照することによってインポートされる既定のターゲットとプロパティから取得されます。これは、 `Microsoft.NET.Sdk.Web` 多くの場合、単に単に WEB sdk と呼ばれています。 Web SDK には、プロジェクトにコードとコンテンツファイルを簡単に含めることができるワイルドカードやその他の便利なが含まれています。 ファイルを明示的に一覧表示する必要はありません。 .NET Core を対象とする場合、Web SDK は .NET Core と ASP.NET Core の両方の共有フレームワークへのフレームワーク参照も追加します。 フレームワークは、[ソリューションエクスプローラー] ウィンドウの [**依存関係**  >  **フレームワーク**] ノードに表示されます。 **Solution Explorer** 共有フレームワークは、.NET Core をインストールするときにコンピューターにインストールされたアセンブリのコレクションです。

これらはサポートされていますが、.NET Core プロジェクトでは、個々のアセンブリ参照はあまり一般的ではありません。 ほとんどのプロジェクトの依存関係は、NuGet パッケージ参照として処理されます。 .NET Core プロジェクトでは、最上位レベルのパッケージの依存関係を参照する必要があります。 推移的な依存関係は自動的に含まれます。 ASP.NET Web フォームプロジェクトでよく見られる*packages.config*ファイルを使用してパッケージを参照するのではなく、要素を使用してパッケージ参照をプロジェクトファイルに追加し `<PackageReference>` ます。

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
</ItemGroup>
```

## <a name="entry-point"></a>エントリ ポイント

Blazorサーバーアプリのエントリポイントは、コンソールアプリで見られるように、 *Program.cs*ファイルで定義されます。 アプリを実行すると、web アプリ固有の既定値を使用して web ホストインスタンスが作成され、実行されます。 Web ホストは、 Blazor サーバーアプリのライフサイクルを管理し、ホストレベルのサービスを設定します。 このようなサービスの例としては、構成、ログ記録、依存関係の注入、HTTP サーバーなどがあります。 このコードはほとんどが定型であり、変更されることはほとんどありません。

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

BlazorWebAssemblyアプリでは、 *Program.cs*にエントリポイントを定義することもできます。 コードは少し異なります。 コードは、同じホストレベルのサービスをアプリに提供するようにアプリホストを設定するという点で似ています。 WebAssemblyただし、アプリホストは、ブラウザーで直接実行されるため、HTTP サーバーを設定しません。

Blazorアプリには、 `Startup` アプリのスタートアップロジックを定義するための、 *global.asax*ファイルではなくクラスがあります。 クラスは、 `Startup` アプリとアプリ固有のサービスを構成するために使用されます。 Blazorサーバーアプリで `Startup` は、クラスを使用して、クライアントブラウザーとサーバーの間で使用されるリアルタイム接続のエンドポイントを設定し Blazor ます。 アプリでは、クラスによって、 Blazor WebAssembly `Startup` アプリのルートコンポーネントと、それらをレンダリングする場所が定義されます。 このクラスについては `Startup` 、「[アプリのスタートアップ](./app-startup.md)」セクションで詳しく説明します。

## <a name="static-files"></a>静的ファイル

ASP.NET Web フォームプロジェクトとは異なり、プロジェクト内のすべてのファイルを Blazor 静的ファイルとして要求することはできません。 *Wwwroot*フォルダー内のファイルのみが web アドレスを指定できます。 このフォルダーは、アプリの "web ルート" と呼ばれます。 アプリの web ルート以外のものは、web アドレスを指定でき*ません*。 このセットアップでは、web 経由でプロジェクトファイルが誤って公開されないようにするための追加のセキュリティレベルが提供されます。

## <a name="configuration"></a>構成

ASP.NET Web フォームアプリの構成は、通常、1つ以上の*web.config*ファイルを使用して処理されます。 Blazor通常、アプリには*web.config*ファイルがありません。 ファイルがある場合は、IIS でホストされている場合にのみ、ファイルが IIS 固有の設定を構成するために使用されます。 代わりに、 Blazor サーバーアプリは ASP.NET Core 構成の抽象化を使用し Blazor WebAssembly ます (現在、アプリでは同じ構成の抽象化はサポートされていませんが、将来追加される機能である可能性があります)。 たとえば、既定のサーバーアプリでは、 Blazor 一部の設定が*appsettings.js*に格納されます。

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

構成の詳細については、[構成](./config.md)セクションの ASP.NET Core プロジェクトに関するページを参照してください。

## <a name="razor-components"></a>Razor のコンポーネント

プロジェクト内のほとんどのファイル Blazor は、 *razor*ファイルです。 Razor は、web UI を動的に生成するために使用される HTML および C# に基づくテンプレート言語です。 この*razor*ファイルは、アプリの UI を構成するコンポーネントを定義します。 ほとんどの場合、コンポーネントはサーバーとアプリの両方で同一です Blazor Blazor WebAssembly 。 のコンポーネント Blazor は、ASP.NET Web フォームのユーザーコントロールに似ています。

各 Razor コンポーネントファイルは、プロジェクトのビルド時に .NET クラスにコンパイルされます。 生成されたクラスは、コンポーネントの状態、レンダリングロジック、ライフサイクルメソッド、イベントハンドラー、およびその他のロジックをキャプチャします。 「[再利用可能な UI コンポーネントの構築 Blazor ](./components.md) 」セクションの「コンポーネントの作成」を参照してください。

*_Imports razor*ファイルは razor コンポーネントファイルではありません。 代わりに、同じフォルダーおよびそのサブフォルダー内の他の*razor*ファイルにインポートする razor ディレクティブのセットを定義します。 たとえば、_Imports の*razor*ファイルは、 `using` 一般的に使用される名前空間のディレクティブを追加する従来の方法です。

```razor
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop
@using BlazorApp1
@using BlazorApp1.Shared
```

## <a name="pages"></a>ページ

アプリ内のページはどこにあり Blazor ますか。 Blazorでは、ASP.NET Web フォームアプリの *.aspx*ファイルのように、アドレス指定可能なページに対して個別のファイル拡張子は定義されません。 代わりに、ページはコンポーネントにルートを割り当てることによって定義されます。 ルートは通常、Razor ディレクティブを使用して割り当てられ `@page` ます。 たとえば、 `Counter` *Pages/Counter. razor*ファイルで作成されたコンポーネントは、次のルートを定義します。

```razor
@page "/counter"
```

でのルーティング Blazor は、サーバー上ではなく、クライアント側で処理されます。 ユーザーがブラウザーで移動すると、はナビゲーションをインターセプトし、 Blazor 一致するルートを使用してコンポーネントをレンダリングします。

コンポーネントのルートは、現在、 *.aspx*ページのようなコンポーネントのファイルの場所によって推測されていません。 この機能は今後追加される可能性があります。 各ルートは、コンポーネントに対して明示的に指定する必要があります。 ルーティング可能なコンポーネントを*Pages*フォルダーに格納することは、特別な意味を持たず、純粋に規則です。

詳細につい Blazor ては、「[ページ、ルーティング、およびレイアウト](./pages-routing-layouts.md)」セクションの「ルーティング」を参照してください。

## <a name="layout"></a>レイアウト

ASP.NET Web フォームアプリでは、共通ページレイアウトはマスターページ (*.master*) を使用して処理されます。 Blazorアプリでは、ページレイアウトはレイアウトコンポーネント (*Shared/mainlayout. razor*) を使用して処理されます。 レイアウトコンポーネントの詳細につい[ては、「ページ、ルーティング、レイアウト](./pages-routing-layouts.md)」セクションを参照してください。

## <a name="bootstrap-blazor"></a>ブートストラップBlazor

ブートストラップの Blazor 場合、アプリは次のことを行う必要があります。

- ページ上のルートコンポーネント (*app.xaml*) を表示する場所を指定します。
- 対応する Blazor フレームワークスクリプトを追加します。

Blazorサーバーアプリでは、ルートコンポーネントのホストページは *_Host*ファイルに定義されています。 このファイルは、コンポーネントではなく Razor ページを定義します。 Razor 構文 Razor Pages 使用して、サーバーアドレス指定可能なページを定義し*ます。* これは .aspx ページとよく似ています。 `Html.RenderComponentAsync<TComponent>(RenderMode)`メソッドは、ルートレベルのコンポーネントを表示する場所を定義するために使用されます。 オプションは、 `RenderMode` コンポーネントを表示する方法を示します。 次の表に、サポートされるオプションの概要を示し `RenderMode` ます。

|オプション                        |説明       |
|------------------------------|------------------|
|`RenderMode.Server`           |ブラウザーとの接続が確立されると、対話形式で表示されます。|
|`RenderMode.ServerPrerendered`|最初の prerendered してから対話形式で表示する|
|`RenderMode.Static`           |静的コンテンツとしてレンダリング|

*_Framework/blazor.server.js*へのスクリプト参照は、サーバーとのリアルタイム接続を確立し、すべてのユーザー操作と UI 更新を処理します。

```razor
@page "/"
@namespace BlazorApp1.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>BlazorApp1</title>
    <base href="~/" />
    <link rel="stylesheet" href="css/bootstrap/bootstrap.min.css" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>
        @(await Html.RenderComponentAsync<App>(RenderMode.ServerPrerendered))
    </app>

    <script src="_framework/blazor.server.js"></script>
</body>
</html>
```

アプリで Blazor WebAssembly は、ホストページは*wwwroot/index.html*の下の単純な静的 HTML ファイルです。 要素は、 `<app>` ルートコンポーネントを表示する場所を示すために使用されます。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>BlazorApp2</title>
    <base href="/" />
    <link href="css/bootstrap/bootstrap.min.css" rel="stylesheet" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>Loading...</app>

    <script src="_framework/blazor.webassembly.js"></script>
</body>
</html>
```

レンダリングする特定のコンポーネントは、アプリのメソッドで構成され、 `Startup.Configure` 対応する CSS セレクターによってコンポーネントのレンダリング先が示されます。

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
    }

    public void Configure(IComponentsApplicationBuilder app)
    {
        app.AddComponent<App>("app");
    }
}
```

## <a name="build-output"></a>ビルド出力

プロジェクトを Blazor ビルドすると、すべての Razor コンポーネントとコードファイルが1つのアセンブリにコンパイルされます。 ASP.NET Web フォームプロジェクトとは異なり、は Blazor UI ロジックのランタイムコンパイルをサポートしていません。

## <a name="run-the-app"></a>アプリを実行する

サーバーアプリを実行するには Blazor 、 `F5` Visual Studio でを押します。 Blazorアプリはランタイムコンパイルをサポートしていません。 コードとコンポーネントのマークアップの変更結果を表示するには、デバッガーがアタッチされた状態でアプリをリビルドして再起動します。 デバッガーがアタッチされていない状態でを実行した場合 ( `Ctrl+F5` )、Visual Studio はファイルの変更を監視し、変更が加えられるとアプリを再起動します。 変更が行われると、ブラウザーが手動で更新されます。

アプリを実行するには Blazor WebAssembly 、次のいずれかの方法を選択します。

- 開発サーバーを使用して、クライアントプロジェクトを直接実行します。
- ASP.NET Core を使用してアプリをホストするときに、サーバープロジェクトを実行します。

BlazorWebAssemblyアプリは、Visual Studio を使用したデバッグをサポートしていません。 アプリを実行するには、の代わりにを使用 `Ctrl+F5` `F5` します。 代わりに Blazor WebAssembly 、ブラウザーで直接アプリをデバッグすることができます。 詳細については、「[デバッグ ASP.NET Core Blazor ](/aspnet/core/blazor/debug) 」を参照してください。

>[!div class="step-by-step"]
>[前へ](hosting-models.md)
>[次へ](app-startup.md)
