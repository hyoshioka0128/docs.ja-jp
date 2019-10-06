---
title: dotnet test コマンド
description: dotnet test コマンドは、指定されたプロジェクトで単体テストを実行する場合に使用されます。
ms.date: 05/29/2018
ms.openlocfilehash: c3115d546efb1f076ae9f9731f83a12183aa4154
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182515"
---
# <a name="dotnet-test"></a>dotnet test

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet test` - 単体テストを実行するために使用される .NET テスト ドライバー。

## <a name="synopsis"></a>構文

<!-- markdownlint-disable MD025 -->

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [--blame] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] 
    [-v|--verbosity] [-- <RunSettings arguments>]

dotnet test [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] [-v|--verbosity]

dotnet test [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```dotnetcli
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [-o|--output] [-s|--settings] [-t|--list-tests]  [-v|--verbosity]

dotnet test [-h|--help]
```

---

## <a name="description"></a>説明

`dotnet test` コマンドは、指定されたプロジェクトで単体テストを実行する場合に使用されます。 `dotnet test` コマンドは、プロジェクト用に指定されたテスト ランナーのコンソール アプリケーションを起動します。 テスト ランナーでは、単体テスト フレームワーク (MSTest、NUnit、xUnit など) 用に定義されたテストを実行し、各テストの成功または失敗をレポートします。 すべてのテストが成功した場合、テスト ランナーは 0 の終了コードを返します。それ以外の、いずれかのテストに失敗した場合は、1 を返します。 テスト ランナーと単体テスト ライブラリは、NuGet パッケージとしてパッケージ化され、プロジェクトの通常の依存関係として復元されます。

テスト プロジェクトでは、通常の `<PackageReference>` 要素を使用してテスト ランナーを指定します。次のサンプル プロジェクト ファイルのようになります。

[!code-xml[XUnit Basic Template](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="arguments"></a>引数

`PROJECT`

テスト プロジェクトへのパス。 指定しない場合は、既定で現在のディレクトリに設定されます。

## <a name="options"></a>オプション

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

テスト実行で指定されたパスからカスタムのテスト アダプターを使用します。

`--blame`

変更履歴モードでテストを実行します。 このオプションは、テスト ホストのクラッシュを引き起こす問題のあるテストを分離するのに役立ちます。 これは、現在のディレクトリ内に出力ファイルを *Sequence.xml* として作成します。このファイルは、クラッシュ前にテストの実行順序をキャプチャします。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 既定値は `Debug` ですが、プロジェクトの構成がこの既定の SDK 設定をオーバーライドする可能性があります。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

テストの実行のためのデータ コレクターを有効にします。 詳細については、[「Monitor and analyze test run」](https://aka.ms/vstest-collect) (テストの実行のモニターと分析) を参照してください。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

テスト プラットフォームの診断モードを有効にし、指定したファイルに診断メッセージを出力します。

`-f|--framework <FRAMEWORK>`

特定の[フレームワーク](../../standard/frameworks.md)のテスト バイナリを検索します。

`--filter <EXPRESSION>`

指定された式を使用して、現在のプロジェクト内のテストを除外します。 詳細については、「[フィルター オプションの詳細](#filter-option-details)」セクションをご覧ください。 選択的単体テストのフィルター処理の使用方法に関する詳細と例については、「[選択的単体テストの実行](../testing/selective-unit-tests.md)」をご覧ください。

`-h|--help`

コマンドの短いヘルプを印刷します。

`-l|--logger <LoggerUri/FriendlyName>`

テスト結果のロガーを指定します。

`--no-build`

実行前にテスト プロジェクトをビルドしません。 また、`--no-restore` フラグを暗黙的に設定します。

`--no-restore`

コマンドを実行するときに、暗黙的な復元を実行しません。

`-o|--output <OUTPUT_DIRECTORY>`

実行するバイナリを検索するディレクトリです。

`-r|--results-directory <PATH>`

テスト結果が配置されるディレクトリです。 指定されたディレクトリが存在しない場合は、作成されます。

`-s|--settings <SETTINGS_FILE>`

テストの実行に使用する `.runsettings` ファイルです。 [`.runsettings` ファイルを使用して単体テストを構成します。](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

現在のプロジェクトで検出されたすべてのテストを一覧表示します。

`-v|--verbosity <LEVEL>`

コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

`RunSettings arguments`

テストの RunSettings 構成として渡される引数です。 引数は、"-- " に続く `[name]=[value]` のペアとして指定されます (-- の後ろのスペースに注意してください)。 複数の `[name]=[value]` のペアを区切るにはスペースを使用します。

例 : `dotnet test -- MSTest.DeploymentEnabled=false MSTest.MapInconclusiveToFailed=True`

RunSettings について詳しくは、[vstest.console.exe:RunSettings 引数渡し](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md)に関するページをご覧ください。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

テスト実行で指定されたパスからカスタムのテスト アダプターを使用します。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 既定値は `Debug` ですが、プロジェクトの構成がこの既定の SDK 設定をオーバーライドする可能性があります。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

テストの実行のためのデータ コレクターを有効にします。 詳細については、[「Monitor and analyze test run」](https://aka.ms/vstest-collect) (テストの実行のモニターと分析) を参照してください。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

テスト プラットフォームの診断モードを有効にし、指定したファイルに診断メッセージを出力します。

`-f|--framework <FRAMEWORK>`

特定の[フレームワーク](../../standard/frameworks.md)のテスト バイナリを検索します。

`--filter <EXPRESSION>`

指定された式を使用して、現在のプロジェクト内のテストを除外します。 詳細については、「[フィルター オプションの詳細](#filter-option-details)」セクションをご覧ください。 選択的単体テストのフィルター処理の使用方法に関する詳細と例については、「[選択的単体テストの実行](../testing/selective-unit-tests.md)」をご覧ください。

`-h|--help`

コマンドの短いヘルプを印刷します。

`-l|--logger <LoggerUri/FriendlyName>`

テスト結果のロガーを指定します。

`--no-build`

実行前にテスト プロジェクトをビルドしません。 また、`--no-restore` フラグを暗黙的に設定します。

`--no-restore`

コマンドを実行するときに、暗黙的な復元を実行しません。

`-o|--output <OUTPUT_DIRECTORY>`

実行するバイナリを検索するディレクトリです。

`-r|--results-directory <PATH>`

テスト結果が配置されるディレクトリです。 指定されたディレクトリが存在しない場合は、作成されます。

`-s|--settings <SETTINGS_FILE>`

テストの実行に使用する `.runsettings` ファイルです。 [`.runsettings` ファイルを使用して単体テストを構成します。](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

現在のプロジェクトで検出されたすべてのテストを一覧表示します。

`-v|--verbosity <LEVEL>`

コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

テスト実行で指定されたパスからカスタムのテスト アダプターを使用します。

`-c|--configuration {Debug|Release}`

ビルド構成を定義します。 既定値は `Debug` ですが、プロジェクトの構成がこの既定の SDK 設定をオーバーライドする可能性があります。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

テスト プラットフォームの診断モードを有効にし、指定したファイルに診断メッセージを出力します。

`-f|--framework <FRAMEWORK>`

特定の[フレームワーク](../../standard/frameworks.md)のテスト バイナリを検索します。

`--filter <EXPRESSION>`

指定された式を使用して、現在のプロジェクト内のテストを除外します。 詳細については、「[フィルター オプションの詳細](#filter-option-details)」セクションをご覧ください。 選択的単体テストのフィルター処理の使用方法に関する詳細と例については、「[選択的単体テストの実行](../testing/selective-unit-tests.md)」をご覧ください。

`-h|--help`

コマンドの短いヘルプを印刷します。

`-l|--logger <LoggerUri/FriendlyName>`

テスト結果のロガーを指定します。

`--no-build`

実行前にテスト プロジェクトをビルドしません。

`-o|--output <OUTPUT_DIRECTORY>`

実行するバイナリを検索するディレクトリです。

`-s|--settings <SETTINGS_FILE>`

テストの実行に使用する `.runsettings` ファイルです。 [`.runsettings` ファイルを使用して単体テストを構成します。](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)

`-t|--list-tests`

現在のプロジェクトで検出されたすべてのテストを一覧表示します。

`-v|--verbosity <LEVEL>`

コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

---

## <a name="examples"></a>使用例

現在のディレクトリのプロジェクトでテストを実行します。

`dotnet test`

`test1` プロジェクトでテストを実行します。

`dotnet test ~/projects/test1/test1.csproj`

現在のディレクトリでプロジェクトのテストを実行し、trx 形式でテスト結果ファイルを生成します。

`dotnet test --logger trx`

## <a name="filter-option-details"></a>フィルター オプションの詳細

`--filter <EXPRESSION>`

`<Expression>` の形式は `<property><operator><value>[|&<Expression>]` です。

`<property>` は `Test Case` の属性です。 よく利用される単体テスト フレームワークでサポートされるプロパティは以下の通りです。

| テスト フレームワーク | サポートされるプロパティ                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>name</li><li>ClassName</li><li>優先度</li><li>TestCategory</li></ul> |
| xUnit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>Traits</li></ul>                                   |

`<operator>` は、プロパティと値の関係を示します。

| 演算子 | 関数        |
| :------: | --------------- |
| `=`      | 完全一致     |
| `!=`     | 完全一致ではない |
| `~`      | 内容        |

`<value>` は文字列です。 すべての参照で大文字と小文字が区別されます。

`<operator>` を含まない式は、自動的に `FullyQualifiedName` プロパティの `contains` とみなされます (たとえば、`dotnet test --filter xyz` は `dotnet test --filter FullyQualifiedName~xyz` と同じです)。

式は条件演算子を使用して結合できます。

| 演算子            | 関数 |
| ------------------- | -------- |
| <code>&#124;</code> | OR       |
| `&`                 | AND      |

条件演算子を使用する場合は、式をかっこで囲みます (例: `(Name~TestMethod1) | (Name~TestMethod2)`)。

選択的単体テストのフィルター処理の使用方法に関する詳細と例については、「[選択的単体テストの実行](../testing/selective-unit-tests.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [フレームワークとターゲット](../../standard/frameworks.md)
- [.NET Core のランタイム識別子 (RID) のカタログ](../rid-catalog.md)
