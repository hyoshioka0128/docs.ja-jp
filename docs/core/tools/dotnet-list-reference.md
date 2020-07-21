---
title: dotnet list reference コマンド
description: dotnet list 参照コマンドは、プロジェクト間参照を列挙する便利なオプションを提供します。
ms.date: 02/14/2020
ms.openlocfilehash: b9b34c17102c6218f3d99f6e2620e99f70140284
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83802763"
---
# <a name="dotnet-list-reference"></a>dotnet list reference

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet list reference` - プロジェクト間参照を列挙します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet list [<PROJECT>] reference

dotnet list -h|--help
```

## <a name="description"></a>説明

`dotnet list reference` コマンドは、特定のプロジェクトのプロジェクト参照を列挙する便利なオプションを提供します。

## <a name="arguments"></a>引数

* **`PROJECT`**

  操作するプロジェクト ファイル。 ファイルを指定しない場合、コマンドによって現在のディレクトリから検索されます。

## <a name="options"></a>オプション

* **`-h|--help`**

  コマンドの短いヘルプを印刷します。

## <a name="examples"></a>使用例

* 指定したプロジェクトのプロジェクト参照を列挙する:

  ```dotnetcli
  dotnet list app/app.csproj reference
  ```

* 現在のディレクトリ内のプロジェクトのプロジェクト参照を列挙する:

  ```dotnetcli
  dotnet list reference
  ```
