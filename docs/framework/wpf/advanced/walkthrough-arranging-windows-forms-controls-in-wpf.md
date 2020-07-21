---
title: WPF で Windows フォーム コントロールを配置する
titleSuffix: ''
ms.date: 04/03/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- arranging controls [WPF]
ms.assetid: a1db8049-15c7-45d6-ae3d-36a6735cb848
ms.openlocfilehash: 5cf48b347be2d0ca6a9b55f3e19affb8b471aa2b
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095100"
---
# <a name="walkthrough-arranging-windows-forms-controls-in-wpf"></a>チュートリアル: WPF での Windows フォーム コントロールの配置

このチュートリアルでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト機能を使用して、ハイブリッド アプリケーションで Windows フォーム コントロールを配置する方法について説明します。

このチュートリアルでは、以下のタスクを行います。

- プロジェクトの作成。
- 既定のレイアウト設定の使用。
- コンテンツに合わせたサイズの変更。
- 絶対配置の使用。
- サイズの明示的な指定。
- レイアウト プロパティの設定。
- z オーダーの制限の理解。
- ドッキング。
- 可視性の設定。
- 伸縮しないコントロールのホスト。
- スケーリング。
- 回転。
- パディングとマージンの設定。
- 動的レイアウト コンテナーの使用。

このチュートリアルで示すタスクの完全なコード一覧については、[WPF での Windows フォーム コントロールの配置のサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WpfLayoutHostingWfWithXaml)を参照してください。

完了すると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションでの Windows フォーム レイアウトの機能について理解できます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを完了するには Visual Studio が必要です。

## <a name="creating-the-project"></a>プロジェクトの作成

プロジェクトを作成して設定するには、次の手順を実行します。

1. `WpfLayoutHostingWf` という名前の WPF アプリケーション プロジェクトを作成します。

2. ソリューション エクスプローラーで、次のアセンブリへの参照を追加します。

    - WindowsFormsIntegration
    - System.Windows.Forms
    - System.Drawing

3. *MainWindow.xaml* をダブルクリックして、XAML ビューで開きます。

4. <xref:System.Windows.Window> 要素に、次の Windows フォーム名前空間マッピングを追加します。

    ```xaml
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"
    ```

