---
title: dotnet msbuild コマンド
description: dotnet msbuild コマンドは、MSBuild コマンド ラインへのアクセスを提供します。
ms.date: 02/14/2020
ms.openlocfilehash: 9739fe782e17db3955db087ca1781ad4280cd491
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803169"
---
# <a name="dotnet-msbuild"></a>dotnet msbuild

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet msbuild` - プロジェクトとそのすべての依存関係をビルドします。 メモ:複数存在するとき、ソリューションまたはプロジェクト ファイルを場合によっては指定する必要があります。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet msbuild <MSBUILD_ARGUMENTS>

dotnet msbuild -h
```

## <a name="description"></a>説明

`dotnet msbuild` コマンドでは、完全に機能する MSBuild へのアクセスを許可します。

このコマンドには、SDK スタイルのプロジェクトに対してのみ、既存の MSBuild コマンド ライン クライアントとまったく同じ機能があります。 オプションはすべて同じです。 使用可能なオプションの詳細については、「[MSBuild コマンド ライン リファレンス](/visualstudio/msbuild/msbuild-command-line-reference)」を参照してください。

[dotnet build](dotnet-build.md) コマンドは、`dotnet msbuild -restore` に相当します。 プロジェクトをビルドしないが、特定のターゲットを実行する場合、`dotnet build` または `dotnet msbuild` を使用し、ターゲットを指定します。

## <a name="examples"></a>使用例

- プロジェクトとその依存関係をビルドします。

  ```dotnetcli
  dotnet msbuild
  ```

- リリース構成を使用して、プロジェクトとその依存関係をビルドします。

  ```dotnetcli
  dotnet msbuild -property:Configuration=Release
  ```

- 発行先を実行して、RID `osx.10.11-x64` に発行します。

  ```dotnetcli
  dotnet msbuild -target:Publish -property:RuntimeIdentifiers=osx.10.11-x64
  ```

- プロジェクト全体と SDK に付属するすべてのターゲットをご覧ください。

  ```dotnetcli
  dotnet msbuild -preprocess
  dotnet msbuild -preprocess:<fileName>.xml
  ```
