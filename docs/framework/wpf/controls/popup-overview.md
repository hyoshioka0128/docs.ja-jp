---
title: ポップアップの概要
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Popup
- Popup control [WPF], about Popup control
ms.assetid: 774f53ca-bff8-470e-9ce9-3928b4cf3d4c
ms.openlocfilehash: 911130d52744c5ba54750f214829a5d1900e083c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185949"
---
# <a name="popup-overview"></a>ポップアップの概要
<xref:System.Windows.Controls.Primitives.Popup> コントロールには、指定された要素や画面座標を基準として現在のアプリケーション ウインドウの上を浮動する別のウィンドウにコンテンツを表示する方法が用意されています。 このトピックでは、<xref:System.Windows.Controls.Primitives.Popup> コントロールとその使用方法について説明します。  

<a name="What_Is_a_Popup_"></a>
## <a name="what-is-a-popup"></a>ポップアップとは  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールでは、画面上の要素またはポイントを基準とする別のウィンドウに、コンテンツが表示されます。 <xref:System.Windows.Controls.Primitives.Popup> が表示されているときは、<xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> プロパティが `true` に設定されています。  
  
> [!NOTE]
> マウス ポインターをその親オブジェクトの上に移動しても、<xref:System.Windows.Controls.Primitives.Popup> が自動的に開くことはありません。 <xref:System.Windows.Controls.Primitives.Popup> が自動的に開くようにするには、<xref:System.Windows.Controls.ToolTip> クラスまたは <xref:System.Windows.Controls.ToolTipService> クラスを使用します。 詳細については、[ToolTip の概要](tooltip-overview.md)を参照してください。  
  
