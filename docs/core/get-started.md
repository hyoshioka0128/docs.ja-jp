---
title: .NET Core の概要
description: Windows、Linux、macOS で .NET Core アプリケーションをビルドする方法を学習するためのリソースを示します。
author: thraka
ms.author: adegeo
ms.date: 09/19/2019
ms.openlocfilehash: 78066f2904f6a874b71165e4fe1769b6b778ae41
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74428868"
---
# <a name="get-started-with-net-core"></a>.NET Core の概要

この記事では、.NET Core の概要について説明します。 .NET Core は、Windows、Linux、および macOS にインストールすることができます。 任意のテキスト エディターでコーディングし、クロスプラットフォーム ライブラリとアプリケーションを作成できます。 

.NET Core が何であるかや、他の .NET テクノロジとどのように関連しているのかがわからない場合は、まず、[.NET の概要](https://dotnet.microsoft.com/learn/dotnet/what-is-dotnet)を確認してください。 簡単に言うと、.NET Core は .NET のオープンソースのクロスプラットフォーム実装です。

## <a name="create-an-application"></a>アプリケーションの作成

まず、ご利用のコンピューターで [NET Core SDK](https://dotnet.microsoft.com/download) をダウンロードしてインストールします。

次に、**PowerShell**、**コマンド プロンプト**、**bash** などのターミナルを開きます。 次の `dotnet` コマンドを入力し、C# アプリケーションを作成して実行します。

```dotnetcli
dotnet new console --output sample1
dotnet run --project sample1
```

次の出力が表示されます。

```console
Hello World!
```

おめでとうございます! シンプルな .NET Core アプリケーションが作成されました。 [Visual Studio Code](tutorials/with-visual-studio-code.md)、[Visual Studio](tutorials/with-visual-studio.md) (Windows のみ)、または [Visual Studio for Mac](tutorials/using-on-mac-vs.md) (macOS のみ) を使用して、.NET Core アプリケーションを作成することもできます。

## <a name="tutorials"></a>チュートリアル

次のステップ バイ ステップのチュートリアルに従って、.NET Core アプリケーションの開発を開始できます。

<!-- markdownlint-disable MD025 -->

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

- [Visual Studio 2017 での .NET Core を使用した C# Hello World アプリケーションの構築。](./tutorials/with-visual-studio.md)
- [Visual Studio 2017 の C# および .NET Core を使用したクラス ライブラリの構築。](./tutorials/library-with-visual-studio.md)
- [Visual Studio 2017 での .NET Core を使用した Visual Basic Hello World アプリケーションの構築。](./tutorials/vb-with-visual-studio.md)
- [Visual Studio 2017 で Visual Basic と .NET Core を使用したクラス ライブラリの構築。](./tutorials/vb-library-with-visual-studio.md)  
- [Visual Studio Code と .NET Core をインストールして使用する方法](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core/)に関するビデオを見る。
- [Visual Studio 2017 と .NET Core をインストールして使用する方法](https://channel9.msdn.com/Blogs/dotnet/Get-Started-NET-Core-Visual-Studio-2017/)に関するビデオを見る。
- [.NET Core でのコマンド ラインの使用に関する概要。](tutorials/using-with-xplat-cli.md)

サポートされている Windows バージョンの一覧については、[.NET Core の依存関係と要件](install/dependencies.md?tabs=netcore30&pivots=os-windows)に関する記事を参加してください。

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

次のステップ バイ ステップのチュートリアルに従って、.NET Core アプリケーションの開発を開始できます。

- [.NET Core でのコマンド ラインの使用に関する概要。](tutorials/using-with-xplat-cli.md)
- [Ubuntu 上の Visual Studio Code での C# と .NET Core の使用に関する概要](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu)のビデオを見る。

サポートされている Linux のディストリビューションとバージョンの一覧については、[.NET Core の依存関係と要件](install/dependencies.md?tabs=netcore30&pivots=os-linux)に関する記事を参加してください。

# <a name="macostabmacos"></a>[macOS](#tab/macos)

次のステップ バイ ステップのチュートリアルに従って、.NET Core アプリケーションの開発を開始できます。

- [macOS 上の Visual Studio Code での C# と .NET Core の使用に関する概要](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-NET-Core-Mac)のビデオを見る。
- [macOS 上の .NET Core での Visual Studio Code の使用に関する概要。](tutorials/using-on-macos.md)
- [.NET Core でのコマンド ラインの使用に関する概要。](tutorials/using-with-xplat-cli.md)
- [Visual Studio for Mac を使用した macOS での .NET Core の概要。](tutorials/using-on-mac-vs.md)
- [Visual Studio for Mac を使用した macOS での完全な .NET Core ソリューションの構築。](tutorials/using-on-mac-vs-full-solution.md)

サポートされている OS X / macOS バージョンの一覧については、[.NET Core の依存関係と要件](install/dependencies.md?tabs=netcore30&pivots=os-macos)に関する記事を参加してください。

---
