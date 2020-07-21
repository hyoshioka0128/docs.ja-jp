---
title: Visual Studio を使用して .NET Core コンソール アプリケーションをデバッグする
description: Visual Studio を使用して .NET Core コンソール アプリをデバッグする方法について説明します。
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: 743603cb037406948190c7090ca3527bfc40db18
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702068"
---
# <a name="tutorial-debug-a-net-core-console-application-using-visual-studio"></a>チュートリアル: Visual Studio を使用して .NET Core コンソール アプリケーションをデバッグする

このチュートリアルでは、Visual Studio で使用できるデバッグ ツールについて説明します。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio 2019 での .NET Core コンソール アプリケーションの作成](with-visual-studio.md)に関するページで作成した、コンソール アプリを使用します。

## <a name="use-debug-build-configuration"></a>デバッグ ビルド構成の使用

"*デバッグ*" と "*リリース*" は、Visual Studio の組み込みビルド構成です。 デバッグ用のデバッグ ビルド構成と、最終リリース配布用のリリース構成を使用します。

デバッグ構成では、プログラムのコンパイルにシンボリック デバッグ情報が完全に含まれ、最適化は行われません。 ソース コードと生成された命令の関係は非常に複雑であり、最適化を行うとデバッグが困難になるためです。 プログラムのリリース構成は、シンボリック デバッグ情報を含まず、完全に最適化されます。

 既定では、Visual Studio Code ではデバッグ ビルド構成が使用されるため、デバッグの前に変更する必要はありません。

1. Visual Studio を起動します。

1. [Visual Studio 2019 での .NET Core コンソール アプリケーションの作成](with-visual-studio.md)に関する記事で作成したプロジェクトを開きます。

   現時点のビルド構成はツールバーに表示されています。 次のツール バーの画像では、アプリのデバッグ バージョンをコンパイルするように Visual Studio が構成されています。

   ![デバッグが強調表示された Visual Studio のツールバー](./media/debugging-with-visual-studio/visual-studio-toolbar-debug.png)

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

"*ブレークポイント*" によって、ブレークポイントを含む行が実行される前に、アプリケーションの実行が一時的に中断されます。

1. 名前、日付、時刻を表示する行のコード ウィンドウの左側の余白をクリックして、その行に "*ブレークポイント*" 設定します。 左余白は、行番号の左側にあります。  ブレークポイントを設定するもう 1 つの方法は、コード行にカーソルを置き、メニュー バーから **[デバッグ]**  >  **[ブレークポイントの設定/解除]** を選択することです。

   次の図のとおり、Visual Studio では、ブレークポイントが設定された行を強調表示し、左端の余白に赤い点を表示することで、その行を示しています。

   ![ブレークポイントが設定された Visual Studio のプログラム ウィンドウ](./media/debugging-with-visual-studio/set-breakpoint-in-editor.png)

1. <kbd>F5</kbd> キーを押して、プログラムをデバッグ モードで実行します。 デバッグを開始するもう 1 つの方法は、メニューから **[デバッグ]**  >  **[デバッグの開始]** を選択することです。

1. プログラムが名前の入力を求めたら、コンソール ウィンドウに文字列を入力して、<kbd>Enter</kbd> キーを押します。

1. プログラムがブレークポイントに到達すると、プログラム実行は停止します。`Console.WriteLine` メソッドが実行される前にも停止します。 **[ローカル]** ウィンドウには、現在実行しているメソッドで定義されている変数の値が表示されます。

   ![Visual Studio でのブレークポイントのスクリーンショット](./media/debugging-with-visual-studio/breakpoint-hit.png)

## <a name="use-the-immediate-window"></a>[イミディエイト] ウィンドウを使用する

**[イミディエイト]** ウィンドウでは、デバッグ中のアプリケーションと対話できます。 変数の値を対話的に変更して、プログラムにどのような影響があるかを確認できます。

1. **[イミディエイト]** ウィンドウが表示されない場合は、 **[デバッグ]**  >  **[Windows]**  >  **[イミディエイト]** の順に選択して表示します。

1. **[イミディエイト]** ウィンドウに「`name = "Gracie"`」と入力して、<kbd>Enter</kbd> キーを押します。

1. **[イミディエイト]** ウィンドウに「`date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()`」と入力して、<kbd>Enter</kbd> キーを押します。

   **[イミディエイト]** ウィンドウに、文字列変数の値と、<xref:System.DateTime> 値のプロパティが表示されます。 さらに、変数の値は **[ローカル]** ウィンドウで更新されます。

   ![Visual Studio 2019 の [ローカル] と [イミディエイト] ウィンドウ](./media/debugging-with-visual-studio/locals-immediate-window.png)

