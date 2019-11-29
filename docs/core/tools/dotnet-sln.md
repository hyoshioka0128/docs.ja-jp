---
title: dotnet sln コマンド
description: dotnet-sln コマンドは、ソリューション ファイルでプロジェクトを追加、削除、一覧表示するための便利なオプションを提供します。
ms.date: 10/29/2019
ms.openlocfilehash: 18702c7638798117bd04d5c6a829d64cc6bf18a8
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73191822"
---
# <a name="dotnet-sln"></a>dotnet sln

**この記事の対象: ✓** .NET Core 1.x SDK 以降のバージョン

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet sln` - .NET Core ソリューション ファイルを変更します。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet sln [<SOLUTION_FILE>] [command] [-h|--help]
```

## <a name="description"></a>説明

`dotnet sln` コマンドは、ソリューション ファイルでプロジェクトを追加、削除、一覧表示するための便利な方法を提供します。

`dotnet sln` コマンドを使用するには、ソリューション ファイルが既に存在している必要があります。 作成する必要がある場合、下の例のように [dotnet new](dotnet-new.md) コマンドを使用します。

```dotnetcli
dotnet new sln
```

## <a name="arguments"></a>引数

- **`SOLUTION_FILE`**

  使用するソリューション ファイル。 指定されていない場合、現在のディレクトリで検索されます。 ディレクトリに複数のソリューション ファイルがある場合、1 つを指定する必要があります。

## <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

## <a name="commands"></a>コマンド

### `add`

ソリューション ファイルに 1 つまたは複数のプロジェクトを追加します。

#### <a name="synopsis"></a>構文

```dotnetcli
dotnet sln [<SOLUTION_FILE>] add [--in-root] [-s|--solution-folder] <PROJECT_PATH>
dotnet sln add [-h|--help]
```

#### <a name="arguments"></a>引数

- **`SOLUTION_FILE`**

  使用するソリューション ファイル。 指定されていない場合、現在のディレクトリで検索されます。 ディレクトリに複数のソリューション ファイルがある場合、1 つを指定する必要があります。

- **`PROJECT_PATH`**

  ソリューションに追加するプロジェクトへのパス。 複数のプロジェクトを追加するには、それぞれをスペースで区切って順に追加します。 Unix/Linux シェルの[glob パターン](https://en.wikipedia.org/wiki/Glob_(programming))拡張機能は、`dotnet sln`コマンドで正しく処理されます。

#### <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--in-root`**

  ソリューション フォルダーを作成するのではなく、プロジェクトをソリューションのルートに配置します。 .NET Core 3.0 SDK 以降で使用できます。

- **`-s|--solution-folder`**

  プロジェクトの追加先のソリューション フォルダーのパス。 .NET Core 3.0 SDK 以降で使用できます。

### `remove`

ソリューション ファイルから 1 つまたは複数のプロジェクトを削除します。

#### <a name="synopsis"></a>構文

```dotnetcli
dotnet sln [<SOLUTION_FILE>] remove <PROJECT_PATH>
dotnet sln [<SOLUTION_FILE>] remove [-h|--help]
```

#### <a name="arguments"></a>引数

- **`SOLUTION_FILE`**

  使用するソリューション ファイル。 指定されていない場合、現在のディレクトリで検索されます。 ディレクトリに複数のソリューション ファイルがある場合、1 つを指定する必要があります。

- **`PROJECT_PATH`**

  ソリューションから削除するプロジェクトへのパス。 複数のプロジェクトを削除するには、それぞれをスペースで区切って順に追加します。 Unix/Linux シェルの[glob パターン](https://en.wikipedia.org/wiki/Glob_(programming))拡張機能は、`dotnet sln`コマンドで正しく処理されます。

#### <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

### `list`

ソリューション ファイルのすべてのプロジェクトを一覧表示します。

#### <a name="synopsis"></a>構文

```dotnetcli
dotnet sln list [-h|--help]
```
  
#### <a name="arguments"></a>引数

- **`SOLUTION_FILE`**

  使用するソリューション ファイル。 指定されていない場合、現在のディレクトリで検索されます。 ディレクトリに複数のソリューション ファイルがある場合、1 つを指定する必要があります。

#### <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

## <a name="examples"></a>使用例

ソリューションに 1 つの C# プロジェクトを追加する:

```dotnetcli
dotnet sln todo.sln add todo-app/todo-app.csproj
```

ソリューションから 1 つの C# プロジェクトを削除する:

```dotnetcli
dotnet sln todo.sln remove todo-app/todo-app.csproj
```

ソリューションに複数の C# プロジェクトを追加する:

```dotnetcli
dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj
```

ソリューションから複数の C# プロジェクトを削除する:

```dotnetcli
dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj
```

glob パターンを使用して、ソリューションに複数の C# プロジェクトを追加する (Unix/Linux のみ):

```dotnetcli
dotnet sln todo.sln add **/*.csproj
```

glob パターンを使用して、ソリューションから複数の C# プロジェクトを削除する (Unix/Linux のみ):

```dotnetcli
dotnet sln todo.sln remove **/*.csproj
```
