---
title: レイアウト
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF layout system [WPF]
- controls [WPF], layout system
- layout system [WPF]
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
ms.openlocfilehash: d4ea8d105b2d956323566a42108c7db3bfc4936d
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046337"
---
# <a name="layout"></a>レイアウト

このトピックでは、Windows Presentation Foundation (WPF) レイアウト システムについて説明します。 WPF でユーザー インターフェイスを作成するには、レイアウトの計算が発生するタイミングと方法を理解することが非常に重要です。

このトピックは、次のセクションで構成されています。

- [要素の境界ボックス](#LayoutSystem_BoundingBox)

- [レイアウト システム](#LayoutSystem_Overview)

- [子の測定と配置](#LayoutSystem_Measure_Arrange)

- [パネル要素とカスタム レイアウトの動作](#LayoutSystem_PanelsCustom)

- [レイアウトのパフォーマンスの考慮事項](#LayoutSystem_Performance)

- [サブピクセル レンダリングとレイアウトの丸め処理](#LayoutSystem_LayoutRounding)

- [次の内容](#LayoutSystem_whatsnext)

<a name="LayoutSystem_BoundingBox"></a>

## <a name="element-bounding-boxes"></a>要素の境界ボックス

WPF でレイアウトについて考えるときは、すべての要素を囲む境界ボックスを理解することが重要です。 レイアウト システムによって使用される各 <xref:System.Windows.FrameworkElement> は、レイアウトに挿入される四角形と考えることができます。 <xref:System.Windows.Controls.Primitives.LayoutInformation> クラスは、要素のレイアウト割り当て (スロット) の境界を返します。 四角形のサイズは、使用可能な画面スペース、サイズの制約、レイアウトに固有のプロパティ (余白やパディングなど)、親 <xref:System.Windows.Controls.Panel> 要素の個々の動作を計算することによって決まります。 このデータを処理することで、レイアウト システムは特定の <xref:System.Windows.Controls.Panel> のすべての子の位置を計算できるようになります。 <xref:System.Windows.Controls.Border> などの親要素で定義されているサイジング特性が、その子に影響することを覚えておくことが重要です。

次の図は、シンプルなレイアウトを示しています。

![一般的なグリッドを示すスクリーンショット、重ね合わせる境界ボックスなし。](./media/layout/grid-no-bounding-box-superimpose.png)

このレイアウトは、次の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して実現できます。

[!code-xaml[LayoutInformation#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]

1 つの <xref:System.Windows.Controls.TextBlock> 要素が <xref:System.Windows.Controls.Grid> 内でホストされています。 最初の列の左上隅だけにテキストが入力されているのに対し、<xref:System.Windows.Controls.TextBlock> に割り当てられた領域は実際にはそれよりずっと大きくなっています。 <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> メソッドを使用すると、任意の <xref:System.Windows.FrameworkElement> の境界ボックスを取得できます。 次の図は、<xref:System.Windows.Controls.TextBlock> 要素の境界ボックスを示しています。

![TextBlock 境界ボックスが表示されていることを示すスクリーンショット。](./media/layout/visible-textblock-bounding-box.png)

黄色の四角形で示されているように、<xref:System.Windows.Controls.TextBlock> 要素には、その外観よりもはるかに大きい領域が割り当てられています。 <xref:System.Windows.Controls.Grid> にさらに要素を追加すると、追加される要素の種類とサイズによって、この割り当てが縮小または拡大される場合があります。

<xref:System.Windows.Controls.TextBlock> のレイアウト スロットは、<xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> メソッドを使用して <xref:System.Windows.Shapes.Path> に変換されます。 この方法は、要素の境界ボックスの表示に役立ちます。

[!code-csharp[LayoutInformation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
[!code-vb[LayoutInformation#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]

<a name="LayoutSystem_Overview"></a>

## <a name="the-layout-system"></a>レイアウト システム

簡単に言うと、レイアウトは、要素のサイズ測定、配置、および描画を繰り返す再帰的なシステムです。 より具体的には、レイアウトは <xref:System.Windows.Controls.Panel> 要素の <xref:System.Windows.Controls.Panel.Children%2A> コレクションのメンバーを測定および配置するプロセスを記述します。 レイアウトは集中的なプロセスです。 <xref:System.Windows.Controls.Panel.Children%2A> コレクションが大きいほど、より多くの計算を行う必要があります。 コレクションを所有する <xref:System.Windows.Controls.Panel> 要素で定義されたレイアウト動作に基づく複雑さが加わる場合もあります。 <xref:System.Windows.Controls.Canvas> などの比較的単純な <xref:System.Windows.Controls.Panel> は、<xref:System.Windows.Controls.Grid> などのより複雑な <xref:System.Windows.Controls.Panel> よりも大幅にパフォーマンスが向上する可能性があります。

子 <xref:System.Windows.UIElement> がその位置を変更するたびに、レイアウト システムによる新しいパスがトリガーされる可能性があります。 したがって、不要な呼び出しはアプリケーション パフォーマンスの低下につながる可能性があるため、レイアウト システムを呼び出す可能性があるイベントを理解することが重要です。 以下に、レイアウト システムが呼び出されたときに発生するプロセスについて説明します。

1. 子 <xref:System.Windows.UIElement> は、最初にそのコア プロパティを測定して、レイアウト プロセスを開始します。

2. <xref:System.Windows.FrameworkElement> で定義されているサイズ設定プロパティ (<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Margin%2A> など) が評価されます。

3. <xref:System.Windows.Controls.Dock> の方向や積み重ねの <xref:System.Windows.Controls.StackPanel.Orientation%2A> などの <xref:System.Windows.Controls.Panel> 固有のロジックが適用されます。

4. すべての子が測定された後にコンテンツが配置されます。

5. <xref:System.Windows.Controls.Panel.Children%2A> コレクションが画面に描画されます。

6. コレクションにさらに <xref:System.Windows.Controls.Panel.Children%2A> が追加された場合、<xref:System.Windows.FrameworkElement.LayoutTransform%2A> が適用された場合、または <xref:System.Windows.UIElement.UpdateLayout%2A> メソッドが呼び出された場合には、プロセスがもう一度呼び出されます。

このプロセスとその呼び出し方法は、次のセクションで詳細に定義します。

<a name="LayoutSystem_Measure_Arrange"></a>

## <a name="measuring-and-arranging-children"></a>子の測定と配置

レイアウト システムは、<xref:System.Windows.Controls.Panel.Children%2A> コレクションのメンバーごとに、測定パスと配置パスの 2 つのパスを実行します。 それぞれの子 <xref:System.Windows.Controls.Panel> は、独自の <xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドと <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドを提供して、独自の特定のレイアウト動作を実行します。

測定パスの実行中に、<xref:System.Windows.Controls.Panel.Children%2A> コレクションの各メンバーが評価されます。 プロセスは <xref:System.Windows.UIElement.Measure%2A> メソッドの呼び出しで開始します。 このメソッドは、親 <xref:System.Windows.Controls.Panel> 要素の実装内で呼び出されます。レイアウトで発生させるために明示的に呼び出す必要はありません。

最初に、<xref:System.Windows.UIElement.Clip%2A> や <xref:System.Windows.UIElement.Visibility%2A> などの <xref:System.Windows.UIElement> のネイティブ サイズのプロパティが評価されます。 これにより、<xref:System.Windows.FrameworkElement.MeasureCore%2A> に渡される `constraintSize` という名前の値が生成されます。

次に、<xref:System.Windows.FrameworkElement> で定義されているフレームワーク プロパティが処理されます。これは `constraintSize` の値に影響します。 一般に、これらのプロパティは、基になる <xref:System.Windows.UIElement> のサイズ変更特性 (<xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.FrameworkElement.Style%2A> など) を記述します。 これらの各プロパティは、要素を表示するために必要な領域を変更できます。 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> は、`constraintSize` でパラメーターとして呼び出されます。

> [!NOTE]
> <xref:System.Windows.FrameworkElement.Height%2A> と <xref:System.Windows.FrameworkElement.Width%2A> および <xref:System.Windows.FrameworkElement.ActualHeight%2A> と <xref:System.Windows.FrameworkElement.ActualWidth%2A> のプロパティには違いがあります。 たとえば、<xref:System.Windows.FrameworkElement.ActualHeight%2A> プロパティは、他の高さ入力とレイアウト システムに基づいて計算された値です。 この値は、実際のレンダリング パスに基づいて、レイアウト システム自体で設定されるため、入力の変更の基準である <xref:System.Windows.FrameworkElement.Height%2A> などのプロパティの設定値よりもわずかに遅れる場合があります。
>
> <xref:System.Windows.FrameworkElement.ActualHeight%2A> は計算された値であるため、レイアウト システムによるさまざまな操作の結果として、その値に対して複数の変更や増分変更が報告される可能性があることにご注意ください。 レイアウト システムが、子要素に必要な測定スペース、親要素による制約などを計算している場合があります。

測定パスの最終的な目標は、子が <xref:System.Windows.FrameworkElement.MeasureCore%2A> の呼び出し中に発生する、その <xref:System.Windows.UIElement.DesiredSize%2A> を決定することです。 <xref:System.Windows.UIElement.DesiredSize%2A> 値は、コンテンツの配置パスの実行中に使用するため、<xref:System.Windows.UIElement.Measure%2A> によって格納されます。

配置パスは <xref:System.Windows.UIElement.Arrange%2A> メソッドの呼び出しで開始します。 配置パスの実行中に、親 <xref:System.Windows.Controls.Panel> 要素が子のバインドを表す四角形を生成します。 この値は処理のために <xref:System.Windows.FrameworkElement.ArrangeCore%2A> メソッドに渡されます。

<xref:System.Windows.FrameworkElement.ArrangeCore%2A> メソッドは、子の <xref:System.Windows.UIElement.DesiredSize%2A> を評価し、要素のレンダリングされるサイズに影響する可能性のある追加の余白をすべて評価します。 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> は `arrangeSize` を生成します。これは<xref:System.Windows.Controls.Panel> の <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドにパラメーターとして渡されます。 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> は子の `finalSize` を生成します。 最後に、<xref:System.Windows.FrameworkElement.ArrangeCore%2A> メソッドは、余白や配置などのオフセット プロパティの最終評価を行い、レイアウト スロット内に子を配置します。 子は割り当てられた領域全体を埋める必要はありません (そうしない場合もよくあります)。 その後、コントロールが親 <xref:System.Windows.Controls.Panel> に返され、レイアウト プロセスが完了します。

<a name="LayoutSystem_PanelsCustom"></a>

## <a name="panel-elements-and-custom-layout-behaviors"></a>パネル要素とカスタム レイアウトの動作

WPF には、<xref:System.Windows.Controls.Panel> から派生した要素のグループが含まれています。 これらの <xref:System.Windows.Controls.Panel> 要素により、多数の複雑なレイアウトが可能になります。 たとえば、スタッキング要素は、<xref:System.Windows.Controls.StackPanel> 要素を使用して簡単に実現できますが、より複雑で流動性の高いレイアウトは、<xref:System.Windows.Controls.Canvas> を使用することで可能になります。

次の表に、使用可能なレイアウト <xref:System.Windows.Controls.Panel> 要素をまとめています。

|パネル名|説明|
|----------------|-----------------|
|<xref:System.Windows.Controls.Canvas>|<xref:System.Windows.Controls.Canvas> 領域に対する座標により子要素を明示的に配置できる領域を定義します。|
|<xref:System.Windows.Controls.DockPanel>|子要素を互いに水平方向または垂直方向に整列する領域を定義します。|
|<xref:System.Windows.Controls.Grid>|行と列で構成される柔軟性のあるグリッド領域を定義します。|
|<xref:System.Windows.Controls.StackPanel>|子要素を水平方向または垂直方向の単一行に整列します。|
|<xref:System.Windows.Controls.VirtualizingPanel>|子のデータ コレクションを仮想化する <xref:System.Windows.Controls.Panel> 要素のフレームワークを提供します。 これは抽象クラスです。|
|<xref:System.Windows.Controls.WrapPanel>|左から右へ順に子要素を配置し、ボックスの端で改行してコンテンツを次の行へ送ります。 後続の配置は、<xref:System.Windows.Controls.WrapPanel.Orientation%2A> プロパティの値に応じて、上から下または右から左に向かって行われます。|

定義済みの <xref:System.Windows.Controls.Panel> 要素を使用してできないレイアウトを必要とするアプリケーションに対しては、<xref:System.Windows.Controls.Panel> から継承し、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドと <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドをオーバーライドすることで、カスタム レイアウト動作を実現できます。

<a name="LayoutSystem_Performance"></a>

## <a name="layout-performance-considerations"></a>レイアウトのパフォーマンスの考慮事項

レイアウトは再帰的なプロセスです。 <xref:System.Windows.Controls.Panel.Children%2A> コレクション内の各子要素は、レイアウト システムの呼び出しごとに処理されます。 そのため、必要ない場合はレイアウト システムをトリガーしないようにしてください。 次の考慮事項は、パフォーマンスを向上させるのに役立ちます。

- どのプロパティ値の変更がレイアウト システムによる再帰的な更新を強制するかに注意してください。

  レイアウト システムを初期化できる値が設定されている依存関係プロパティは、パブリック フラグでマークされます。 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> と <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> は、どのプロパティ値の変更がレイアウト システムによる再帰的な更新を強制するかに関する役立つヒントを提供します。 一般に、要素の境界ボックスのサイズに影響を与えるプロパティでは、<xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> フラグを true に設定する必要があります。 依存関係プロパティの詳細については、「[依存関係プロパティの概要](dependency-properties-overview.md)」を参照してください。

- 可能であれば、<xref:System.Windows.FrameworkElement.LayoutTransform%2A> の代わりに <xref:System.Windows.UIElement.RenderTransform%2A> を使用します。

  <xref:System.Windows.FrameworkElement.LayoutTransform%2A> は [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] のコンテンツに影響を与える非常に便利な方法となります。 ただし、変換の効果を他の要素の位置に影響させる必要がない場合は、代わりに <xref:System.Windows.UIElement.RenderTransform%2A> を使用することをお勧めします。これは <xref:System.Windows.UIElement.RenderTransform%2A> がレイアウト システムを呼び出さないためです。 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> はその変換を適用し、影響を受ける要素の新しい位置を考慮するため、再帰的なレイアウトの更新を強制します。

- <xref:System.Windows.UIElement.UpdateLayout%2A> の不要な呼び出しを回避します。

  <xref:System.Windows.UIElement.UpdateLayout%2A> メソッドは、再帰的なレイアウトの更新を強制しますが、多くの場合、必要ありません。 完全な更新が必要であると確信できる場合を除き、このメソッドの呼び出しはレイアウト システムに任せます。

- 大規模な <xref:System.Windows.Controls.Panel.Children%2A> コレクションを使用する場合は、通常の <xref:System.Windows.Controls.StackPanel> の代わりに <xref:System.Windows.Controls.VirtualizingStackPanel> を使用することを検討してください。

  子コレクションを仮想化することで、<xref:System.Windows.Controls.VirtualizingStackPanel> は、現在、親のビューポート内にあるメモリ内オブジェクトのみを保持します。 その結果、ほとんどのシナリオでパフォーマンスが大幅に向上します。

<a name="LayoutSystem_LayoutRounding"></a>

## <a name="sub-pixel-rendering-and-layout-rounding"></a>サブピクセル レンダリングとレイアウトの丸め処理

WPF グラフィックス システムでは、デバイスに依存しない単位を使用して、解像度とデバイスの独立性を可能にします。 デバイスに依存しない各ピクセルは、システムのドット/インチ (dpi) 設定に応じて自動的にスケーリングされます。 これにより、異なる dpi 設定に対して WPF アプリケーションに適切なスケーリングを提供し、アプリケーションを自動的に dpi 対応にします。

ただし、この dpi 非依存は、アンチエイリアシングのため、不規則なエッジ レンダリングが作成される場合があります。 これらの成果物 (通常はぼやけたエッジや半透明のエッジが見られます) は、エッジの場所がデバイス ピクセルの間ではなく、デバイス ピクセルの中間にある場合に発生します。 レイアウト システムは、レイアウトの丸め処理でこれを調整する方法を提供します。 レイアウトの丸め処理では、レイアウト システムがレイアウト パスの実行中に任意の整数以外のピクセル値を丸めます。

レイアウトの丸め処理は既定で無効になっています。 レイアウトの丸め処理を有効にするには、任意の <xref:System.Windows.FrameworkElement> で <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> プロパティを `true` に設定します。 これは依存関係プロパティであるため、値はビジュアル ツリー内のすべての子に反映されます。 UI 全体のレイアウトの丸め処理を有効にするには、ルートコンテナーで <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> を `true` に設定します。 例については、「<xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>」を参照してください。

<a name="LayoutSystem_whatsnext"></a>

## <a name="whats-next"></a>次の内容

要素の測定方法と配置方法を理解することが、レイアウトを理解する最初のステップです。 使用可能な <xref:System.Windows.Controls.Panel> 要素の詳細については、「[パネルの概要](../controls/panels-overview.md)」を参照してください。 レイアウトに影響を与えるさまざまな配置プロパティをより理解するには、「[配置、余白、パディングの概要](alignment-margins-and-padding-overview.md)」を参照してください。 軽量のアプリケーションにまとめて配置する準備ができたら、「[チュートリアル:初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.UIElement>
- [パネルの概要](../controls/panels-overview.md)
- [配置、余白、パディングの概要](alignment-margins-and-padding-overview.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
