---
title: .NET Core グローバル ツール
description: .NET Core グローバル ツールとそれらに使用できる .NET Core CLI コマンドの概要。
author: KathleenDollard
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 40a0aabcf523e8dac9a3ad226064bbb3c1b3ce5b
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332017"
---
# <a name="net-core-global-tools-overview"></a>.NET core グローバル ツールの概要

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

.NET Core グローバル ツールは、コンソール アプリケーションを含む特殊な NuGet パッケージです。 グローバル ツールは、PATH 環境変数に含まれている既定の場所またはカスタムの場所のマシンにインストールできます。

.NET Core グローバル ツールを使用する場合は、次のことを行います。

* ツールに関する情報を検索します (通常は Web サイトまたは GitHub ページ)。
* フィードのホーム (通常は NuGet.org) で作成者と統計情報を確認します。
* ツールをインストールします。
* ツールを呼び出します。
* ツールを更新します。
* ツールをアンインストールします。

> [!IMPORTANT]
> .NET Core グローバル ツールは、パス上に表示され、完全な信頼で実行されます。 作成者が信頼できる場合を除き、.NET Core グローバル ツールをインストールしないでください。

## <a name="find-a-net-core-global-tool"></a>.NET Core グローバル ツールの検索

現時点では、.NET Core コマンド ライン インターフェイス (CLI) には、グローバル ツールの検索機能はありません。

.NET Core グローバル ツールは、[NuGet](https://www.nuget.org) で見つけることができます。 ただし、NuGet では、具体的に .NET Core グローバル ツールを検索することはまだできません。

ブログの投稿や [natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) GitHub リポジトリでも、ツールの推奨事項を検索することができます。

また、[aspnet/DotNetTools](https://github.com/aspnet/DotNetTools/) GitHub リポジトリでは、ASP.NET チームによって作成されたグローバル ツールのソース コードを確認することもできます。

## <a name="check-the-author-and-statistics"></a>作成者と統計情報の確認

.NET Core グローバル ツールは、完全な信頼で実行され、通常はパス上にインストールされるため、非常に強力です。 信頼できないユーザーからツールをダウンロードしないでください。

ツールが NuGet でホストされている場合は、ツールを検索することで作成者と統計情報を確認できます。

## <a name="install-a-global-tool"></a>グローバル ツールのインストール

グローバル ツールをインストールするには、[dotnet tool install](dotnet-tool-install.md) .NET Core CLI コマンドを使用します。 次の例では、既定の場所にグローバル ツールをインストールする方法を示しています。

```dotnetcli
dotnet tool install -g dotnetsay
```

ツールがインストールできない場合は、エラー メッセージが表示されます。 予定していたフィードがチェックされていることを確認します。

ツールのプレリリース バージョンまたは特定のバージョンをインストールしようとしている場合は、次の形式を使用してバージョン番号を指定できます。

```dotnetcli
dotnet tool install -g <package-name> --version <version-number>
```

インストールが成功すると、ツールの呼び出しに使用したコマンドとインストールされたバージョンを示す、次の例のようなメッセージが表示されます。

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.0.0') was successfully installed.
```

グローバル ツールは、既定のディレクトリ内または特定の場所にインストールすることができます。 既定のディレクトリは次のとおりです。

| OS          | パス                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

これらの場所は、そこにインストールされたグローバル ツールを直接呼び出せるように、SDK が最初に実行されるときにユーザーのパスに追加されます。

グローバル ツールは、マシン全体ではなく、ユーザーに固有であることに注意してください。 ユーザーに固有であることは、そのマシンのすべてのユーザーが使用できるグローバル ツールをインストールできないことを意味します。 このツールは、ツールがインストールされた各ユーザー プロファイルでしか使用できません。

グローバル ツールは、特定のディレクトリにインストールすることもできます。 特定のディレクトリにインストールした場合は、ユーザーはコマンドが使用できることを確認する必要があります。それには、そのディレクトリをパスに含めるか、指定されたディレクトリでコマンドを呼び出すか、指定したディレクトリ内からツールを呼び出します。
この場合、.NET Core CLI によりこの場所が PATH 環境変数に自動的に追加されることはありません。

## <a name="use-the-tool"></a>ツールの使用

ツールをインストールすると、そのコマンドを使用してツールを呼び出すことができます。 コマンドが、パッケージ名と異なる場合があることに注意してください。

コマンドが `dotnetsay` の場合、次を使用して呼び出します。

```console
dotnetsay
```

ツールの作成者が `dotnet` プロンプトのコンテキストにツールを表示するようにした場合は、次のように、`dotnet <command>` として呼び出す方法でツールを記述している場合があります。

```dotnetcli
dotnet doc
```

インストールしたグローバル ツール パッケージに含まれているツールを確認するには、[dotnet tool list](dotnet-tool-list.md) コマンドを使用してインストールされているパッケージを一覧表示します。

ツールの使用方法については、ツールの Web サイトで検索するか、次のいずれかのコマンドを入力して検索することもできます。

```console
<command> --help
dotnet <command> --help
```

## <a name="other-cli-commands"></a>その他の CLI コマンド

.NET Core SDK には、.NET Core グローバル ツールをサポートするその他のコマンドが含まれています。 次のいずれかのオプションを使用して、任意の `dotnet tool` コマンドを使用します。

* `--global` または `-g` は、コマンドがユーザー全体のグローバル ツールに適用可能なことを指定します。
* `--tool-path` は、グローバル ツールのカスタムの場所を指定します。

グローバル ツールで使用できるコマンドを調べるには、次のコマンドを使用します。

```dotnetcli
dotnet tool --help
```

グローバル ツールを更新するには、ツールをアンインストールしてから、最新の安定バージョンで再インストールする必要があります。 グローバル ツールを更新するには、[dotnet tool update](dotnet-tool-update.md) コマンドを使用します。

```dotnetcli
dotnet tool update -g <packagename>
```

[dotnet tool uninstall](dotnet-tool-uninstall.md) を使用してグローバル ツールを削除します。

```dotnetcli
dotnet tool uninstall -g <packagename>
```

マシンに現在インストールされているすべてのグローバル ツールと、それらのバージョンとコマンドを表示するには、[dotnet tool list](dotnet-tool-list.md) コマンドを使用します。

```dotnetcli
dotnet tool list -g
```

## <a name="see-also"></a>関連項目

* [.NET Core ツールの使用に関する問題のトラブルシューティング](troubleshoot-usage-issues.md)
