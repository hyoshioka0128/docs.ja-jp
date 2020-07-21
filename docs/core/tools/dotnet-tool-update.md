---
title: dotnet tool update コマンド
description: dotnet tool update コマンドでは、お使いのコンピューター上の指定された .NET Core ツールを更新します。
ms.date: 07/08/2020
ms.openlocfilehash: 7c4bde44ac9964828074baeb1a697ba64ed17887
ms.sourcegitcommit: 67cf756b033c6173a1bbd1cbd5aef1fccac99e34
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86226622"
---
# <a name="dotnet-tool-update"></a>dotnet tool update

**この記事の対象:** ✔️ .NET Core 2.1 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet tool update` - お使いのコンピューター上の指定された [.NET Core ツール](global-tools.md)を更新します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet tool update <PACKAGE_ID> -g|--global
    [--configfile <FILE>] [--framework <FRAMEWORK>]
    [--add-source <SOURCE>] [--disable-parallel]
    [--ignore-failed-sources] [--interactive] [--no-cache]
    [-v|--verbosity <LEVEL>] [--version <VERSION>]

dotnet tool update <PACKAGE_ID> --tool-path <PATH>
    [--configfile <FILE>] [--framework <FRAMEWORK>]
    [--add-source <SOURCE>] [--disable-parallel]
    [--ignore-failed-sources] [--interactive] [--no-cache]
    [-v|--verbosity <LEVEL>] [--version <VERSION>]

dotnet tool update <PACKAGE_ID> --local
    [--configfile <FILE>] [--framework <FRAMEWORK>]
    [--add-source <SOURCE>] [--disable-parallel]
    [--ignore-failed-sources] [--interactive] [--no-cache]
    [--tool-manifest <PATH>]
    [-v|--verbosity <LEVEL>] [--version <VERSION>]

dotnet tool update -h|--help
```

## <a name="description"></a>説明

`dotnet tool update` コマンドでは、お使いのコンピューター上の .NET Core ツールをパッケージの最新の安定バージョンに更新するための方法を提供します。 このコマンドは、ツールをアンインストールして再インストールして、効果的に更新します。 コマンドを使用するには、次のいずれかのオプションを指定します。

* 既定の場所にインストールされたグローバル ツールを更新するには、`--global` オプションを使用します
* カスタムの場所にインストールされたグローバル ツールを更新するには、`--tool-path` オプションを使用します。
* ローカル ツールを更新するには、`--local` オプションを使用します。

**ローカル ツールは .NET Core SDK 3.0 以降で使用できます。**

## <a name="arguments"></a>引数

- **`PACKAGE_ID`**

  更新する .NET Core グローバル ツールが格納されている NuGet パッケージの名前または ID。 パッケージを見つけるには、[dotnet tool list](dotnet-tool-list.md) コマンドを使用できます。

## <a name="options"></a>オプション

- **`--add-source <SOURCE>`**

  インストール時に使用するために追加の NuGet パッケージ ソースを追加します。

- **`--configfile <FILE>`**

  使用する NuGet 構成 (*nuget.config*) ファイル。

- **`--disable-parallel`**

  複数のプロジェクトを並行して復元できないようにします。

- **`--framework <FRAMEWORK>`**

  ツールを更新する[ターゲット フレームワーク](../../standard/frameworks.md)を指定します。

- **`--ignore-failed-sources`**

  パッケージ ソース エラーを警告として処理します。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます (たとえば、認証を完了する場合)。

- **`--local`**

  ツールとローカル ツール マニフェストを更新します。 `--global` オプションと組み合わせることはできません。

- **`--no-cache`**

  パッケージと HTTP 要求はキャッシュしないでください。

- **`--tool-manifest <PATH>`**

  マニフェスト ファイルへのパス。

- **`--tool-path <PATH>`**

  グローバル ツールがインストールされている場所を指定します。 PATH は絶対パスでも相対パスでもかまいません。 `--global` オプションと組み合わせることはできません。 `--global` と `--tool-path` の両方を省略すると、更新されるツールはローカル ツールであると指定されます。

- **`--version <VERSION>`**

  更新対象のツール パッケージのバージョン範囲。 これはバージョンのダウングレードに使用できません。その前に新しいバージョンを `uninstall` する必要があります。

- **`-g|--global`**

  更新プログラムがユーザー全体のツール用であることを指定します。 `--tool-path` オプションと組み合わせることはできません。 `--global` と `--tool-path` の両方を省略すると、更新されるツールはローカル ツールであると指定されます。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

## <a name="examples"></a>使用例

- **`dotnet tool update -g dotnetsay`**

  [dotnetsay](https://www.nuget.org/packages/dotnetsay/) グローバル ツールを更新します。

- **`dotnet tool update dotnetsay --tool-path c:\global-tools`**

  特定の Windows ディレクトリに配置されている [dotnetsay](https://www.nuget.org/packages/dotnetsay/) グローバル ツールを更新します。

- **`dotnet tool update dotnetsay --tool-path ~/bin`**

  特定の Linux/macOS ディレクトリに配置されている [dotnetsay](https://www.nuget.org/packages/dotnetsay/) グローバル ツールを更新します。

- **`dotnet tool update dotnetsay`**

  現在のディレクトリに対してインストールされている [dotnetsay](https://www.nuget.org/packages/dotnetsay/) ローカル ツールを更新します。

- **`dotnet tool update -g dotnetsay --version 2.0.*`**

  [dotnetsay](https://www.nuget.org/packages/dotnetsay/) グローバル ツールを最新パッチ バージョンに更新します。メジャー バージョンが `2` で、マイナー バージョンが `0` です。

- **`dotnet tool update -g dotnetsay --version (2.0.*,2.1.4)`**

  指定の範囲 `(> 2.0.0 && < 2.1.4)` 内で [dotnetsay](https://www.nuget.org/packages/dotnetsay/) グローバル ツールを一番下のバージョンに更新します。バージョン `2.1.0` がインストールされます。 セマンティック バージョン管理の範囲に関する詳細については、[NuGet パッケージのバージョン管理範囲](/nuget/concepts/package-versioning#version-ranges)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [.NET Core ツール](global-tools.md)
- [セマンティック バージョン管理](https://semver.org)
- [チュートリアル: .NET Core CLI を使って .NET Core グローバル ツールをインストールして使用する](global-tools-how-to-use.md)
- [チュートリアル: .NET Core CLI を使って .NET Core ローカル ツールをインストールして使用する](local-tools-how-to-use.md)
