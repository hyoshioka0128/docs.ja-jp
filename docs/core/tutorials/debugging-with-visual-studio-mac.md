---
title: Visual Studio for Mac を使用して .NET Core コンソール アプリケーションをデバッグする
description: Visual Studio Mac を使用して .NET Core コンソール アプリをデバッグする方法について説明します。
ms.date: 06/08/2020
ms.openlocfilehash: 7e2a25266fab40b5ef1d0a38b8bbf06a6843746b
ms.sourcegitcommit: 3492dafceb5d4183b6b0d2f3bdf4a1abc4d5ed8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86416014"
---
# <a name="tutorial-debug-a-net-core-console-application-using-visual-studio-for-mac"></a>チュートリアル: Visual Studio for Mac を使用して .NET Core コンソール アプリケーションをデバッグする

このチュートリアルでは、Visual Studio for Mac で使用できるデバッグ ツールについて説明します。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio for Mac での .NET Core コンソール アプリケーションの作成](with-visual-studio-mac.md)に関する記事で作成したコンソール アプリを使用します。

## <a name="use-debug-build-configuration"></a>デバッグ ビルド構成の使用

"*デバッグ*" と "*リリース*" は、Visual Studio の組み込みビルド構成です。 デバッグ用のデバッグ ビルド構成と、最終リリース配布用のリリース構成を使用します。

デバッグ構成では、プログラムのコンパイルにシンボリック デバッグ情報が完全に含まれ、最適化は行われません。 ソース コードと生成された命令の関係は非常に複雑であり、最適化を行うとデバッグが困難になるためです。 プログラムのリリース構成は、シンボリック デバッグ情報を含まず、完全に最適化されます。

既定では、Visual Studio ではデバッグ ビルド構成が使用されるため、デバッグの前に変更を加える必要はありません。

1. Visual Studio for Mac を起動します。

1. [Visual Studio for Mac での .NET Core コンソール アプリケーションの作成](with-visual-studio-mac.md)に関する記事で作成したプロジェクトを開きます。

   現時点のビルド構成はツールバーに表示されています。 次のツール バーの画像では、アプリのデバッグ バージョンをコンパイルするように Visual Studio が構成されています。

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-debug.png" alt-text="デバッグが強調表示された Visual Studio のツールバー":::

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

"*ブレークポイント*" によって、ブレークポイントを含む行が実行される前に、アプリケーションの実行が一時的に中断されます。

1. 名前、日付、および時刻を表示する行にブレークポイントを設定します。 これを行うには、コード行にカーソルを置き、<kbd>⌘</kbd><kbd>\\</kbd> (<kbd>command</kbd> + <kbd>\\</kbd>) キーを押します。 ブレークポイントを設定するもう 1 つの方法は、メニューから **[実行]**  >  **[ブレークポイントの設定/解除]** を選択することです。

   Visual Studio では、ブレークポイントが設定された行を強調表示し、左余白に赤い点を表示することで、その行が示されます。

   :::image type="content" source="media/debugging-with-visual-studio-mac/set-breakpoint-in-editor.png" alt-text="ブレークポイントが設定された Visual Studio のプログラム ウィンドウ":::

1. <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>enter</kbd>) キーを押して、デバッグ モードでプログラムを起動します。 デバッグを開始するもう 1 つの方法は、メニューから **[実行]**  >  **[デバッグの開始]** を選択することです。

1. プログラムから名前の入力を求められたら、ターミナル ウィンドウに文字列を入力して、<kbd>enter</kbd> キーを押します。

1. プログラムの実行は、ブレークポイントに到達するときに、`Console.WriteLine` メソッドが実行される前に停止します。

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-hit.png" alt-text="Visual Studio でのブレークポイントのスクリーンショット":::

## <a name="use-the-immediate-window"></a>[イミディエイト] ウィンドウを使用する

**[イミディエイト]** ウィンドウでは、デバッグ中のアプリケーションと対話できます。 変数の値を対話的に変更して、プログラムにどのような影響があるかを確認できます。

