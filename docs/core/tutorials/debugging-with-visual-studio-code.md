---
title: Visual Studio Code を使用して .NET Core コンソール アプリケーションをデバッグする
description: Visual Studio Code を使用して .NET Core コンソール アプリをデバッグする方法について説明します。
ms.date: 05/26/2020
ms.openlocfilehash: 40e9b114df1bd12fb05bfb773781d6009d087a06
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702128"
---
# <a name="tutorial-debug-a-net-core-console-application-using-visual-studio-code"></a>チュートリアル: Visual Studio Code を使用して .NET Core コンソール アプリケーションをデバッグする

このチュートリアルでは、.NET Core アプリを操作するために Visual Studio Code で使用できるデバッグ ツールについて説明します。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio Code での .NET Core コンソール アプリケーションの作成](with-visual-studio-code.md)に関するページで作成した、コンソール アプリを使用します。

## <a name="use-debug-build-configuration"></a>デバッグ ビルド構成の使用

"*デバッグ*" と "*リリース*" は、.NET Core の組み込みビルド構成です。 デバッグ用のデバッグ ビルド構成と、最終リリース配布用のリリース構成を使用します。

デバッグ構成では、プログラムのコンパイルにシンボリック デバッグ情報が完全に含まれ、最適化は行われません。 ソース コードと生成された命令の関係は非常に複雑であり、最適化を行うとデバッグが困難になるためです。 プログラムのリリース構成は、シンボリック デバッグ情報を含まず、完全に最適化されます。

既定では、Visual Studio Code の起動設定ではデバッグ ビルド構成が使用されるため、デバッグの前に変更を加える必要はありません。

1. Visual Studio Code を開始します。

1. [Visual Studio Code での .NET Core コンソール アプリケーションの作成](with-visual-studio-code.md)に関する記事で作成したプロジェクトのフォルダーを開きます。

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

"*ブレークポイント*" によって、ブレークポイントを含む行が実行される前に、アプリケーションの実行が一時的に中断されます。

1. *Program.cs* ファイルを開きます。

1. コード ウィンドウの左側の余白をクリックして、名前、日付、時刻を表示する行に "*ブレークポイント*" を設定します。 左余白は、行番号の左側にあります。 ブレークポイントを設定するその他の方法としては、コード行を選択した状態で <kbd>F9</kbd> キーを押すか、メニューから **[実行]**  >  **[ブレークポイントの設定/解除]** を選択します。

   Visual Studio Code では、左余白に赤い点を表示することで、ブレークポイントが設定されている行が示されます。

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-set.png" alt-text="ブレークポイントの設定":::

## <a name="set-up-for-terminal-input"></a>ターミナル入力用の設定

ブレークポイントは、`Console.ReadLine` メソッドの呼び出しの後に配置されます。 **デバッグ コンソール** は、実行中のプログラムのターミナル入力を受け入れません。 デバッグ中にターミナル入力を処理するには、統合ターミナル (Visual Studio Code ウィンドウの 1 つ) または外部ターミナルを使用できます。 このチュートリアルでは、統合ターミナルを使用します。

1. *.vscode/launch.json* を開きます。

1. `console` 設定を `integratedTerminal` に変更します。

   差出人:

   ```
   "console": "internalConsole",
   ```

   移動先:

   ```
   "console": "integratedTerminal",
   ```

1. 変更内容を保存します。

## <a name="start-debugging"></a>[デバッグ開始]

1. 左側のメニューにある [デバッグ] アイコンを選択して、デバッグ ビューを開きます。

   :::image type="content" source="media/debugging-with-visual-studio-code/select-debug-pane.png" alt-text="Visual Studio Code で [デバッグ] タブを開く":::

1. ペインの上部にある **[.NET Core Launch (console)]\(.NET Core の起動 (コンソール)\)** の横の緑色の矢印を選択します。 デバッグ モードでプログラムを起動するもう 1 つの方法は、メニューから **[実行]**  >  **[デバッグの開始]** を選択することです。

   :::image type="content" source="media/debugging-with-visual-studio-code/start-debugging.png" alt-text="デバッグの開始":::

1. **[ターミナル]** タブを選択すると、"What is your name?" (あなたのお名前は?) の プロンプトが表示されます。これは応答を待機する前にプログラムによって表示されます。

   :::image type="content" source="media/debugging-with-visual-studio-code/select-terminal.png" alt-text="[ターミナル] タブを選択":::

