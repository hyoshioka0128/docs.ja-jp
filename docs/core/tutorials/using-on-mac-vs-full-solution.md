---
title: Visual Studio for Mac を使用した macOS での完全な .NET Core ソリューションの構築
description: このトピックでは、再利用可能なライブラリと単体テストを含む .NET Core ソリューションの構築方法を示します。
author: mairaw
ms.date: 06/12/2017
ms.custom: seodec18
ms.openlocfilehash: 0081463c0a99acc5cb4e02bb96e2218bbcf61131
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74428628"
---
# <a name="building-a-complete-net-core-solution-on-macos-using-visual-studio-for-mac"></a>Visual Studio for Mac を使用した macOS での完全な .NET Core ソリューションの構築

Visual Studio for Mac では、.NET Core アプリケーション開発用の機能をすべて備えた統合開発環境 (IDE) が提供されます。 このトピックでは、再利用可能なライブラリと単体テストを含む .NET Core ソリューションの構築方法を示します。

このチュートリアルでは、ユーザーが入力した検索語とテキスト文字列を受け入れ、クラス ライブラリでメソッドを使用した場合に文字列に検索語が表示される回数をカウントし、ユーザーに結果を返すアプリケーションの作成方法を示します。 ソリューションには、単体テストの概念を紹介するため、クラス ライブラリの単体テストも含まれています。 完全なサンプルでチュートリアルを続行する場合は、[サンプル ソリューション](https://github.com/dotnet/samples/blob/master/core/tutorials/using-on-mac-vs-full-solution/WordCounter)をダウンロードしてください。 ダウンロード方法については、「[サンプルおよびチュートリアル](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)」を参照してください。

> [!NOTE]
> お客様のフィードバックは非常に貴重です。 次の 2 つの方法で Visual Studio for Mac の開発チームにフィードバックを送信できます。
>
> - Visual Studio for Mac で、メニューから **[ヘルプ]**  >  **[問題の報告]** の順に選択するか、ようこそ画面から **[問題の報告]** を選択して、バグ報告を提出するためのウィンドウを開きます。 お客様のフィードバックは、[開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/41/index.html) ポータルで追跡することができます。
> - 提案するには、メニューから **[ヘルプ]**  >  **[提案の送信]** の順に選択するか、ようこそ画面から **[提案の送信]** を選択し、[Visual Studio for Mac の開発者コミュニティの Web ページ](https://developercommunity.visualstudio.com/content/idea/post.html?space=41)に移動します。

## <a name="prerequisites"></a>必須コンポーネント

- OpenSSL (.NET Core 1.1 が実行されている場合):[.NET Core の依存関係と要件](../install/dependencies.md?tabs=netcore30&pivots=os-macos)に関するトピックを参照してください。
- [.NET Core SDK 1.1 以降](https://dotnet.microsoft.com/download)
- [Visual Studio 2017 for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)

前提条件の詳細については、[.NET Core の依存関係と要件](../install/dependencies.md?tabs=netcore30&pivots=os-macos)に関する記事を参照してください。 Visual Studio 2017 for Mac の完全なシステム要件については、「[Visual Studio 2017 for Mac 製品ファミリのシステム要件](/visualstudio/productinfo/vs2017-system-requirements-mac)」をご覧ください。

## <a name="building-a-library"></a>ライブラリのビルド

1. ようこそ画面で、 **[新しいプロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログで、 **[.NET Core]** ノードの下にある **[.NET Standard ライブラリ]** テンプレートを選択します。 これにより、.NET Core を対象とする .NET Standard ライブラリと、[.NET Standard](../../standard/net-standard.md) のバージョン 2.0 をサポートするその他の .NET 実装が作成されます。 **[次へ]** を選択します。

   ![Visual Studio for Mac の [新しいプロジェクト] ダイアログ](./media/using-on-mac-vs-full-solution/visual-studio-mac-new-project.png)

1. プロジェクトには "TextUtils" ("Text Utilities" の短い名前)、ソリューションには "WordCounter" という名前を付けます。 **[ソリューション ディレクトリ内にプロジェクト ディレクトリを作成します]** チェック ボックスはそのままにしておきます。 **[作成]** を選択します。

   ![Visual Studio for Mac の [新しいプロジェクト] ダイアログのオプション](./media/using-on-mac-vs-full-solution/visual-studio-mac-new-project-options.png)

1. **[ソリューション]** サイドバーで、`TextUtils` ノードを展開し、テンプレートで提供される *Class1.cs* というクラス ファイルを表示します。 ファイルを右クリックし、コンテキスト メニューから **[名前の変更]** を選択して、ファイル名を *WordCount.cs* に変更します。 ファイルを開き、内容を次のコードに置き換えます。

   [!code-csharp[Main](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/TextUtils/WordCount.cs)]

1. ファイルを保存します。その場合、3 つの異なる方法 (キーボード ショートカット <kbd>&#8984;</kbd>+<kbd>s</kbd> キーを使用する、メニューから **[ファイル]**  >  **[保存]** の順に選択する、ファイルのタブを右クリックしてコンテキスト メニューから **[保存]** を選択する) のいずれかを使用します。 次のイメージは IDE ウィンドウを示しています。

   ![クラス ライブラリ ファイルとメソッドが示された Visual Studio for Mac IDE ウィンドウ](./media/using-on-mac-vs-full-solution/visual-studio-mac-editor.png)

1. IDE ウィンドウの下部の余白にある **[エラー]** を選択して、 **[エラー]** パネルを開きます。 **[ビルド出力]** ボタンを選択します。

   ![[エラー] ボタンが示された Visual Studio Mac IDE の下余白](./media/using-on-mac-vs-full-solution/visual-studio-mac-error-button.png)

1. メニューから **[ビルド]**  >  **[すべてビルド]** の順に選択します。

   ソリューションがビルドされます。 ビルド出力パネルに、ビルドが成功したことが示されます。

   ![ビルドの成功メッセージが表示された、[エラー] パネルの Visual Studio Mac のビルド出力ウィンドウ](./media/using-on-mac-vs-full-solution/visual-studio-mac-build-panel.png)

## <a name="creating-a-test-project"></a>テスト プロジェクトの作成

単体テストでは、開発および公開時に自動化されたソフトウェア テストが提供されます。 このチュートリアルで使用するテスト フレームワークは [xUnit (バージョン 2.2.0 以降)](https://xunit.github.io/) です。これは、以下の手順で xUnit テスト プロジェクトをソリューションに追加したときに自動的にインストールされます。

1. **[ソリューション]** サイドバーで、`WordCounter` ソリューション名を右クリックし、 **[追加]**  >  **[新しいプロジェクトの追加]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログで、 **[.NET Core]** ノードから **[テスト]** を選択します。 **[xUnit Test Project (xUnit テスト プロジェクト)]** を選択してから **[次へ]** を選択します。

   ![xUnit テスト プロジェクトを作成する Visual Studio Mac の [新しいプロジェクト] ダイアログ](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-project.png)

1. 新しいプロジェクトに "TestLibrary" という名前を付けて、 **[作成]** を選択します。

   ![プロジェクト名を指定する Visual Studio Mac の [新しいプロジェクト] ダイアログ](./media/using-on-mac-vs-full-solution/visual-studio-mac-new-project-name.png)

1. テスト ライブラリを `WordCount` クラスで使用するには、`TextUtils` プロジェクトへの参照を追加します。 **[ソリューション]** サイドバーで、**TestLibrary** の下にある **[依存関係]** を右クリックします。 コンテキスト メニューから **[参照の編集]** を選択します。

1. **[参照の編集]** ダイアログで、 **[プロジェクト]** タブの **[TextUtils]** プロジェクトを選択します。 **[OK]** を選択します。

   ![Visual Studio Mac の [参照の編集] ダイアログ](./media/using-on-mac-vs-full-solution/visual-studio-mac-edit-references.png)

1. **[TestLibrary]** プロジェクトで、*UnitTest1.cs* ファイルの名前を *TextUtilsTests.cs* に変更します。

1. ファイルを開き、コードを次のものと置き換えます。

   ```csharp
   using Xunit;
   using TextUtils;
   using System.Diagnostics;

   namespace TestLibrary
   {
       public class TextUtils_GetWordCountShould
       {
           [Fact]
           public void IgnoreCasing()
           {
               var wordCount = WordCount.GetWordCount("Jack", "Jack jack");

               Assert.NotEqual(2, wordCount);
           }
       }
   }
   ```

   次のイメージは、単体テスト コードが配置済みの IDE を示しています。 `Assert.NotEqual` ステートメントに注目してください。

   ![IDE のメイン ウィンドウでの Visual Studio for Mac の最初の単体テスト](./media/using-on-mac-vs-full-solution/visual-studio-mac-assert-test.png)

   新しいテストを一度失敗させてテスト ロジックが正しいことを確認することが重要です。 メソッドは "Jack" (先頭が大文字) という名前と、"Jack" および "jack" (先頭が大文字のものと小文字のもの) を含む文字列を渡します。 `GetWordCount` メソッドが正しく機能している場合は、検索語の 2 つのインスタンスのカウントが返されます。 このテストを意図的に失敗させるには、まず、検索語 "Jack" の 2 つのインスタンスが `GetWordCount` メソッドで返されないことをアサートするテストを実装します。 次の手順に進んで意図的にテストを失敗させます。

1. 画面の右側の **[単体テスト]** パネルを開きます。

   ![Visual Studio for Mac の [単体テスト] パネル](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-panel.png)

1. **[ドッキング]** アイコンをクリックして、パネルを開いたままにします。

   ![Visual Studio for Mac の [単体テスト] パネルの [ドッキング] アイコン](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-dock-icon.png)

1. **[すべて実行]** ボタンをクリックします。

   テストは失敗します。これが正しい結果です。 テスト メソッドは、`GetWordCount` メソッドに指定された文字列 "Jack jack" から `inputString` "Jack" の 2 つのインスタンスが返されないことをアサートします。 単語の大文字と小文字は `GetWordCount` メソッドでは考慮されないため、2 つのインスタンスが返されます。 2 *is not equal to* 2 というアサーションは失敗します。 これは正しい結果であり、テストのロジックは適切です。

   ![Visual Studio for Mac のテスト エラーの表示](./media/using-on-mac-vs-full-solution/visual-studio-for-mac-unit-test-failure.png)

1. `Assert.NotEqual` から `Assert.Equal` に変更して `IgnoreCasing` テスト メソッドを変更します。 ファイルを保存します。その場合、キーボード ショートカット <kbd>&#8984;</kbd>+<kbd>s</kbd> を使用するか、メニューの **[ファイル]**  >  **[保存]** の順に選択するか、ファイルのタブを右クリックしてコンテキスト メニューから **[保存]** を選択します。

   `searchWord` "Jack" は `GetWordCount` に渡された `inputString` "Jack jack" を含む 2 つのインスタンスを返すことが予想されます。 **[単体テスト]** パネルの **[テストの実行]** ボタン、または画面下部の **[テスト結果]** パネルの **[テストの再実行]** ボタンをクリックして、テストを再実行します。 テストに合格します。 文字列 "Jack jack" (大文字と小文字の区別は無視) に "Jack" のインスタンスが 2 つあり、テスト アサーションは `true` です。

   ![Visual Studio for Mac のテスト成功の表示](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-pass.png)

1. `Fact` での個々の戻り値のテストは、単体テストで実行できることのほんの一部に過ぎません。 別の強力な手法では、`Theory` を使用して一度に複数の値をテストすることができます。 次のメソッドを `TextUtils_GetWordCountShould` クラスに追加します。 このメソッドを追加すると、クラスのメソッドは 2 つになります。

   ```csharp
   [Theory]
   [InlineData(0, "Ting", "Does not appear in the string.")]
   [InlineData(1, "Ting", "Ting appears once.")]
   [InlineData(2, "Ting", "Ting appears twice with Ting.")]
   public void CountInstancesCorrectly(int count,
                                       string searchWord,
                                       string inputString)
   {
       Assert.NotEqual(count, WordCount.GetWordCount(searchWord,
                                                  inputString));
   }
   ```

   `CountInstancesCorrectly` は、`GetWordCount` メソッドが正しくカウントすることを確認します。 `InlineData` は確認するカウント、検索語、および入力文字列を示します。 テスト メソッドはデータの行ごとに一度実行されます。 繰り返しますが、データのカウントが正しく、値が `GetWordCount` メソッドで返されるカウントと一致することがわかっている場合でも、まず、`Assert.NotEqual` を使用して失敗をアサートする必要があります。 意図的にテストを失敗させる手順を実行するのは、最初は時間の無駄と思えるかもしれませんが、まず、テストを失敗させてロジックを確認することはテストのロジックを確認するうえで重要なことです。 失敗させようとしたのに成功するテスト メソッドがある場合、そのテストのロジックにバグがあります。 テスト メソッドを作成するたびに、この手順を実行することをお勧めします。

1. ファイルを保存し、もう一度テストを実行します。 大文字と小文字のテストは成功しますが、3 つのカウント テストは失敗します。 これは予想したとおりの結果です。

   ![Visual Studio for Mac の予測されるテスト エラー](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-failure.png)

1. `Assert.NotEqual` から `Assert.Equal` に変更して `CountInstancesCorrectly` テスト メソッドを変更します。 ファイルを保存します。 テストをもう一度実行します。 すべてのテストに成功します。

   ![Visual Studio for Mac の予測されるテスト成功](./media/using-on-mac-vs-full-solution/visual-studio-mac-unit-test-pass.png)

## <a name="adding-a-console-app"></a>コンソール アプリの追加

1. **[ソリューション]** サイドバーで、`WordCounter` ソリューションを右クリックします。 **[.NET Core]**  >  **[アプリ]** テンプレートの順に移動してテンプレートを選択し、新しい**コンソール アプリケーション**プロジェクトを追加します。 **[次へ]** を選択します。 プロジェクトに **WordCounterApp** という名前を付けます。 **[作成]** を選択し、ソリューションでプロジェクトを作成します。

1. **[ソリューション]** サイドバーで、新しい **WordCounterApp** プロジェクトの **[依存関係]** ノードを右クリックします。 **[参照の編集]** ダイアログで、**TextUtils** にチェック マークを付けて **[OK]** を選択します。

1. *Program.cs* ファイルを開きます。 このコードを次のコードを使って置き換えます。

   [!code-csharp[Main](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/WordCounterApp/Program.cs)]

1. IDE ではなく、コンソール ウィンドウでアプリを実行するには、`WordCounterApp` プロジェクトを右クリックして **[オプション]** を選択し、 **[構成]** の下の **[既定]** ノードを開きます。 **[外部コンソールで実行]** のチェック ボックスをオンにします。 **[コンソール出力を一時停止する]** オプションはオンのままにしておきます。 この設定により、コンソール ウィンドウでアプリが起動し、`Console.ReadLine` ステートメントに入力できるようになります。 IDE でそのままアプリを実行すると、`Console.WriteLine` ステートメントの出力が表示されるだけです。 `Console.ReadLine` ステートメントは、IDE の **[アプリケーション出力]** パネルでは機能しません。

   ![Visual Studio for Mac の [プロジェクト オプション] ウィンドウ](./media/using-on-mac-vs-full-solution/visual-studio-mac-project-options.png)

1. Visual Studio for Mac の現在のバージョンでは、ソリューションの実行時にテストを実行できないため、コンソール アプリを直接実行します。 `WordCounterApp` プロジェクトを右クリックし、コンテキスト メニューから **[Run item (項目の実行)]** を選択します。 [再生] ボタンでアプリを実行しようとすると、テスト ランナーとアプリの実行は失敗します。 この問題への取り組みの状態について詳しくは、[xunit/xamarinstudio.xunit (#60)](https://github.com/xunit/xamarinstudio.xunit/issues/60) を参照してください。 アプリを実行する際に、コンソール ウィンドウで入力を求めるメッセージが表示されたら、検索語と入力文字列の値を入力します。 アプリには、文字列での検索語の表示回数が示されます。

   ![アプリが実行中であることを示す Visual Studio for Mac のコンソール ウィンドウ](./media/using-on-mac-vs-full-solution/visual-studio-mac-console-window.png)

1. 確認する最後の機能は、Visual Studio for Mac でのデバッグです。 `Console.WriteLine` ステートメントにブレークポイントを設定します。23 行目の左余白を選択すると、コード行の横に赤い丸が表示されます。 コード行の任意の場所を選択し、メニューから **[実行]**  >  **[ブレークポイントの設定/解除]** の順に選択することもできます。

   ![Visual Studio for Mac のブレークポイントの設定](./media/using-on-mac-vs-full-solution/visual-studio-mac-breakpoint.png)

1. `WordCounterApp` プロジェクトを右クリックします。 コンテキスト メニューから **[Start Debugging item (項目のデバッグの開始)]** を選択します。 アプリが実行されたら、検索語 "cat" と検索文字列 "The dog chased the cat, but the cat escaped" を入力します。 `Console.WriteLine` ステートメントに達した時点でプログラムの実行が停止します。その後、ステートメントが実行されます。 **[ローカル]** タブで、`searchWord`、`inputString`、`wordCount`、および `pluralChar` の各値を確認できます。

   ![Visual Studio for Mac の停止されたデバッガー プログラムの実行](./media/using-on-mac-vs-full-solution/visual-studio-mac-debugger.png)

1. **[イミディエイト]** ウィンドウで、「wordCount = 999;」と入力してから Enter キーを押します。 これで、`wordCount` 変数に 999 という意味のない値が割り当てられます。これは、デバッグ中に変数値の置き換えが可能であることを示します。

   ![Visual Studio for Mac の [イミディエイト] ウィンドウで値を変更する](./media/using-on-mac-vs-full-solution/visual-studio-mac-immediate-window.png)

1. ツールバーで、*続行*矢印をクリックします。 コンソール ウィンドウの出力を確認します。 アプリのデバッグ時に設定した 999 という不適切な値が報告されます。

   ![Visual Studio for Mac ツールバーの続行ボタン](./media/using-on-mac-vs-full-solution/visual-studio-mac-toolbar.png)

   ![Visual Studio for Mac のコンソール ウィンドウの出力](./media/using-on-mac-vs-full-solution/visual-studio-mac-output.png)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 for Mac リリース ノート](/visualstudio/releasenotes/vs2017-mac-relnotes)
