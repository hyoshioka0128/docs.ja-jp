---
title: コントロール
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], about WPF controls
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
ms.openlocfilehash: 2aab0fc8adaf17a8e9820a6269a740ef09540cda
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646482"
---
# <a name="controls"></a>コントロール
<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Label><xref:System.Windows.Controls.TextBox>、<xref:System.Windows.Controls.Menu> や <xref:System.Windows.Controls.ListBox> など、ほとんどの Windows アプリケーションで使用される共通の UI コンポーネントが多数付属しています。 これまで、これらのオブジェクトはコントロールと呼ばれてきました。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK では、アプリケーションで表示可能なオブジェクトを表すクラスに、広義で「コントロール」という用語が使用され続けていますが、クラスは、表示可能な部分を持つために <xref:System.Windows.Controls.Control> クラスを継承する必要がないことに注意してください。 <xref:System.Windows.Controls.Control> クラスを継承するクラスには、<xref:System.Windows.Controls.ControlTemplate> が含まれます。これを使用すると、コントロールのコンシューマーは、新しいサブクラスを作成しなくても、コントロールの外観を大幅に変更できます。  このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でのコントロール (<xref:System.Windows.Controls.Control> クラスを継承するものとそうでないものの両方) の一般的な使用方法について説明します。  

<a name="creating_an_instance_of_a_control"></a>
## <a name="creating-an-instance-of-a-control"></a>コントロールのインスタンスの作成  
 アプリケーションにコントロールを追加するには、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] またはコードのいずれかを使用します。  次の例では、ユーザーに姓と名の入力を求める単純なアプリケーションの作成方法を示します。  この例では、ラベル 2 個、テキスト ボックス 2 個、ボタン 2 個の合計 6 個のコントロールを [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で作成します。 どのコントロールも同じ方法で作成できます。  
  
 [!code-xaml[ControlsOverview#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 次の例では、同じアプリケーションをコードで作成します。 簡略化するために、<xref:System.Windows.Controls.Grid> である `grid1` の作成はサンプルから除外しています。 `grid1` には、上記の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の例で示したのと同じ列と行が定義されています。  
  
 [!code-csharp[ControlsOverview#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)]
 [!code-vb[ControlsOverview#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>
## <a name="changing-the-appearance-of-a-control"></a>コントロールの外観の変更  
 通常は、アプリケーションの外観に合わせてコントロールの外観を変更します。 コントロールの外観を変更するには、目的に応じて、次のいずれかの手順を実行します。  
  
- コントロールのプロパティ値を変更します。  
  
- コントロールに <xref:System.Windows.Style> を作成します。  
  
- コントロールに新しい <xref:System.Windows.Controls.ControlTemplate> を作成します。  
  
### <a name="changing-a-controls-property-value"></a>コントロールのプロパティ値の変更  
 多くのコントロールには、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> など、コントロールの外観を変更するプロパティがあります。 値プロパティは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] とコードで設定できます。 次の例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.FontSize%2A>、<xref:System.Windows.Controls.Control.FontWeight%2A> の各プロパティを設定しています。  
  
 [!code-xaml[ControlsOverview#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 次の例では、同じプロパティをコードで設定しています。  
  
 [!code-csharp[ControlsOverview#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)]
 [!code-vb[ControlsOverview#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### <a name="creating-a-style-for-a-control"></a>コントロールのスタイル作成  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、アプリケーションの各インスタンスのさまざまなプロパティを設定する代わりに、<xref:System.Windows.Style> を作成して、コントロールの外観を多数指定する機能があります。 次の例では、アプリケーションの各 <xref:System.Windows.Controls.Button> に適用される <xref:System.Windows.Style> が作成されます。 <xref:System.Windows.Style> の定義は、通常、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では <xref:System.Windows.ResourceDictionary> に定義されます。たとえば、<xref:System.Windows.FrameworkElement> の <xref:System.Windows.FrameworkElement.Resources%2A> プロパティがそれに該当します。  
  
 [!code-xaml[ControlsOverview#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 スタイルにキーを割り当て、そのキーをお使いのコントロールの `Style` プロパティで指定することによって、特定の種類のコントロールのみにスタイルを適用することもできます。  スタイルの詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。  
  
### <a name="creating-a-controltemplate"></a>ControlTemplate の作成  
 <xref:System.Windows.Style> を使用すると、複数のコントロールのプロパティを一度に設定できますが、<xref:System.Windows.Style> の作成だけでできる以上に、<xref:System.Windows.Controls.Control> の外観をカスタマイズしたい場合もあります。 <xref:System.Windows.Controls.Control> クラスを継承するクラスには、<xref:System.Windows.Controls.Control> の構造と外観を定義する、<xref:System.Windows.Controls.ControlTemplate> があります。 <xref:System.Windows.Controls.Control> の <xref:System.Windows.Controls.Control.Template%2A> プロパティはパブリックであるため、<xref:System.Windows.Controls.Control> に既定とは異なる <xref:System.Windows.Controls.ControlTemplate> を付与できます。 一般的に、<xref:System.Windows.Controls.Control> の外観のカスタマイズには、コントロールの継承ではなく、<xref:System.Windows.Controls.Control> に新しい <xref:System.Windows.Controls.ControlTemplate> を指定します。  
  
 よく使用される <xref:System.Windows.Controls.Button> というコントロールについて考えてみます。  <xref:System.Windows.Controls.Button> の主な動作は、ユーザーがクリックしたときに、アプリケーションが一定のアクションを実行することです。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、<xref:System.Windows.Controls.Button> は既定で浮き出し表示の四角形で表されます。  アプリケーションの開発時、ボタンのクリック イベントを処理する <xref:System.Windows.Controls.Button> の動作は利用し、ボタンのプロパティの変更では実現できないボタンの外観の変更を行いたい場合があります。  このような場合には、新しい <xref:System.Windows.Controls.ControlTemplate> を作成します。  
  
 次の例では、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.ControlTemplate> を作成します。  この <xref:System.Windows.Controls.ControlTemplate> では、角が丸くて背景がグラデーションになっている <xref:System.Windows.Controls.Button> が作成されます。  この <xref:System.Windows.Controls.ControlTemplate> には、<xref:System.Windows.Controls.Border.Background%2A> が 2 つの <xref:System.Windows.Media.GradientStop> オブジェクトを持つ <xref:System.Windows.Media.LinearGradientBrush> である <xref:System.Windows.Controls.Border> が含まれています。  最初の <xref:System.Windows.Media.GradientStop> では、データ バインディングを使用して、<xref:System.Windows.Media.GradientStop> の <xref:System.Windows.Media.GradientStop.Color%2A> プロパティがボタンの背景色にバインドされています。  <xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> プロパティを設定すると、その値の色が最初の <xref:System.Windows.Media.GradientStop> として使用されます。 データ バインディングの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。 この例ではまた、<xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> が `true` のときに <xref:System.Windows.Controls.Button> の外観が変更される <xref:System.Windows.Trigger> も作成されています。  
  
 [!code-xaml[ControlsOverview#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xaml[ControlsOverview#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
> この例が正常に動作するには、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> プロパティが <xref:System.Windows.Media.SolidColorBrush> に設定されている必要があります。  
  
<a name="subscribing_to_events"></a>
## <a name="subscribing-to-events"></a>イベントのサブスクライブ  
 コントロールのイベントをサブスクライブするには、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] またはコードを使用できますが、コードではイベントの処理しかできません。  次の例では、<xref:System.Windows.Controls.Button> の `Click` イベントをサブスクライブする方法を示します。  
  
 [!code-xaml[ControlsOverview#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)]
 [!code-vb[ControlsOverview#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 次の例では、<xref:System.Windows.Controls.Button> の `Click` イベントが処理されています。  
  
 [!code-csharp[ControlsOverview#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)]
 [!code-vb[ControlsOverview#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>
## <a name="rich-content-in-controls"></a>コントロールでのリッチ コンテンツ  
 <xref:System.Windows.Controls.Control> クラスを継承するほとんどのクラスには、リッチ コンテンツを格納する容量があります。 たとえば、<xref:System.Windows.Controls.Label> は、文字列、<xref:System.Windows.Controls.Image>、<xref:System.Windows.Controls.Panel> などの任意のオブジェクトを格納できます。  以下のクラスは、リッチ コンテンツをサポートし、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のほとんどのコントロールの基本クラスとして機能します。  
  
- <xref:System.Windows.Controls.ContentControl>-- このクラスを継承するクラスは、<xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.ToolTip> などです。  
  
- <xref:System.Windows.Controls.ItemsControl>-- このクラスを継承するクラスは、<xref:System.Windows.Controls.ListBox>、<xref:System.Windows.Controls.Menu>、<xref:System.Windows.Controls.Primitives.StatusBar> などです。  
  
- <xref:System.Windows.Controls.HeaderedContentControl>-- このクラスを継承するクラスは、<xref:System.Windows.Controls.TabItem>、<xref:System.Windows.Controls.GroupBox>、<xref:System.Windows.Controls.Expander> などです。  
  
- <xref:System.Windows.Controls.HeaderedItemsControl>-- このクラスを継承するクラスは、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.TreeViewItem>、<xref:System.Windows.Controls.ToolBar> などです。  

 これらの基本クラスの詳細については、「[WPF のコンテンツ モデル](wpf-content-model.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [カテゴリ別のコントロール](controls-by-category.md)
- [コントロール ライブラリ](control-library.md)
- [データ テンプレートの概要](../data/data-templating-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [入力](../advanced/input-wpf.md)
- [コマンドを有効にする](../advanced/how-to-enable-a-command.md)
- [チュートリアル: カスタム アニメーション ボタンの作成](walkthroughs-create-a-custom-animated-button.md)
- [コントロールのカスタマイズ](control-customization.md)
