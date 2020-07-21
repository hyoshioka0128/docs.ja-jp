---
title: dotnet add reference コマンド
description: dotnet add 参照コマンドは、プロジェクト間参照を追加する便利なオプションを提供します。
ms.date: 02/14/2020
ms.openlocfilehash: b261e24ed6a9d5bd489d317d2663b1420b5c34ff
ms.sourcegitcommit: c2c1269a81ffdcfc8675bcd9a8505b1a11ffb271
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82158321"
---
# <a name="dotnet-add-reference"></a>dotnet add reference

**この記事の対象:** ✔️ .NET Core 2.x SDK 以降のバージョン

## <a name="name"></a>名前

`dotnet add reference` - プロジェクト間 (P2P) 参照を追加します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet add [<PROJECT>] reference [-f|--framework <FRAMEWORK>]
     [--interactive] <PROJECT_REFERENCES>

dotnet add reference -h|--help
```

## <a name="description"></a>説明

`dotnet add reference` コマンドは、プロジェクトにプロジェクト参照を追加する便利なオプションを提供します。 このコマンドを実行すると、`<ProjectReference>` 要素がプロジェクト ファイルに追加されます。

```xml
<ItemGroup>
  <ProjectReference Include="app.csproj" />
  <ProjectReference Include="..\lib2\lib2.csproj" />
  <ProjectReference Include="..\lib1\lib1.csproj" />
</ItemGroup>
```

## <a name="arguments"></a>引数

- **`PROJECT`**

  プロジェクト ファイルを指定します。 指定されていない場合、現在のディレクトリで検索されます。

- **`PROJECT_REFERENCES`**

  追加するプロジェクト間参照 (P2P) です。 1 つ以上のプロジェクトを指定します。 [glob パターン](https://en.wikipedia.org/wiki/Glob_(programming))は Unix/Linux ベースのシステムで利用できます。

## <a name="options"></a>オプション

- **`-f|--framework <FRAMEWORK>`**

  TFM 形式を使用して特定の[フレームワーク](../../standard/frameworks.md)を対象にしている場合にのみ、プロジェクト参照を追加します。

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--interactive`**

  コマンドを停止して、ユーザーの入力または操作のために待機させることができます (通常は、認証を完了する場合)。 .NET Core 3.0 SDK 以降で使用できます。

## <a name="examples"></a>使用例

- プロジェクト参照を追加する:

  ```dotnetcli
  dotnet add app/app.csproj reference lib/lib.csproj
  ```

- 現在のディレクトリのプロジェクトに複数のプロジェクト参照を追加する:

  ```dotnetcli
  dotnet add reference lib1/lib1.csproj lib2/lib2.csproj
  ```

- Linux/Unix で glob パターンを使って複数のプロジェクト参照を追加する:

  ```dotnetcli
  dotnet add app/app.csproj reference **/*.csproj
  ```
