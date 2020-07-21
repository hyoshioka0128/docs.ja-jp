---
title: dotnet tool restore コマンド
description: dotnet tool restore コマンドでは、現在のディレクトリのスコープ内にある .NET Core ローカル ツールをお使いのコンピューター上にインストールします。
ms.date: 02/14/2020
ms.openlocfilehash: a518c2d45bbe9522bddfed4bbef61b30f1ad634b
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463341"
---
# <a name="dotnet-tool-restore"></a>dotnet tool restore

**この記事の対象:** ✔️ .NET Core 3.0 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet tool restore` - 現在のディレクトリのスコープ内にある .NET Core ローカル ツールをお使いのコンピューター上にインストールします。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet tool restore <PACKAGE_NAME>
    [--configfile <FILE>] [--add-source <SOURCE>]
    [tool-manifest <PATH_TO_MANIFEST_FILE>] [--disable-parallel]
    [--ignore-failed-sources] [--no-cache] [--interactive]
    [-v|--verbosity <LEVEL>]

dotnet tool restore -h|--help
```

## <a name="description"></a>説明

`dotnet tool restore` コマンドでは、現在のディレクトリのスコープ内にあるツール マニフェスト ファイルを検索し、そこに一覧表示されたツールをインストールします。 マニフェスト ファイルの詳細については、「[ローカル ツールのインストール](global-tools.md#install-a-local-tool)」および「[ローカル ツールの起動](global-tools.md#invoke-a-local-tool)」を参照してください。

## <a name="arguments"></a>引数

- **`PACKAGE_NAME`**

インストールする .NET Core ツールが格納されている NuGet パッケージの名前または ID。

## <a name="options"></a>オプション

- **`--configfile <FILE>`**

  使用する NuGet 構成 (*nuget.config*) ファイル。

- **`--add-source <SOURCE>`**

  インストール時に使用するために追加の NuGet パッケージ ソースを追加します。

- **`--tool-manifest <PATH>`**

  マニフェスト ファイルへのパス。

- **`--disable-parallel`**

  複数のプロジェクトを並行して復元できないようにします。

- **`--ignore-failed-sources`**

  パッケージ ソース エラーを警告として処理します。

- **`--no-cache`**

  パッケージと HTTP 要求をキャッシュしません。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます (たとえば、認証を完了する場合)。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`-v|--verbosity <LEVEL>`**

  コマンドの詳細レベルを設定します。 指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。

## <a name="example"></a>例

- **`dotnet tool restore`**

  現在のディレクトリのローカル ツールを復元します。

## <a name="see-also"></a>関連項目

- [.NET Core ツール](global-tools.md)
- [チュートリアル: .NET Core CLI を使って .NET Core ローカル ツールをインストールして使用する](local-tools-how-to-use.md)
