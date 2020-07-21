---
title: dotnet pack コマンド
description: dotnet pack コマンドでは、.NET Core プロジェクトの NuGet パッケージを作成します。
ms.date: 04/28/2020
ms.openlocfilehash: 00cda2c52a12a7a3aef5f61291120f522536131d
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442229"
---
# <a name="dotnet-pack"></a>dotnet pack

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet pack` - NuGet パッケージにコードをパックします。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet pack [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [--force] [--include-source] [--include-symbols] [--interactive]
    [--no-build] [--no-dependencies] [--no-restore] [--nologo]
    [-o|--output <OUTPUT_DIRECTORY>] [--runtime <RUNTIME_IDENTIFIER>]
    [-s|--serviceable] [-v|--verbosity <LEVEL>]
    [--version-suffix <VERSION_SUFFIX>]

dotnet pack -h|--help
```

## <a name="description"></a>説明

`dotnet pack` コマンドはプロジェクトをビルドし、NuGet パッケージを作成します。 このコマンドの結果が NuGet パッケージ (つまり、 *.nupkg* ファイル) です。

デバッグ シンボルを含むパッケージを生成する場合、使用可能なオプションが 2 つあります。

- `--include-symbols` -シンボル パッケージを作成します。
- `--include-source` -ソース ファイルが含まれた `src` フォルダーを含むシンボル パッケージを作成します。

パックされるプロジェクトの NuGet 依存関係が *.nuspec* ファイルに追加されるため、パッケージのインストール時に適切に解決されます。 プロジェクト間参照はプロジェクト内にはパッケージ化されません。 現時点では、プロジェクト間の依存関係がある場合は、プロジェクトごとにパッケージが必要になります。

既定では、`dotnet pack` は最初にプロジェクトをビルドします。 この動作を避けたい場合は、`--no-build` オプションを渡します。 このオプションは、コードが既にビルドされていることがわかっている場合の継続的インテグレーション (CI) ビルド シナリオで役立つことがよくあります。

> [!NOTE]
> 場合によっては、暗黙的なビルドは実行できません。 これは、ビルドとパック ターゲット間の循環依存を回避するため `GeneratePackageOnBuild` が設定されている場合に発生します。 ロックされているファイルがある場合や、その他の問題がある場合にも、ビルドは失敗します。

