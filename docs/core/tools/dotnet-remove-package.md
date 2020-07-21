---
title: dotnet remove package コマンド
description: dotnet remove package コマンドは、プロジェクトへの NuGet パッケージ参照を削除する便利なオプションを提供します。
ms.date: 02/14/2020
ms.openlocfilehash: fc74ac1364a0ed027b83dab270d382f238dc00e5
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463453"
---
# <a name="dotnet-remove-package"></a>dotnet remove package

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>name

`dotnet remove package` - プロジェクト ファイルからパッケージ参照を削除します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet remove [<PROJECT>] package <PACKAGE_NAME>

dotnet remove package -h|--help
```

## <a name="description"></a>[説明]

`dotnet remove package` コマンドは、NuGet パッケージ参照をプロジェクトから削除する便利なオプションを提供します。

## <a name="arguments"></a>引数

`PROJECT`

プロジェクト ファイルを指定します。 指定されていない場合、現在のディレクトリで検索されます。

`PACKAGE_NAME`

削除するパッケージ参照。

## <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

## <a name="examples"></a>例

- 現在のディレクトリにあるプロジェクトから `Newtonsoft.Json` NuGet パッケージを削除する:

  ```dotnetcli
  dotnet remove package Newtonsoft.Json
  ```
