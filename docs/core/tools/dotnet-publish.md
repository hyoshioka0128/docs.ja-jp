---
title: dotnet publish コマンド
description: dotnet publish コマンドを実行すると、.NET Core プロジェクトまたはソリューションをディレクトリに発行できます。
ms.date: 02/24/2020
ms.openlocfilehash: 61cfcf06586f3ac66526de69a17b8aef3cf0c795
ms.sourcegitcommit: 63bb83322814f5e5e5c5b69939b14a3139a6ca7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85365584"
---
# <a name="dotnet-publish"></a>dotnet publish

**この記事の対象:** ✔️ .NET Core 2.1 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet publish` - ホスティング システムへの展開のため、アプリケーションとその依存関係をフォルダーに発行します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet publish [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [-f|--framework <FRAMEWORK>] [--force] [--interactive]
    [--manifest <PATH_TO_MANIFEST_FILE>] [--no-build] [--no-dependencies]
    [--no-restore] [--nologo] [-o|--output <OUTPUT_DIRECTORY>]
    [-p:PublishReadyToRun=true] [-p:PublishSingleFile=true] [-p:PublishTrimmed=true]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [--self-contained [true|false]]
    [--no-self-contained] [-v|--verbosity <LEVEL>]
    [--version-suffix <VERSION_SUFFIX>]

dotnet publish -h|--help
```

## <a name="description"></a>説明

`dotnet publish` はアプリケーションをコンパイルし、プロジェクト ファイルに指定されたその依存関係を読み取り、結果のファイル セットをディレクトリに発行します。 出力には次のアセットが含まれます。

- アセンブリの中間言語 (IL) コード (*dll* 拡張子)。
- *.deps.json* ファイル。プロジェクトのすべての依存関係が含まれます。
- *.runtimeconfig.json* ファイル。アプリケーションが想定する共有ランタイムと、ランタイム用の他の構成オプション (ガベージ コレクションの種類など) を指定します。
- アプリケーションの依存関係。NuGet キャッシュから出力フォルダーにコピーされます。

`dotnet publish` コマンドの出力は、実行のためにホスト システム (サーバー、PC、Mac、ラップトップなど) にすぐに展開できます。 これは、アプリケーションの展開を準備するための正式にサポートされている唯一の方法です。 プロジェクトに指定されている展開の種類によっては、ホスティング システムに .NET Core 共有ランタイムがインストールされている場合とされていない場合があります。 詳細については、「[.NET Core CLI を使用して .NET Core アプリを発行する](../deploying/deploy-with-cli.md)」を参照してください。

### <a name="implicit-restore"></a>暗黙的な復元

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

### <a name="msbuild"></a>MSBuild

`dotnet publish` コマンドは、`Publish` ターゲットを呼び出す MSBuild を呼び出します。 `dotnet publish` に渡されたすべてのパラメーターが MSBuild に渡されます。 `-c` と `-o` のパラメーターは、それぞれ MSBuild の `Configuration` と `PublishDir` にマップします。

`dotnet publish` コマンドは、プロパティを設定する `-p` やロガーを定義する `-l` などの MSBuild オプションも受け入れます。 たとえば、`-p:<NAME>=<VALUE>` という形式を使用して、MSBuild プロパティを設定できます。 また、 *.pubxml* ファイルを参照することで、公開関連のプロパティを設定することもできます。次に例を示します。

```dotnetcli
dotnet publish -p:PublishProfile=Properties\PublishProfiles\FolderProfile.pubxml
```

詳細については、次のリソースを参照してください。

- [MSBuild コマンド ライン リファレンス](/visualstudio/msbuild/msbuild-command-line-reference)
- [ASP.NET Core アプリを配置するための Visual Studio 発行プロファイル (.pubxml)](/aspnet/core/host-and-deploy/visual-studio-publish-profiles)
- [dotnet msbuild](dotnet-msbuild.md)

## <a name="arguments"></a>引数