パッキング プロセスのために `dotnet pack` コマンドに MSBuild のプロパティを使用できます。 詳細については、「[NuGet メタデータ プロパティ](csproj.md#nuget-metadata-properties)」と「[MSBuild コマンド ライン リファレンス](/visualstudio/msbuild/msbuild-command-line-reference)」を参照してください。 「[例](#examples)」のセクションでは、MSBuild の -p スイッチを使用する方法について、2 つの異なるシナリオで説明します。

Web プロジェクトは既定でパッケージ化可能ではありません。 既定の動作をオーバーライドするには、 *.csproj* ファイルに次のプロパティを追加します。

```xml
<PropertyGroup>
   <IsPackable>true</IsPackable>
</PropertyGroup>
```

### <a name="implicit-restore"></a>暗黙的な復元

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>引数

`PROJECT | SOLUTION`

  パックするプロジェクトまたはソリューション。 [csproj ファイル](csproj.md)、vbproj ファイル、fsproj ファイル、ソリューション ファイル、またはディレクトリのいずれかへのパスです。 指定されていない場合、コマンドによりプロジェクトまたはソリューション ファイルが現在のディレクトリで検索されます。

## <a name="options"></a>オプション

- **`-c|--configuration <CONFIGURATION>`**

  ビルド構成を定義します。 ほとんどのプロジェクトの既定値は `Debug` ですが、プロジェクトでビルド構成設定をオーバーライドできます。

- **`--force`**

  最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、*project.assets.json* ファイルを削除することと同じです。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--include-source`**

  通常の NuGet パッケージに加えて、デバッグ シンボル NuGet パッケージが出力ディレクトリ内に含まれます。 ソース ファイルは、シンボル パッケージ内の `src` フォルダーに含まれます。

- **`--include-symbols`**

  通常の NuGet パッケージに加えて、デバッグ シンボル NuGet パッケージが出力ディレクトリ内に含まれます。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます (たとえば、認証を完了する場合)。 .NET Core 3.0 SDK 以降で使用できます。

- **`--no-build`**

  パッキングの前にプロジェクトをビルドしません。 また、`--no-restore` フラグが暗黙的に設定されます。

- **`--no-dependencies`**

  プロジェクト間参照を無視し、ルート プロジェクトのみを復元します。

- **`--no-restore`**

  コマンドを実行するときに、暗黙的な復元を実行しません。

- **`--nologo`**

  著作権情報を表示しません。 .NET Core 3.0 SDK 以降で使用できます。

- **`-o|--output <OUTPUT_DIRECTORY>`**

  指定したディレクトリにビルド済みパッケージを配置します。

- **`--runtime <RUNTIME_IDENTIFIER>`**

  パッケージを復元するターゲット ランタイムを指定します。 ランタイム ID (RID) の一覧については、[RID カタログ](../rid-catalog.md)に関するページをご覧ください。

- **`-s|--serviceable`**

  パッケージに処理可能フラグを設定します。 詳しくは、「[.NET Blog: .NET 4.5.1 Supports Microsoft Security Updates for .NET NuGet Libraries](https://aka.ms/nupkgservicing)」(.NET ブログ: .NET 4.5.1 は .NET NuGet ライブラリに対する Microsoft セキュリティ更新プログラムをサポートする) をご覧ください。

- **`--version-suffix <VERSION_SUFFIX>`**

  プロジェクトの `$(VersionSuffix)` MSBuild プロパティの値を定義します。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

## <a name="examples"></a>使用例

- 現在のディレクトリのプロジェクトをパックします。

  ```dotnetcli
  dotnet pack
  ```

- `app1` プロジェクトをパックします。

  ```dotnetcli
  dotnet pack ~/projects/app1/project.csproj
  ```

- プロジェクトを現在のディレクトリにパックし、`nupkgs` フォルダーに生成されたパッケージを配置します。

  ```dotnetcli
  dotnet pack --output nupkgs
  ```

- 現在のディレクトリのプロジェクトを `nupkgs` フォルダーにパックし、ビルド ステップをスキップします。

  ```dotnetcli
  dotnet pack --no-build --output nupkgs
  ```

- *.csproj* ファイルで `<VersionSuffix>$(VersionSuffix)</VersionSuffix>` として構成されているプロジェクトのバージョン サフィックスで、現在のプロジェクトをパックし、結果のパッケージ バージョンを指定されたサフィックスで更新します。

  ```dotnetcli
  dotnet pack --version-suffix "ci-1234"
  ```

- `PackageVersion` MSBuild プロパティで `2.1.0` にパッケージ バージョンを設定します。

  ```dotnetcli
  dotnet pack -p:PackageVersion=2.1.0
  ```

- プロジェクトを特定の[ターゲット フレームワーク](../../standard/frameworks.md)用にパックします。

  ```dotnetcli
  dotnet pack -p:TargetFrameworks=net45
  ```

- プロジェクトをパックして、復元操作用の特定のランタイム (Windows 10) を使用する:

  ```dotnetcli
  dotnet pack --runtime win10-x64
  ```

- *.nuspec ファイル*を使用してプロジェクトをパックします。

  ```dotnetcli
  dotnet pack ~/projects/app1/project.csproj -p:NuspecFile=~/projects/app1/project.nuspec -p:NuspecBasePath=~/projects/app1/nuget
  ```

  `NuspecFile`、`NuspecBasePath`、`NuspecProperties` の詳細については、次のリソースを参照してください。
  
  - [.nuspec を使用したパック](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-using-a-nuspec)
  - [カスタマイズされたパッケージを作成するための高度な拡張ポイント](https://docs.microsoft.com/nuget/reference/msbuild-targets#advanced-extension-points-to-create-customized-package)
  - [グローバル プロパティ](https://docs.microsoft.com/visualstudio/msbuild/msbuild-properties?view=vs-2019#global-properties)
