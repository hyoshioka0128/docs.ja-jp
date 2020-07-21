---
title: dotnet restore コマンド
description: dotnet restore コマンドを使用して、依存関係とプロジェクト固有のツールを復元する方法について説明します。
ms.date: 02/27/2020
ms.openlocfilehash: 276fad896a6a8a647ed05a9de8c582d463d9ab8f
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84005319"
---
# <a name="dotnet-restore"></a>dotnet restore

**この記事の対象:** ✔️ .NET Core 2.1 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet restore` - プロジェクトの依存関係とツールを復元します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet restore [<ROOT>] [--configfile <FILE>] [--disable-parallel]
    [-f|--force] [--force-evaluate] [--ignore-failed-sources]
    [--interactive] [--lock-file-path <LOCK_FILE_PATH>] [--locked-mode]
    [--no-cache] [--no-dependencies] [--packages <PACKAGES_DIRECTORY>]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [-s|--source <SOURCE>]
    [--use-lock-file] [-v|--verbosity <LEVEL>]

dotnet restore -h|--help
```

## <a name="description"></a>説明

`dotnet restore` コマンドでは NuGet を使用して、依存関係と、プロジェクト ファイルに指定されているプロジェクト固有のツールを復元します。  ほとんどの場合、次のコマンドを実行すると、必要に応じて NuGet の復元が暗黙的に実行されるため、`dotnet restore` コマンドを明示的に使用する必要はありません。

- [`dotnet new`](dotnet-new.md)
- [`dotnet build`](dotnet-build.md)
- [`dotnet build-server`](dotnet-build-server.md)
- [`dotnet run`](dotnet-run.md)
- [`dotnet test`](dotnet-test.md)
- [`dotnet publish`](dotnet-publish.md)
- [`dotnet pack`](dotnet-pack.md)

場合によっては、これらのコマンドを使用して NuGet の暗黙的な復元を実行するのが不便なことがあります。 たとえば、ビルド システムなど、一部の自動化されているシステムでは、ネットワーク使用状況を制御できるように、`dotnet restore` を明示的に呼び出し、復元のタイミングを制御する必要があります。 NuGet の暗黙的な復元が行われないようにするには、`--no-restore` フラグと共にこれらのコマンドのいずれかを使用し、暗黙的復元を無効にします。

### <a name="specify-feeds"></a>フィードを指定する

依存関係を復元するには、NuGet で、パッケージを配置するフィードが必要になります。 フィードは、通常、"*nuget.config*" 構成ファイルを通じて提供されます。 既定の構成ファイルは、.NET Core SDK がインストールされている場合に提供されます。 追加のフィードを指定するには、次のいずれかの操作を行います。

