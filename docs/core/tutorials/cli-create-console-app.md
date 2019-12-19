---
title: CLI ツールを使用する .NET Core に関する概要 - .NET Core CLI
description: Windows、Linux、または macOS の .NET Core での、.NET Core コマンド ライン インターフェイス (CLI) の使用方法を段階的に説明するチュートリアル。
author: thraka
ms.author: adegeo
ms.date: 12/05/2019
ms.technology: dotnet-cli
ms.custom: seodec18,updateeachrelease
ms.openlocfilehash: 4c6a8e495d8532a0ab2e90368663a287731a9af0
ms.sourcegitcommit: 68a4b28242da50e1d25aab597c632767713a6f81
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74884263"
---
# <a name="get-started-with-net-core-on-windowslinuxmacos-using-the-command-line"></a>Windows/Linux/macOS の .NET Core でのコマンド ラインの使用に関する概要

この記事では、.NET Core CLI ツールを使用して、お使いのコンピューターでプラットフォームに依存しないアプリを開発する方法について説明します。

.NET Core CLI ツールセットに慣れていない場合は、[.NET Core SDK の概要](../tools/index.md) に関するページを参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- [.NET Core SDK 3.1](https://dotnet.microsoft.com/download) 以降のバージョン。
- ユーザーが選んだテキスト エディターまたはコード エディター。

## <a name="hello-console-app"></a>Hello コンソール アプリ

GitHub の dotnet/samples レポジトリから、[サンプル コードを表示またはダウンロード](https://github.com/dotnet/samples/tree/master/core/console-apps/HelloMsBuild)することができます。 ダウンロード方法については、「[サンプルおよびチュートリアル](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)」を参照してください。

コマンド プロンプトを開き、*Hello* という名前のフォルダーを作成します。 作成したフォルダーに移動して、次のように入力します。

```dotnetcli
dotnet new console
dotnet run
```

簡単に説明します。

01. `dotnet new console`

    [dotnet new](../tools/dotnet-new.md) で、コンソール アプリのビルドに必要な依存関係を含む最新の *Hello.csproj* プロジェクト ファイルが作成されます。 また、アプリケーションのエントリ ポイントを含む基本的なファイルである *Program.cs* も作成します。
    
    *Hello.csproj*:
    
    [!code-xml[Hello.csproj](~/samples/core/console-apps/HelloMsBuild/Hello.csproj)]
    
    プロジェクト ファイルでは、依存関係を復元し、プログラムをビルドするために必要なすべてのものを指定します。
    
    - `<OutputType>` 要素で、実行可能ファイル (つまり、コンソール アプリケーション) をビルドすることが示されます。
    - `<TargetFramework>` 要素で、ターゲットの .NET 実装が指定されます。 高度なシナリオでは、複数の対象フレームワークを指定し、1 回の操作でそれらすべてにビルドすることができます。 このチュートリアルでは、.NET Core 3.1 の場合のビルドについてのみ説明します。
    
    *Program.cs*:
    
    [!code-csharp[Program.cs](~/samples/core/console-apps/HelloMsBuild/Program.cs)]
    
    プログラムは `using System` で始まります。これは、"`System` 名前空間のすべてがこのファイルのスコープになる" こと意味します。 `System` 名前空間には、`Console` クラスが含まれています。
    
    次に、`Hello` という名前空間を定義します。 これを必要なものに変更できます。 その名前空間に、`Program` という名前のクラスが、`args` という名前の文字列配列を使用する `Main` メソッドと共に定義されます。 この配列には、プログラムの実行時に渡される引数のリストが含まれます。 このままではこの配列は使用されず、プログラムは単に "Hello World!" というテキストを 記述するだけです。 後に、この引数を利用するようにコードを変更します。
    
    `dotnet new` で、[dotnet restore](../tools/dotnet-restore.md) が暗黙的に呼び出されます。 `dotnet restore` は、[NuGet](https://www.nuget.org/) (.NET パッケージ マネージャー) を呼び出して依存関係ツリーを復元します。 NuGet は、*Hello.csproj* ファイルを分析し、ファイルに記載されている依存関係をダウンロードし (またはコンピューターのキャッシュから取得し)、サンプルをコンパイルして実行するために必要な *obj/project.assets.json* ファイルを記述します。

02. `dotnet run`

    [dotnet run](../tools/dotnet-run.md) で [dotnet build](../tools/dotnet-build.md) が呼び出され、ビルド ターゲットがビルドされていることを確認した後、`dotnet <assembly.dll>` が呼び出されてターゲット アプリケーションが実行されます。
    
    ```console
    dotnet run

    Hello World!
    ```
    
    または、`dotnet build` を実行して、ビルド コンソール アプリケーションを実行しないでコードをコンパイルすることもできます。 これにより、プロジェクトの名前に基づいて、コンパイル済みのアプリケーションが DLL ファイルとして生成されます。 この場合、作成されるファイルの名前は *Hello.dll* になります。 このアプリを、Windows 上で `dotnet bin\Debug\netcoreapp3.1\Hello.dll` を使用して実行できます (Windows 以外のシステムでは `/` を使用します)。
    
    ```console
    dotnet bin\Debug\netcoreapp3.1\Hello.dll

    Hello World!
    ```
    
    アプリがコンパイルされると、オペレーティング システム固有の実行可能ファイルが `Hello.dll` と共に作成されます。 Windows では、これは `Hello.exe` になります。Linux または macOS では、これは `hello` になります。 上記の例では、ファイルの名前は `Hello.exe` または `Hello` になります。 その実行可能ファイルを直接実行できます。

    ```console
    .\bin\Debug\netcoreapp3.1\Hello.exe

    Hello World!
    ```

## <a name="modify-the-program"></a>プログラムを変更する

プログラムを少し変更してみましょう。 フィボナッチ数列はおもしろいので、これを追加しましょう。また、引数を使用してアプリを実行している人にあいさつしましょう。

01. *Program.cs* ファイルの内容を次のコードで置き換えます。

    [!code-csharp[Fibonacci](~/samples/core/console-apps/fibonacci-msbuild/Program.cs)]

02. [dotnet build](../tools/dotnet-build.md) を実行して、変更をコンパイルします。

03. アプリにパラメーターを渡すプログラムを実行します。 `dotnet` コマンドを使用してアプリを実行する場合は、`--` を末尾に追加します。 `--` の右側にあるものは、パラメーターとしてアプリに渡されます。 次の例では、値 `John` がアプリに渡されます。

    ```console
    $ dotnet run -- John
    Hello John!
    Fibonacci Numbers 1-15:
    1: 0
    2: 1
    3: 1
    4: 2
    5: 3
    6: 5
    7: 8
    8: 13
    9: 21
    10: 34
    11: 55
    12: 89
    13: 144
    14: 233
    15: 377
    ```

以上です。 *Program.cs* を自由に拡張できます。

## <a name="working-with-multiple-files"></a>複数のファイルの操作

単純な 1 回だけのプログラムには 1 つのファイルで十分ですが、より複雑なアプリを構築する場合は、プロジェクトでおそらく複数のコード ファイルを使用するでしょう。 先のフィボナッチのサンプルから作成してみましょう。いくつかのフィボナッチ値をキャッシュしてから、再帰機能をいくつか追加します。

01. 次のコードを利用し、*FibonacciGenerator.cs* という名前の *Hello* ディレクトリ内に新しいファイルを追加します。

    [!code-csharp[Fibonacci Generator](~/samples/core/console-apps/FibonacciBetterMsBuild/FibonacciGenerator.cs)]

02. *Program.cs* ファイルの `Main` メソッドを変更し、次の例のように新しいクラスをインスタンス化し、そのメソッドを呼び出します。

    [!code-csharp[New Program.cs](~/samples/core/console-apps/FibonacciBetterMsBuild/Program.cs)]

03. [dotnet build](../tools/dotnet-build.md) を実行して、変更をコンパイルします。

04. [dotnet run](../tools/dotnet-run.md) を実行することで、アプリを実行します。 プログラムの出力は次のようになります。

    ```console
    $ dotnet run
    0
    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    89
    144
    233
    377
    ```

## <a name="publish-your-app"></a>アプリケーションの発行

アプリを配布する準備ができたら、[dotnet publish](../tools/dotnet-publish.md) コマンドを使用して、_bin\\debug\\netcoreapp3.1\\publish\\_ に _publish_ フォルダーを生成します (Windows 以外のシステムの場合は `/` を使用します)。 dotnet ランタイムが既にインストールされている他のプラットフォームには、_publish_ フォルダーの内容を配布できます。

```console
dotnet publish
Microsoft (R) Build Engine version 16.4.0+e901037fe for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 20 ms for C:\Code\Temp\Hello\Hello.csproj.
  Hello -> C:\Code\Temp\Hello\bin\Debug\netcoreapp3.1\Hello.dll
  Hello -> C:\Code\Temp\Hello\bin\Debug\netcoreapp3.1\publish\
```

上記の出力は、現在のフォルダーとオペレーティング システムによって異なっている場合がありますが、出力は似ています。

[dotnet](../tools/dotnet.md) コマンドを使って、発行されたアプリを実行できます。

```console
dotnet bin\Debug\netcoreapp3.1\publish\Hello.dll

Hello World!
```

この記事の冒頭で説明したように、オペレーティング システム固有の実行可能ファイルが `Hello.dll` と共に作成されています。 Windows では、これは `Hello.exe` になります。Linux または macOS では、これは `hello` になります。 上記の例では、ファイルの名前は `Hello.exe` または `Hello` になります。 この発行済みの実行可能ファイルを直接実行できます。

```console
.\bin\Debug\netcoreapp3.1\Hello.exe

Hello World!
```

## <a name="conclusion"></a>まとめ

以上です。 これで、ここで学習した基本的な概念を利用し、自分だけのプログラムを作成できます。

## <a name="see-also"></a>関連項目

- [.NET Core CLI ツールを使用したプロジェクトの整理およびテスト](testing-with-cli.md)
- [CLI を使用して .NET Core アプリを公開する](../deploying/deploy-with-cli.md)
- [アプリの展開についてさらに学習する](../deploying/index.md)