5. <xref:System.Windows.Controls.Grid> 要素で <xref:System.Windows.Controls.Grid.ShowGridLines%2A> プロパティを `true` に設定し、5 つの行と 3 つの列を定義します。

     [!code-xaml[WpfLayoutHostingWfWithXaml#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#2)]

## <a name="using-default-layout-settings"></a>既定のレイアウト設定の使用

既定で、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、ホストされている Windows フォーム コントロールのレイアウトが処理されます。

既定のレイアウト設定を使用するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#3)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 Windows フォーム <xref:System.Windows.Forms.Button?displayProperty=nameWithType> コントロールが <xref:System.Windows.Controls.Canvas> に表示されます。 ホストされているコントロールは、そのコンテンツに基づいてサイズが変更され、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は、ホストされているコントロールに合わせてサイズが変更されます。

## <a name="sizing-to-content"></a>コンテンツに合わせたサイズの変更

<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を使用すると、ホストされているコントロールは、そのコンテンツが適切に表示されるように確実にサイズが変更されます。

コンテンツに合わせてサイズを変更するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#4)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 2 つの新しいボタン コントロールは、長いテキスト文字列と大きなフォント サイズが適切に表示されるようにサイズが変更され、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は、ホストされるコントロールに合わせてサイズが変更されます。

## <a name="using-absolute-positioning"></a>絶対配置の使用

絶対配置を使用すると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素をユーザー インターフェイス (UI) の任意の場所に配置できます。

絶対配置を使用するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#5](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#5)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は、グリッド セルの上端から 20 ピクセル、左端から 20 ピクセルの位置に配置されます。

## <a name="specifying-size-explicitly"></a>サイズの明示的な指定

<xref:System.Windows.FrameworkElement.Width%2A> および <xref:System.Windows.FrameworkElement.Height%2A> プロパティを使用して、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素のサイズを指定できます。

サイズを明示的に指定するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#6](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#6)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は幅 50 ピクセル、高さ 70 ピクセルのサイズに設定されています。これは既定のレイアウト設定よりも小さいサイズです。 Windows フォーム コントロールのコンテンツは、それに応じて再配置されます。

## <a name="setting-layout-properties"></a>レイアウト プロパティの設定

ホストされているコントロールには、常に、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素のプロパティを使用してレイアウト関連のプロパティを設定します。 ホストされているコントロールで直接レイアウト プロパティを設定すると、予期しない結果になります。

 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でホストされているコントロールにレイアウト関連プロパティを設定しても何も起こりません。

ホストされているコントロールでプロパティを設定した場合の結果を確認するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#7](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#7)]

2. **ソリューション エクスプローラー**で、*MainWindow.xaml.vb* または *MainWindow.xaml.cs* をダブルクリックして、コード エディターで開きます。

3. 次のコードを `MainWindow` クラス定義にコピーします。

     [!code-csharp[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#101)]
     [!code-vb[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#101)]

4. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。

5. **[Click me]\(ここをクリック\)** ボタンをクリックします。 `button1_Click` イベント ハンドラーによって、ホストされているコントロールに <xref:System.Windows.Forms.Control.Top%2A> および <xref:System.Windows.Forms.Control.Left%2A> プロパティが設定されます。 これにより、ホストされているコントロールが <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素内に再配置されます。 ホストは同じ画面領域を維持しますが、ホストされているコントロールはクリップされます。 そうではなく、ホストされているコントロールが常に <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素に合わせてサイズが変更されるようにする必要があります。

## <a name="understanding-z-order-limitations"></a>z オーダーの制限の理解

可視の <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は常に他の WPF 要素の上に描画され、z オーダーの影響を受けません。 この Z オーダーの動作を確認するために、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#8](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#8)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は label 要素の上に描画されます。

## <a name="docking"></a>ドッキング

<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のドッキングをサポートします。 ホストされているコントロールを <xref:System.Windows.Controls.DockPanel> 要素にドッキングするように <xref:System.Windows.Controls.DockPanel.Dock%2A> 添付プロパティを設定します。

ホストされているコントロールをドッキングするには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#9](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#9)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は、<xref:System.Windows.Controls.DockPanel> 要素の右側にドッキングされます。

## <a name="setting-visibility"></a>可視性の設定

<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素に <xref:System.Windows.UIElement.Visibility%2A> プロパティを設定することで、Windows フォーム コントロールを非表示にしたり折りたたんだりすることができます。 コントロールを非表示にすると、そのコントロールは表示されませんが、レイアウト空間は使用されます。 コントロールを折りたたむと、そのコントロールは表示されず、レイアウト空間も使用されません。

ホストされているコントロールの可視性を設定するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#10](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#10)]

2. *MainWindow.xaml.vb* または *MainWindow.xaml.cs* で、次のコードをクラス定義にコピーします。

     [!code-csharp[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#102)]
     [!code-vb[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#102)]

3. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。

4. **[Click to make invisible]\(クリックして非表示にする\)** ボタンをクリックして <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を非表示にします。

5. **[Click to collapse]\(クリックして折りたたむ\)** ボタンをクリックして、レイアウトから <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を完全に非表示にします。 Windows フォーム コントロールが折りたたまれ、周りの要素が再配置されて、そのスペースが使用されます。

## <a name="hosting-a-control-that-does-not-stretch"></a>伸縮しないコントロールのホスト

一部の Windows フォーム コントロールは、サイズが固定され、レイアウト内の使用可能なスペースに合わせて伸縮しません。 たとえば、<xref:System.Windows.Forms.MonthCalendar> コントロールでは、固定されたスペースに月が表示されます。

伸縮しないコントロールをホストするには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#11)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素はグリッド行で中央揃えになりますが、使用可能なスペースに合わせて伸縮されることはありません。 ウィンドウが十分に大きい場合は、ホストされている <xref:System.Windows.Forms.MonthCalendar> コントロールによって 2 か月以上の月が表示される場合もありますが、これらは行内で中央揃えになります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト エンジンによって、使用可能なスペースに合わせてサイズを変更できない要素が中央揃えにされます。

## <a name="scaling"></a>スケーリング

WPF 要素と異なり、ほとんどの Windows フォーム コントロールは継続的にスケーリングすることはできません。 カスタムのスケーリングを提供するには、<xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A?displayProperty=nameWithType> メソッドをオーバーライドします。

既定の動作を使用してホストされているコントロールをスケーリングするには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#12)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 ホストされているコントロールとその周りの要素は、0.5 倍でスケーリングされます。 ただし、ホストされているコントロールのフォントはスケーリングされません。

<!-- This could use an example of custom scaling. -->

## <a name="rotating"></a>回転

WPF 要素とは異なり、Windows フォーム コントロールは回転をサポートしません。 回転変換が適用されても、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は WPF の他の要素とともに回転しません。 回転値が 180 度の場合を除き、<xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> イベントが発生します。

ハイブリッド アプリケーションでの回転の効果を確認するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#13)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 ホストされているコントロールは回転しませんが、その周りの要素は 180 度の角度で回転します。 要素を表示するためにウィンドウのサイズを変更する必要がある場合があります。

## <a name="setting-padding-and-margins"></a>パディングとマージンの設定

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウトのパディングとマージンは、Windows フォーム のパディングとマージンと同様です。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素に <xref:System.Windows.Controls.Control.Padding%2A> および <xref:System.Windows.FrameworkElement.Margin%2A> プロパティを設定するだけです。

ホストされているコントロールのパディングとマージンを設定するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#14)]
    [!code-xaml[WpfLayoutHostingWfWithXaml#15](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#15)]

2. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 パディングとマージンの設定が、Windows フォーム で適用される場合と同じように、ホストされている Windows フォーム コントロールに適用されます。

## <a name="using-dynamic-layout-containers"></a>動的レイアウト コンテナーの使用

Windows フォームには、<xref:System.Windows.Forms.FlowLayoutPanel> と <xref:System.Windows.Forms.TableLayoutPanel> という 2 つの動的レイアウト コンテナーが用意されています。 これらのコンテナーは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウトで使用することもできます。

動的レイアウト コンテナーを使用するには、次の手順を実行します。

1. 次の XAML を <xref:System.Windows.Controls.Grid> 要素にコピーします。

     [!code-xaml[WpfLayoutHostingWfWithXaml#16](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#16)]

2. *MainWindow.xaml.vb* または *MainWindow.xaml.cs* で、次のコードをクラス定義にコピーします。

     [!code-csharp[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#103)]
     [!code-vb[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#103)]

3. コンストラクター内の `InitializeFlowLayoutPanel` メソッドに呼び出しを追加します。

     [!code-csharp[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#104)]
     [!code-vb[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#104)]

4. <kbd>F5</kbd> キーを押してアプリケーションをビルドし、実行します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を使用すると、<xref:System.Windows.Controls.DockPanel> に合わせてサイズが変更され、<xref:System.Windows.Forms.FlowLayoutPanel> を使用すると、既定の <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> にその子コントロールが配置されます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [WindowsFormsHost 要素のレイアウトに関する考慮事項](layout-considerations-for-the-windowsformshost-element.md)
- [WPF での Windows フォーム コントロールの配置のサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WpfLayoutHostingWfWithXaml)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
