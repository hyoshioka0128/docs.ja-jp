---
title: パネルの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Panel control [WPF], about Panel control
- controls [WPF], Panel
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
ms.openlocfilehash: 7810bfbf4f5bedf51e0797a4b9017f589e0b0a8a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187580"
---
# <a name="panels-overview"></a>パネルの概要
<xref:System.Windows.Controls.Panel> 要素は、要素のレンダリング (サイズ、次元、位置、子コンテンツの配置) を制御するコンポーネントです。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、定義済みの多数の <xref:System.Windows.Controls.Panel> 要素と共に、カスタム <xref:System.Windows.Controls.Panel> 要素の作成機能が提供されています。  
  
 このトピックは、次のセクションで構成されています。  
  
- [パネル クラス](#Panels_view_from_10000_feet)  
  
- [パネルの要素の一般的なメンバー](#Panels_declared_members)  
  
- [派生パネル要素](#Panels_derived_elements)  
  
- [ユーザー インターフェイス パネル](#Panels_main_UI_elements)  
  
- [入れ子になったパネル要素](#Panels_nested_panel_elements)  
  
- [カスタム パネル要素](#Panels_custom_panel_elements)  
  
- [ローカライズ/グローバリゼーション サポート](#Panels_global_localization)  
  
<a name="Panels_view_from_10000_feet"></a>
## <a name="the-panel-class"></a>パネル クラス  
 <xref:System.Windows.Controls.Panel> は、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でのレイアウト サポートを提供するすべての要素の基底クラスです。 派生要素 <xref:System.Windows.Controls.Panel> は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] とコードで要素を配置および整列するために使用されます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、多くの複雑なレイアウトを可能にする派生パネル実装の総合的なスイートが含まれます。 これらの派生クラスは、標準 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] シナリオのほとんどを可能にするプロパティとメソッドを公開します。 ニーズを満たす子整列動作を見つけることができない開発者は、<xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドと <xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドをオーバーライドすることにより、新しいレイアウトを作成できます。 カスタム レイアウト動作の詳細については、「[カスタム パネル要素](#Panels_custom_panel_elements)」を参照してください。  
  
<a name="Panels_declared_members"></a>
## <a name="panel-common-members"></a>パネルの一般的なメンバー  
 すべての <xref:System.Windows.Controls.Panel> 要素では、<xref:System.Windows.FrameworkElement> によって定義されているベースのサイズ変更と配置のプロパティ (<xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.FrameworkElement.LayoutTransform%2A> など) がサポートされています。 <xref:System.Windows.FrameworkElement> によって定義される配置プロパティの詳細については、「[配置、余白、パディングの概要](../advanced/alignment-margins-and-padding-overview.md)」を参照してください。  
  
 <xref:System.Windows.Controls.Panel> では、レイアウトを理解して使用するうえできわめて重要なその他のプロパティが公開されています。 <xref:System.Windows.Controls.Panel.Background%2A> プロパティは、<xref:System.Windows.Media.Brush> で派生パネル要素の境界の間の領域を塗りつぶすために使用されます。 <xref:System.Windows.Controls.Panel.Children%2A> は、<xref:System.Windows.Controls.Panel> を構成する要素の子コレクションを表します。 <xref:System.Windows.Controls.Panel.InternalChildren%2A> は、<xref:System.Windows.Controls.Panel.Children%2A> コレクションの内容に加え、データ バインディングによって生成されるメンバーを表します。 どちらも、親 <xref:System.Windows.Controls.UIElementCollection> 内でホストされている子要素の <xref:System.Windows.Controls.Panel> で構成されます。  
  
 パネルでは、派生 <xref:System.Windows.Controls.Panel> のレイヤー化された順序を実現するために使用される <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> 添付プロパティも公開されています。 パネルの <xref:System.Windows.Controls.Panel.Children%2A> コレクションのメンバーは、<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> の値が大きいものの方が、小さい <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> の値のものより前面に表示されます。 これは、子に同じ座標領域を共有できるようにする <xref:System.Windows.Controls.Canvas> や <xref:System.Windows.Controls.Grid> などのパネルに特に役立ちます。  
  
 また、<xref:System.Windows.Controls.Panel> では <xref:System.Windows.Controls.Panel.OnRender%2A> メソッドも定義されており、これを使用して <xref:System.Windows.Controls.Panel> の既定のプレゼンテーション動作をオーバーライドできます。  
  
#### <a name="attached-properties"></a>アタッチされるプロパティ  
 派生パネル要素は、添付プロパティを広く活用しています。 添付プロパティは、従来の共通言語ランタイム (CLR) プロパティ "ラッパー" を持たない特殊な形式の依存関係プロパティです。 添付プロパティは、下記の例に見られるとおり、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 内に特殊な構文を持ちます。  
  
 添付プロパティの目的の 1 つは、親要素によって実際に定義されたプロパティの一意の値を子要素が格納できるようにすることです。 この機能の応用方法の 1 つは、子要素から親要素に [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] でどのように表示したいかを通知させることであり、これはアプリケーション レイアウトに非常に役立ちます。 詳細については、「[添付プロパティの概要](../advanced/attached-properties-overview.md)」を参照してください。  
  
<a name="Panels_derived_elements"></a>
## <a name="derived-panel-elements"></a>派生パネル要素  
 <xref:System.Windows.Controls.Panel> から多くのオブジェクトが派生されますが、それらのすべてがルート レイアウト プロバイダーとして使用されるわけではありません。 アプリケーションの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 作成専用に設計された 6 つの定義済みパネル クラス (<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.VirtualizingStackPanel>、<xref:System.Windows.Controls.WrapPanel>) があります。  
  
 次の表に各パネル要素でカプセル化されているそれぞれの特殊機能を示します。  
  
|要素名|UI パネル?|説明|  
|------------------|---------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|はい|<xref:System.Windows.Controls.Canvas> 領域に対する座標により子要素を明示的に配置できる領域が定義されています。|  
|<xref:System.Windows.Controls.DockPanel>|はい|子要素を互いに水平方向または垂直方向に整列する領域を定義します。|  
|<xref:System.Windows.Controls.Grid>|はい|列と行で構成されている柔軟なグリッド領域を定義します。 <xref:System.Windows.Controls.Grid> の子要素は、<xref:System.Windows.FrameworkElement.Margin%2A> プロパティを使用して正確に配置できます。|  
|<xref:System.Windows.Controls.StackPanel>|はい|子要素を水平方向または垂直方向の単一行に整列します。|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|いいえ|<xref:System.Windows.Controls.TabControl> でのタブ ボタンのレイアウトが処理されます。|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|いいえ|<xref:System.Windows.Controls.ToolBar> コントロール内のコンテンツが整列されます。|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|いいえ|<xref:System.Windows.Controls.Primitives.UniformGrid> は、グリッド内の子をすべて同じセル サイズで整列するために使用されます。|  
|<xref:System.Windows.Controls.VirtualizingPanel>|いいえ|子コレクションを "仮想化" できるパネルに基本クラスを提供します。|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|はい|水平方向または垂直方向の単一行でコンテンツを整列し、仮想化します。|  
|<xref:System.Windows.Controls.WrapPanel>|はい|<xref:System.Windows.Controls.WrapPanel> では、左から右へ順に子要素が配置され、外側のボックスの端で改行してコンテンツは次の行へ送られます。 後続の配置は、<xref:System.Windows.Controls.WrapPanel.Orientation%2A> プロパティの値に応じて、上から下または右から左に向かって行われます。|  
  
<a name="Panels_main_UI_elements"></a>
## <a name="user-interface-panels"></a>ユーザー インターフェイス パネル  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のシナリオをサポートするために最適化された次の 6 つのパネル クラスがあります。それは、<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.VirtualizingStackPanel>、<xref:System.Windows.Controls.WrapPanel> です。 これらのパネル要素は使いやすく、用途が広く、ほとんどのアプリケーションに対する拡張性があります。  
  
 派生要素 <xref:System.Windows.Controls.Panel> ごとに、サイズ制約の処理方法が異なります。 水平方向または垂直方向での <xref:System.Windows.Controls.Panel> による制約の処理方法を理解することで、レイアウトをより予測しやすくなります。  
  
|**パネル名**|**x 方向**|**y 方向**|  
|--------------------|----------------------|----------------------|  
|<xref:System.Windows.Controls.Canvas>|コンテンツに対する制約あり。|コンテンツに対する制約あり。|  
|<xref:System.Windows.Controls.DockPanel>|制約あり。|制約あり。|  
|<xref:System.Windows.Controls.StackPanel> (垂直方向)|制約あり。|コンテンツに対する制約あり。|  
|<xref:System.Windows.Controls.StackPanel> (水平方向)|コンテンツに対する制約あり。|制約あり。|  
|<xref:System.Windows.Controls.Grid>|制約あり。|制約あり。ただし、<xref:System.Windows.GridUnitType.Auto> が行と列に適用される場合を除きます|  
|<xref:System.Windows.Controls.WrapPanel>|コンテンツに対する制約あり。|コンテンツに対する制約あり。|  
  
 これらの各要素の詳細な説明と使用例を次に示します。  
  
<a name="Panels_overview_Canvas_subsection"></a>
### <a name="canvas"></a>Canvas  
 <xref:System.Windows.Controls.Canvas> 要素を使うと、*x* と *y* の絶対座標に従って、コンテンツの位置を設定できます。 要素は一意の場所に描画できます。または、要素が同じ座標を占める場合、マークアップに表示される順序が要素の描画順序を決定します。  
  
 <xref:System.Windows.Controls.Canvas> を使うと、<xref:System.Windows.Controls.Panel> を最も柔軟にレイアウトできます。 Height および Width プロパティがキャンバスの領域の定義に使用され、内側の要素には、親の <xref:System.Windows.Controls.Canvas> 領域に対する絶対座標が割り当てられます。 4 つの添付プロパティ <xref:System.Windows.Controls.Canvas.Left%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=nameWithType> を使って、<xref:System.Windows.Controls.Canvas> 内のオブジェクトの配置を細かく制御できるので、開発者は画面上で要素の配置と整列を正確に行うことができます。  
  
#### <a name="cliptobounds-within-a-canvas"></a>キャンバス内の ClipToBounds  
 <xref:System.Windows.Controls.Canvas> を使うと、画面の任意の位置に子要素を配置できます。それ自体に定義された <xref:System.Windows.FrameworkElement.Height%2A> および <xref:System.Windows.FrameworkElement.Width%2A> の範囲外の座標でもかまいません。 また、<xref:System.Windows.Controls.Canvas> は子要素のサイズの影響を受けません。 その結果、子要素では親の <xref:System.Windows.Controls.Canvas> の外接する四角形の外側に他の要素を描画できます。 <xref:System.Windows.Controls.Canvas> の既定動作では、親 <xref:System.Windows.Controls.Canvas> の境界の外側に子要素を描画できます。 この動作が必要でない場合は、<xref:System.Windows.UIElement.ClipToBounds%2A> プロパティを `true` に設定します。 これにより、<xref:System.Windows.Controls.Canvas> は独自のサイズに切り取られます。 <xref:System.Windows.Controls.Canvas> は、境界の外側に子要素を描画できる唯一のレイアウト要素です。  
  
 この動作は、[Width のプロパティの比較のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Elements/WidthProperties)に図示されています。  
  
#### <a name="defining-and-using-a-canvas"></a>キャンバスの定義と使用  
 <xref:System.Windows.Controls.Canvas> は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] またはコードを使用して、簡単にインスタンス化できます。 次の例では、<xref:System.Windows.Controls.Canvas> を使用してコンテンツを絶対的に配置する方法を示します。 このコードでは、100 ピクセルの四角形を 3 つ生成します。 最初の四角形は赤色で、左上 (*x, y*) の位置が (0, 0) に指定されます。 2 番目の四角形は緑色で、左上の位置は (100, 100) となり、最初の四角形の右下になります。 3 番目の四角形は青色で、左上の位置は (50, 50) となるため、最初の四角形の右下の象限および 2 番目の四角形の左上の象限を囲む状態になります。 3 番目の四角形が最後にレイアウトされるため、他の 2 つの四角形の上に重なっているように見えます。つまり、重複している部分は 3 番目の四角形の色とみなされます。  
  
 [!code-csharp[CanvasOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xaml[CanvasOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![一般的なキャンバス要素。](./media/panel-intro-canvas.PNG "panel_intro_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>
### <a name="dockpanel"></a>DockPanel  
 <xref:System.Windows.Controls.DockPanel> 要素では、子コンテンツ要素で設定された <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 添付プロパティを使用して、コンテナーの端に沿ってコンテンツが配置されます。 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> を <xref:System.Windows.Controls.Dock.Top> または <xref:System.Windows.Controls.Dock.Bottom> に設定すると、子要素は互いの上または下に配置されます。 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> を <xref:System.Windows.Controls.Dock.Left> または <xref:System.Windows.Controls.Dock.Right> に設定すると、子要素は互いの左または右に配置されます。 <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> プロパティでは、<xref:System.Windows.Controls.DockPanel> の子として追加された最後の要素の位置が決定されます。  
  
 <xref:System.Windows.Controls.DockPanel> を使用して、一連のボタンなど、関連コントロールのグループを配置できます。 または、これを使用して、Microsoft Outlook と同様の "ペイン形式の" [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を作成できます。  
  
#### <a name="sizing-to-content"></a>コンテンツに合わせたサイズの変更  
 <xref:System.Windows.FrameworkElement.Height%2A> および <xref:System.Windows.FrameworkElement.Width%2A> プロパティが指定されていない場合、<xref:System.Windows.Controls.DockPanel> はそのコンテンツのサイズになります。 サイズは、子要素のサイズに合うように、増減させることができます。 ただし、これらのプロパティが指定されており、次に指定する子要素のためのスペースがない場合、<xref:System.Windows.Controls.DockPanel> ではその子要素または後続の子要素は表示されず、後続の子要素は計測されません。  
  
#### <a name="lastchildfill"></a>LastChildFill  
 既定では、<xref:System.Windows.Controls.DockPanel> 要素の最後の子には、残りの未割り当て領域の "全体が使用" されます。 この動作が適切でない場合は、<xref:System.Windows.Controls.DockPanel.LastChildFill%2A> プロパティを `false` に設定します。  
  
#### <a name="defining-and-using-a-dockpanel"></a>DockPanel の定義と使用  
 次の例では、<xref:System.Windows.Controls.DockPanel> を使用してスペースを分割する方法を示します。 親 <xref:System.Windows.Controls.DockPanel> の子として、5 つの <xref:System.Windows.Controls.Border> 要素が追加されています。 それぞれで <xref:System.Windows.Controls.DockPanel> の異なる配置プロパティが使用されて、スペースが分割されます。 最後の要素が、残っている未割り当て領域の "塗り潰し" を実行します。  
  
 [!code-cpp[DockPanelOvwSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xaml[DockPanelOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![一般的な DockPanel のシナリオ。](./media/panel-intro-dockpanel.PNG "panel_intro_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>
### <a name="grid"></a>グリッド  
 <xref:System.Windows.Controls.Grid> 要素には、絶対配置と表形式データ コントロールの機能がマージされています。 <xref:System.Windows.Controls.Grid> を使うと、要素を容易に配置し、スタイルを設定することができます。 <xref:System.Windows.Controls.Grid> を使うと、行と列のグループを柔軟に定義でき、複数の <xref:System.Windows.Controls.Grid> 要素間でサイズ情報を共有するメカニズムも提供されます。  
  
#### <a name="how-is-grid-different-from-table"></a>グリッドとテーブルを区別する方法  
 <xref:System.Windows.Documents.Table> と <xref:System.Windows.Controls.Grid> には共通の機能がいくつかありますが、それぞれが最も適している状況は異なります。 <xref:System.Windows.Documents.Table> は、フロー コンテンツ内で使用するために設計されています (フロー コンテンツの詳細については、「[フロー ドキュメントの概要](../advanced/flow-document-overview.md)」を参照してください)。 グリッドは、フォーム内で最適に使用される (基本的に任意の場所以外のフロー コンテンツ)。 <xref:System.Windows.Documents.FlowDocument> 内の場合、<xref:System.Windows.Documents.Table> では改ページ位置の自動修正、列のリフロー、コンテンツの選択がサポートされますが、<xref:System.Windows.Controls.Grid> ではサポートされません。 一方、<xref:System.Windows.Controls.Grid> は、さまざまな理由から <xref:System.Windows.Documents.FlowDocument> の外で使用するのに適しています。たとえば、<xref:System.Windows.Controls.Grid> では行と列のインデックスに基づいて要素が追加されますが、<xref:System.Windows.Documents.Table> では追加されません。 <xref:System.Windows.Controls.Grid> 要素により、子のコンテンツのレイヤーが可能になり、1 つの "セル" 内に複数の要素を含むことができます。 <xref:System.Windows.Documents.Table> では、レイヤーはサポートされていません。 <xref:System.Windows.Controls.Grid> の子要素は、"セル" 境界の領域に対して絶対位置で配置できます。 <xref:System.Windows.Documents.Table> では、この機能はサポートされていません。 最後に、<xref:System.Windows.Controls.Grid> は <xref:System.Windows.Documents.Table> より軽量です。  
  
#### <a name="sizing-behavior-of-columns-and-rows"></a>列と行のサイズ変更動作  
 <xref:System.Windows.Controls.Grid> 内で定義された列と行では、<xref:System.Windows.GridUnitType.Star> のサイズ変更機能を利用して、残りのスペースを比率に応じて分配できます。 <xref:System.Windows.GridUnitType.Star> が行または列の Height または Width として選択されていると、その列または行は、使用可能な残りのスペースの領域の加重比率分を受け取ります。 これは、列または行内のコンテンツのサイズに基づいてスペースが均等に分配される <xref:System.Windows.GridUnitType.Auto> とは対照的です。 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用する場合、この値は `*` または `2*` と表現されます。 最初のケースでは、行または列は使用可能なスペース領域を 1 回受け取り、2 番目のケースでは 2 回受け取ることになります。 スペースを比率に応じて分配するこの方法と、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> および <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> の値 `Stretch` を組み合わせることにより、画面スペースのパーセンテージ単位でレイアウト スペースを分割できます。 このような方法でスペースを分配できるレイアウト パネルは、<xref:System.Windows.Controls.Grid> だけです。  
  
#### <a name="defining-and-using-a-grid"></a>グリッドの定義と使用  
 次の例では、Windows の [スタート] メニューで使用可能な [ファイル名を指定して実行] ダイアログ ボックスと同じように、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を構築する方法を示します。  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![一般的なグリッド要素。](./media/avalon-run-dialog.PNG "avalon_run_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>
### <a name="stackpanel"></a>StackPanel  
 <xref:System.Windows.Controls.StackPanel> を使うと、割り当てられた方向に要素を "スタック" できます。 既定のスタック方向は、縦です。 <xref:System.Windows.Controls.StackPanel.Orientation%2A> プロパティを使用して、コンテンツのフローを制御できます。  
  
#### <a name="stackpanel-vs-dockpanel"></a>StackPanel と DockPanel  
 <xref:System.Windows.Controls.DockPanel> でも子要素を "スタック" できますが、シナリオによっては <xref:System.Windows.Controls.DockPanel> と <xref:System.Windows.Controls.StackPanel> で生成される結果が同じにならないことがあります。 たとえば、<xref:System.Windows.Controls.DockPanel> では、子要素の順序がサイズに影響を与えますが、<xref:System.Windows.Controls.StackPanel> では影響を与えません。 これは、<xref:System.Windows.Controls.StackPanel> ではスタックの方向に <xref:System.Double.PositiveInfinity> で測定されるのに対し、<xref:System.Windows.Controls.DockPanel> では使用可能なサイズだけが測定されるためです。  
  
 この主な相違点を次の例に示します。  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 このイメージにはレンダリング動作の違いが見られます。  
  
 ![スクリーンショット: StackPanel と DockPanel のスクリーンショット](./media/layout-smiley-stackpanel.PNG "layout_smiley_stackpanel")  
  
#### <a name="defining-and-using-a-stackpanel"></a>StackPanel の定義と使用  
 次の例では、<xref:System.Windows.Controls.StackPanel> を使用して一連の縦方向配置ボタンを作成する方法を示します。 横方向に配置する場合は、<xref:System.Windows.Controls.StackPanel.Orientation%2A> プロパティを <xref:System.Windows.Controls.Orientation.Horizontal> に設定します。  
  
 [!code-csharp[StackPanel_ovw2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![一般的な StackPanel 要素。](./media/panel-intro-stackpanel.PNG "panel_intro_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>
#### <a name="virtualizingstackpanel"></a>VirtualizingStackPanel  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、データバインドされた子コンテンツを自動的に "仮想化する" <xref:System.Windows.Controls.StackPanel> 要素のバリエーションも提供されています。 ここで、"仮想化" は、どの項目を画面に表示するかに基づいて、要素のサブセットを多数のデータ項目から生成する手法を指します。 特定の時間に画面に UI 要素が少ししか表示されていない場合に多数の UI 要素を生成すると、メモリおよびプロセッサの両方に負荷がかかります。 <xref:System.Windows.Controls.VirtualizingStackPanel> を使うと (<xref:System.Windows.Controls.VirtualizingPanel> で提供される機能を通じて) 表示できる項目が計算され、<xref:System.Windows.Controls.ItemsControl> (<xref:System.Windows.Controls.ListBox> や <xref:System.Windows.Controls.ListView> など) からの <xref:System.Windows.Controls.ItemContainerGenerator> を使用して、表示できる項目に対する要素だけが作成されます。  
  
 <xref:System.Windows.Controls.VirtualizingStackPanel> 要素は、<xref:System.Windows.Controls.ListBox> などのコントロールに対する項目ホストとして自動的に設定されます。 データ バインドされたコレクションをホストすると、コンテンツが <xref:System.Windows.Controls.ScrollViewer> の境界内にある限り、コンテンツは自動的に仮想化されます。 これにより、多くの子項目をホストする際のパフォーマンスが大幅に向上します。  
  
 次のマークアップでは、項目ホストとして <xref:System.Windows.Controls.VirtualizingStackPanel> を使用する方法を示します。 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizingProperty?displayProperty=nameWithType> 添付プロパティを `true` (既定値) に設定して、仮想化が行われるようにする必要があります。  
  
 [!code-xaml[VirtualizingStackPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>
### <a name="wrappanel"></a>WrapPanel  
 <xref:System.Windows.Controls.WrapPanel> を使用して、子要素を左から右に順に配置し、親コンテナーの端に達すると、次の行に改行させます。 コンテンツは水平方向または垂直方向に設定できます。 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] は、フローが単純な <xref:System.Windows.Controls.WrapPanel> のシナリオに役立ちます。 また、子要素すべてに均等なサイズを適用する際にも使用できます。  
  
 次の例では、コンテナーの端に達した時点でラップする <xref:System.Windows.Controls.Button> コントロールを表示するための、<xref:System.Windows.Controls.WrapPanel> の作成方法を示します。  
  
 [!code-cpp[WrapPanel_Intro#1](~/samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xaml[WrapPanel_Intro#1](~/samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![一般的な WrapPanel 要素。](./media/wrappanel-element.PNG "WrapPanel_Element")  
  
<a name="Panels_nested_panel_elements"></a>
## <a name="nested-panel-elements"></a>入れ子になったパネル要素  
 <xref:System.Windows.Controls.Panel> 要素を互いに入れ子にして、複雑なレイアウトを生成することができます。 これは、<xref:System.Windows.Controls.Panel> が [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のある部分には適しているが [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の別の部分のニーズに合致しない場合に、役立つことがあります。  
  
 アプリケーションがサポートできる入れ子の量に決められた制限はありませんが、一般的に、目的のレイアウトに必要なパネルのみを使用するようアプリケーションを制限することをお勧めします。 多くの場合、<xref:System.Windows.Controls.Grid> 要素はレイアウト コンテナーとしての柔軟性を持つため、入れ子になったパネルの代用として使用できます。 これにより、ツリーから不要な要素が排除され、アプリケーションのパフォーマンスが向上します。  
  
 次の例では、特定のレイアウトを達成するために、入れ子になった <xref:System.Windows.Controls.Panel> 要素を利用する [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を作成する方法を示します。 このような特定のケースでは、<xref:System.Windows.Controls.DockPanel> 要素を使用して [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 構造を提供し、入れ子になった <xref:System.Windows.Controls.StackPanel> 要素、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.Canvas> を使用して、親の <xref:System.Windows.Controls.DockPanel> 内で子要素を正しく配置します。  
  
 [!code-csharp[Nested_Panels#1](~/samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 コンパイルされたアプリケーションは、これと同様の新しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を生成します。  
  
 ![入れ子になったパネルを利用する UI。](./media/nested-panels.PNG "nested_panels")  
  
<a name="Panels_custom_panel_elements"></a>
## <a name="custom-panel-elements"></a>カスタム パネル要素  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] により柔軟なレイアウト コントロールの配列が提供されますが、<xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドと <xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドをオーバーライドすることにより、カスタム レイアウト動作も実現できます。 このオーバーライド メソッド内で新しい配置動作を定義することにより、カスタムのサイズ変更と配置が実行されます。  
  
 同様に、派生クラス (<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Controls.Grid> など) に基づくカスタム レイアウト動作は、<xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドと <xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドをオーバーライドすることにより定義できます。  
  
 次のマークアップでは、カスタム <xref:System.Windows.Controls.Panel> 要素を作成する方法を示します。 `PlotPanel` として定義されたこの新しい <xref:System.Windows.Controls.Panel> では、ハードコーディングされた *x* および *y* 座標を使って子要素の配置がサポートされます。 この例では、<xref:System.Windows.Shapes.Rectangle> 要素 (表示されていません) は、プロット位置 50 (*x*) と 50 (*y*) に配置されます。  
  
 [!code-cpp[PlotPanel#1](~/samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 より複雑なカスタム パネルの実装を確認するには、[カスタム コンテンツ折り返しパネルの作成のサンプル](https://go.microsoft.com/fwlink/?LinkID=159979)を参照してください。  
  
<a name="Panels_global_localization"></a>
## <a name="localizationglobalization-support"></a>ローカライズ/グローバリゼーション サポート  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、ローカライズ可能な [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の作成を支援する多数の機能をサポートしています。  
  
 すべてのパネル要素で <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティがネイティブにサポートされており、ユーザーのロケールまたは言語設定に基づいてコンテンツを動的にリフローするために使用できます。 詳細については、「<xref:System.Windows.FrameworkElement.FlowDirection%2A>」を参照してください。  
  
 <xref:System.Windows.Window.SizeToContent%2A> プロパティでは、アプリケーション開発者がローカライズされた [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のニーズを予測できるメカニズムが提供されます。 このプロパティの <xref:System.Windows.SizeToContent.WidthAndHeight> 値を使用することにより、親 <xref:System.Windows.Window> はコンテンツに合わせて常に動的にサイズが変更され、人為的な高さまたは幅の制限によって制約されません。  
  
 <xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.StackPanel> はすべて、ローカライズできる [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] に適しています。 一方、<xref:System.Windows.Controls.Canvas> は、コンテンツが絶対的に配置され、ローカライズが困難なため、適切ではありません。  
  
 ローカライズ可能なユーザー インターフェイス (UI) を備えた [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの作成方法の詳細については、「[自動レイアウトの使用の概要](../advanced/use-automatic-layout-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [WPF レイアウト ギャラリー サンプル](https://go.microsoft.com/fwlink/?LinkID=160054)
- [レイアウト](../advanced/layout.md)
- [WPF Controls Gallery Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/ControlsAndLayout)
- [配置、余白、パディングの概要](../advanced/alignment-margins-and-padding-overview.md)
- [カスタム コンテンツ折り返しパネルの作成のサンプル](https://go.microsoft.com/fwlink/?LinkID=159979)
- [添付プロパティの概要](../advanced/attached-properties-overview.md)
- [自動レイアウトの使用の概要](../advanced/use-automatic-layout-overview.md)
- [レイアウトとデザイン](../advanced/optimizing-performance-layout-and-design.md)