1. **[イミディエイト]** ウィンドウが表示されない場合は、 **[表示]**  >  **[Debug Pads]\(デバッグ パッド\)**  >  **[イミディエイト]** の順に選択して表示します。

1. **[イミディエイト]** ウィンドウに「`name = "Gracie"`」と入力し、<kbd>enter</kbd> キーを押します。

1. **[イミディエイト]** ウィンドウに「`date = date.AddDays(1)`」と入力し、<kbd>enter</kbd> キーを押します。

   **[イミディエイト]** ウィンドウに、文字列変数の新しい値と、<xref:System.DateTime> 値のプロパティが表示されます。

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window.png" alt-text="Visual Studio の [イミディエイト] ウィンドウ":::

   **[ローカル]** ウィンドウには、現在実行しているメソッドで定義されている変数の値が表示されます。 変更したばかりの変数の値は **[ローカル]** ウィンドウで更新されます。

   :::image type="content" source="media/debugging-with-visual-studio-mac/locals-window.png" alt-text="Visual Studio の [ローカル] ウィンドウ":::

1. <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) キーを押してデバッグを続行します。

   ターミナルに表示される値は、 **[イミディエイト]** ウィンドウで行った変更に対応しています。

   ターミナルが表示されない場合は、下部のナビゲーション バーで **[Terminal - HelloWorld]\(ターミナル - HelloWorld\)** を選択します。

   :::image type="content" source="media/debugging-with-visual-studio-mac/terminal-hello-world.png" alt-text="下部のナビゲーション バーの [Terminal - HelloWorld]\(ターミナル - HelloWorld\)":::

1. 任意のキーを押してプログラムを終了します。

1. ターミナル ウィンドウを閉じます。

## <a name="set-a-conditional-breakpoint"></a>条件付きブレークポイントの設定

プログラムによって、ユーザーが入力する文字列が表示されます。 ユーザーが何も入力しないとどうなるでしょうか。 これは、"*条件付きブレークポイント*" と呼ばれる便利なデバッグ機能を使用してテストできます。

1. <kbd>ctrl</kbd> キーを押しながら、ブレークポイントを表す赤い点をクリックします。 コンテキスト メニューで **[ブレークポイントの編集]** を選択します。

1. **[ブレークポイントの編集]** ダイアログで、 **[さらに次の条件が真の場合]** の後に続くフィールドに次のコードを入力して、 **[適用]** を選択します。

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-settings.png" alt-text="ブレークポイントの設定パネルが表示されているエディター":::

   ブレークポイントにヒットするたびに、デバッガーは `String.IsNullOrEmpty(name)` メソッドを呼び出し、メソッド呼び出しが `true` を返す場合にのみ、この行で中断します。

   条件式の代わりに、"*ヒット カウント*" を指定できます。この場合、ステートメントが指定された回数実行される前にプログラムの実行が中断されます。

1. <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) キーを押してデバッグを開始します。

1. ターミナル ウィンドウで、名前の入力を求められたら、<kbd>enter</kbd> キーを押します。

   指定した条件 (`name` が `null` または <xref:System.String.Empty?displayProperty=nameWithType>) が満たされたため、ブレークポイントに到達すると、プログラムの実行が停止します。

1. **[ローカル]** ウィンドウを選ぶと、現在実行しているメソッドに対してローカルな変数の値が表示されます。 この場合、`Main` は現在実行中のメソッドです。 `name` 変数の値が `""` (つまり、<xref:System.String.Empty?displayProperty=nameWithType>) であることを確認します。

1. 値が空の文字列であることは、 **[イミディエイト]** ウィンドウに `name` という変数名を入力して <kbd>enter</kbd> キーを押すことでも確認できます。

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window-output.png" alt-text="name が空の文字列であることを示す [イミディエイト] ウィンドウ":::

1. <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) キーを押してデバッグを続行します。

1. ターミナル ウィンドウで、任意のキーを押してプログラムを終了します。

1. ターミナル ウィンドウを閉じます。