1. 名前のプロンプトに応答する文字列を **[ターミナル]** ウィンドウに入力し、<kbd>Enter</kbd> キーを押します。

   プログラムがブレークポイントに到達すると、プログラム実行は停止します。`Console.WriteLine` メソッドが実行される前にも停止します。 **[変数]** ウィンドウの **[ローカル]** セクションには、現在実行しているメソッドで定義されている変数の値が表示されます。

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-hit.png" alt-text="ブレークポイントのヒット、ローカルの表示":::

## <a name="use-the-debug-console"></a>デバッグ コンソールを使用する

**[デバッグ コンソール]** ウィンドウでは、デバッグ中のアプリケーションと対話できます。 変数の値を変更して、プログラムにどのような影響があるかを確認できます。

1. **[デバッグ コンソール]** タブを選択します。

1. **[デバッグ コンソール]** ウィンドウの下部にあるプロンプトで `name = "Gracie"` を入力し、<kbd>Enter</kbd> キーを押します。

   :::image type="content" source="media/debugging-with-visual-studio-code/change-variable-values.png" alt-text="変数の値の変更":::

1. **[デバッグ コンソール]** ウィンドウの下部に `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` を入力し、<kbd>Enter</kbd> キーを押します。

   **[変数]** ウィンドウには、`name` 変数と `date` 変数の新しい値が表示されます。

1. ツール バーの **[続行]** ボタンを選択して、プログラムの実行を続けます。 続行するもう 1 つの方法は、<kbd>F5</kbd> キーを押すことです。

   :::image type="content" source="media/debugging-with-visual-studio-code/continue-debugging.png" alt-text="デバッグの続行":::

1. もう一度 **[ターミナル]** タブを選択します。

   コンソール ウィンドウに表示される値は、 **[デバッグ コンソール]** で行った変更に対応しています。

   :::image type="content" source="media/debugging-with-visual-studio-code/changed-variable-values.png" alt-text="入力した値を示すターミナル":::

1. 任意のキーを押してアプリケーションを終了し、デバッグを停止します。

## <a name="set-a-conditional-breakpoint"></a>条件付きブレークポイントの設定

プログラムによって、ユーザーが入力した文字列が表示されます。 ユーザーが何も入力しないとどうなるでしょうか。 これは、"*条件付きブレークポイント*" と呼ばれる便利なデバッグ機能を使用してテストできます。

1. ブレークポイントを表す赤い点を右クリック (macOS では <kbd>Ctrl</kbd> キーを押しながらクリック) します。 コンテキスト メニューで **[ブレークポイントの編集]** を選択して、条件式を入力するためのダイアログボックスを開きます。

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-context-menu.png" alt-text="ブレークポイント コンテキスト メニュー":::

1. ドロップダウン リストで [`Expression`] を選択し、次の条件式を入力して、<kbd>Enter</kbd> キーを押します。

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/conditional-expression.png" alt-text="条件式の入力":::

   ブレークポイントにヒットするたびに、デバッガーは `String.IsNullOrEmpty(name)` メソッドを呼び出し、メソッド呼び出しが `true` を返す場合にのみ、この行で中断します。

   条件式の代わりに、"*ヒット カウント*" を指定できます。この場合、ステートメントが指定された回数実行される前にプログラムの実行が中断されます。 もう 1 つのオプションは、"*フィルター条件*" を指定することです。これにより、スレッド識別子、プロセス名、またはスレッド名などの属性に基づいてプログラムの実行が中断されます。

1. <kbd>F5</kbd> を押して、デバッグとともにプログラムを開始します。

1. **[ターミナル]** タブで、自分の名前を入力するように求められたら、<kbd>Enter</kbd> キーを押します。

   指定した条件 (`name` が `null` または <xref:System.String.Empty?displayProperty=nameWithType>) が満たされたため、ブレークポイントに到達すると、`Console.WriteLine` メソッドが実行される前に、プログラムの実行が停止します。

   **[変数]** ウィンドウには、`name` 変数の値が `""` または <xref:System.String.Empty?displayProperty=nameWithType> であることが表示されます。

