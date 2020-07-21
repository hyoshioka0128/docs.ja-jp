---
title: dotnet nuget remove source コマンド
description: dotnet nuget remove source コマンドを使うと、NuGet 構成ファイルから既存のソースを削除できます。
ms.date: 03/20/2020
ms.openlocfilehash: b259873e1885644b272136fa31414410bdfd9f27
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463489"
---
# <a name="dotnet-nuget-remove-source"></a>dotnet nuget remove source

**この記事の対象:** ✔️ .NET Core 3.1.200 SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet nuget remove source` - NuGet ソースを削除します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet nuget remove source <NAME> [--configfile <FILE>]

dotnet nuget remove source -h|--help
```

## <a name="description"></a>説明

`dotnet nuget remove source` コマンドを使うと、NuGet 構成ファイルから既存のソースを削除できます。

## <a name="arguments"></a>引数

- **`NAME`**

  ソースの名前。

## <a name="options"></a>オプション

- **`--configfile`**

  NuGet 構成ファイル。 指定した場合、このファイルの設定のみが使用されます。 指定しない場合、現在のディレクトリからの構成ファイルの階層が使用されます。 詳細については、「[一般的な NuGet 構成](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)」をご覧ください。

## <a name="examples"></a>使用例

- `mySource` という名前のソースを削除します。

  ```dotnetcli
  dotnet nuget remove source mySource
  ```

## <a name="see-also"></a>関連項目

- [NuGet.config ファイルのパッケージ ソース セクション](/nuget/reference/nuget-config-file#package-source-sections)

- [sources コマンド (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
