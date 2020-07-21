---
title: Visual Studio Code を使用して .NET Core コンソール アプリケーションを作成する
description: Visual Studio Code と .NET Core CLI を使用して .NET Core コンソール アプリケーションを作成する方法について説明します。
ms.date: 05/22/2020
ms.openlocfilehash: 466a1353b574711a73570428569b58eab7ad8135
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84811695"
---
# <a name="tutorial-create-a-net-core-console-application-using-visual-studio-code"></a>チュートリアル: Visual Studio Code を使用して .NET Core コンソール アプリケーションを作成する

このチュートリアルでは、Visual Studio Code と .NET Core CLI を使用して .NET Core コンソール アプリケーションを作成して実行する方法について説明します。 プロジェクトの作成、コンパイル、実行などのプロジェクト タスクは、.NET Core CLI を使用して実行されます。 必要に応じて、別のコード エディターを使用してこのチュートリアルに従い、ターミナルでコマンドを実行することができます。

## <a name="prerequisites"></a>必須コンポーネント

1. [C# 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)がインストールされている [Visual Studio Code](https://code.visualstudio.com/)。 Visual Studio Code に拡張機能をインストールする方法については、[VS Code Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery) を参照してください。
2. [.Net Core 3.1 SDK 以降](https://dotnet.microsoft.com/download)

## <a name="create-the-app"></a>アプリを作成する

"HelloWorld" という名前の .NET Core コンソール アプリ プロジェクトを作成します。

1. Visual Studio Code を開始します。

1. メイン メニューから **[ファイル]**  >  **[フォルダーを開く]** (macOS では **[ファイル]**  >  **[開く...]** ) の順に選択します。

1. **[フォルダーを開く]** ダイアログで、*HelloWorld* フォルダーを作成し、 **[フォルダーの選択]** (macOS では **[開く]** ) をクリックします。

   フォルダー名は既定でプロジェクト名と名前空間名になります。 このチュートリアルでは後でコードを追加しますが、プロジェクト名前空間は `HelloWorld` にします。

1. メイン メニューで **[表示]**  >  **[ターミナル]** の順に選択して、Visual Studio Code で**ターミナル**を開きます。

   **ターミナル**が開き、*HelloWorld* フォルダーにコマンド プロンプトが表示されます。

1. **ターミナル**で、次のコマンドを入力します。

   ```dotnetcli
   dotnet new console
   ```

このテンプレートでは、シンプルな "Hello World" アプリケーションを作成します。 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> メソッドを呼び出し、"Hello World!" を コンソール ウィンドウに表示します。

テンプレート コードでは、引数として <xref:System.String> 配列を受け取る単一のメソッド `Main` を含む、`Program` というクラスが定義されます。

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

`Main` はアプリケーションのエントリ ポイントで、アプリケーションを起動するときに、ランタイムによって自動的に呼び出されるメソッドです。 アプリケーションが起動されるときに提供されるコマンドライン引数はすべて *args* 配列にあります。

## <a name="run-the-app"></a>アプリを実行する

**ターミナル**で次のコマンドを実行します。

```dotnetcli
dotnet run
```

プログラムによって "Hello World!" が表示されて 終了します。

![dotnet run コマンド](media/with-visual-studio-code/dotnet-run-command.png)

## <a name="enhance-the-app"></a>アプリを拡張する

アプリケーションを拡張し、ユーザーに名前の入力を求め、日付と時刻と共にそれを表示するようにします。

1. *Program.cs* をクリックして開きます。

   Visual Studio Code で初めて C# ファイルを開くと、[OmniSharp](https://www.omnisharp.net/) がエディターに読み込まれます。

   ![Program.cs ファイルを開く](media/with-visual-studio-code/open-program-cs.png)

1. Visual Studio Code で、アプリのビルドとデバッグに必要なアセットの追加を求められたら、 **[はい]** を選択します。

   ![足りない資産の入力を求める](media/with-visual-studio-code/missing-assets.png)

1. *Program.cs* の `Main` メソッドの内容 (`Console.WriteLine` を呼び出す行) を以下のコードに置き換えます。

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   このコードは、"What is your name?" と コンソール ウィンドウに表示して、ユーザーが文字列を入力して <kbd>Enter</kbd> キーを押すまで待機します。 これはこの文字列を `name` という変数に格納します。 さらに現在の現地時刻を含む <xref:System.DateTime.Now?displayProperty=nameWithType> プロパティの値を取得して、それを `date` という変数に代入します。 最後に、これらの値がコンソール ウィンドウに表示されます。

   `\n` は、改行文字を表します。

   文字列の前にドル記号 (`$`) を付けると、変数名などの式を文字列で中かっこで囲むことができます。 式の値が、式の代わりに文字列に挿入されます。 この構文は、[補間された文字列](../../csharp/language-reference/tokens/interpolated.md)と呼ばれます。

1. 変更内容を保存します。

   > [!IMPORTANT]
   > Visual Studio Code では、変更を明示的に保存する必要があります。 Visual Studio とは異なり、アプリをビルドして実行してもファイルの変更は自動的には保存されません。

1. もう一度プログラムを実行します。

   ```dotnetcli
   dotnet run
   ```

1. プロンプトに対し、名前を入力し、<kbd>Enter</kbd> キーを押します。

   :::image type="content" source="media/debugging-with-visual-studio-code/run-modified-program.png" alt-text="プログラムの出力が変更されたターミナル ウィンドウ":::

1. 任意のキーを押してプログラムを終了します。

## <a name="additional-resources"></a>その他の技術情報

- [Visual Studio Code の設定](https://code.visualstudio.com/docs/setup/setup-overview)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、.NET Core コンソール アプリケーションを作成しました。 次のチュートリアルでは、アプリをデバッグします。

> [!div class="nextstepaction"]
> [Visual Studio Code を使用して .NET Core コンソール アプリケーションをデバッグする](debugging-with-visual-studio-code.md)