1. **デバッグ コンソール** プロンプトで次のステートメントを入力し、<kbd>Enter</kbd> キーを押して、値が空の文字列であることを確認します。 結果は `true` になります。

   ```csharp
   name == String.Empty
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/expression-in-debug-console.png" alt-text="ステートメントの実行後に true の値を返すデバッグ コンソール":::

1. ツール バーの **[続行]** を選んで、プログラムの実行を続けます。

1. **[ターミナル]** タブを選択し、任意のキーを押してプログラムを終了し、デバッグを停止します。

1. コード ウィンドウの左余白のドットをクリックして、ブレークポイントをクリアします。 ブレークポイントをクリアするその他の方法としては、コード行を選択した状態で <kbd>F9</kbd> キーを押すか、メニューから **[実行] > [ブレークポイントの設定/解除]** を選択します。

1. ブレークポイントの条件が失われることを示す警告が表示された場合は、 **[ブレークポイントの削除]** を選択します。

## <a name="step-through-a-program"></a>プログラムのステップ実行

Visual Studio Code では、1 行ずつプログラムをステップ実行して、実行を監視することもできます。 通常は、ブレークポイントを設定して、プログラム コードのごく一部を通じてプログラム フローに従います。 このプログラムは小さいため、次の手順に従ってプログラム全体をステップ実行できます。

1. `Main` メソッドの左中かっこにブレークポイントを設定します。

1. <kbd>F5</kbd> キーを押してデバッグを開始します。

   Visual Studio Code では、ブレークポイント行が強調表示されます。

   この時点で、 **[変数]** ウィンドウに `args` 配列が空であることが示され、`name` と `date` には既定値が設定されています。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   :::image type="content" source="media/debugging-with-visual-studio-code/step-into.png" alt-text="[ステップイン] ボタン":::

   Visual Studio Code では次の行が強調表示されます。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   Visual Studio Code では、名前プロンプトの `Console.WriteLine` が実行され、次に実行される行が強調表示されます。 次の行は、`name` の `Console.ReadLine` です。 **[変数]** ウィンドウは変更されず、 **[ターミナル]** タブに "What is your name?" プロンプトが表示されます。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   Visual Studio によって、`name` 変数代入が強調表示されます。 **[変数]** ウィンドウに、`name` がまだ `null` であることが示されます。

1. [ターミナル] タブに文字列を入力し、<kbd>Enter</kbd> キーを押して、このプロンプトに応答します。

   **[ターミナル]** タブには、入力時に入力した文字列が表示されない場合がありますが、<xref:System.Console.ReadLine%2A?displayProperty=nameWithType> メソッドによって入力がキャプチャされます。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   Visual Studio Code によって、`date` 変数代入が強調表示されます。 **[変数]** ウィンドウには、<xref:System.Console.ReadLine%2A?displayProperty=nameWithType> メソッドの呼び出しによって返された値が表示されます。 **[ターミナル]** タブには、プロンプトで入力した文字列が表示されます。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   **[変数]** ウィンドウには、<xref:System.DateTime.Now?displayProperty=nameWithType> プロパティから代入された後の `date` 変数の値が表示されます。

1. **[実行]**  >  **[ステップ イン]** を選択するか、<kbd>F11</kbd> キーを押します。

   Visual Studio Code によって <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> メソッドが呼び出されます。 コンソール ウィンドウには書式設定された文字列が表示されます。

1. **[実行]**  >  **[ステップ アウト]** の順に選択するか、<kbd>Shift</kbd> + <kbd>F11</kbd> キーを押します。

   :::image type="content" source="media/debugging-with-visual-studio-code/step-out.png" alt-text="[ステップアウト] ボタン":::

1. **[ターミナル]** タブを選択します。

   ターミナルに、"Press any key to exit..." (終了するには何かキーを押してください...) が表示されます。

1. 任意のキーを押してプログラムを終了します。

## <a name="use-release-build-configuration"></a>リリース ビルド構成を使用する

アプリケーションのデバッグ バージョンのテストが終了したら、リリース バージョンもコンパイルしてテストする必要があります。 リリース バージョンには、アプリケーションの動作に影響を与える可能性があるコンパイラの最適化が組み込まれています。 たとえば、パフォーマンスを向上させるように設計されたコンパイラの最適化では、マルチスレッド アプリケーションで競合状態が生じる場合があります。

コンソール アプリケーションのリリース バージョンをビルドしてテストするには、**ターミナル**を開き、次のコマンドを実行します。

```dotnetcli
dotnet run --configuration Release
```

## <a name="additional-resources"></a>その他の技術情報

* [Visual Studio Code でのデバッグ](https://code.visualstudio.com/docs/editor/debugging)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio Code のデバッグ ツールを使用しました。 次のチュートリアルでは、アプリの展開可能なバージョンを発行します。

> [!div class="nextstepaction"]
> [Visual Studio Code を使用して .NET Core コンソール アプリケーションを発行する](publishing-with-visual-studio-code.md)