1. コード ウィンドウの左余白の赤い点をクリックして、ブレークポイントをクリアします。 ブレークポイントをクリアするもう 1 つの方法は、コード行を選択した状態で **[実行] > [ブレークポイントの設定/解除]** を選択することです。

## <a name="step-through-a-program"></a>プログラムのステップ実行

Visual Studio では、1 行ずつプログラムをステップ実行して、実行を監視することもできます。 通常は、ブレークポイントを設定して、プログラム コードのごく一部を通じてプログラム フローに従います。 このプログラムは小さいため、次の手順に従ってプログラム全体をステップ実行できます。

1. `Main` メソッドの開始を示す中かっこにブレークポイントを設定します (<kbd>command</kbd> + <kbd>\\</kbd> キーを押す)。

1. <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) キーを押してデバッグを開始します。

   ブレークポイントがある行で Visual Studio が停止します。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>I</kbd>) キーを押すか、 **[実行]**  >  **[ステップ イン]** を選択して、1 行進めます。

   次に実行される行が強調表示されて、横に矢印が表示されます。

   :::image type="content" source="media/debugging-with-visual-studio-mac/step-into-method.png" alt-text="Visual Studio のステップ イン メソッド":::

   この時点で、 **[ローカル]** ウィンドウに `args` 配列が空であることが示され、`name` と `date` には既定値が設定されています。 さらに、Visual Studio によって空のターミナルが開かれています。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>I</kbd>) キーを押します。

   `name` の変数代入を含むステートメントが強調表示されます。 **[ローカル]** ウィンドウに `name` が `null` であると表示され、ターミナルに "What is your name?" という文字列が表示されます。

1. コンソール ウィンドウに文字列を入力して <kbd>enter</kbd> キーを押すことで、このプロンプトに応答します。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>I</kbd>) キーを押します。

   `date` の変数代入を含むステートメントが強調表示されます。 **[ローカル]** ウィンドウには、<xref:System.Console.ReadLine%2A?displayProperty=nameWithType> メソッドの呼び出しによって返された値が表示されます。 ターミナルには、プロンプトで入力した文字列が表示されます。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>I</kbd>) キーを押します。

   **[ローカル]** ウィンドウには、<xref:System.DateTime.Now?displayProperty=nameWithType> プロパティから代入された後の `date` 変数の値が表示されます。 ターミナルは変更されません。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>I</kbd>) キーを押します。

   Visual Studio は、<xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> メソッドを呼び出します。 ターミナルには、書式設定された文字列が表示されます。

1. <kbd>⇧</kbd><kbd>⌘</kbd><kbd>U</kbd> (<kbd>shift</kbd> + <kbd>command</kbd> + <kbd>U</kbd>) キーを押すか、 **[実行]**  >  **[ステップ アウト]** を選択します。

   ターミナルにメッセージが表示され、任意のキーを押すよう求められます。

1. 任意のキーを押してプログラムを終了します。

## <a name="use-release-build-configuration"></a>リリース ビルド構成を使用する

アプリケーションのデバッグ バージョンのテストが終了したら、リリース バージョンもコンパイルしてテストする必要があります。 リリース バージョンには、アプリケーションの動作に悪影響を与える可能性があるコンパイラの最適化が組み込まれています。 たとえば、パフォーマンスを向上させるように設計されたコンパイラの最適化では、マルチスレッド アプリケーションで競合状態が生じる場合があります。

コンソール アプリケーションのリリース バージョンをビルドしてテストするには、次の手順を実行します。

1. ツール バーのビルド構成を **[デバッグ]** から **[リリース]** に変更します。

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="デバッグが強調表示された Visual Studio の既定のツール バー":::

1. <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd> + <kbd>command</kbd> + <kbd>enter</kbd>) キーを押して、デバッグなしで実行します。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio のデバッグ ツールを使用しました。 次のチュートリアルでは、アプリの展開可能なバージョンを発行します。

> [!div class="nextstepaction"]
> [Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを発行する](publishing-with-visual-studio-mac.md)
