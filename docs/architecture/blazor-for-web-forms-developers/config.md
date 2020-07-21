---
title: アプリの構成
description: ConfigurationManager を使用せずにアプリを構成する方法につい Blazor て説明します。
author: csharpfritz
ms.author: jefritz
no-loc:
- Blazor
ms.date: 04/01/2020
ms.openlocfilehash: a13f663c2c6908ba906e42cb939c3b8707b8cccd
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173316"
---
# <a name="app-configuration"></a>アプリの構成

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Web フォームでアプリ構成を読み込む主な方法は、 *web.config*ファイルのエントリを、 &mdash; サーバー上または*web.config*が参照する関連構成ファイルに入力することです。静的オブジェクトを使用して、アプリ `ConfigurationManager` の設定、データリポジトリの接続文字列、およびアプリに追加されたその他の拡張構成プロバイダーとやり取りすることができます。 一般的に、次のコードに示すように、アプリ構成との相互作用を確認します。

```csharp
var configurationValue = ConfigurationManager.AppSettings["ConfigurationSettingName"];
var connectionString = ConfigurationManager.ConnectionStrings["MyDatabaseConnectionName"].ConnectionString;
```

ASP.NET Core とサーバー側で Blazor は、アプリが WINDOWS IIS サーバーでホストされている場合、 *web.config*ファイルが存在する可能性があります。 ただし、 `ConfigurationManager` この構成は相互作用しないため、他のソースからさらに構造化されたアプリ構成を受け取ることができます。 構成の収集方法と、 *web.config*ファイルから構成情報にアクセスする方法を見てみましょう。

## <a name="configuration-sources"></a>構成元

ASP.NET Core は、アプリに使用できる多くの構成ソースがあることを認識しています。 フレームワークは、既定では、これらの機能の最適な提供を試みます。 構成は、ASP.NET Core によって、これらのさまざまなソースから読み取りおよび集計されます。 同じ構成キーの後で読み込まれる値は、以前の値よりも優先されます。

ASP.NET Core は、クラウド対応であり、オペレーターと開発者の両方にとってアプリの構成を容易にするように設計されています。 ASP.NET Core は環境に対応し、または環境内で実行されているかどうかを認識し `Production` `Development` ます。 環境インジケーターは、システム環境変数で設定され `ASPNETCORE_ENVIRONMENT` ます。 値が構成されていない場合、アプリは既定で環境で実行され `Production` ます。

アプリは、環境の名前に基づいて複数のソースから構成をトリガーし、構成を追加することができます。 既定では、構成は次のリソースから順に読み込まれます。

1. ファイル*のappsettings.js* (存在する場合)
1. *appsettings。{ENVIRONMENT_NAME}. json*ファイル (存在する場合)
1. ディスク上のユーザーシークレットファイル (存在する場合)
1. 環境変数
1. コマンド ライン引数

## <a name="appsettingsjson-format-and-access"></a>形式とアクセスに appsettings.js

ファイル*のappsettings.js*は、次の JSON のように構造化された値を使用して階層化できます。

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  }
}
```

上記の JSON が表示された場合、構成システムは子の値を平坦化し、完全修飾された階層パスを参照します。 コロン ( `:` ) 文字は、階層内の各プロパティを区切ります。 たとえば、構成キーは、 `section1:key0` `section1` オブジェクトリテラルの値にアクセスし `key0` ます。

## <a name="user-secrets"></a>ユーザーシークレット

ユーザーシークレットは次のとおりです。

* アプリ開発フォルダーの外部にある、開発者のワークステーション上の JSON ファイルに格納されている構成値。
* 環境内での実行時にのみ読み込ま `Development` れます。
* 特定のアプリに関連付けられています。
* .NET Core CLI のコマンドを使用して管理さ `user-secrets` れます。

次のコマンドを実行して、シークレットストレージ用にアプリを構成し `user-secrets` ます。

```dotnetcli
dotnet user-secrets init
```

上記のコマンドは、 `UserSecretsId` プロジェクトファイルに要素を追加します。 要素には、シークレットをアプリに関連付けるために使用される GUID が含まれています。 その後、コマンドを使用してシークレットを定義でき `set` ます。 次に例を示します。

```dotnetcli
dotnet user-secrets set "Parent:ApiKey" "12345"
```

上記のコマンドは、 `Parent:ApiKey` 値を使用して、開発者のワークステーションで構成キーを使用できるようにし `12345` ます。

ユーザーシークレットの作成、格納、および管理の詳細については、 [ASP.NET Core ドキュメントの「開発におけるアプリシークレットの安全な格納](/aspnet/core/security/app-secrets)」を参照してください。

## <a name="environment-variables"></a>環境変数

アプリケーション構成に読み込まれる次の値のセットは、システムの環境変数です。 システムの環境変数のすべての設定は、構成 API を使用してアクセスできるようになりました。 アプリケーション内で読み取られるときに、階層値はフラット化され、コロン文字で区切られます。 ただし、一部のオペレーティングシステムでは、コロン文字環境変数名を使用できません。 ASP.NET Core は、2つのアンダースコア () を持つ値をアクセス時にコロンに変換することによって、この制限に対処 `__` します。 `Parent:ApiKey`上記のユーザーシークレットセクションの値は、環境変数でオーバーライドでき `Parent__ApiKey` ます。

## <a name="command-line-arguments"></a>コマンド ライン引数

アプリを起動するときに、構成をコマンドライン引数として指定することもできます。 `--` `/` 設定する構成値の名前と構成する値を示すには、二重ダッシュ () またはスラッシュ () 表記を使用します。 構文は次のコマンドのようになります。

```dotnetcli
dotnet run CommandLineKey1=value1 --CommandLineKey2=value2 /CommandLineKey3=value3
dotnet run --CommandLineKey1 value1 /CommandLineKey2 value2
dotnet run Parent:ApiKey=67890
```

## <a name="the-return-of-webconfig"></a>web.config の戻り値

アプリを IIS の Windows にデプロイした場合、 *web.config*ファイルによって、アプリケーションを管理するための iis が引き続き構成されます。 既定では、IIS は ASP.NET Core モジュール (モジュール) への参照を追加します。 モジュールは、Kestrel web サーバーの代わりにアプリをホストするネイティブ IIS モジュールです。 この*web.config*セクションは、次の XML マークアップに似ています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe"
                  stdoutLogEnabled="false"
                  stdoutLogFile=".\logs\stdout"
                  hostingModel="inprocess" />
    </system.webServer>
  </location>
</configuration>
```

