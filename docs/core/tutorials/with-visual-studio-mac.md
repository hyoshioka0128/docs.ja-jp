---
title: Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを作成する
description: Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを作成する方法について説明します。
ms.date: 06/02/2020
ms.openlocfilehash: 9cab838eaab2c59d8a0270267514f57acb7c60fb
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84811669"
---
# <a name="tutorial-create-a-net-core-console-application-using-visual-studio-for-mac"></a>チュートリアル: Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを作成する

このチュートリアルでは、Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを作成および実行する方法について説明します。

> [!NOTE]
> お客様のフィードバックは非常に貴重です。 次の 2 つの方法で Visual Studio for Mac の開発チームにフィードバックを送信できます。
>
> * Visual Studio for Mac で、メニューから **[ヘルプ]**  >  **[問題の報告]** の順に選択するか、ようこそ画面から **[問題の報告]** を選択して、バグ報告を提出するためのウィンドウを開きます。 お客様のフィードバックは、[開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/8/index.html) ポータルで追跡することができます。
> * 提案するには、メニューから **[ヘルプ]**  >  **[提案の送信]** の順に選択するか、ようこそ画面から **[提案の送信]** を選択し、[Visual Studio for Mac の開発者コミュニティの Web ページ](https://developercommunity.visualstudio.com/content/idea/post.html?space=41)に移動します。

## <a name="prerequisites"></a>必須コンポーネント

* [Visual Studio for Mac バージョン 8.6 以降](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。 .NET Core をインストールするオプションを選択します。 .NET Core 開発の場合、Xamarin のインストールは省略可能です。 詳細については、次のリソースを参照してください。

  * [チュートリアル: Visual Studio for Mac をインストールする](/visualstudio/mac/installation)。
  * [サポート対象の macOS のバージョン](../install/dependencies.md?pivots=os-macos)。
  * [Visual Studio for Mac でサポートされている .NET Core のバージョン](/visualstudio/mac/net-core-support)。

## <a name="create-the-app"></a>アプリを作成する

"HelloWorld" という名前の .NET Core コンソール アプリ プロジェクトを作成します。

1. Visual Studio for Mac を起動します。

1. スタート ウィンドウで **[新規]** を選択します。

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="Visual Studio for Mac のスタート ウィンドウの [新規] ボタン":::

1. **[新しいプロジェクト]** ダイアログで、 **[Web and Console]\(Web とコンソール\)** ノードの下にある **[アプリ]** を選択します。 **[コンソール アプリケーション]** テンプレートを選択し、 **[次へ]** を選択します。

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-dialog.png" alt-text="新しいプロジェクト テンプレートの一覧":::

1. **[Configure your new Console Application]\(新しいコンソール アプリケーションの構成\)** ダイアログの **[ターゲット フレームワーク]** ドロップダウンで、 **[.NET Core 3.1]** を選択し、 **[次へ]** を選択します。

   :::image type="content" source="media/with-visual-studio-mac/target-framework.png" alt-text="ターゲット フレームワークの選択":::

1. **[プロジェクト名]** に「HelloWorld」と入力し、 **[作成]** を選択します。

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-options.png" alt-text="[Configure your new Console Application]\(新しいコンソール アプリケーションの構成\) ダイアログ":::

このテンプレートでは、シンプルな "Hello World" アプリケーションを作成します。 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> メソッドを呼び出し、"Hello World!" を ターミナル ウィンドウに表示します。

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

`Main` はアプリケーションのエントリ ポイントで、アプリケーションを起動するときに、ランタイムによって自動的に呼び出されるメソッドです。 アプリケーションの起動時に指定されるコマンドライン引数は、`args` 配列から利用できます。

## <a name="run-the-app"></a>アプリを実行する

1. <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd> + <kbd>command</kbd> + <kbd>enter</kbd>) キーを押して、デバッグなしでアプリを実行します。

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-output.png" alt-text="ターミナルに Hello World! が表示される":::

1. **ターミナル** ウィンドウを閉じます。

## <a name="enhance-the-app"></a>アプリを拡張する

アプリケーションを拡張し、ユーザーに名前の入力を求め、日付と時刻と共にそれを表示するようにします。

1. *Program.cs* で、`Main` メソッドの内容 (`Console.WriteLine` を呼び出す行) を以下のコードに置き換えます。

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   このコードは、"What is your name?" と コンソール ウィンドウに表示して、ユーザーが文字列を入力して <kbd>enter</kbd> キーを押すまで待機します。 これはこの文字列を `name` という変数に格納します。 さらに現在の現地時刻を含む <xref:System.DateTime.Now?displayProperty=nameWithType> プロパティの値を取得して、それを `date` という変数に代入します。 最後に、これらの値がコンソール ウィンドウに表示されます。

   `\n` は、改行文字を表します。

   文字列の前にドル記号 (`$`) を付けると、変数名などの式を文字列で中かっこで囲むことができます。 式の値が、式の代わりに文字列に挿入されます。 この構文は、[補間された文字列](../../csharp/language-reference/tokens/interpolated.md)と呼ばれます。

1. <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd> + <kbd>command</kbd> + <kbd>enter</kbd>) キーを押して、アプリを実行します。

1. 名前を入力して <kbd>enter</kbd> キーを押すことで、このプロンプトに応答します。

   :::image type="content" source="media/with-visual-studio-mac/hello-world-update.png" alt-text="変更されたプログラムの出力を示すターミナル":::

1. ターミナルを閉じます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、.NET Core コンソール アプリケーションを作成しました。 次のチュートリアルでは、アプリをデバッグします。

> [!div class="nextstepaction"]
> [Visual Studio で .NET Core コンソール アプリケーションをデバッグする](debugging-with-visual-studio-mac.md)
