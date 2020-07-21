---
title: ポップアップの配置動作
ms.date: 03/30/2017
helpviewer_keywords:
- popups [WPF]
- Popup control [WPF], placing
- placing popups [WPF]
- positioning popups [WPF]
ms.assetid: fbf642e9-f670-4efd-a7af-a67468a1c8e1
ms.openlocfilehash: 1c377e62ffd334638031baee4d4831ac5a31acf3
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81243259"
---
# <a name="popup-placement-behavior"></a>ポップアップの配置動作
<xref:System.Windows.Controls.Primitives.Popup> コントロールでは、アプリケーション上をフローティングする別のウィンドウにコンテンツが表示されます。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>、<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> の各プロパティを使用することにより、コントロール、マウス、または画面を基準にして <xref:System.Windows.Controls.Primitives.Popup> の位置を指定できます。  これらのプロパティが連携することで、<xref:System.Windows.Controls.Primitives.Popup> の位置を柔軟に指定できます。  
  
> [!NOTE]
> <xref:System.Windows.Controls.ToolTip> クラスと <xref:System.Windows.Controls.ContextMenu> クラスでも、これら 5 つのプロパティと動作が同じように定義されています。  

<a name="Positioning"></a>
## <a name="positioning-the-popup"></a>ポップアップの配置  
 <xref:System.Windows.Controls.Primitives.Popup> は、<xref:System.Windows.UIElement> または画面全体を基準にして配置できます。  次の例では、<xref:System.Windows.UIElement> (ここでは画像) を基準として 4 つの <xref:System.Windows.Controls.Primitives.Popup> コントロールを作成します。 すべての <xref:System.Windows.Controls.Primitives.Popup> コントロールで <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> プロパティが `image1` に設定されていますが、各 <xref:System.Windows.Controls.Primitives.Popup> の配置プロパティの値は異なります。  
  
 [!code-xaml[PopupPositionSnippet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#3)]  
  
 次の図は、画像と <xref:System.Windows.Controls.Primitives.Popup> コントロールを示したものです  
  
 ![4 つのポップアップ コントロールを含む画像](./media/popup-placement-behavior/popup-placement-intro.png "4 つのポップアップを含む画像")
  
 この簡単な例では、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> プロパティと <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティを設定する方法が示されていますが、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>、<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> の各プロパティを使用することにより、<xref:System.Windows.Controls.Primitives.Popup> を配置する場所をさらに細かく制御できます。  
  
<a name="Definitions"></a>
## <a name="definitions-of-terms-the-anatomy-of-a-popup"></a>用語の定義: ポップアップの構造  
 次の用語は、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>、<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> の各プロパティの相互関係および <xref:System.Windows.Controls.Primitives.Popup> との関係を理解するのに役立ちます。  
  
- ターゲット オブジェクト  
  
- ターゲット領域  
  
- ターゲットの始点  
  
- ポップアップ配置ポイント  
  
 これらの用語は、<xref:System.Windows.Controls.Primitives.Popup> とそれに関連付けられたコントロールのさまざまな側面を参照するのに役立ちます。  
  
### <a name="target-object"></a>ターゲット オブジェクト  
 "*ターゲット オブジェクト*" は、<xref:System.Windows.Controls.Primitives.Popup> が関連付けられている要素です。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> プロパティが設定されている場合は、それによってターゲット オブジェクトが指定されます。  <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> が設定されておらず、<xref:System.Windows.Controls.Primitives.Popup> に親がある場合は、その親がターゲット オブジェクトになります。  <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> の値が設定されておらず、親がない場合は、ターゲット オブジェクトは存在せず、<xref:System.Windows.Controls.Primitives.Popup> は画面を基準にして配置されます。  
  
 次の例では、<xref:System.Windows.Controls.Canvas> の子である <xref:System.Windows.Controls.Primitives.Popup> を作成します。  この例では、<xref:System.Windows.Controls.Primitives.Popup> の <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> プロパティは設定されていません。 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> の既定値は <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom?displayProperty=nameWithType> であるため、<xref:System.Windows.Controls.Primitives.Popup> は <xref:System.Windows.Controls.Canvas> の下に表示されます。  
  
 [!code-xaml[PopupPositionSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#1)]  
  
 次の図では、<xref:System.Windows.Controls.Canvas> を基準にして配置された <xref:System.Windows.Controls.Primitives.Popup> が示されています。  
  
 ![PlacementTarget がないポップアップ コントロール](./media/popup-placement-behavior/popup-placement-no-placement-target.png "PlacementTarget がないポップアップ。")  

 次の例では、<xref:System.Windows.Controls.Canvas> の子である <xref:System.Windows.Controls.Primitives.Popup> が作成されますが、ここでは <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> を `ellipse1` に設定しているため、ポップアップは <xref:System.Windows.Shapes.Ellipse> の下に表示されます。  
  
 [!code-xaml[PopupPositionSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#2)]  
  
 次の図では、<xref:System.Windows.Shapes.Ellipse> を基準にして配置された <xref:System.Windows.Controls.Primitives.Popup> が示されています。  
  
 ![楕円を基準にして配置されるポップアップ](./media/popup-placement-behavior/popup-placement-with-placement-target.png "PlacementTarget があるポップアップ")
  
> [!NOTE]
> <xref:System.Windows.Controls.ToolTip> の場合、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> の既定値は <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> です。  <xref:System.Windows.Controls.ContextMenu> の場合、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> の既定値は <xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint> です。 これらの値については、後ほど「プロパティの連携のしくみ」で説明します。  
  
### <a name="target-area"></a>ターゲット領域  
 "*ターゲット領域*" は、<xref:System.Windows.Controls.Primitives.Popup> が基準とする画面上の領域です。 前の例では、<xref:System.Windows.Controls.Primitives.Popup> はターゲット オブジェクトの境界に揃えられますが、<xref:System.Windows.Controls.Primitives.Popup> にターゲット オブジェクトがある場合でも、<xref:System.Windows.Controls.Primitives.Popup> が他の境界に揃えられることがあります。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> プロパティが設定されている場合、ターゲット領域はターゲット オブジェクトの境界とは異なります。  
  
 次の例では、2 つの <xref:System.Windows.Controls.Canvas> オブジェクトが作成され、それぞれに <xref:System.Windows.Shapes.Rectangle> と <xref:System.Windows.Controls.Primitives.Popup> が含まれます。  いずれの場合も、<xref:System.Windows.Controls.Primitives.Popup> のターゲット オブジェクトは <xref:System.Windows.Controls.Canvas> です。 1 つ目の <xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Primitives.Popup> では <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> が設定されており、<xref:System.Windows.Rect.X%2A> プロパティは 50、<xref:System.Windows.Rect.Y%2A> プロパティは 50、<xref:System.Windows.Rect.Width%2A> プロパティは 50、<xref:System.Windows.Rect.Height%2A> プロパティは 100 に設定されています。 2 つ目の <xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Primitives.Popup> では、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> は設定されていません。  そのため、1 つ目の <xref:System.Windows.Controls.Primitives.Popup> は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の下に配置され、2 つ目の <xref:System.Windows.Controls.Primitives.Popup> は <xref:System.Windows.Controls.Canvas> の下に配置されます。 各 <xref:System.Windows.Controls.Canvas> には、1 つ目の <xref:System.Windows.Controls.Primitives.Popup> に対する <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の境界と同じ境界をもつ <xref:System.Windows.Shapes.Rectangle> も含まれています。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> では、アプリケーションに表示される要素が作成されないことに注意してください。例では、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> を表すために <xref:System.Windows.Shapes.Rectangle> が作成されています。  
  
 [!code-xaml[PopupPositionSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#4)]  
  
 次の図は、前の例の結果を示しています。  
  
 ![PlacementRectangle がある (またはない) ポップアップ](./media/popup-placement-behavior/popup-placement-placement-rectangle.png "PlacementRectangle がある (またはない) ポップアップ。")  

### <a name="target-origin-and-popup-alignment-point"></a>ターゲットの始点とポップアップ配置ポイント  
 *ターゲットの始点*と*ポップアップ配置ポイント*は、それぞれターゲット領域とポップアップ上の基準点であり、配置に使用します。 <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> プロパティと <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> プロパティを使用して、ターゲット領域からポップアップをオフセットすることができます。  <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> と <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> は、ターゲットの始点とポップアップ配置ポイントが基準になります。 ターゲットの始点とポップアップ配置ポイントの位置は、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティの値によって決まります。  
  
 次の例では、<xref:System.Windows.Controls.Primitives.Popup> を作成し、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> プロパティと <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> プロパティを 20 に設定しています。  <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティが <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> (既定値) に設定されているため、ターゲットの始点はターゲット領域の左下隅で、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の左上隅になります。  
  
 [!code-xaml[PopupPositionSnippet#5](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#5)]  
  
 次の図は、前の例の結果を示しています。  
  
 ![ターゲットの始点の配置ポイントを含むポップアップ配置](./media/popup-placement-behavior/popup-placement-target-origin-alignment-point.png "HorizontalOffset と VerticalOffset があるポップアップ。")
  
<a name="How"></a>
## <a name="how-the-properties-work-together"></a>プロパティの連携のしくみ  
 適切なターゲット領域、ターゲットの始点、ポップアップ配置ポイントを見出すには、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> の値をまとめて考慮する必要があります。  たとえば、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> の値が <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> の場合は、ターゲット オブジェクトは存在せず、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> は無視されて、マウス ポインターの境界がターゲット領域になります。 一方、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> の場合は、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親によってターゲット オブジェクトが決定され、ターゲット領域は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> によって決まります。  
  
 次の表では、ターゲット オブジェクト、ターゲット領域、ターゲットの原点、ポップアップ配置ポイントについて説明し、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> と <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> がそれぞれの <xref:System.Windows.Controls.Primitives.PlacementMode> 列挙値で使用されるかどうかを示します。  
  
|PlacementMode|ターゲット オブジェクト|ターゲット領域|ターゲットの始点|ポップアップ配置ポイント|  
|-------------------|-------------------|-----------------|-------------------|---------------------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>|該当なし。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> は無視されます。|画面、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準は画面です。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint>|該当なし。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> は無視されます。|画面、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準は画面です。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の左下隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Center>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の中央。|<xref:System.Windows.Controls.Primitives.Popup> の中心。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Custom>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|<xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> によって定義されます。|<xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> によって定義されます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Left>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の右上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>|該当なし。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> は無視されます。|マウス ポインターの境界。 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> は無視されます。|ターゲット領域の左下隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint>|該当なし。 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> は無視されます。|マウス ポインターの境界。 <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> は無視されます。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Relative>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Right>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の右上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左上隅。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Top>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> または親。|ターゲット オブジェクト、または設定されている場合は <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>。  <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> の基準はターゲット オブジェクトです。|ターゲット領域の左上隅。|<xref:System.Windows.Controls.Primitives.Popup> の左下隅。|  
  
 次の図では、<xref:System.Windows.Controls.Primitives.PlacementMode> の各値に対する <xref:System.Windows.Controls.Primitives.Popup>、ターゲット領域、ターゲットの始点、ポップアップ配置ポイントが示されています。 各図で、ターゲット領域は黄色、<xref:System.Windows.Controls.Primitives.Popup> は青色です。  
  
 ![Absolute または AbsolutePoint 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-absolute.png "Placement が Absolute または AbsolutePoint。")
  
 ![Bottom 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-bottom.png "Placement が Bottom。")
  
 ![Center 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-center.png "Placement が Center。")
  
 ![Left 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-left.png "Placement が Left。")
  
 ![Mouse 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-mouse.png "Placement が Mouse。")  
  
 ![MousePoint 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-mousepoint.png "Placement が MousePoint。")  
  
 ![Relative または RelativePoint 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-relative.png "Placement が Relative または RelativePoint。")
  
 ![Right 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-right.png "Placement が Right。")
  
 ![Top 配置を含むポップアップ](./media/popup-placement-behavior/popup-placement-top.png "Placement が Top。")
  
<a name="When"></a>
## <a name="when-the-popup-encounters-the-edge-of-the-screen"></a>ポップアップが画面の端と重なった場合  
 セキュリティ上の理由から、<xref:System.Windows.Controls.Primitives.Popup> が画面の端で隠れることはありません。 <xref:System.Windows.Controls.Primitives.Popup> が画面の端と重なると、次の 3 つの処理のいずれかが行われます。  
  
- <xref:System.Windows.Controls.Primitives.Popup> が画面の端で隠れないよう、ポップアップが画面の端に揃うように再調整されます。  
  
- ポップアップは別のポップアップ配置ポイントを使用します。  
  
- ポップアップは別のターゲットの始点とポップアップ配置ポイントを使用します。  
  
 これらのオプションについては、このセクションの後半で詳しく説明します。  
  
 <xref:System.Windows.Controls.Primitives.Popup> が画面の端と重なった場合の動作は、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティの値と、ポップアップが重なった画面端の位置によって異なります。 次の表は、<xref:System.Windows.Controls.Primitives.Popup> が画面の端と重なった場合の動作を <xref:System.Windows.Controls.Primitives.PlacementMode> の値ごとにまとめたものです。  
  
|PlacementMode|上端|下端|左端|右端|  
|-------------------|--------------|-----------------|---------------|----------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>|上端に揃えます。|下端に揃えます。|左端に揃えます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint>|上端に揃えます。|ポップアップ配置ポイントが、<xref:System.Windows.Controls.Primitives.Popup> の左下隅に変更されます。|左端に揃えます。|ポップアップ配置ポイントが、<xref:System.Windows.Controls.Primitives.Popup> の右上隅に変更されます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>|上端に揃えます。|ターゲットの始点がターゲット領域の左上隅に変更され、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の左下隅に変更されます。|左端に揃えます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Center>|上端に揃えます。|下端に揃えます。|左端に揃えます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Left>|上端に揃えます。|下端に揃えます。|ターゲットの始点がターゲット領域の右上隅に変更され、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の左上隅に変更されます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>|上端に揃えます。|ターゲットの始点がターゲット領域の左上隅 (マウス ポインターの境界) に変更され、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の左下隅に変更されます。|左端に揃えます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint>|上端に揃えます。|ポップアップ配置ポイントが、<xref:System.Windows.Controls.Primitives.Popup> の左下隅に変更されます。|左端に揃えます。|ポップアップ配置ポイントが、ポップアップの右上隅に変更されます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Relative>|上端に揃えます。|下端に揃えます。|左端に揃えます。|右端に揃えます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>|上端に揃えます。|ポップアップ配置ポイントが、<xref:System.Windows.Controls.Primitives.Popup> の左下隅に変更されます。|左端に揃えます。|ポップアップ配置ポイントが、ポップアップの右上隅に変更されます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Right>|上端に揃えます。|下端に揃えます。|左端に揃えます。|ターゲットの始点がターゲット領域の左上隅に変更され、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の右上隅に変更されます。|  
|<xref:System.Windows.Controls.Primitives.PlacementMode.Top>|ターゲットの始点がターゲット領域の左下隅に変更され、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の左上隅に変更されます。 つまりこれは、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> の場合と同じです。|下端に揃えます。|左端に揃えます。|右端に揃えます。|  
  
### <a name="aligning-to-the-screen-edge"></a>画面の端への配置  
 <xref:System.Windows.Controls.Primitives.Popup> 全体が画面に表示されるよう、<xref:System.Windows.Controls.Primitives.Popup> を再配置して画面の端に揃えることができます。  この場合、ターゲットの始点とポップアップ配置ポイントの間の距離は、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> および <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> の値と異なることがあります。 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Absolute>、<xref:System.Windows.Controls.Primitives.PlacementMode.Center>、または <xref:System.Windows.Controls.Primitives.PlacementMode.Relative> の場合、<xref:System.Windows.Controls.Primitives.Popup> は画面のすべての端に揃えて配置されます。  たとえば、<xref:System.Windows.Controls.Primitives.Popup> で、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Relative> に設定され、<xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> が 100 に設定されているとします。  画面の下端によって <xref:System.Windows.Controls.Primitives.Popup> の全部または一部が隠れる場合、<xref:System.Windows.Controls.Primitives.Popup> は画面の下端に揃えて再配置され、ターゲットの始点とポップアップ配置ポイントの間の垂直距離は 100 未満になります。 これを次の図で示します。  
  
 ![画面の端に揃えて配置されたポップアップ](./media/popup-placement-behavior/popup-placement-relative-screen-edge.png "ポップアップが画面の端に揃えて配置される。")
  
### <a name="changing-the-popup-alignment-point"></a>ポップアップ配置ポイントの変更  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.AbsolutePoint>、<xref:System.Windows.Controls.Primitives.PlacementMode.RelativePoint>、または <xref:System.Windows.Controls.Primitives.PlacementMode.MousePoint> の場合、ポップアップが画面の下端または右端と重なると、ポップアップ配置ポイントが変更されます。  
  
 次の図では、画面の下端によって <xref:System.Windows.Controls.Primitives.Popup> の全部または一部が隠れた場合、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の左下隅になることが示されています。  
  
 ![画面の下端による新しい配置ポイント](./media/popup-placement-behavior/popup-placement-relative-point-screen-edge.png "ポップアップが画面の下端と重なり、ポップアップ配置ポイントが変更される。")  

 次の図では、<xref:System.Windows.Controls.Primitives.Popup> が画面の右端で隠れた場合、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の右上隅になることが示されています。  
  
 ![画面の端による新しいポップアップ配置ポイント](./media/popup-placement-behavior/popup-placement-relative-point-right-screen-edge.png "ポップアップが画面の右端と重なり、ポップアップ配置ポイントが変更される。")
  
 <xref:System.Windows.Controls.Primitives.Popup> が画面の下端と右端に重なると、ポップアップ配置ポイントは <xref:System.Windows.Controls.Primitives.Popup> の右下隅になります。  
  
### <a name="changing-the-target-origin-and-popup-alignment-point"></a>ターゲットの始点とポップアップ配置ポイントの変更  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom>、<xref:System.Windows.Controls.Primitives.PlacementMode.Left>、<xref:System.Windows.Controls.Primitives.PlacementMode.Mouse>、<xref:System.Windows.Controls.Primitives.PlacementMode.Right>、または <xref:System.Windows.Controls.Primitives.PlacementMode.Top> の場合は、画面の端と重なるとターゲットの始点とポップアップ配置ポイントが変更されます。  位置の変更が発生する画面の端は、<xref:System.Windows.Controls.Primitives.PlacementMode> の値によって異なります。  
  
 次の図では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Bottom> で、<xref:System.Windows.Controls.Primitives.Popup> が画面の下端と重なった場合、ターゲットの始点がターゲット領域の左上隅、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の左下隅になることが示されています。  
  
 ![画面の下端による新しい配置ポイント](./media/popup-placement-behavior/popup-placement-bottom-screen-edge.png "Placement が Bottom で、ポップアップが画面の下端と重なる。")
  
 次の図では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Left> で、<xref:System.Windows.Controls.Primitives.Popup> が画面の左端と重なった場合、ターゲットの始点がターゲット領域の右上隅、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の左上隅になることが示されています。  
  
 ![画面の左端による新しい配置ポイント](./media/popup-placement-behavior/popup-placement-left-screen-edge.png "Placement が Left で、ポップアップが画面の左端と重なる。")  
  
 次の図では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Right> で、<xref:System.Windows.Controls.Primitives.Popup> が画面の右端と重なった場合、ターゲットの始点がターゲット領域の左上隅、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の右上隅になることが示されています。  
  
 ![画面の右端による新しい配置ポイント](./media/popup-placement-behavior/popup-placement-right-screen-edge.png "Placement が Right で、ポップアップが画面の右端と重なる。")  

 次の図では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Top> で、<xref:System.Windows.Controls.Primitives.Popup> が画面の上端と重なった場合、ターゲットの始点がターゲット領域の左下隅、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の左上隅になることが示されています。  
  
 ![画面の上端による新しい配置ポイント](./media/popup-placement-behavior/popup-placement-top-screen-edge.png "Placement が Top で、ポップアップが画面の上端と重なる。")  
  
 次の図では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> が <xref:System.Windows.Controls.Primitives.PlacementMode.Mouse> で、<xref:System.Windows.Controls.Primitives.Popup> が画面の下端と重なった場合、ターゲットの始点がターゲット領域 (マウス ポインターの境界) の左上隅、ポップアップ配置ポイントが <xref:System.Windows.Controls.Primitives.Popup> の左下隅になることが示されています。  
  
 ![画面の端に近いマウスによる新しい配置ポイント](./media/popup-placement-behavior/popup-placement-mouse-screen-edge.png "Placement が Mouse で、ポップアップが画面の下端と重なる。")
  
### <a name="customizing-popup-placement"></a>ポップアップの配置のカスタマイズ  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティを <xref:System.Windows.Controls.Primitives.PlacementMode.Custom> に設定することで、ターゲットの始点とポップアップ配置ポイントをカスタマイズできます。 次に、<xref:System.Windows.Controls.Primitives.Popup> に対して可能な一連の配置ポイントとプライマリ軸を (優先順に) 返す <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> デリゲートを定義します。 <xref:System.Windows.Controls.Primitives.Popup> の表示が最大になるポイントが選択されます。  画面の端で <xref:System.Windows.Controls.Primitives.Popup> が隠れた場合は、<xref:System.Windows.Controls.Primitives.Popup> の位置が自動的に調整されます。 例については、「[方法 : ポップアップのカスタム位置を指定する](how-to-specify-a-custom-popup-position.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [ポップアップの配置のサンプル](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS)