アプリ固有の構成は、要素内に要素を入れ子にすることによって定義でき `environmentVariables` `aspNetCore` ます。 このセクションで定義されている値は、環境変数として ASP.NET Core アプリに提示されます。 環境変数は、アプリの起動のセグメント中に適切に読み込まれます。

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout"
      hostingModel="inprocess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="Parent:ApiKey" value="67890" />
  </environmentVariables>
</aspNetCore>
```

## <a name="read-configuration-in-the-app"></a>アプリの構成の読み取り

ASP.NET Core は、インターフェイスを使用してアプリの構成を提供 <xref:Microsoft.Extensions.Configuration.IConfiguration> します。 この構成インターフェイスは、 Blazor コンポーネント、 Blazor ページ、および構成へのアクセスを必要とするその他の ASP.NET Core マネージクラスによって要求される必要があります。 ASP.NET Core framework は、前に構成した解決済みの構成をこのインターフェイスに自動的に設定します。 Blazorページまたはコンポーネントの razor マークアップでは、次のように、 `IConfiguration` `@inject` *razor*ファイルの先頭にディレクティブを使用してオブジェクトを挿入できます。

```razor
@inject IConfiguration Configuration
```

この前のステートメントにより、オブジェクトは、 `IConfiguration` `Configuration` Razor テンプレートの残りの部分を通じて変数として使用できるようになります。

インデクサーパラメーターとして使用する構成設定の階層を指定することで、個々の構成設定を読み取ることができます。

```csharp
var mySetting = Configuration["section1:key0"];
```

<xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> `GetSection("section1")` 前の例から section1 の構成を取得する場合と同様の構文を使用して、メソッドを使用して構成セクション全体を取得できます。

## <a name="strongly-typed-configuration"></a>厳密に型指定された構成

Web フォームでは、 <xref:System.Configuration.ConfigurationSection> 型とそれに関連付けられている型から継承される厳密に型指定された構成の型を作成できました。 では、 `ConfigurationSection` これらの構成値に対していくつかのビジネスルールと処理を構成できます。

ASP.NET Core では、構成値を受け取るクラス階層を指定できます。 次のクラス:

* 親クラスから継承する必要はありません。
* には、 `public` キャプチャする構成構造のプロパティおよび型参照に一致するプロパティが含まれている必要があります。

サンプルの前の*appsettings.js*では、次のクラスを定義して値をキャプチャできます。

```csharp
public class MyConfig
{
    public MyConfigSection section0 { get; set;}

    public MyConfigSection section1 { get; set;}
}

public class MyConfigSection
{
    public string key0 { get; set; }

    public string key1 { get; set; }
}
```

このクラス階層は、メソッドに次の行を追加することによって設定でき `Startup.ConfigureServices` ます。

```csharp
services.Configure<MyConfig>(Configuration);
```

アプリの残りの部分では、厳密に型 `@inject` 指定された構成設定を受け取るために、型の Razor テンプレート内のクラスまたはディレクティブに入力パラメーターを追加でき `IOptions<MyConfig>` ます。 プロパティは、 `IOptions<MyConfig>.Value` 構成設定から設定された値を生成し `MyConfig` ます。

```razor
@inject IOptions<MyConfig> options
@code {
    var MyConfiguration = options.Value;
    var theSetting = MyConfiguration.section1.key0;
}
```

オプションの機能の詳細については ASP.NET Core ドキュメント[のオプションパターン](/aspnet/core/fundamentals/configuration/options#options-interfaces)を参照してください。

>[!div class="step-by-step"]
>[前へ](middleware.md)
>[次へ](security-authentication-authorization.md)
