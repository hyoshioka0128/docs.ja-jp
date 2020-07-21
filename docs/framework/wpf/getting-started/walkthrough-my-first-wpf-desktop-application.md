---
title: Visual Studio 2019 で最初の WPF アプリを作成する - .NET Framework
titleSuffix: ''
description: ほとんどの WPF アプリケーションに共通する要素を含む、Windows Presentation Foundation (WPF) デスクトップ アプリケーションを開発します。
ms.date: 09/06/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting started [WPF], WPF
- WPF [WPF], getting started
ms.assetid: b96bed40-8946-4285-8fe4-88045ab854ed
ms.topic: tutorial
ms.custom: mvc,vs-dotnet
ms.openlocfilehash: c9af988bcf291325b11df4fd22827b47090c0b48
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853889"
---
# <a name="tutorial-create-your-first-wpf-application-in-visual-studio-2019"></a>チュートリアル: Visual Studio 2019 で最初の WPF アプリケーションを作成する

この記事では、ほとんどの WPF アプリケーションに共通する次の要素が含まれる Windows Presentation Foundation (WPF) デスクトップ アプリケーションを開発する方法について説明します: Extensible Application Markup Language (XAML) マークアップ、コードビハインド、アプリケーション定義、コントロール、レイアウト、データ バインディング、スタイル。 アプリケーションを開発するには、Visual Studio を使用します。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
>
> - WPF プロジェクトを作成する。
> - XAML を使用して、アプリケーションのユーザー インターフェイス (UI) の外観をデザインする。
> - アプリケーションの動作を構築するコードを記述する。
> - アプリケーションを管理するためのアプリケーション定義を作成する。
> - コントロールを追加し、レイアウトを作成して、アプリケーションの UI を構成する。
> - アプリケーションの UI 全体に一貫性のある外観を持たせるためのスタイルを作成する。
> - UI にデータを設定し、データと UI の同期を保つために、UI をデータにバインドする。

このチュートリアルの最後には、ユーザーが選択した個人の経費報告書を表示できる、スタンドアロンの Windows アプリケーションが完成します。 このアプリケーションは、ブラウザー スタイルのウィンドウでホストされる、複数の WPF ページから構成されます。

> [!TIP]
> このチュートリアルで使用するサンプル コードには Visual Basic 版と C# 版があり、[WPF アプリ チュートリアルのサンプル コード](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp)で入手できます。
>
> このページの先頭にある言語セレクターを使用して、サンプル コードのコード言語を C# と Visual Basic の間で切り替えることができます。

## <a name="prerequisites"></a>必須コンポーネント

- **.NET デスクトップ開発**ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)。

   Visual Studio の最新バージョンのインストールの詳細については、「[Visual Studio のインストール](/visualstudio/install/install-visual-studio)」を参照してください。

## <a name="create-the-application-project"></a>アプリケーション プロジェクトを作成する

最初のステップでは、アプリケーション定義、2 つのページ、および 1 つの画像が含まれる、アプリケーション インフラストラクチャを作成します。

