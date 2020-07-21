---
title: Visual Studio for Mac を使用して .NET Standard クラス ライブラリを作成する
description: Visual Studio for Mac を使用して .NET Standard クラス ライブラリを作成する方法について説明します。
ms.date: 06/08/2020
ms.openlocfilehash: 3a107fff2fd6aef5e06d9af3eac334fbf5688fa5
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84713419"
---
# <a name="tutorial-create-a-net-standard-library-using-visual-studio-for-mac"></a>チュートリアル: Visual Studio for Mac を使用して .NET Standard ライブラリを作成する

このチュートリアルでは、1 つの文字列処理メソッドを含むシンプルなクラス ライブラリを作成します。 それを[拡張メソッド](../../csharp/programming-guide/classes-and-structs/extension-methods.md)として実装し、<xref:System.String> クラスのメンバーと同じように呼び出すことができるようにします。

"*クラス ライブラリ*" は、アプリケーションから呼び出される型とメソッドを定義します。 .NET Standard 2.1 をターゲットとするクラス ライブラリは、バージョン 2.1 の .NET Standard をサポートする任意の .NET 実装をターゲットとするアプリケーションで使用できます。 クラス ライブラリが完成したら、サードパーティ製のコンポーネントとして配布するか、1 つ以上のアプリケーションを含むバンドルされたコンポーネントとして配布することができます。

