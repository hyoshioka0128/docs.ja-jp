---
title: dotnet test コマンド
description: dotnet test コマンドは、指定されたプロジェクトで単体テストを実行する場合に使用されます。
ms.date: 04/29/2020
ms.openlocfilehash: 911d10917c2262c0bd32ef30d48da0f85ac39a39
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803154"
---
# <a name="dotnet-test"></a>dotnet test

**この記事の対象:** ✔️ .NET Core 2.1 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet test` - 単体テストを実行するために使用される .NET テスト ドライバー。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet test [<PROJECT> | <SOLUTION> | <DIRECTORY> | <DLL>]
    [-a|--test-adapter-path <PATH_TO_ADAPTER>] [--blame]
    [-c|--configuration <CONFIGURATION>]
    [--collect <DATA_COLLECTOR_FRIENDLY_NAME>]
    [-d|--diag <PATH_TO_DIAGNOSTICS_FILE>] [-f|--framework <FRAMEWORK>]
    [--filter <EXPRESSION>] [--interactive]
    [-l|--logger <LOGGER_URI/FRIENDLY_NAME>] [--no-build]
    [--nologo] [--no-restore] [-o|--output <OUTPUT_DIRECTORY>]
    [-r|--results-directory <PATH>] [--runtime <RUNTIME_IDENTIFIER>]
    [-s|--settings <SETTINGS_FILE>] [-t|--list-tests]
    [-v|--verbosity <LEVEL>] [[--] <RunSettings arguments>]

dotnet test -h|--help
```

## <a name="description"></a>説明

`dotnet test` コマンドは、指定されたソリューションで単体テストを実行する場合に使用されます。 `dotnet test` コマンドを実行すると、ソリューションがビルドされ、ソリューション内の各テスト プロジェクトのテスト ホスト アプリケーションが実行されます。 テスト ホストは、指定されたプロジェクトで、テスト フレームワークを使用してテストを実行します。たとえば、MSTest、NUnit、xUnit などです。そして、各テストの成功または失敗を報告します。 すべてのテストが成功した場合、テスト ランナーは 0 の終了コードを返します。それ以外の、いずれかのテストに失敗した場合は、1 を返します。

複数の対象を持つプロジェクトでは、対象となる各フレームワークに対してテストが実行されます。 テスト ホストと単体テスト フレームワークは、NuGet パッケージとしてパッケージ化され、プロジェクトの通常の依存関係として復元されます。

テスト プロジェクトでは、通常の `<PackageReference>` 要素を使用してテスト ランナーを指定します。次のサンプル プロジェクト ファイルのようになります。

