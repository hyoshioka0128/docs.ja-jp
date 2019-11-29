---
title: dotnet run コマンド
description: dotnet run コマンドは、ソース コードからアプリケーションを実行する便利なオプションを提供します。
ms.date: 10/31/2019
ms.openlocfilehash: 87e9a57e874116533951a9c5eb676be76be2c98d
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73454777"
---
# <a name="dotnet-run"></a>dotnet run

**この記事の対象: ✓** .NET Core 1.x SDK 以降のバージョン

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet run` -- 明示的なコンパイルや起動コマンドなしで、ソース コードを実行します。

## <a name="synopsis"></a>構文

<!-- markdownlint-disable MD025 -->

# <a name="net-core-30tabnetcore30"></a>[.NET Core 3.0](#tab/netcore30)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--interactive] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [-r|--runtime] [-v|--verbosity] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [-v|--verbosity] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

---

## <a name="description"></a>説明

`dotnet run` コマンドは、1 つのコマンドを使用して、ソース コードからアプリケーションを実行する便利なオプションを提供します。 コマンド ラインからの短期間の反復開発に便利です。 このコマンドは [`dotnet build`](dotnet-build.md) コマンドに依存し、コードをビルドします。 そのため、プロジェクトを最初に復元する必要があるなど、ビルドに要件があれば、それが `dotnet run` にも適用されます。

出力ファイルは既定の場所である `bin/<configuration>/<target>` に書き込まれます。 たとえば、`netcoreapp2.1` というアプリケーションがあり、`dotnet run` を実行する場合、`bin/Debug/netcoreapp2.1` に出力されます。 必要に応じて、ファイルは上書きされます。 一時ファイルは `obj` ディレクトリに置かれます。

フレームワークを複数指定するプロジェクトの場合、`-f|--framework <FRAMEWORK>` オプションを使用してフレームワークを指定しない限り、`dotnet run` を実行するとエラーが発生します。

`dotnet run` コマンドは、ビルド済みのアセンブリではなく、プロジェクトのコンテキストで使用されます。 代わりにフレームワークに依存するアプリケーション DLL の実行を試みる場合は、コマンドなしで [dotnet](dotnet.md) を実行する必要があります。 たとえば、`myapp.dll` を実行する場合は、次のコードを使用します。

```dotnetcli
dotnet myapp.dll
```

`dotnet` ドライバーの詳細については、[.NET Core コマンド ライン ツール (CLI)](index.md) に関する記事を参照してください。

アプリケーションを実行するため、`dotnet run` コマンドは、NuGet キャッシュから共有ランタイムの外にあるアプリケーションの依存関係を解決します。 このコマンドではキャッシュされた依存関係を使用するため、`dotnet run` を使用してアプリケーションを実稼働環境で実行することは推奨されません。 代わりに、[`dotnet publish`](dotnet-publish.md) コマンドを使用して[展開を作成](../deploying/index.md)し、発行された出力を展開します。

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a>オプション

# <a name="net-core-30tabnetcore30"></a>[.NET Core 3.0](#tab/netcore30)

`--`

実行中のアプリケーションの引数と `dotnet run` の引数を区切ります。 この区切り記号の後の引数はすべて実行中のアプリケーションに渡されます。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 ほとんどのプロジェクトの既定値は、`Debug` です。

`-f|--framework <FRAMEWORK>`

指定された[フレームワーク](../../standard/frameworks.md)を使用してアプリをビルドし、実行します。 フレームワークはプロジェクト ファイルに指定する必要があります。

`--force`

最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

`-h|--help`

コマンドの短いヘルプを印刷します。

`--interactive`

コマンドを停止して、ユーザーの入力または操作のために待機させることができます (たとえば、認証を完了する場合)。

`--launch-profile <NAME>`

アプリケーションを起動する場合に使用する起動プロファイル (存在する場合) の名前です。 起動プロファイルは *launchSettings.json* ファイル内に定義されており、通常は、`Development`、`Staging`、`Production` と呼ばれています。 詳細については、[「Working with multiple environments」](/aspnet/core/fundamentals/environments) (複数の環境での使用) をご覧ください。

`--no-build`

実行前にプロジェクトをビルドしません。 また、`--no-restore` フラグが暗黙的に設定されます。

`--no-dependencies`

プロジェクト間 (P2P) 参照を含むプロジェクトを復元する場合は、参照ではなく、ルート プロジェクトを復元します。

`--no-launch-profile`

アプリケーションを構成するための *launchSettings.json* の使用を試みません。

`--no-restore`

コマンドを実行するときに、暗黙的な復元を実行しません。

`-p|--project <PATH>`

実行するプロジェクト ファイルのパスを指定します (フォルダー名または完全なパス)。 指定しない場合は、既定で現在のディレクトリに設定されます。

`--runtime <RUNTIME_IDENTIFIER>`

パッケージを復元するターゲット ランタイムを指定します。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。

`-v|--verbosity <LEVEL>`

コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--`

実行中のアプリケーションの引数と `dotnet run` の引数を区切ります。 この区切り記号の後の引数はすべて実行中のアプリケーションに渡されます。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 ほとんどのプロジェクトの既定値は、`Debug` です。

