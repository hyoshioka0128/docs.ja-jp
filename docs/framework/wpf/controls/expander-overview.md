---
title: エキスパンダーの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], Expander
- Expander control [WPF], about Expander control
ms.assetid: 877bf425-0e54-49ec-8fd2-13a211377abb
ms.openlocfilehash: 892d972a5704d50e91d04e05d6fdea7180a3155d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187109"
---
# <a name="expander-overview"></a>エキスパンダーの概要
<xref:System.Windows.Controls.Expander> コントロールでは、ウィンドウに似た、ヘッダーを持つ展開可能な領域内にコンテンツを表示する手段が提供されます。  

<a name="CreatinganExpanderinXAML"></a>
## <a name="creating-a-simple-expander"></a>単純なエキスパンダーの作成  
 次の例では、単純な <xref:System.Windows.Controls.Expander> コントロールの作成方法を示します。 この例では、前の図のような外観の <xref:System.Windows.Controls.Expander> を作成します。  
  
 [!code-xaml[ExpanderExample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderExample/CSharp/Page1.xaml#2)]  
  
 <xref:System.Windows.Controls.Expander> の <xref:System.Windows.Controls.ContentControl.Content%2A> および <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> には、<xref:System.Windows.Controls.RadioButton> オブジェクトや <xref:System.Windows.Controls.Image> オブジェクトなどの複雑なコンテンツも格納できます。  
  
<a name="SettingtheDirectionoftheExpandingWindow"></a>
## <a name="setting-the-direction-of-the-expanding-content-area"></a>コンテンツ エリアの展開方向の設定  
 <xref:System.Windows.Controls.ExpandDirection> プロパティを使用することにより、<xref:System.Windows.Controls.Expander> コントロールのコンテンツ領域を 4 つの方向 (<xref:System.Windows.Controls.ExpandDirection.Down>、<xref:System.Windows.Controls.ExpandDirection.Up>、<xref:System.Windows.Controls.ExpandDirection.Left>、<xref:System.Windows.Controls.ExpandDirection.Right>) のいずれかに展開するように設定できます。 コンテンツ領域が折りたたまれると、<xref:System.Windows.Controls.Expander> の <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> とそのトグル ボタンのみが表示されます。 コンテンツ領域を展開したり、折りたたんだりするトグル ボタンとしては、方向矢印を表示する <xref:System.Windows.Controls.Button> コントロールが使用されます。 展開時には、<xref:System.Windows.Controls.Expander> により、ウィンドウに似た領域内にそのすべてのコンテンツの表示が試みられます。  
  
<a name="SettingSizeDimensionsonanExpanderinaPanel"></a>
## <a name="controlling-the-size-of-an-expander-in-a-panel"></a>パネル内のエキスパンダーのサイズの制御  
 <xref:System.Windows.Controls.Expander> コントロールが <xref:System.Windows.Controls.Panel> から継承される <xref:System.Windows.Controls.StackPanel> などのレイアウト コントロールの内側にあり、<xref:System.Windows.Controls.Expander.ExpandDirection%2A> プロパティが <xref:System.Windows.Controls.ExpandDirection.Down> または <xref:System.Windows.Controls.ExpandDirection.Up> に設定されている場合は、<xref:System.Windows.Controls.Expander> に対して <xref:System.Windows.FrameworkElement.Height%2A> を指定しないでください。 同様に、<xref:System.Windows.Controls.Expander.ExpandDirection%2A> プロパティが <xref:System.Windows.Controls.ExpandDirection.Left> または <xref:System.Windows.Controls.ExpandDirection.Right> に設定されている場合は、<xref:System.Windows.Controls.Expander> に対して <xref:System.Windows.FrameworkElement.Width%2A> を指定しないでください。  
  
 展開されたコンテンツが表示される方向のサイズを <xref:System.Windows.Controls.Expander> コントロールに対して設定すると、コンテンツで使用される領域が <xref:System.Windows.Controls.Expander> によって制御され、その周囲に境界線が表示されます。 コンテンツが折りたたまれても、境界線は表示されます。 展開されたコンテンツ エリアのサイズを設定するには、<xref:System.Windows.Controls.Expander> のコンテンツに対してサイズを設定します。スクロール可能にする場合は、コンテンツを囲む <xref:System.Windows.Controls.ScrollViewer> に対してサイズを設定します。  
  
 <xref:System.Windows.Controls.Expander> コントロールが <xref:System.Windows.Controls.DockPanel> の最後の要素である場合は、<xref:System.Windows.Controls.DockPanel> の残りの領域に等しくなるように、<xref:System.Windows.Controls.Expander> のサイズが [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] によって自動的に設定されます。 この既定の動作を回避するには、<xref:System.Windows.Controls.DockPanel> オブジェクトの <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> プロパティを `false` に設定するか、<xref:System.Windows.Controls.Expander> が <xref:System.Windows.Controls.DockPanel> の最後の要素にならないようにします。  
  
<a name="CreatingScrollableContent"></a>
## <a name="creating-scrollable-content"></a>スクロール可能なコンテンツの作成  
 コンテンツが大きすぎて、コンテンツ領域に表示できない場合は、<xref:System.Windows.Controls.Expander> のコンテンツを <xref:System.Windows.Controls.ScrollViewer> 内にラップすることで、コンテンツをスクロール可能にすることができます。 <xref:System.Windows.Controls.Expander> コントロールでは、スクロール機能は自動的には提供されません。 次の図では、<xref:System.Windows.Controls.ScrollViewer> コントロールが含まれる <xref:System.Windows.Controls.Expander> コントロールを示します。  
  
 **ScrollViewer 内のエキスパンダー**  
  
 ![ScrollBar 付きのエキスパンダーを示すスクリーンショット。](./media/expander-overview/expander-scrollbar-control.jpg)  
  
 <xref:System.Windows.Controls.Expander> コントロールを <xref:System.Windows.Controls.ScrollViewer> 内に配置する場合は、<xref:System.Windows.Controls.Expander> のコンテンツが開く方向に対応する <xref:System.Windows.Controls.ScrollViewer> サイズ プロパティを、<xref:System.Windows.Controls.Expander> のコンテンツ領域のサイズに設定します。 たとえば、<xref:System.Windows.Controls.Expander> の <xref:System.Windows.Controls.Expander.ExpandDirection%2A> プロパティを <xref:System.Windows.Controls.ExpandDirection.Down> (コンテンツ領域を下に開く) に設定する場合は、<xref:System.Windows.Controls.ScrollViewer> コントロールの <xref:System.Windows.FrameworkElement.Height%2A> プロパティを、コンテンツ領域に必要な高さに設定します。 このように設定しないで、コンテンツ自体の高さにサイズを設定しても、この設定は <xref:System.Windows.Controls.ScrollViewer> に認識されないため、コンテンツはスクロール可能になりません。  
  
 次の例では、コンテンツが複雑で、<xref:System.Windows.Controls.ScrollViewer> コントロールが含まれる <xref:System.Windows.Controls.Expander> コントロールを作成する方法を示します。 この例では、このセクションの冒頭で示した図のような <xref:System.Windows.Controls.Expander> を作成します。  
  
 [!code-csharp[ExpanderRichContent#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ExpanderRichContent#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpanderRichContent/VisualBasic/Window1.xaml.vb#1)]
 [!code-xaml[ExpanderRichContent#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#1)]  
  
<a name="UsingtheAlignmentProperties"></a>
## <a name="using-the-alignment-properties"></a>配置プロパティの使用  
 コンテンツの配置を設定するには、<xref:System.Windows.Controls.Expander> コントロールの <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> プロパティと <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> プロパティを設定します。 これらのプロパティを設定すると、配置がヘッダーに適用され、展開されたコンテンツにも適用されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Expander>
- <xref:System.Windows.Controls.ExpandDirection>
- [方法トピック](expander-how-to-topics.md)
