---
title: dotnet nuget list source コマンド
description: dotnet nuget list source コマンドを使うと、NuGet 構成ファイルの既存のソースをすべて一覧表示できます。
ms.date: 03/20/2020
ms.openlocfilehash: 8b14413949bd60ddeed977d19eec9bb99982da70
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463551"
---
# <a name="dotnet-nuget-list-source"></a>dotnet nuget list source

**この記事の対象:** ✔️ .NET Core 3.1.200 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet nuget list source` - 構成されている NuGet ソースをすべて一覧表示します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet nuget list source [--format [Detailed|Short]] [--configfile <FILE>]

dotnet nuget list source -h|--help
```

## <a name="description"></a>説明

`dotnet nuget list source` コマンドを使うと、NuGet 構成ファイルの既存のソースをすべて一覧表示できます。

## <a name="options"></a>オプション

- **`--configfile <FILE>`**

  NuGet 構成ファイル。 指定した場合、このファイルの設定のみが使用されます。 指定しない場合、現在のディレクトリからの構成ファイルの階層が使用されます。 詳細については、「[一般的な NuGet 構成](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)」をご覧ください。

- **`--format [Detailed|Short]`**

  list コマンドの出力の形式: `Detailed` (既定) と `Short`。

## <a name="examples"></a>使用例

- 現在のディレクトリから構成されているソースを一覧表示します:

  ```dotnetcli
  dotnet nuget list source
  ```

## <a name="see-also"></a>関連項目

- [NuGet.config ファイルのパッケージ ソース セクション](/nuget/reference/nuget-config-file#package-source-sections)

- [sources コマンド (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