<a name="APopupExample"></a>
## <a name="creating-a-popup"></a>ポップアップの作成  
 次の例では、<xref:System.Windows.Controls.Button> コントロールの子要素である <xref:System.Windows.Controls.Primitives.Popup> コントロールを定義する方法を示します。 <xref:System.Windows.Controls.Button> は子要素を 1 つしか持てないため、この例では <xref:System.Windows.Controls.Button> コントロールと <xref:System.Windows.Controls.Primitives.Popup> コントロールのテキストを <xref:System.Windows.Controls.StackPanel> 内に配置しています。 <xref:System.Windows.Controls.Primitives.Popup> の内容は <xref:System.Windows.Controls.TextBlock> コントロールに表示されます。このコントロールでは、アプリケーション ウインドウの関連する <xref:System.Windows.Controls.Button> コントロールの近くに浮動表示される別のウィンドウ内に、テキストが表示されます。  
  
 [!code-xaml[PopupSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#1)]  
  
 [!code-xaml[PopupSimple#CreatePopupCodeXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#createpopupcodexaml)]  
  
<a name="PopupUses"></a>
## <a name="controls-that-implement-a-popup"></a>ポップアップを実装するコントロール  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールは他のコントロール内に作成できます。 次のコントロールでは、特定の使用目的で <xref:System.Windows.Controls.Primitives.Popup> コントロールが実装されています:  
  
- <xref:System.Windows.Controls.ToolTip>。 要素のツールヒントを作成する場合は、<xref:System.Windows.Controls.ToolTip> クラスと <xref:System.Windows.Controls.ToolTipService> クラスを使用します。 詳細については、[ToolTip の概要](tooltip-overview.md)を参照してください。  
  
- <xref:System.Windows.Controls.ContextMenu>。 要素のコンテキスト メニューを作成する場合は、<xref:System.Windows.Controls.ContextMenu> コントロールを使用します。 詳細については、[ContextMenu の概要](contextmenu-overview.md)を参照してください。  
  
- <xref:System.Windows.Controls.ComboBox>。 表示または非表示にできるドロップダウン リスト ボックスがある選択コントロールを作成する場合は、<xref:System.Windows.Controls.ComboBox> コントロールを使用します。  
  
- <xref:System.Windows.Controls.Expander>。 コンテンツを表示する折りたたみ可能な領域を持つヘッダーを表示するコントロールを作成する場合は、<xref:System.Windows.Controls.Expander> コントロールを使用します。 詳細については、 [Expander の概要](expander-overview.md)を参照してください。  
  
<a name="PopupBehaviorandAppearance"></a>
## <a name="popup-behavior-and-appearance"></a>ポップアップの動作と外観  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールには、その動作と外観をカスタマイズできる機能が用意されています。 たとえば、開くときと閉じるときの動作、アニメーション、不透明度とビットマップ効果、<xref:System.Windows.Controls.Primitives.Popup> のサイズと位置を設定できます。  
  
<a name="OpenandCloseBehavior"></a>
### <a name="open-and-close-behavior"></a>オープンとクローズの動作  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールの内容は、<xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> プロパティが `true` に設定されていると表示されます。 既定では、<xref:System.Windows.Controls.Primitives.Popup> は、<xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> プロパティが `false` に設定されるまで開いた状態を保ちます。 ただし、<xref:System.Windows.Controls.Primitives.Popup.StaysOpen%2A> プロパティを `false` に設定することで、既定の動作を変更できます。 このプロパティを `false` に設定すると、<xref:System.Windows.Controls.Primitives.Popup> のコンテンツ ウィンドウにマウス キャプチャが設定されます。 <xref:System.Windows.Controls.Primitives.Popup> ウィンドウの外側でマウス イベントが発生すると、<xref:System.Windows.Controls.Primitives.Popup> はマウス キャプチャを失い、ウィンドウが閉じます。  
  
 <xref:System.Windows.Controls.Primitives.Popup> のコンテンツ ウィンドウが開かれるか、閉じられると、<xref:System.Windows.Controls.Primitives.Popup.Opened> イベントおよび <xref:System.Windows.Controls.Primitives.Popup.Closed> イベントが発生します。  
  
<a name="Animation"></a>
### <a name="animation"></a>アニメーション  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールには、通常はフェードインやスライドインのような動作に関連付けられているアニメーションの組み込みサポートがあります。 <xref:System.Windows.Controls.Primitives.Popup.PopupAnimation%2A> プロパティを <xref:System.Windows.Controls.Primitives.PopupAnimation> 列挙値に設定することで、これらのアニメーションをオンにできます。 <xref:System.Windows.Controls.Primitives.Popup> アニメーションが正常に動作するには、<xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> プロパティを `true` に設定する必要があります。  
  
 <xref:System.Windows.Media.Animation.Storyboard> のようなアニメーションを <xref:System.Windows.Controls.Primitives.Popup> コントロールに適用することもできます。  
  
<a name="OpacityandBitmapEffects"></a>
### <a name="opacity-and-bitmap-effects"></a>不透明度とビットマップ効果  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールの <xref:System.Windows.UIElement.Opacity%2A> プロパティによって、その内容が影響を受けることはありません。 既定では、<xref:System.Windows.Controls.Primitives.Popup> のコンテンツ ウィンドウは非透過的です。 透過的な <xref:System.Windows.Controls.Primitives.Popup> を作成するには、<xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> プロパティを `true` に設定します。  
  
 <xref:System.Windows.Controls.Primitives.Popup> の内容では、<xref:System.Windows.Controls.Primitives.Popup> コントロールまたは親ウィンドウの他の要素に直接設定されているビットマップ効果 (<xref:System.Windows.Media.Effects.DropShadowBitmapEffect> など) は継承されません。 ビットマップ効果が <xref:System.Windows.Controls.Primitives.Popup> の内容に表示されるにするには、その内容に直接ビットマップ効果を設定する必要があります。 たとえば、<xref:System.Windows.Controls.Primitives.Popup> の子が <xref:System.Windows.Controls.StackPanel> の場合は、<xref:System.Windows.Controls.StackPanel> にビットマップ効果を設定します。  
  
<a name="PopupSize"></a>
### <a name="popup-size"></a>ポップアップのサイズ  
 既定では、<xref:System.Windows.Controls.Primitives.Popup> のサイズはその内容に合わせて自動的に調整されます。 自動サイズ調整が発生したとき、<xref:System.Windows.Controls.Primitives.Popup> の内容に対して定義された画面領域の既定のサイズがビットマップ効果を表示するのに十分でないため、一部のビットマップ効果が非表示になる場合があります。  
  
 <xref:System.Windows.Controls.Primitives.Popup> の内容に <xref:System.Windows.UIElement.RenderTransform%2A> を設定すると、内容が見えにくくなることもあります。 このシナリオでは、変換された <xref:System.Windows.Controls.Primitives.Popup> が元の <xref:System.Windows.Controls.Primitives.Popup> の領域からはみ出して拡大された場合、一部の内容が隠れる場合があります。 ビットマップ効果または変換によって必要な領域が増える場合、より多くの領域をコントロールに提供するために、<xref:System.Windows.Controls.Primitives.Popup> のコンテンツの周囲に余白を定義することができます。  
  
<a name="DefiningPopupPosition"></a>
## <a name="defining-the-popup-position"></a>ポップアップ位置の定義  
 ポップアップの位置は、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>、<xref:System.Windows.Controls.Primitives.Popup.VerticalOffsetProperty> の各プロパティで設定できます。 詳細については、「[Popup Placement Behavior](popup-placement-behavior.md)」を参照してください。 画面に <xref:System.Windows.Controls.Primitives.Popup> が表示されている場合、その親の位置を変更しても、それ自体の位置は変更されません。  
  
<a name="CustomizingPopupPlacement"></a>
### <a name="customizing-popup-placement"></a>ポップアップの配置のカスタマイズ  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールの配置は、<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> を基準として、<xref:System.Windows.Controls.Primitives.Popup> を表示する場所の座標のセットを指定することにより、カスタマイズできます。  
  
 配置をカスタマイズするには、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティを <xref:System.Windows.Controls.Primitives.PlacementMode.Custom> に設定します。 次に、<xref:System.Windows.Controls.Primitives.Popup> に対して可能な一連の配置ポイントとプライマリ軸を (優先順に) 返す <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> デリゲートを定義します。 <xref:System.Windows.Controls.Primitives.Popup> の表示が最大になるポイントが自動的に選択されます。 例については、「[方法 : ポップアップのカスタム位置を指定する](how-to-specify-a-custom-popup-position.md)」をご覧ください。  
  
<a name="PopupandtheVisualTree"></a>
## <a name="popup-and-the-visual-tree"></a>ポップアップとビジュアル ツリー  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールには独自のビジュアル ツリーはありません。<xref:System.Windows.Controls.Primitives.Popup> の <xref:System.Windows.Controls.Primitives.Popup.MeasureOverride%2A> メソッドを呼び出すと、代わりにサイズ 0 (ゼロ) が返されます。 ただし、<xref:System.Windows.Controls.Primitives.Popup> の <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> プロパティを `true` に設定すると、独自のビジュアル ツリーが含まれる新しいウィンドウが作成されます。 新しいウィンドウには、<xref:System.Windows.Controls.Primitives.Popup> の <xref:System.Windows.Controls.Primitives.Popup.Child%2A> の内容が含まれます。 新しいウィンドウの幅および高さは、画面の幅または高さの 75% より大きくすることはできません。  
  
 <xref:System.Windows.Controls.Primitives.Popup> コントロールには、その <xref:System.Windows.Controls.Primitives.Popup.Child%2A> の内容に対する参照が、論理的な子として維持されています。 新しいウィンドウが作成されると、<xref:System.Windows.Controls.Primitives.Popup> の内容がウィンドウのビジュアルな子になり、<xref:System.Windows.Controls.Primitives.Popup> の論理的な子はそのままになります。 逆に、<xref:System.Windows.Controls.Primitives.Popup> は、その <xref:System.Windows.Controls.Primitives.Popup.Child%2A> の内容の論理的な親のままになります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.Popup>
- <xref:System.Windows.Controls.Primitives.PopupPrimaryAxis>
- <xref:System.Windows.Controls.Primitives.PlacementMode>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>
- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [方法トピック](popup-how-to-topics.md)
- [方法トピック](tooltip-how-to-topics.md)
