---
title: dotnet remove reference コマンド
description: dotnet remove reference コマンドは、プロジェクト間参照を削除する便利なオプションを提供します。
ms.date: 02/14/2020
ms.openlocfilehash: a45153376d7d6eb764c1d2c6b473d04a273a2de1
ms.sourcegitcommit: c2c1269a81ffdcfc8675bcd9a8505b1a11ffb271
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82158334"
---
# <a name="dotnet-remove-reference"></a>dotnet remove reference

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet remove reference` - プロジェクト間 (P2P) 参照を削除します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet remove [<PROJECT>] reference [-f|--framework <FRAMEWORK>]
     <PROJECT_REFERENCES>

dotnet remove reference -h|--help
```

## <a name="description"></a>説明

`dotnet remove reference` コマンドは、プロジェクトからプロジェクト参照を削除する便利なオプションを提供します。

## <a name="arguments"></a>引数

`PROJECT`

ターゲット プロジェクト ファイル。 指定されていない場合、現在のディレクトリで検索されます。

`PROJECT_REFERENCES`

削除するプロジェクト間 (P2P) 参照。 1 つまたは複数のプロジェクトを指定できます。 [glob パターン](https://en.wikipedia.org/wiki/Glob_(programming))は Unix/Linux ベースの端末でサポートされています。

## <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`-f|--framework <FRAMEWORK>`**

  TFM 形式を使用して特定の[フレームワーク](../../standard/frameworks.md)を対象にしている場合にのみ、参照を削除します。

## <a name="examples"></a>使用例

- 指定したプロジェクトからプロジェクト参照を削除する:

  ```dotnetcli
  dotnet remove app/app.csproj reference lib/lib.csproj
  ```

- 現在のディレクトリ内のプロジェクトから複数のプロジェクト参照を削除する:

  ```dotnetcli
  dotnet remove reference lib1/lib1.csproj lib2/lib2.csproj
  ```

- Unix/Linux で glob パターンを使用して複数のプロジェクト参照を削除する:

  ```dotnetcli
  dotnet remove app/app.csproj reference **/*.csproj`
  ```