- プロジェクト ディレクトリに独自の *nuget.config* ファイルを作成します。 詳しくは、「[一般的な NuGet 構成](/nuget/consume-packages/configuring-nuget-behavior)」と、この記事の「[nuget.config の相違点](#nugetconfig-differences)」をご覧ください。
- [`dotnet nuget add source`](dotnet-nuget-add-source.md) などの `dotnet nuget` コマンドを使用します。

`-s` オプションを使用して *nuget.config* フィードをオーバーライドできます。

認証済みフィードの使用方法の詳細については、「[認証済みフィードからのパッケージの使用](/nuget/consume-packages/consuming-packages-authenticated-feeds)」をご覧ください。

### <a name="global-packages-folder"></a>グローバル パッケージ フォルダー

依存関係については、`--packages` 引数を使用して復元操作中に復元されたパッケージの配置場所を指定することができます。 指定されていない場合は、既定の NuGet パッケージ キャッシュが使用されます。これは、すべてのオペレーティング システムのユーザーのホーム ディレクトリ内の `.nuget/packages` ディレクトリにあります。 たとえば、Linux の場合は */home/user1*、Windows の場合は *C:\Users\user1* です。

### <a name="project-specific-tooling"></a>プロジェクト固有のツール

プロジェクト固有のツールについては、`dotnet restore` はまず、ツールがパックされているパッケージを復元し、プロジェクト ファイルに指定されているツールの依存関係の復元に進みます。

### <a name="nugetconfig-differences"></a>nuget.config の相違点

"*nuget.config*" がある場合、`dotnet restore` コマンドの動作はその設定に影響を受けます。 たとえば、"*nuget.config*" に `globalPackagesFolder` を設定すると、指定されたフォルダーに NuGet パッケージが復元されます。 これは `dotnet restore` コマンドで `--packages` オプションを指定する操作の代替方法です。 詳細については、「[nuget の .config リファレンス](/nuget/schema/nuget-config-file)」を参照してください。

`dotnet restore` によって無視される、特定の設定が 3 つあります。

- [bindingRedirects](/nuget/schema/nuget-config-file#bindingredirects-section)

  バインド リダイレクトは、`<PackageReference>` 要素では機能しません。また、.NET Core では、NuGet パッケージの `<PackageReference>` 要素のみサポートされます。

- [solution](/nuget/schema/nuget-config-file#solution-section)

  これは、Visual Studio 固有の設定であり、.NET Core には適用されません。 .NET Core では、`packages.config` ファイルは使用されず、代わりに NuGet パッケージの `<PackageReference>` 要素が使用されます。

- [trustedSigners](/nuget/schema/nuget-config-file#trustedsigners-section)

  この設定は、信頼できるパッケージの[クロスプラットフォーム検証が NuGet でまだサポートされていない](https://github.com/NuGet/Home/issues/7939)ため、適用されません。

## <a name="arguments"></a>引数

- **`ROOT`**

  復元するプロジェクト ファイルへのオプションのパスです。

## <a name="options"></a>オプション

- **`--configfile <FILE>`**

  復元操作で使用する NuGet 構成ファイル ("*nuget.config*") です。

- **`--disable-parallel`**

  複数プロジェクトの並行復元を無効にします。

- **`--force`**

  最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

- **`--force-evaluate`**

  ロック ファイルが既に存在する場合でも、すべての依存関係を再評価するように強制的に復元します。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--ignore-failed-sources`**

  バージョン要件を満たしているパッケージがある場合は、失敗したソースに関する警告のみです。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます (たとえば、認証を完了する場合)。 .NET Core 2.1.400 以降。

- **`--lock-file-path <LOCK_FILE_PATH>`**

  プロジェクトのロック ファイルの書き込み先である出力場所。 既定でこれは *PROJECT_ROOT\packages.lock.json* です。

- **`--locked-mode`**

  プロジェクト ロック ファイルの更新は許可されません。

- **`--no-cache`**

  HTTP 要求をキャッシュしないように指定します。

- **`--no-dependencies`**

  プロジェクト間 (P2P) 参照を含むプロジェクトを復元する場合は、参照ではなく、ルート プロジェクトを復元します。

- **`--packages <PACKAGES_DIRECTORY>`**

  復元されるパッケージのディレクトリを指定します。

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  パッケージの復元用のランタイムを指定します。 これは、 *.csproj* ファイルの `<RuntimeIdentifiers>` タグに明示的にリストされていないランタイムのパッケージを復元するために使用されます。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。 このオプションを複数回指定して、複数の RID を指定します。

- **`-s|--source <SOURCE>`**

  復元操作時に使用する NuGet パッケージ ソースの URI を指定します。 この設定により、"*nuget.config*" ファイルに指定されているすべてのソースがオーバーライドされます。 このオプションを複数回指定することによって、複数のソースを指定できます。

- **`--use-lock-file`**

  プロジェクト ロック ファイルを生成して復元で使用できるようにします。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。 既定値は `minimal`にする必要があります。

## <a name="examples"></a>使用例

- 現在のディレクトリでプロジェクトの依存関係とツールを復元します。

  ```dotnetcli
  dotnet restore
  ```

- 指定されたパスで見つかった `app1` プロジェクトの依存関係とツールを復元します。

  ```dotnetcli
  dotnet restore ~/projects/app1/app1.csproj
  ```

- ソースとして指定されたファイル パスを使用して、現在のディレクトリでプロジェクトの依存関係とツールを復元します。

  ```dotnetcli
  dotnet restore -s c:\packages\mypackages
  ```

- ソースとして指定された 2 つのファイル パスを使用して、現在のディレクトリでプロジェクトの依存関係とツールを復元します。

  ```dotnetcli
  dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages
  ```

- 詳細な出力を示して、現在のディレクトリでプロジェクトの依存関係とツールを復元します。

  ```dotnetcli
  dotnet restore --verbosity detailed
  ```