- **`PROJECT|SOLUTION`**

  発行するプロジェクトまたはソリューション。
  
  * `PROJECT` は、[C#](csproj.md)、F#、または Visual Basic のプロジェクト ファイルのパスおよびファイル名か、C#、F#、または Visual Basic のプロジェクト ファイルを含むディレクトリへのパスです。 ディレクトリが指定されていない場合は、既定で現在のディレクトリに設定されます。

  * `SOLUTION` は、ソリューション ファイルのパスとファイル名 ( *.sln* 拡張子)、またはソリューション ファイルを含むディレクトリのパスです。 ディレクトリが指定されていない場合は、既定で現在のディレクトリに設定されます。 .NET Core 3.0 SDK 以降で使用できます。

## <a name="options"></a>オプション

- **`-c|--configuration <CONFIGURATION>`**

  ビルド構成を定義します。 ほとんどのプロジェクトの既定値は `Debug` ですが、プロジェクトでビルド構成設定をオーバーライドできます。

- **`-f|--framework <FRAMEWORK>`**

  指定した[ターゲット フレームワーク](../../standard/frameworks.md)のアプリケーションを発行します。 ターゲット フレームワークはプロジェクト ファイルで指定する必要があります。

- **`--force`**

  最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます。 たとえば、認証を完了する場合があります。 .NET Core 3.0 SDK 以降で使用できます。

- **`--manifest <PATH_TO_MANIFEST_FILE>`**

  アプリによって公開された一連のパッケージをトリミングするために使用する[ターゲット マニフェスト](../deploying/runtime-store.md)を 1 つまたは複数指定します。 マニフェスト ファイルは、[`dotnet store` コマンド](dotnet-store.md)の出力の一部です。 複数のマニフェストを指定するには、マニフェストごとに `--manifest` を追加します。

- **`--no-build`**

  発行の前にプロジェクトをビルドしません。 また、`--no-restore` フラグが暗黙的に設定されます。

- **`--no-dependencies`**

  プロジェクト間参照を無視し、ルート プロジェクトのみを復元します。

- **`--nologo`**

  著作権情報を表示しません。 .NET Core 3.0 SDK 以降で使用できます。

- **`--no-restore`**

  コマンドを実行するときに、暗黙的な復元を実行しません。

- **`-o|--output <OUTPUT_DIRECTORY>`**

  出力ディレクトリのパスを指定します。
  
  指定しない場合、ランタイムに依存する実行可能ファイルおよびクロスプラットフォーム バイナリの既定値は *[project_file_folder]./bin/[configuration]/[framework]/publish/* に設定されます。 自己完結型の実行可能ファイルの場合、既定値は *[project_file_folder]/bin/[configuration]/[framework]/[runtime]/publish/* に設定されます。

  Web プロジェクトで、出力フォルダーがプロジェクト フォルダー内にある場合、`dotnet publish` コマンドを連続して実行すると、出力フォルダーが入れ子になって生成されます。 たとえば、プロジェクト フォルダーが *myproject* で、発行の出力フォルダーが *myproject/publish* であり、`dotnet publish` を 2 回実行した場合、2 回目の実行では *myproject/publish/publish* に *.config* および *.json* ファイルなどのコンテンツ ファイルが配置されます。 発行フォルダーが入れ子にならないようにするには、プロジェクト フォルダーの**直下以外**の発行フォルダーを指定するか、またはプロジェクトから発行フォルダーを除外します。 *publishoutput* という名前の発行フォルダーを除外するには、 *.csproj* ファイルの `PropertyGroup` 要素に次の要素を追加します。

  ```xml
  <DefaultItemExcludes>$(DefaultItemExcludes);publishoutput**</DefaultItemExcludes>
  ```

  - .NET Core 3.x SDK 以降
  
    プロジェクトの発行時に相対パスが指定された場合、生成された出力ディレクトリは、プロジェクト ファイルの場所ではなく、現在の作業ディレクトリに相対的なパスとなります。

    ソリューションの発行時に相対パスが指定されている場合、すべてのプロジェクトに対する出力はすべて、現在の作業ディレクトリと相対的な指定されたフォルダーに移動されます。 発行の出力が各プロジェクトの個別のフォルダーに移動されるようにするには、`--output` オプションの代わりに、msbuild `PublishDir` プロパティを使用して相対パスを指定します。 たとえば、`dotnet publish -p:PublishDir=.\publish` を使用すると、プロジェクト ファイルが格納されているフォルダーの下にある `publish` フォルダーに、各プロジェクトの発行の出力が送信されます。

  - .NET Core 2.x SDK
  
    プロジェクトの発行時に相対パスが指定された場合、生成された出力ディレクトリは、現在の作業ディレクトリではなく、プロジェクト ファイルの場所に相対的なパスとなります。

    ソリューションの発行時に相対パスを指定すると、各プロジェクトの出力は、プロジェクト ファイルの場所に相対的な別のフォルダーに移動されます。 ソリューションの発行時に絶対パスを指定すると、すべてのプロジェクトに対する発行の出力はすべて、指定されたフォルダーに移動されます。

- **`-p:PublishReadyToRun=true`**

  アプリケーション アセンブリは ReadyToRun (R2R) 形式にコンパイルされます。 R2R とは、Ahead-Of-Time (AOT) コンパイルの一種です。 詳細については、「[ReadyToRun イメージ](../whats-new/dotnet-core-3-0.md#readytorun-images)」を参照してください。 .NET Core 3.0 SDK 以降で使用できます。

  このオプションは、コマンド ラインではなく、発行プロファイルで指定することをお勧めします。 詳細については、「[MSBuild](#msbuild)」を参照してください。

- **`-p:PublishSingleFile=true`**

  アプリを、プラットフォームごとに単一の実行可能ファイルにパッケージ化します。 この実行可能ファイルは自己展開型であり、アプリの実行に必要なすべての依存関係 (ネイティブを含む) を含んでいます。 アプリを初めて実行すると、アプリ名とビルド ID に基づいてアプリケーションがディレクトリに抽出されます。 アプリケーションを再実行すると、起動は速くなります。 新しいバージョンが使用されない限り、アプリケーションは自身を 2 回抽出する必要がありません。 .NET Core 3.0 SDK 以降で使用できます。

  単一ファイルの発行の詳細については、[単一ファイル バンドラー設計のドキュメント](https://github.com/dotnet/designs/blob/master/accepted/2020/single-file/design.md)を参照してください。

  このオプションは、コマンド ラインではなく、発行プロファイルで指定することをお勧めします。 詳細については、「[MSBuild](#msbuild)」を参照してください。

- **`-p:PublishTrimmed=true`**

  自己完結型の実行可能ファイルを発行するとき、使用されていないライブラリをトリミングして、アプリの展開サイズを減らします。 詳細については、「[自己完結型の展開と実行可能ファイルのトリミング](../deploying/trim-self-contained.md)」を参照してください。 .NET Core 3.0 SDK 以降で使用できます。

  このオプションは、コマンド ラインではなく、発行プロファイルで指定することをお勧めします。 詳細については、「[MSBuild](#msbuild)」を参照してください。

- **`--self-contained [true|false]`**

  アプリケーションと一緒に .NET Core ランタイムを発行します。これにより、ランタイムをターゲット コンピューターにインストールする必要がなくなります。 ランタイム識別子が指定され、プロジェクトが (ライブラリ プロジェクトではなく) 実行可能なプロジェクトである場合、既定値は `true` です。 詳細については、[.NET Core アプリケーションの発行](../deploying/index.md)に関する記事と「[.NET Core CLI を使用して .NET Core アプリを発行する](../deploying/deploy-with-cli.md)」を参照してください。

  `true` または `false` を指定せずに、このオプションを使用した場合、既定値は `true` になります。 その場合は、その位置で `true` または `false` が想定されているため、`--self-contained` の直後にソリューションまたはプロジェクト引数を配置しないでください。

- **`--no-self-contained`**

  これは、`--self-contained false` に相当します。 .NET Core 3.0 SDK 以降で使用できます。

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  指定されたランタイムのアプリケーションを発行します。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。 詳細については、[.NET Core アプリケーションの発行](../deploying/index.md)に関する記事と「[.NET Core CLI を使用して .NET Core アプリを発行する](../deploying/deploy-with-cli.md)」を参照してください。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。 既定値は `minimal`にする必要があります。

- **`--version-suffix <VERSION_SUFFIX>`**

  プロジェクト ファイルのバージョン フィールドでアスタリスク (`*`) を置き換えるバージョン サフィックスを定義します。

## <a name="examples"></a>使用例

- 現在のディレクトリ内にプロジェクト用の[ランタイムに依存するクロスプラットフォーム バイナリ](../deploying/index.md#produce-a-cross-platform-binary)を作成します。

  ```dotnetcli
  dotnet publish
  ```

  .NET Core 3.0 SDK 以降の場合、この例では、現在のプラットフォーム用の[ランタイムに依存する実行可能ファイル](../deploying/index.md#publish-runtime-dependent)も作成されます。

- 特定のランタイムに対して、現在のディレクトリ内にプロジェクト用の[自己完結型の実行可能ファイル](../deploying/index.md#publish-self-contained)を作成します。

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64
  ```

  RID をプロジェクト ファイルに含める必要があります。

- 特定のプラットフォーム用に、プロジェクト用の[ランタイムに依存する実行可能ファイル](../deploying/index.md#publish-runtime-dependent)を現在のディレクトリに作成します。

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64 --self-contained false
  ```

  RID をプロジェクト ファイルに含める必要があります。 この例は、.NET Core 3.0 SDK 以降のバージョンに適用されます。

- 特定のランタイムとターゲット フレームワーク用に、現在のディレクトリのプロジェクトを発行します。

  ```dotnetcli
  dotnet publish --framework netcoreapp3.1 --runtime osx.10.11-x64
  ```

- 指定されたプロジェクト ファイルを発行します。

  ```dotnetcli
  dotnet publish ~/projects/app1/app1.csproj
  ```

- 現在のアプリケーションを発行します。ただし、復元操作中はルート プロジェクトのみを復元し、プロジェクト間 (P2P) 参照は復元しないでください。

  ```dotnetcli
  dotnet publish --no-dependencies
  ```

## <a name="see-also"></a>関連項目

- [.NET Core アプリケーションの発行の概要](../deploying/index.md)
- [.NET Core CLI を使用して .NET Core アプリを発行する](../deploying/deploy-with-cli.md)
- [ターゲット フレームワーク](../../standard/frameworks.md)
- [ランタイム識別子 (RID) のカタログ](../rid-catalog.md)
- [macOS Catalina の公証に対応する](../install/macos-notarization-issues.md)
- [発行されたアプリケーションのディレクトリ構造](/aspnet/core/hosting/directory-structure)
- [MSBuild コマンド ライン リファレンス](/visualstudio/msbuild/msbuild-command-line-reference)
- [ASP.NET Core アプリを配置するための Visual Studio 発行プロファイル (.pubxml)](/aspnet/core/host-and-deploy/visual-studio-publish-profiles)
- [dotnet msbuild](dotnet-msbuild.md)
- [ILLInk.Tasks](https://aka.ms/dotnet-illink)