1. <kbd>F5</kbd> キーを押して、プログラムの実行を続行します。 続行するもう 1 つの方法は、メニューから **[デバッグ]**  >  **[続行]** を選択することです。

   コンソール ウィンドウに表示される値は、 **[イミディエイト]** ウィンドウで行った変更に対応しています。

   ![入力した値が表示されているコンソール ウィンドウ](./media/debugging-with-visual-studio/console-window.png)

1. 任意のキーを押してアプリケーションを終了し、デバッグを停止します。

## <a name="set-a-conditional-breakpoint"></a>条件付きブレークポイントの設定

プログラムによって、ユーザーが入力した文字列が表示されます。 ユーザーが何も入力しないとどうなるでしょうか。 これは、"*条件付きブレークポイント*" と呼ばれる便利なデバッグ機能を使用してテストできます。

1. ブレークポイントを表す赤丸を右クリックします。 コンテキスト メニューで **[条件]** を選んで、 **[ブレークポイント設定]** ダイアログを開きます。 **[条件]** のチェック ボックスをオンにします (まだオンになっていない場合)。

   ![[ブレークポイント設定] パネルが表示されているエディター - C#](./media/debugging-with-visual-studio/breakpoint-settings.png)

1. **[条件式]** には、`x` が 5 かどうかをテストするコード例を示す次のコードをフィールドに入力します。 使用する言語が表示されていない場合は、ページの上部にある言語セレクターを変更します。

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   ```vb
   String.IsNullOrEmpty(name)
   ```

   ブレークポイントにヒットするたびに、デバッガーは `String.IsNullOrEmpty(name)` メソッドを呼び出し、メソッド呼び出しが `true` を返す場合にのみ、この行で中断します。

   条件式の代わりに、"*ヒット カウント*" を指定できます。この場合、ステートメントが指定された回数実行される前にプログラムの実行が中断されます。 もう 1 つのオプションは、"*フィルター条件*" を指定することです。これにより、スレッド識別子、プロセス名、またはスレッド名などの属性に基づいてプログラムの実行が中断されます。

1. **[閉じる]** を選択して、ダイアログを閉じます。

1. <kbd>F5</kbd> を押して、デバッグとともにプログラムを開始します。

1. コンソール ウィンドウで、名前の入力を求められたら、<kbd>Enter</kbd> キーを押します。

1. 指定した条件 (`name` は `null` または <xref:System.String.Empty?displayProperty=nameWithType> のどちらか) が満たされたため、ブレークポイントに到達すると、`Console.WriteLine` メソッドが実行される前に、プログラムの実行が停止します。

1. **[ローカル]** ウィンドウを選ぶと、現在実行しているメソッドに対してローカルな変数の値が表示されます。 この場合、`Main` は現在実行中のメソッドです。 `name` 変数の値が `""` または <xref:System.String.Empty?displayProperty=nameWithType> であることを調べます。

1. **[イミディエイト]** ウィンドウに次のステートメントを入力し、<kbd>Enter</kbd> キーを押して、値が空の文字列であることを確認します。 結果は `true` になります。

   ```csharp
   ? name == String.Empty
   ```

   ```vb
   ? String.IsNullOrEmpty(name)
   ```

   疑問符は、イミディエイト ウィンドウに、[式を評価](/visualstudio/ide/reference/immediate-window#enter-commands)するように指示します。

   ![ステートメントが実行された後で値 true を返す [イミディエイト ウィンドウ] - C#](./media/debugging-with-visual-studio/immediate-window-output.png)

1. <kbd>F5</kbd> キーを押して、プログラムの実行を続行します。

1. 任意のキーを押してコンソール ウィンドウを閉じ、デバッグを停止します。

1. コード ウィンドウの左端の余白のドットをクリックして、ブレークポイントをクリアします。 ブレークポイントをクリアするもう 1 つの方法は、コード行が選択されている間に **[デバッグ] > [ブレークポイントの設定/解除]** を選択することです。

## <a name="step-through-a-program"></a>プログラムのステップ実行

Visual Studio では、1 行ずつプログラムをステップ実行して、実行を監視することもできます。 通常は、ブレークポイントを設定して、プログラム コードのごく一部を通じてプログラム フローに従います。 このプログラムは小さいため、次の手順に従ってプログラム全体をステップ実行できます。

1. **[デバッグ]**  >  **[ステップ イン]** の順に選択します。 1 つのステートメントを一度にデバッグするもう 1 つの方法は、<kbd>F11</kbd> キーを押すことです。

   次に実行される行が強調表示されて、横に矢印が表示されます。

   C#

   ![Visual Studio のステップ イン メソッド - C#](./media/debugging-with-visual-studio/step-into-method.png)

   Visual Basic

   ![Visual Studio のステップ イン メソッド - Visual Basic](./media/debugging-with-visual-studio/vb-step-into-method.png)

   この時点で、 **[ローカル]** ウィンドウに `args` 配列が空であることが示され、`name` と `date` には既定値が設定されています。 さらに、空のコンソール ウィンドウが開かれています。

1. <kbd>F11</kbd> キーを押します。 次に実行される行が強調表示されます。 **[ローカル]** ウィンドウは変更されず、コンソール ウィンドウは空白のままになります。

   C#

   ![Visual Studio のステップ イン メソッド ソース - C#](./media/debugging-with-visual-studio/step-into-source-method.png)

   Visual Basic

   ![Visual Studio のステップ イン メソッド ソース - Visual Basic](./media/debugging-with-visual-studio/vb-step-into-source-method.png)

1. <kbd>F11</kbd> キーを押します。 `name` の変数代入を含むステートメントが強調表示されます。 **[ローカル]** ウィンドウに `name` が `null` であると表示され、コンソール ウィンドウに "What is your name?" という文字列が表示されます。

1. コンソール ウィンドウに文字列を入力し、<kbd>Enter</kbd> キーを押して、このプロンプトに応答します。 コンソールは応答せず、入力した文字列はコンソール ウィンドウに表示されませんが、それでも <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> メソッドにより入力が取り込まれます。

1. <kbd>F11</kbd> キーを押します。 Visual Studio によって、`date` 変数代入 (Visual Basic では `currentDate`) を含むステートメントが強調表示されます。 **[ローカル]** ウィンドウには、<xref:System.Console.ReadLine%2A?displayProperty=nameWithType> メソッドの呼び出しによって返された値が表示されます。 コンソール ウィンドウには、プロンプトで入力した文字列も表示されます。

1. <kbd>F11</kbd> キーを押します。 **[ローカル]** ウィンドウには、<xref:System.DateTime.Now?displayProperty=nameWithType> プロパティから代入された後の `date` 変数の値が表示されます。 コンソール ウィンドウに変更はありません。

1. <kbd>F11</kbd> キーを押します。 Visual Studio は、<xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> メソッドを呼び出します。 コンソール ウィンドウには書式設定された文字列が表示されます。

1. **[デバッグ]**  >  **[ステップ アウト]** の順に選択します。ステップ バイ ステップの実行を停止するもう 1 つの方法は、<kbd>Shift</kbd>+<kbd>F11</kbd> キーを押すことです。

   コンソール ウィンドウにメッセージが表示され、任意のキーを押すよう求められます。

1. 任意のキーを押してコンソール ウィンドウを閉じ、デバッグを停止します。

## <a name="use-release-build-configuration"></a>リリース ビルド構成を使用する

アプリケーションのデバッグ バージョンのテストが終了したら、リリース バージョンもコンパイルしてテストする必要があります。 リリース バージョンには、アプリケーションの動作に悪影響を与える可能性があるコンパイラの最適化が組み込まれています。 たとえば、パフォーマンスを向上させるように設計されたコンパイラの最適化では、マルチスレッド アプリケーションで競合状態が生じる場合があります。

コンソール アプリケーションのリリース バージョンをビルドしてテストするには、ツール バーのビルド構成を **[デバッグ]** から **[リリース]** に変更します。

![デバッグが強調表示された Visual Studio の既定のツールバー](./media/debugging-with-visual-studio/visual-studio-toolbar-release.png)

<kbd>F5</kbd> キーを押すか、 **[ビルド]** メニューの **[ソリューションのビルド]** を選ぶと、アプリケーションのリリース バージョンが Visual Studio でコンパイルされます。 それをデバッグ バージョンと同様にテストできます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio のデバッグ ツールを使用しました。 次のチュートリアルでは、アプリの展開可能なバージョンを発行します。

> [!div class="nextstepaction"]
> [Visual Studio での .NET Core コンソール アプリケーションの発行](publishing-with-visual-studio.md)