`-f|--framework <FRAMEWORK>`

指定された[フレームワーク](../../standard/frameworks.md)を使用してアプリをビルドし、実行します。 フレームワークはプロジェクト ファイルに指定する必要があります。

`--force`

最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

`-h|--help`

コマンドの短いヘルプを印刷します。

`--launch-profile <NAME>`

アプリケーションを起動する場合に使用する起動プロファイル (存在する場合) の名前です。 起動プロファイルは *launchSettings.json* ファイル内に定義されており、通常は、`Development`、`Staging`、`Production` と呼ばれています。 詳細については、[「Working with multiple environments」](/aspnet/core/fundamentals/environments) (複数の環境での使用) をご覧ください。

`--no-build`

実行前にプロジェクトをビルドしません。 また、`--no-restore` フラグが暗黙的に設定されます。

`--no-dependencies`

プロジェクト間 (P2P) 参照を含むプロジェクトを復元する場合は、参照ではなく、ルート プロジェクトを復元します。

`--no-launch-profile`

アプリケーションを構成するための *launchSettings.json* の使用を試みません。

`--no-restore`

コマンドを実行するときに、暗黙的な復元を実行しません。

`-p|--project <PATH>`

実行するプロジェクト ファイルのパスを指定します (フォルダー名または完全なパス)。 指定しない場合は、既定で現在のディレクトリに設定されます。

`--runtime <RUNTIME_IDENTIFIER>`

パッケージを復元するターゲット ランタイムを指定します。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。

`-v|--verbosity <LEVEL>`

コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--`

実行中のアプリケーションの引数と `dotnet run` の引数を区切ります。 この区切り記号の後の引数はすべて実行中のアプリケーションに渡されます。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 ほとんどのプロジェクトの既定値は、`Debug` です。

`-f|--framework <FRAMEWORK>`

指定された[フレームワーク](../../standard/frameworks.md)を使用してアプリをビルドし、実行します。 フレームワークはプロジェクト ファイルに指定する必要があります。

`--force`

最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

`-h|--help`

コマンドの短いヘルプを印刷します。

`--launch-profile <NAME>`

アプリケーションを起動する場合に使用する起動プロファイル (存在する場合) の名前です。 起動プロファイルは *launchSettings.json* ファイル内に定義されており、通常は、`Development`、`Staging`、`Production` と呼ばれています。 詳細については、[「Working with multiple environments」](/aspnet/core/fundamentals/environments) (複数の環境での使用) をご覧ください。

`--no-build`

実行前にプロジェクトをビルドしません。 また、`--no-restore` フラグが暗黙的に設定されます。

`--no-dependencies`

プロジェクト間 (P2P) 参照を含むプロジェクトを復元する場合は、参照ではなく、ルート プロジェクトを復元します。

`--no-launch-profile`

アプリケーションを構成するための *launchSettings.json* の使用を試みません。

`--no-restore`

コマンドを実行するときに、暗黙的な復元を実行しません。

`-p|--project <PATH>`

実行するプロジェクト ファイルのパスを指定します (フォルダー名または完全なパス)。 指定しない場合は、既定で現在のディレクトリに設定されます。

`--runtime <RUNTIME_IDENTIFIER>`

パッケージを復元するターゲット ランタイムを指定します。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--`

実行中のアプリケーションの引数と `dotnet run` の引数を区切ります。 この区切り記号の後の引数はすべて実行中のアプリケーションに渡されます。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 ほとんどのプロジェクトの既定値は、`Debug` です。

`-f|--framework <FRAMEWORK>`

指定された[フレームワーク](../../standard/frameworks.md)を使用してアプリをビルドし、実行します。 フレームワークはプロジェクト ファイルに指定する必要があります。

`-h|--help`

コマンドの短いヘルプを印刷します。

`-p|--project <PATH/PROJECT.csproj>`

プロジェクト ファイルのパスと名前を指定します (注を参照)。指定しない場合は、既定で現在のディレクトリに設定されます。

> [!NOTE]
> `-p|--project` オプションでプロジェクト ファイルのパスと名前を使用します。 CLI の回帰により、.NET Core SDK 1.x でフォルダー パスを指定できなくなります。 この問題の詳細については、[「dotnet run -p, can not start a project (dotnet/cli #5992)」](https://github.com/dotnet/cli/issues/5992) (dotnet run -p でプロジェクトを開始できない (dotnet/cli #5992)) を参照してください。

---

## <a name="examples"></a>使用例

現在のディレクトリのプロジェクトを実行します。

`dotnet run`

指定されたプロジェクトを実行します。

`dotnet run --project ./projects/proj1/proj1.csproj`

現在のディレクトリのプロジェクトを実行します (この例では、空の `--` オプションが使用されているため、`--help` 引数がアプリケーションに渡されます)。

`dotnet run --configuration Release -- --help`

現在のディレクトリでプロジェクトの依存関係とツールを復元し、最小限の出力のみを表示して、プロジェクトを実行します (.NET Core SDK 2.0 以降のバージョン)。

`dotnet run --verbosity m`