[!code-xml[XUnit Basic Template](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

`Microsoft.NET.Test.Sdk` がテスト ホストの場合、`xunit` はテスト フレームワークです。 また、`xunit.runner.visualstudio` はテスト アダプターであり、xUnit フレームワークはテスト ホストと連携できます。

### <a name="implicit-restore"></a>暗黙的な復元

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

## <a name="arguments"></a>引数

- **`PROJECT | SOLUTION | DIRECTORY | DLL`**

  - テスト プロジェクトへのパス。
  - ソリューションへのパス。
  - プロジェクトまたはソリューションを含むディレクトリへのパス。
  - テスト プロジェクト " *.dll*" ファイルへのパス。

  指定されていない場合、プロジェクトまたはソリューションが現在のディレクトリで検索されます。

## <a name="options"></a>オプション

- **`-a|--test-adapter-path <PATH_TO_ADAPTER>`**

  追加のテスト アダプターを検索するディレクトリへのパス。 サフィックス `.TestAdapter.dll` を持つ " *.dll*" ファイルのみが検査されます。 指定しない場合、テスト " *.dll*" のディレクトリが検索されます。

- **`--blame`**

  変更履歴モードでテストを実行します。 このオプションは、テスト ホストがクラッシュする原因となる問題のあるテストを分離するために役立ちます。 クラッシュが検出されると、クラッシュ前に実行されたテストの順序をキャプチャするシーケンス ファイルが `TestResults/<Guid>/<Guid>_Sequence.xml` に作成されます。

- **`-c|--configuration <CONFIGURATION>`**

  ビルド構成を定義します。 既定値は `Debug` ですが、プロジェクトの構成がこの既定の SDK 設定をオーバーライドする可能性があります。

- **`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`**

  テストの実行のためのデータ コレクターを有効にします。 詳細については、[「Monitor and analyze test run」](https://aka.ms/vstest-collect) (テストの実行のモニターと分析) を参照してください。
  
  .NET Core でサポートされている任意のプラットフォーム上のコード カバレッジを収集するには、[Coverlet](https://github.com/coverlet-coverage/coverlet/blob/master/README.md) をインストールし、`--collect:"XPlat Code Coverage"` オプションを使用します。

  Windows では、`--collect "Code Coverage"` オプションを使用してコード カバレッジを収集できます。 このオプションを選択すると、 *.coverage* ファイルが生成されます。このファイルは、Visual Studio 2019 Enterprise で開くことができます。 詳細については、[コード カバレッジの使用](/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested)に関するページと「[コード カバレッジ分析のカスタマイズ](/visualstudio/test/customizing-code-coverage-analysis)」を参照してください。

- **`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`**

  テスト プラットフォームの診断モードを有効にし、指定したファイルとそれ以降のファイルに診断メッセージを出力します。 メッセージをログに記録するプロセスによって、テスト ホスト ログの `*.host_<date>.txt` やデータ コレクター ログの `*.datacollector_<date>.txt` などの、作成されるファイルが決まります。

- **`-f|--framework <FRAMEWORK>`**

  テスト バイナリに `dotnet` または .NET Framework テスト ホストを強制的に使用します。 このオプションでは、使用するホストの種類のみが決定されます。 実際に使用されるフレームワークのバージョンは、テスト プロジェクトの "*runtimeconfig. json*" によって決まります。 指定しない場合、[TargetFramework アセンブリ属性](/dotnet/api/system.runtime.versioning.targetframeworkattribute) を使用してホストの種類が決定されます。 その属性が " *.dll*" から削除されると、.NET Framework ホストが使用されます。

- **`--filter <EXPRESSION>`**

  指定された式を使用して、現在のプロジェクト内のテストを除外します。 詳細については、「[フィルター オプションの詳細](#filter-option-details)」セクションをご覧ください。 選択的単体テストのフィルター処理の使用方法に関する詳細と例については、「[選択的単体テストの実行](../testing/selective-unit-tests.md)」をご覧ください。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます。 たとえば、認証を完了する場合があります。 .NET Core 3.0 SDK 以降で使用できます。

- **`-l|--logger <LOGGER_URI/FRIENDLY_NAME>`**

  テスト結果のロガーを指定します。 MSBuild とは異なり、dotnet テストでは省略形は受け入れられません。`-l "console;v=d"` ではなく `-l "console;verbosity=detailed"` を使用してください。

- **`--no-build`**

  実行前にテスト プロジェクトをビルドしません。 また、- `--no-restore` フラグが暗黙的に設定されます。

- **`--nologo`**

  Microsoft TestPlatform バナーを表示せずにテストを実行します。 .NET Core 3.0 SDK 以降で使用できます。

- **`--no-restore`**

  コマンドを実行するときに、暗黙的な復元を実行しません。

- **`-o|--output <OUTPUT_DIRECTORY>`**

  実行するバイナリを検索するディレクトリです。 指定しない場合、既定のパスは `./bin/<configuration>/<framework>/` になります。  (`TargetFrameworks` プロパティを使用した) ターゲット フレームワークが複数あるプロジェクトの場合は、このオプションを指定するときに `--framework` も定義する必要があります。 `dotnet test` では常に、出力ディレクトリからテストが実行されます。 <xref:System.AppDomain.BaseDirectory%2A?displayProperty=nameWithType> を使用して、出力ディレクトリ内のテスト資産を使用できます。

- **`-r|--results-directory <PATH>`**

  テスト結果が配置されるディレクトリです。 指定されたディレクトリが存在しない場合は、作成されます。 既定値は、プロジェクト ファイルが含まれるディレクトリの `TestResults` です。

- **`--runtime <RUNTIME_IDENTIFIER>`**

  テスト対象のターゲット ランタイム。

- **`-s|--settings <SETTINGS_FILE>`**

  テストの実行に使用する `.runsettings` ファイルです。 `TargetPlatform` 要素 (x86|x64) は `dotnet test` には影響しません。 x86 を対象とするテストを実行するには、x86 バージョンの .NET Core をインストールします。 パスにある *dotnet.exe* のビットは、テストを実行するために使用されるものです。 詳細については、次のリソースを参照してください。

  - [`.runsettings` ファイルを使用して単体テストを構成します。](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)
  - [テスト実行を構成する](https://github.com/Microsoft/vstest-docs/blob/master/docs/configure.md)

- **`-t|--list-tests`**

  現在のプロジェクトで検出されたすべてのテストを一覧表示します。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。 既定値は、`minimal` です。 詳細については、「<xref:Microsoft.Build.Framework.LoggerVerbosity>」を参照してください。

- **`RunSettings`** 引数

 インラインの `RunSettings` は、コマンド ラインの最後の引数として "-- " の後に渡されます (-- の後のスペースに注意してください)。 インラインの `RunSettings` は `[name]=[value]` のペアとして指定されます。 複数の `[name]=[value]` のペアを区切るにはスペースを使用します。

  例 : `dotnet test -- MSTest.DeploymentEnabled=false MSTest.MapInconclusiveToFailed=True`

  詳しくは、「[コマンド ラインで RunSettings 引数を渡す](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md)」をご覧ください。

## <a name="examples"></a>使用例

- 現在のディレクトリのプロジェクトでテストを実行します。

  ```dotnetcli
  dotnet test
  ```

- `test1` プロジェクトでテストを実行します。

  ```dotnetcli
  dotnet test ~/projects/test1/test1.csproj
  ```

- 現在のディレクトリでプロジェクトのテストを実行し、trx 形式でテスト結果ファイルを生成します。

  ```dotnetcli
  dotnet test --logger trx
  ```

- 現在のディレクトリでプロジェクトのテストを実行し、([Coverlet](https://github.com/coverlet-coverage/coverlet/blob/master/Documentation/VSTestIntegration.md) コレクター統合をインストールした後) コード カバレッジ ファイルを生成します。

  ```dotnetcli
  dotnet test --collect:"XPlat Code Coverage"
  ```

- 現在のディレクトリでプロジェクトのテストを実行し、コード カバレッジ ファイルを生成します (Windows のみ)。

  ```dotnetcli
  dotnet test --collect "Code Coverage"
  ```

- 現在のディレクトリでプロジェクトのテストを実行し、詳細をコンソールに記録します。

  ```dotnetcli
  dotnet test --logger "console;verbosity=detailed"
  ```

- 現在のディレクトリのプロジェクトでテストを実行し、テスト ホストがクラッシュしたときに実行されていたテストを報告します。

  ```dotnetcli
  dotnet test --blame
  ```

## <a name="filter-option-details"></a>フィルター オプションの詳細

`--filter <EXPRESSION>`

`<Expression>` の形式は `<property><operator><value>[|&<Expression>]` です。

`<property>` は `Test Case` の属性です。 よく利用される単体テスト フレームワークでサポートされるプロパティは以下の通りです。

| テスト フレームワーク | サポートされるプロパティ                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>名前</li><li>ClassName</li><li>優先度</li><li>TestCategory</li></ul> |
| xUnit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>Traits</li></ul>                                   |
| NUnit          | <ul><li>FullyQualifiedName</li><li>名前</li><li>TestCategory</li><li>優先度</li></ul>                                   |

`<operator>` は、プロパティと値の関係を示します。

| 演算子 | 関数        |
| :------: | --------------- |
| `=`      | 完全一致     |
| `!=`     | 完全一致ではない |
| `~`      | 内容        |
| `!~`     | 含まない    |

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
- [コマンドラインを使用して runsettings 引数を渡す](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md)