> [!NOTE]
> お客様のフィードバックは非常に貴重です。 次の 2 つの方法で Visual Studio for Mac の開発チームにフィードバックを送信できます。
>
> - Visual Studio for Mac で、メニューから **[ヘルプ]**  >  **[問題の報告]** の順に選択するか、ようこそ画面から **[問題の報告]** を選択して、バグ報告を提出するためのウィンドウを開きます。 お客様のフィードバックは、[開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/41/index.html) ポータルで追跡することができます。
> - 提案するには、メニューから **[ヘルプ]**  >  **[提案の送信]** の順に選択するか、ようこそ画面から **[提案の送信]** を選択し、[Visual Studio for Mac の開発者コミュニティの Web ページ](https://developercommunity.visualstudio.com/content/idea/post.html?space=41)に移動します。

## <a name="prerequisites"></a>必須コンポーネント

* [Visual Studio for Mac バージョン 8.6 以降をインストールします](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。 .NET Core をインストールするオプションを選択します。 .NET Core 開発の場合、Xamarin のインストールは省略可能です。 詳細については、次のリソースを参照してください。

  * [チュートリアル: Visual Studio for Mac をインストールする](/visualstudio/mac/installation)。
  * [サポート対象の macOS のバージョン](../install/dependencies.md?pivots=os-macos)。
  * [Visual Studio for Mac でサポートされている .NET Core のバージョン](/visualstudio/mac/net-core-support)。

## <a name="create-a-solution-with-a-class-library-project"></a>クラス ライブラリ プロジェクトを含むソリューションの作成

1 つの Visual Studio のソリューションは、1 つまたは複数のプロジェクトのコンテナーとして機能します。 ソリューションと、そのソリューション内のクラス ライブラリ プロジェクトを作成します。 後ほど、さらに関連するプロジェクトを同じソリューションに追加します。

1. Visual Studio for Mac を起動します。

1. スタート ウィンドウで、 **[新しいプロジェクト]** を選択します。

1. **[新しいプロジェクト]** ダイアログで、 **[マルチプラットフォーム]** ノードの下にある **[ライブラリ]** を選択し、 **[.NET Standard ライブラリ]** テンプレートを選択して、 **[次へ]** を選択します。

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="[新しいプロジェクト] ダイアログ":::

1. **[Configure your new .NET Standard Library]\(新しい .NET Standard ライブラリの構成\)** ダイアログで、[.NET Standard 2.1] を選択し、 **[次へ]** を選択します。

   :::image type="content" source="media/library-with-visual-studio-mac/choose-net-std-21.png" alt-text=".NET Standard 2.1 を選択する":::

1. プロジェクトに「StringLibrary」という名前を指定し、ソリューションに「ClassLibraryProjects」という名前を指定します。 **[ソリューション ディレクトリ内にプロジェクト ディレクトリを作成する]** はオンのままにしておきます。 **[作成]** を選択します。

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project-options.png" alt-text="Visual Studio for Mac の [新しいプロジェクト] ダイアログのオプション":::

1. メイン メニューから **[表示]**  >  **[パッド]**  >  **[ソリューション]** の順に選択し、ドッキング アイコンを選択してパッドを開いたままにします。

   :::image type="content" source="media/library-with-visual-studio-mac/solution-dock-icon.png" alt-text="ソリューション パッドのドッキング アイコン":::

1. **[ソリューション]** パッドで、`StringLibrary` ノードを展開し、テンプレートで提供される *Class1.cs* というクラス ファイルを表示します。 <kbd>ctrl</kbd> キーを押しながらファイルをクリックし、コンテキスト メニューから **[名前の変更]** を選択して、ファイル名を *StringLibrary.cs* に変更します。 ファイルを開き、内容を次のコードに置き換えます。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

1. <kbd>⌘</kbd><kbd>S</kbd> (<kbd>command</kbd> + <kbd>S</kbd>) キーを押して、ファイルを保存します。

1. IDE ウィンドウの下部の余白にある **[エラー]** を選択して、 **[エラー]** パネルを開きます。 **[ビルド出力]** ボタンを選択します。

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-error-button.png" alt-text="[エラー] ボタンが示された Visual Studio Mac IDE の下部余白":::

1. メニューから **[ビルド]**  >  **[すべてビルド]** の順に選択します。

   ソリューションがビルドされます。 ビルド出力パネルに、ビルドが成功したことが示されます。

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-build-panel.png" alt-text="ビルドの成功メッセージが表示された、[エラー] パネルの Visual Studio Mac のビルド出力ウィンドウ":::

## <a name="add-a-console-app-to-the-solution"></a>ソリューションにコンソール アプリを追加する

このクラス ライブラリを使用するコンソール アプリケーションを追加します。 アプリによって、ユーザーに文字列の入力が求められ、文字列が大文字で始まるかどうかが報告されます。

1. **[ソリューション]** パッドで、<kbd>ctrl</kbd> キーを押しながら `ClassLibraryProjects` ソリューションをクリックします。 **[Web and Console]\(Web とコンソール\)**  >  **[アプリ]** テンプレートからテンプレートを選択することで、新しい **[コンソール アプリケーション]** プロジェクトを追加し、 **[次へ]** を選択します。

1. **[ターゲット フレームワーク]** として **[.NET Core 3.1]** を選択し、 **[次へ]** を選択します。

1. プロジェクトに「**ShowCase**」という名前を付けます。 **[作成]** を選択し、ソリューションでプロジェクトを作成します。

   :::image type="content" source="media/library-with-visual-studio-mac/add-showcase-project.png" alt-text="ShowCase プロジェクトを追加する":::

1. *Program.cs* ファイルを開きます。 このコードを次のコードに置き換えます。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   プログラムは、ユーザーに文字列の入力を要求し、 文字列が大文字で始まるかどうかを示します。 ユーザーが文字列を入力せずに <kbd>enter</kbd> キーを押すと、アプリケーションが終了し、コンソール ウィンドウが閉じます。

   このコードでは、`row` 変数を使って、コンソール ウィンドウに書き込まれるデータの行数のカウントを維持します。 これが 25 以上になると、コードによってコンソール ウィンドウがクリアされ、ユーザーにメッセージが表示されます。

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

最初は、新しいコンソール アプリ プロジェクトにクラス ライブラリへのアクセス権はありません。 クラス ライブラリでメソッドを呼び出せるようにするには、クラス ライブラリ プロジェクトへのプロジェクト参照を作成します。

1. **[ソリューション]** パッドで、<kbd>ctrl</kbd> キーを押しながら、新しい **ShowCase** プロジェクトの **[依存関係]** ノードをクリックします。 コンテキスト メニューから **[参照の追加]** を選択します。

1. **[参照]** ダイアログで、 **[StringLibrary]** を選択して **[OK]** を選択します。

## <a name="run-the-app"></a>アプリを実行する

1. <kbd>ctrl</kbd> キーを押しながら ShowCase プロジェクトをクリックし、コンテキスト メニューから **[プロジェクトの実行]** を選択します。

1. 文字列を入力して <kbd>enter</kbd> キーを押すことでプログラムを試してみます。<kbd>enter</kbd> キーを押して終了します。

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-console-window.png" alt-text="アプリが実行中であることを示す Visual Studio for Mac のコンソール ウィンドウ":::

## <a name="additional-resources"></a>その他の技術情報

* [.NET Core CLI を使用したライブラリの開発](libraries.md)
* [.NET Standard のバージョンとそれらでサポートされているプラットフォーム](../../standard/net-standard.md)。
* [Visual Studio 2019 for Mac リリース ノート](/visualstudio/releasenotes/vs2019-mac-relnotes)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、ソリューションとライブラリ プロジェクトを作成し、そのライブラリを使用するコンソール アプリ プロジェクトを追加しました。 次のチュートリアルでは、ソリューションに単体テスト プロジェクトを追加します。

> [!div class="nextstepaction"]
> [Visual Studio for Mac を使用して .NET Core で .NET Standard ライブラリをテストする](testing-library-with-visual-studio-mac.md)