1. **`ExpenseIt`** という名前の新しい WPF アプリケーション プロジェクトを Visual Basic または Visual C# で作成します。

   1. Visual Studio を開き、 **[作業の開始]** メニューの **[新しいプロジェクトの作成]** を選択します。

      **[新しいプロジェクトの作成]** ダイアログが開きます。

   2. **[言語]** ドロップダウンで、 **[C#]** または **[Visual Basic]** を選択します。

   3. **[WPF アプリ (.NET Framework)]** テンプレートを選択し、 **[次へ]** を選択します。

      ![[新しいプロジェクトの作成] ダイアログ](./media/walkthrough-my-first-wpf-desktop-application/create-new-project-dialog.png)

      **[新しいプロジェクトを構成します]** ダイアログが開きます。

   4. プロジェクトの名前に「 **`ExpenseIt`** 」と入力して、 **[OK]** を選択します。

      ![[新しいプロジェクトを構成します] ダイアログ](./media/walkthrough-my-first-wpf-desktop-application/configure-new-project-dialog.png)

      Visual Studio によってプロジェクトが作成され、デザイナーで **MainWindow.xaml** という名前の既定のアプリケーション ウィンドウが開きます。

2. *Application.xaml* (Visual Basic) または *App.xaml* (C#) を開きます。

    この XAML ファイルでは、WPF アプリケーションとすべてのアプリケーション リソースを定義します。 また、このファイルを使用して、アプリケーションの起動時に自動的に表示される UI (この例では *MainWindow.xaml*) も指定します。

    XAML は、Visual Basic では次のようになります。

    [!code-xaml[ExpenseIt#1_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/Application.xaml#1_a)]

    C# では次のようになります。

    [!code-xaml[ExpenseIt#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/App.xaml#1)]

3. *MainWindow.xaml* を開きます。

    この XAML ファイルは、アプリケーションのメイン ウィンドウです。このファイルには、ページで作成されたコンテンツが表示されます。 <xref:System.Windows.Window> クラスでは、ウィンドウのプロパティ (タイトル、サイズ、アイコンなど) が定義されており、イベント (ウィンドウを閉じたり非表示にしたりするなど) が処理されます。

4. 次の XAML で示されているように、<xref:System.Windows.Window> 要素を <xref:System.Windows.Navigation.NavigationWindow> に変更します。

   ```xaml
   <NavigationWindow x:Class="ExpenseIt.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        ...
   </NavigationWindow>
   ```

   このアプリでは、ユーザーの入力に応じて画面がさまざまなコンテンツに移動します。 このため、メインの <xref:System.Windows.Window> を <xref:System.Windows.Navigation.NavigationWindow> に変更する必要があります。 <xref:System.Windows.Navigation.NavigationWindow> では、<xref:System.Windows.Window> のすべてのプロパティを継承します。 XAML ファイル内の <xref:System.Windows.Navigation.NavigationWindow> 要素では、<xref:System.Windows.Navigation.NavigationWindow> クラスのインスタンスが作成されます。 詳しくは、「[ナビゲーションの概要](../app-development/navigation-overview.md)」をご覧ください。

5. <xref:System.Windows.Navigation.NavigationWindow> タグの間から <xref:System.Windows.Controls.Grid> 要素を削除します。

6. XAML コードで、<xref:System.Windows.Navigation.NavigationWindow> 要素に対する次のプロパティを変更します。

    - <xref:System.Windows.Window.Title%2A> プロパティを "`ExpenseIt`" に設定します。

    - <xref:System.Windows.FrameworkElement.Height%2A> プロパティを 350 ピクセルに設定します。

    - <xref:System.Windows.FrameworkElement.Width%2A> プロパティを 500 ピクセルに設定します。

    XAML は、Visual Basic では次のようになります。

    [!code-xaml[ExpenseIt#2_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt/MainWindow.xaml#2_a)]

    C# では次のようになります。

    [!code-xaml[ExpenseIt#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml#2)]

7. *MainWindow.xaml.vb* または *MainWindow.xaml.cs* を開きます。

    このファイルは、*MainWindow.xaml* で宣言されたイベントを処理するコードが含まれる分離コード ファイルです。 このファイルには、XAML で定義されたウィンドウの部分クラスが含まれています。

8. C# を使用している場合は、<xref:System.Windows.Navigation.NavigationWindow> から派生するように `MainWindow` クラスを変更します。 (Visual Basic では、XAML でウィンドウを変更すると自動的にこの処理が行われます)。これで、C# のコードは次のようになっているはずです。

   [!code-csharp[ExpenseIt#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/MainWindow.xaml.cs?highlight=21)]

## <a name="add-files-to-the-application"></a>ファイルをアプリケーションに追加する

このセクションでは、アプリケーションに 2 つのページと 1 つのイメージを追加します。

1. 新しいページをプロジェクトに追加し、名前を *`ExpenseItHome.xaml`* に設定します。

   1. **ソリューション エクスプローラー**で、 **`ExpenseIt`** プロジェクト ノードを右クリックして、 **[追加]**  >  **[ページ]** を選択します。

   1. **[新しい項目の追加]** ダイアログでは、 **[ページ (WPF)]** テンプレートが既に選択されています。 名前に「 **`ExpenseItHome`** 」と入力し、 **[追加]** を選択します。

    このページが、アプリケーションの起動時に表示される最初のページになります。 経費報告書の表示対象として選択するユーザーの一覧が表示されます。

1. *`ExpenseItHome.xaml`* を開きます。

1. <xref:System.Windows.Controls.Page.Title%2A> を "`ExpenseIt - Home`" に設定します。

1. `DesignHeight` を 350 ピクセルに設定し、`DesignWidth` を 500 ピクセルに設定します。

    XAML は、Visual Basic では次のようになります。

    [!code-xaml[ExpenseIt#6_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml#6_a)]

    C# では次のようになります。

    [!code-xaml[ExpenseIt#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml#6)]

1. *MainWindow.xaml* を開きます。

1. <xref:System.Windows.Navigation.NavigationWindow.Source%2A> プロパティを <xref:System.Windows.Navigation.NavigationWindow> 要素に追加し、それを "`ExpenseItHome.xaml`" に設定します。

    これにより、 *`ExpenseItHome.xaml`* が、アプリケーションの起動時に最初に開くページとして設定されます。

    Visual Basic での XAML の例:

    [!code-xaml[ExpenseIt#7_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml#7_a)]

    C# の場合:

    [!code-xaml[ExpenseIt#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/MainWindow.xaml#7)]

   > [!TIP]
   > また、 **[プロパティ]** ウィンドウの **[Miscellaneous]** カテゴリで、 **[Source]** プロパティを設定することもできます。
   >
   > ![[プロパティ] ウィンドウでの Source プロパティ](./media/properties-source.png)

1. 別の新しい WPF ページをプロジェクトに追加し、*ExpenseReportPage.xaml* という名前にします。

   1. **ソリューション エクスプローラー**で、 **`ExpenseIt`** プロジェクト ノードを右クリックして、 **[追加]**  >  **[ページ]** を選択します。

   1. **[新しい項目の追加]** ダイアログで、 **[ページ (WPF)]** テンプレートを選択します。 名前に「**ExpenseReportPage**」と入力し、 **[追加]** を選択します。

    このページには、 **`ExpenseItHome`** ページで選択されたユーザーの経費報告書が表示されます。

1. *ExpenseReportPage.xaml*を開きます。

1. <xref:System.Windows.Controls.Page.Title%2A> を "`ExpenseIt - View Expense`" に設定します。

1. `DesignHeight` を 350 ピクセルに設定し、`DesignWidth` を 500 ピクセルに設定します。

    *ExpenseReportPage.xaml* は、Visual Basic では次のようになります。

    [!code-xaml[ExpenseIt#4_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml#4_a)]

    C# では次のようになります。

    [!code-xaml[ExpenseIt#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml#4)]

1. *ExpenseItHome.xaml.vb* と *ExpenseReportPage.xaml.vb* を開くか、または *ExpenseItHome.xaml.cs* と *ExpenseReportPage.xaml.cs* を開きます。

    新しいページ ファイルを作成すると、Visual Studio によってその "*分離コード*" ファイルが自動的に作成されます。 これらの分離コード ファイルでは、ユーザー入力に対応するためのロジックを処理します。

    **`ExpenseItHome`** のコードは次のようになります。

    [!code-csharp[ExpenseIt#2_5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml.cs#2_5)]

    [!code-vb[ExpenseIt#2_5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml.vb#2_5)]

    **ExpenseReportPage** は次のようになります。

    [!code-csharp[ExpenseIt#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml.cs#5)]

    [!code-vb[ExpenseIt#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml.vb#5)]

1. *watermark.png* という名前の画像をプロジェクトに追加します。 独自の画像を作成したり、サンプル コードからファイルをコピーしたり、[microsoft/WPF-Samples](https://raw.githubusercontent.com/microsoft/WPF-Samples/master/Getting%20Started/WalkthroughFirstWPFApp/csharp/watermark.png) GitHub リポジトリから取得したりすることができます。

    1. プロジェクト ノードを右クリックし、 **[追加]**  >  **[既存の項目]** を選択するか、**Shift** + **Alt** + **A** キーを押します。

    2. **[Add Existing Item]\(既存項目の追加\)** ダイアログで、ファイル フィルターを **[すべてのファイル]** または **[画像ファイル]** に設定し、使用する画像ファイルを参照して、 **[追加]** を選択します。

## <a name="build-and-run-the-application"></a>アプリケーションのビルドと実行

1. アプリケーションをビルドして実行するには、**F5** キーを押すか、 **[デバッグ]** メニューの **[デバッグの開始]** を選択します。

    <xref:System.Windows.Navigation.NavigationWindow> ボタンが含まれるアプリケーションは、次の図のようになります。

    ![ビルドして実行した後のアプリケーション。](./media/walkthrough-my-first-wpf-desktop-application/build-run-application.png)

2. アプリケーションを閉じて Visual Studio に戻ります。

## <a name="create-the-layout"></a>レイアウトを作成する

レイアウトを使用すると、順序付けされた方法で UI 要素を配置できます。また、UI のサイズが変更された場合の要素のサイズと位置が管理されます。 通常、レイアウトを作成するには、次のいずれかのレイアウト コントロールを使用します。

- <xref:System.Windows.Controls.Canvas> - キャンバス領域に対する相対座標を使用して子要素を明示的に配置する領域を定義します。
- <xref:System.Windows.Controls.DockPanel> - 子要素を互いに水平方向または垂直方向に整列する領域を定義します。
- <xref:System.Windows.Controls.Grid> - 行と列で構成される柔軟性のあるグリッド領域を定義します。
- <xref:System.Windows.Controls.StackPanel> - 子要素を水平方向または垂直方向の単一行に整列します。
- <xref:System.Windows.Controls.VirtualizingStackPanel> - 水平方向または垂直方向の単一行でコンテンツを整列し、仮想化します。
- <xref:System.Windows.Controls.WrapPanel> - 左から右へ順に子要素を配置し、ボックスの端で改行してコンテンツを次の行へ送ります。 後続の配置は、Orientation プロパティの値に応じて、上から下または右から左に向かって行われます。

これらの各レイアウト コントロールでは、その子要素に対する特定の種類のレイアウトがサポートされています。 `ExpenseIt` のページはサイズの変更が可能で、各ページの要素は縦にも横にも他の要素と揃えられます。 この例では、アプリケーションのレイアウト要素として <xref:System.Windows.Controls.Grid> を使用します。

> [!TIP]
> <xref:System.Windows.Controls.Panel> 要素の詳細については、「[パネルの概要](../controls/panels-overview.md)」を参照してください。 レイアウトの詳細については、「[レイアウト](../advanced/layout.md)」を参照してください。

このセクションでは、 *`ExpenseItHome.xaml`* の <xref:System.Windows.Controls.Grid> に列と行の定義を追加して、10 ピクセルのマージンを持つ 3 行 1 列のテーブルを作成します。

1. *`ExpenseItHome.xaml`* で、<xref:System.Windows.Controls.Grid> 要素の <xref:System.Windows.FrameworkElement.Margin%2A> プロパティを "10,0,10,10" に設定します。これは、左、上、右、下の余白に対応しています。

   ```xaml
   <Grid Margin="10,0,10,10">
   ```

   > [!TIP]
   > また、 **[プロパティ]** ウィンドウの **[レイアウト]** カテゴリで、**Margin** の値を設定することもできます。
   >
   > ![プロパティ ウィンドウでの余白の値](./media/properties-margin.png)

2. <xref:System.Windows.Controls.Grid> タグの間に次の XAML を追加して、行と列の定義を作成します。

    [!code-xaml[ExpenseIt#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#8)]

    2 行の <xref:System.Windows.Controls.RowDefinition.Height%2A> は <xref:System.Windows.GridLength.Auto%2A> に設定されます。つまり、行のサイズは、行の内容に基づいて設定されます。 既定の <xref:System.Windows.Controls.RowDefinition.Height%2A> は <xref:System.Windows.GridUnitType.Star> のサイズ設定です。これは、行の高さが使用可能な領域の加重比率であることを意味します。 たとえば、2 つの行それぞれの <xref:System.Windows.Controls.RowDefinition.Height%2A> が "*" の場合、各行の高さは、使用可能なスペースの半分になります。

    <xref:System.Windows.Controls.Grid> は次の XAML のようになっているはずです。

    [!code-xaml[ExpenseIt#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#9)]

## <a name="add-controls"></a>コントロールを追加する

このセクションでは、ホームページの UI を更新して、ユーザーの一覧が表示されるようにします。ここで、経費報告書を表示するユーザーを 1 人選択します。 コントロールとは、ユーザーがアプリケーションと対話できるようにする UI オブジェクトのことです。 詳しくは、「 [コントロール](../controls/index.md)」をご覧ください。

この UI を作成するには、次の要素を *`ExpenseItHome.xaml`* に追加します。

- <xref:System.Windows.Controls.ListBox> (個人の一覧用)。
- <xref:System.Windows.Controls.Label> (一覧のヘッダー用)。
- <xref:System.Windows.Controls.Button> (クリックし、一覧で選択した個人の経費報告書を表示するため)。

各コントロールは、<xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> 添付プロパティを設定することで、<xref:System.Windows.Controls.Grid> の行に配置されます。 添付プロパティについて詳しくは、「[添付プロパティの概要](../advanced/attached-properties-overview.md)」をご覧ください。

1. *`ExpenseItHome.xaml`* で、<xref:System.Windows.Controls.Grid> タグの間のどこかに次の XAML を追加します。

   [!code-xaml[ExpenseIt#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt4/ExpenseItHome.xaml#10)]

   > [!TIP]
   > コントロールを **[ツールボックス]** ウィンドウからデザイン ウィンドウにドラッグし、 **[プロパティ]** ウィンドウでプロパティを設定することよって、コントロールを作成することもできます。

2. アプリケーションをビルドして実行します。

    次の図では、作成したコントロールを示します。

![名前の一覧が表示されている、ExpenseIt サンプルのスクリーンショット](./media/walkthrough-my-first-wpf-desktop-application/add-application-controls.png)

## <a name="add-an-image-and-a-title"></a>画像とタイトルを追加する

このセクションでは、画像とページ タイトルでホーム ページの UI を更新します。

1. *`ExpenseItHome.xaml`* で、<xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> に、<xref:System.Windows.Controls.ColumnDefinition.Width%2A> が 230 ピクセルで固定された新しい列を追加します。

    [!code-xaml[ExpenseIt#11](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=2#NewColumn)]

2. <xref:System.Windows.Controls.Grid.RowDefinitions%2A> に別の行を追加します。全部で 4 行になります。

    [!code-xaml[ExpenseIt#11b](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=2#NewRows)]

3. 3 つの各コントロール (Border、ListBox、Button) で、<xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> プロパティを 1 に設定して、コントロールを 2 列目に移動します。

4. 3 つの各コントロール (Border、ListBox、Button) と Border 要素の <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> の値を 1 だけインクリメントして、各コントロールを 1 行下に移動します。

   3 つのコントロールの XAML は、次のようになります。

    [!code-xaml[ExpenseIt#12](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#12)]

5. `<Grid>` タグと `</Grid>` タグの間のどこかに次の XAML を追加して、<xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> プロパティを *watermark.png* 画像ファイルに設定します。

    [!code-xaml[ExpenseIt#14](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#14)]

6. <xref:System.Windows.Controls.Border> 要素の前に、"View Expense Report" という内容の <xref:System.Windows.Controls.Label> を追加します。 このラベルはページのタイトルです。

    [!code-xaml[ExpenseIt#13](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#13)]

7. アプリケーションをビルドして実行します。

次の図では、追加した結果を示します。

![新しい背景画像とページ タイトルが表示されている ExpenseIt サンプルのスクリーンショット](./media/walkthrough-my-first-wpf-desktop-application/add-application-image-title.png)

## <a name="add-code-to-handle-events"></a>イベントを処理するコードを追加する

1. *`ExpenseItHome.xaml`* で、<xref:System.Windows.Controls.Button> 要素に <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーを追加します。 詳細については、「[方法:単純なイベント ハンドラーを作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100))」を参照してください。

    [!code-xaml[ExpenseIt#15](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml#15)]

2. *`ExpenseItHome.xaml.vb`* または *`ExpenseItHome.xaml.cs`* を開きます。

3. 次のコードを `ExpenseItHome` クラスに追加して、ボタン クリック イベント ハンドラーを追加します。 イベント ハンドラーによって、**ExpenseReportPage** ページが開かれます。

    [!code-csharp[ExpenseIt#16](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml.cs#16)]
    [!code-vb[ExpenseIt#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt6/ExpenseItHome.xaml.vb#16)]

## <a name="create-the-ui-for-expensereportpage"></a>ExpenseReportPage の UI を作成する

*ExpenseReportPage.xaml* には、 **`ExpenseItHome`** ページで選択された個人の経費報告書が表示されます。 このセクションでは、**ExpenseReportPage** ページの UI を作成します。 また、さまざまな UI 要素に背景と塗りつぶしの色も追加します。

1. *ExpenseReportPage.xaml*を開きます。

2. <xref:System.Windows.Controls.Grid> タグの間に次の XAML を追加します。

    [!code-xaml[ExpenseIt#17](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseReportPage.xaml#17)]

    この UI は、<xref:System.Windows.Controls.DataGrid> にレポート データが表示される点を除き、 *`ExpenseItHome.xaml`* と似ています。

3. アプリケーションをビルドして実行します。

4. **[View]** ボタンを選択します。

    経費明細書ページが表示されます。 戻るナビゲーション ボタンが有効になっていることにも注意してください。

*ExpenseReportPage.xaml* に追加された UI 要素を次の図に示します。

![ExpenseReportPage に作成した UI が表示されている ExpenseIt サンプルのスクリーンショット。](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

## <a name="style-controls"></a>スタイル コントロール

多くの場合、UI では、要素の種類が同じであれば、外観もすべて同じになります。 UI では、複数の要素間で外観を再利用できるように、[スタイル](../../../desktop-wpf/fundamentals/styles-templates-overview.md)が使用されます。 スタイルの再利用性により、XAML の作成と管理が簡略化されます。 このセクションでは、これまでの手順で定義した要素ごとの属性を、スタイルに置き換えます。

1. *Application.xaml* または *App.xaml* を開きます。

2. <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> タグの間に次の XAML を追加します。

    [!code-xaml[ExpenseIt#18](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/App.xaml#18)]

    この XAML は、次のスタイルを追加します。

    - `headerTextStyle`:ページ タイトルの <xref:System.Windows.Controls.Label> の書式を設定します。

    - `labelStyle`:<xref:System.Windows.Controls.Label> コントロールの書式を設定します。

    - `columnHeaderStyle`:<xref:System.Windows.Controls.Primitives.DataGridColumnHeader> の書式を設定します。

    - `listHeaderStyle`:リスト ヘッダーの <xref:System.Windows.Controls.Border> コントロールの書式を設定します。

    - `listHeaderTextStyle`:リスト ヘッダーの <xref:System.Windows.Controls.Label> の書式を設定します。

    - `buttonStyle`:`ExpenseItHome.xaml` で <xref:System.Windows.Controls.Button> の書式を設定します。

    スタイルはリソースであり、<xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> プロパティ要素の子であることに注意してください。 ここでは、スタイルはアプリケーション内のすべての要素に適用されます。 .NET アプリでリソースを使用する例については、[アプリケーション リソースの使用](../advanced/how-to-use-application-resources.md)に関する記事を参照してください。

3. *`ExpenseItHome.xaml`* で、<xref:System.Windows.Controls.Grid> 要素の間のすべてを次の XAML に置き換えます。

    [!code-xaml[ExpenseIt#19](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseItHome.xaml#19)]

    各コントロールの外観を定義する <xref:System.Windows.VerticalAlignment> や <xref:System.Windows.Media.FontFamily> などのプロパティは、これらのスタイルを適用することで、削除されて置き換えられます。 たとえば、"View Expense Report" という <xref:System.Windows.Controls.Label> には、`headerTextStyle` が適用されます。

4. *ExpenseReportPage.xaml*を開きます。

5. <xref:System.Windows.Controls.Grid> 要素の間のすべてを、次の XAML に置き換えます。

    [!code-xaml[ExpenseIt#20](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseReportPage.xaml#20)]

    この XAML では、スタイルが <xref:System.Windows.Controls.Label> 要素と <xref:System.Windows.Controls.Border> 要素に追加されます。

6. アプリケーションをビルドして実行します。 ウィンドウの外観は、以前と同じです。

    ![前回のセクションと同じ外観の ExpenseIt サンプルのスクリーンショット。](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

7. アプリケーションを閉じて Visual Studio に戻ります。

## <a name="bind-data-to-a-control"></a>データをコントロールにバインドする

このセクションでは、さまざまなコントロールにバインドされる XML データを作成します。

1. *`ExpenseItHome.xaml`* で、開始 <xref:System.Windows.Controls.Grid> 要素の後に次の XAML を追加して、各個人のデータを含む <xref:System.Windows.Data.XmlDataProvider> を作成します。

    [!code-xaml[ExpenseIt#23](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,16-40,49)]

    データは <xref:System.Windows.Controls.Grid> リソースとして作成されます。 通常、このデータはファイルとして読み込まれますが、説明を簡単にするため、データをインラインで追加します。

2. `<Grid.Resources>` 要素内の `<XmlDataProvider>` 要素の後に、<xref:System.Windows.Controls.ListBox> でのデータの表示方法を定義する次の `<xref:System.Windows.DataTemplate>` 要素を追加します。

    [!code-xaml[ExpenseIt#24](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,43-46,49)]

    データ テンプレートについて詳しくは、「[データ テンプレートの概要](../data/data-templating-overview.md)」をご覧ください。

3. 既存の <xref:System.Windows.Controls.ListBox> を次の XAML に置き換えます。

    [!code-xaml[ExpenseIt#25](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#25)]

    この XAML では、<xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティがデータ ソースにバインドされ、データ テンプレートが <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> として適用されます。

## <a name="connect-data-to-controls"></a>コントロールにデータを接続する

次に、 **`ExpenseItHome`** ページで選択された名前を取得し、それを **ExpenseReportPage** のコンストラクターに渡すコードを追加します。 **ExpenseReportPage** では、渡された項目を使用してデータ コンテキストが設定されます。それが、*ExpenseReportPage.xaml* で定義されているコントロールのバインド先になります。

1. *ExpenseReportPage.xaml.vb* または *ExpenseReportPage.xaml.cs*を開きます。

2. オブジェクトを取得するコンストラクターを追加して、選択した個人の経費報告書データを渡せるようにします。

    [!code-csharp[ExpenseIt#26](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseReportPage.xaml.cs#26)]
    [!code-vb[ExpenseIt#26](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseReportPage.xaml.vb#26)]

3. *`ExpenseItHome.xaml.vb`* または *`ExpenseItHome.xaml.cs`* を開きます。

4. 選択された個人の経費報告書データを渡す新しいコンストラクターを呼び出すように、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーを変更します。

    [!code-csharp[ExpenseIt#27](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml.cs#27)]
    [!code-vb[ExpenseIt#27](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseItHome.xaml.vb#27)]

## <a name="style-data-with-data-templates"></a>データ テンプレートを使用したデータのスタイル設定

このセクションでは、データ テンプレートを使用して、データ バインド リスト内の各項目の UI を更新します。

1. *ExpenseReportPage.xaml*を開きます。

2. "Name" および "Department" の <xref:System.Windows.Controls.Label> 要素の内容を、適切なデータ ソース プロパティにバインドします。 データ バインディングの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。

    [!code-xaml[ExpenseIt#31](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#31)]

3. 開始の <xref:System.Windows.Controls.Grid> 要素の後に、経費報告書データの表示方法を定義する、次のデータ テンプレートを追加します。

    [!code-xaml[ExpenseIt#30](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#30)]

4. <xref:System.Windows.Controls.DataGrid> 要素の下の <xref:System.Windows.Controls.DataGridTextColumn> 要素を <xref:System.Windows.Controls.DataGridTemplateColumn> に置き換えて、それらにテンプレートを適用します。

    [!code-xaml[ExpenseIt#32](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#32)]

5. アプリケーションをビルドして実行します。

6. 個人を選択し、 **[View]** ボタンを選択します。

次の図には、コントロール、レイアウト、スタイル、データ バインディング、データ テンプレートが適用された `ExpenseIt` アプリケーションの両方のページが示されています。

![名前の一覧と経費報告書が表示されているアプリの両方のページ。](./media/walkthrough-my-first-wpf-desktop-application/application-data-templates.png)

> [!NOTE]
> このサンプルは、WPF の特定の機能について説明するものであり、セキュリティ、ローカライズ、アクセシビリティなどのベスト プラクティスには従っていません。 WPF と .NET アプリの開発に関する包括的なベスト プラクティスについては、次のトピックをご覧ください。
>
> - [ユーザー補助](../../ui-automation/accessibility-best-practices.md)
> - [セキュリティ](../security-wpf.md)
> - [WPF のグローバリゼーションとローカライズ](../advanced/wpf-globalization-and-localization-overview.md)
> - [WPF のパフォーマンス](../advanced/optimizing-wpf-application-performance.md)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Windows Presentation Foundation (WPF) を使用して UI を作成するためのいくつかの手法について学習しました。 データ バインドされた .NET アプリの構成要素についての基本を理解することもできました。 WPF のアーキテクチャおよびプログラミング モデルの詳細については、次のトピックを参照してください。

- [WPF のアーキテクチャ](../advanced/wpf-architecture.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [依存関係プロパティの概要](../advanced/dependency-properties-overview.md)
- [レイアウト](../advanced/layout.md)

アプリケーションの作成の詳細については、次のトピックを参照してください。

- [アプリケーション開発](../app-development/index.md)
- [コントロール](../controls/index.md)
- [データバインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [グラフィックスとマルチメディア](../graphics-multimedia/index.md)
- [WPF のドキュメント](../advanced/documents-in-wpf.md)

## <a name="see-also"></a>関連項目

- [パネルの概要](../controls/panels-overview.md)
- [データ テンプレートの概要](../data/data-templating-overview.md)
- [WPF アプリケーションのビルド](../app-development/building-a-wpf-application-wpf.md)
- [スタイルおよびテンプレート](../controls/styles-and-templates.md)
