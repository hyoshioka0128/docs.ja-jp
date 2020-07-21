---
title: 配置、余白、パディングの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- margins [WPF]
- padding [WPF]
- aligning [WPF]
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
ms.openlocfilehash: bec2d9cd224febb650e2de67bb7406365d075963
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79145476"
---
# <a name="alignment-margins-and-padding-overview"></a>配置、余白、パディングの概要
<xref:System.Windows.FrameworkElement> クラスは、子要素の正確な配置に使用されるいくつかのプロパティを公開します。 このトピックでは、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> という 4 つの最も重要なプロパティについて説明します。 これらのプロパティの効果を理解することが重要です。[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションの要素の位置を制御するための基本となるためです。  

<a name="wcpsdk_layout_amp_introduction"></a>
## <a name="introduction-to-element-positioning"></a>要素配置の概要  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を利用し、さまざまな方法で要素を配置できます。 しかしながら、理想的なレイアウトを実現するには、単に正しい <xref:System.Windows.Controls.Panel> 要素を選択する以上の作業が必要になります。 配置を細かく制御するには、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティを理解する必要があります。  
  
 次の図は、いくつかの配置プロパティを利用したレイアウト シナリオのものです。  
  
 ![WPF 位置決めのプロパティのサンプル](./media/layout-margins-padding-alignment-graphic1.PNG "layout_margins_padding_alignment_graphic1")  
  
 一見したところ、この図の <xref:System.Windows.Controls.Button> 要素はランダムに配置されているように見えます。 しかしながら、位置は実際のところ、余白、配置、パディングを組み合わせることで正確に制御されます。  
  
 次の例は、前の図のレイアウトの作成方法を示しています。 <xref:System.Windows.Controls.Border> 要素が親 <xref:System.Windows.Controls.StackPanel> をカプセル化します。<xref:System.Windows.Controls.Border.Padding%2A> 値は 15 ピクセル (デバイス非依存) です。 これで狭い <xref:System.Windows.Media.Brushes.LightBlue%2A> 帯が作られ、それが子 <xref:System.Windows.Controls.StackPanel> を囲みます。 <xref:System.Windows.Controls.StackPanel> の子要素は、このトピックで説明するさまざまな配置プロパティを示します。 3 つの <xref:System.Windows.Controls.Button> 要素は、<xref:System.Windows.FrameworkElement.Margin%2A> プロパティと <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティの両方を示します。  
  
 [!code-csharp[MPALayoutSampleIntro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 次の図は、前のサンプルで使用されたさまざまな配置プロパティを大写しにしたものです。 このトピックの後続のセクションでは、各配置プロパティの使用方法をさらに詳しく説明します。  
  
 ![画面コールアウトを含む位置決めプロパティ](./media/layout-margins-padding-alignment-graphic2.PNG "layout_margins_padding_alignment_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>
## <a name="understanding-alignment-properties"></a>配置プロパティを理解する  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティと <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティは、親要素に割り当てられたレイアウト領域内で子要素をどのように配置するかを記述します。 これらのプロパティを一緒に使用することで、子要素を正確に配置できます。 たとえば、<xref:System.Windows.Controls.DockPanel> の子要素は 4 つの異なる水平配置 (<xref:System.Windows.HorizontalAlignment.Left>、<xref:System.Windows.HorizontalAlignment.Right>、<xref:System.Windows.HorizontalAlignment.Center>、<xref:System.Windows.HorizontalAlignment.Stretch>) を指定し、利用できる領域を埋めることができます。 垂直配置にも同様の値を利用できます。  
  
> [!NOTE]
> ある要素に明示的に設定された <xref:System.Windows.FrameworkElement.Height%2A> プロパティと <xref:System.Windows.FrameworkElement.Width%2A> プロパティは、<xref:System.Windows.HorizontalAlignment.Stretch> プロパティ値に優先します。 `Stretch` の <xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 値を設定すると、`Stretch` の要求が無視されます。  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>
### <a name="horizontalalignment-property"></a>HorizontalAlignment プロパティ  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティは、子要素に適用する水平配置特性を宣言します。 次の表は、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティの入力可能値をまとめたものです。  
  
|メンバー|説明|  
|------------|-----------------|  
|<xref:System.Windows.HorizontalAlignment.Left>|子要素は、親要素に割り当てられたレイアウト領域の左に揃えて配置されます。|  
|<xref:System.Windows.HorizontalAlignment.Center>|子要素は、親要素に割り当てられたレイアウト領域の中央に揃えて配置されます。|  
|<xref:System.Windows.HorizontalAlignment.Right>|子要素は、親要素に割り当てられたレイアウト領域の右に揃えて配置されます。|  
|<xref:System.Windows.HorizontalAlignment.Stretch> (既定値)|子要素は引き伸ばされ、親要素に割り当てられたレイアウト領域を埋めます。 明示的な <xref:System.Windows.FrameworkElement.Width%2A> 値と <xref:System.Windows.FrameworkElement.Height%2A> 値は優先されます。|  
  
 次の例は、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティを <xref:System.Windows.Controls.Button> 要素に適用する方法を示しています。 各属性値が示され、さまざまなレンダリング動作をより良く表しています。  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 前のコードは次の画像のようなレイアウトを作ります。 各 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 値の配置効果が図に現れています。  
  
 ![HorizontalAlignment のサンプル](./media/layout-horizontal-alignment-graphic.PNG "layout_horizontal_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>
### <a name="verticalalignment-property"></a>VerticalAlignment プロパティ  
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティは、子要素に適用する垂直配置特性を宣言します。 次の表は、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティの入力可能値をまとめたものです。  
  
|メンバー|説明|  
|------------|-----------------|  
|<xref:System.Windows.VerticalAlignment.Top>|子要素は、親要素に割り当てられたレイアウト領域の上に揃えて配置されます。|  
|<xref:System.Windows.VerticalAlignment.Center>|子要素は、親要素に割り当てられたレイアウト領域の中央に揃えて配置されます。|  
|<xref:System.Windows.VerticalAlignment.Bottom>|子要素は、親要素に割り当てられたレイアウト領域の下に揃えて配置されます。|  
|<xref:System.Windows.VerticalAlignment.Stretch> (既定値)|子要素は引き伸ばされ、親要素に割り当てられたレイアウト領域を埋めます。 明示的な <xref:System.Windows.FrameworkElement.Width%2A> 値と <xref:System.Windows.FrameworkElement.Height%2A> 値は優先されます。|  
  
 次の例は、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティを <xref:System.Windows.Controls.Button> 要素に適用する方法を示しています。 各属性値が示され、さまざまなレンダリング動作をより良く表しています。 このサンプルの目的として各プロパティ値のレイアウト動作をよく示すために、<xref:System.Windows.Controls.Grid> 要素を親として使用し、目盛りを付けています。  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xaml[MPALayoutVerticalAlignment#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 前のコードは次の画像のようなレイアウトを作ります。 各 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 値の配置効果が図に現れています。  
  
 ![VerticalAlignment プロパティのサンプル](./media/layout-vertical-alignment-graphic.PNG "layout_vertical_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>
## <a name="understanding-margin-properties"></a>余白プロパティを理解する  
 <xref:System.Windows.FrameworkElement.Margin%2A> プロパティは、ある要素とその子または同等要素の間の距離を表します。 <xref:System.Windows.FrameworkElement.Margin%2A> 値は統一することができます。`Margin="20"` のような構文を利用します。 この構文では、20 という均一の <xref:System.Windows.FrameworkElement.Margin%2A> ピクセル (デバイス非依存) が要素に適用されます。 <xref:System.Windows.FrameworkElement.Margin%2A> 値は 4 つの別個の値という形態を取ることもできます。それぞれの値が左、上、右、下に (この順序で) 適用される別個の余白を表します。`Margin="0,10,5,25"` のようになります。 <xref:System.Windows.FrameworkElement.Margin%2A> プロパティを適切に利用することで、要素、その近隣要素、子のレンダリング位置を微調整できます。  
  
> [!NOTE]
> ゼロ以外の余白は、要素の <xref:System.Windows.FrameworkElement.ActualWidth%2A> と <xref:System.Windows.FrameworkElement.ActualHeight%2A> の外にある領域を適用します。  
  
 次の例は、<xref:System.Windows.Controls.Button> 要素のグループの周辺に均一な余白を適用する方法を示しています。 <xref:System.Windows.Controls.Button> 要素の間隔が均一に取られます。各方向に 10 ピクセルの余白が与えられます。  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xaml[MarginPaddingAlignmentSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 多くの場合、均一余白は適切ではありません。 適切でなければ、均一ではない間隔を適用できます。 次の例は、均一ではない余白間隔を子要素に適用する方法を示しています。 余白は左、上、右、下の順序で記述されます。  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xaml[MarginPaddingAlignmentSample#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>
## <a name="understanding-the-padding-property"></a>Padding プロパティを理解する  
 パディングは多くの点で <xref:System.Windows.FrameworkElement.Margin%2A> に似ています。 Padding プロパティは、利便性を主な目的として、ほんの一部のクラスのみで公開されます。<xref:System.Windows.Documents.Block>、<xref:System.Windows.Controls.Border>、<xref:System.Windows.Controls.Control>、<xref:System.Windows.Controls.TextBlock> は Padding プロパティを公開するクラスの一例です。 <xref:System.Windows.Controls.Border.Padding%2A> プロパティは、指定された <xref:System.Windows.Thickness> 値の分だけ子要素の有効サイズを拡大します。  
  
 次の例は、<xref:System.Windows.Controls.Border.Padding%2A> を親の <xref:System.Windows.Controls.Border> 要素に適用する方法を示しています。  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xaml[MarginPaddingAlignmentSample#3](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>
## <a name="using-alignment-margins-and-padding-in-an-application"></a>アプリケーションで配置、余白、パディングを利用する  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> で、複雑な [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] の作成に必要な配置制御が与えられます。 各プロパティの効果を利用し、子要素の配置を変更できます。動的なアプリケーション/ユーザー体験を生み出す柔軟性が与えられます。  
  
 次の例は、このトピックで説明した各概念を示しています。 この例はこのトピックの最初のサンプルのインフラストラクチャで構築されています。最初のサンプルに <xref:System.Windows.Controls.Border> の子として <xref:System.Windows.Controls.Grid> 要素を追加しています。 <xref:System.Windows.Controls.Border.Padding%2A> は、親の <xref:System.Windows.Controls.Border> 要素に適用されます。 <xref:System.Windows.Controls.Grid> は、3 つの子 <xref:System.Windows.Controls.StackPanel> 要素間の空間を仕切るために使用されます。 <xref:System.Windows.Controls.Button> 要素が <xref:System.Windows.FrameworkElement.Margin%2A> と <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> のさまざまな効果を示すために再び使用されています。 <xref:System.Windows.Controls.TextBlock> 要素が各 <xref:System.Windows.Controls.ColumnDefinition> に追加され、各列の <xref:System.Windows.Controls.Button> 要素に適用されるさまざまなプロパティがさらに効果的に定義されます。  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xaml[MarginPaddingAlignmentSample#4](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 コンパイルすると、先のアプリケーションは次の図のような [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] になります。 要素間の間隔でさまざまなプロパティ値の効果が明らかになっています。各列の要素の重要なプロパティ値が <xref:System.Windows.Controls.TextBlock> 要素内で示されています。  
  
 ![1 つのアプリケーション内の複数の位置決めプロパティ](./media/layout-margins-padding-aligment-graphic3.PNG "layout_margins_padding_aligment_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>
## <a name="whats-next"></a>次の内容  
 <xref:System.Windows.FrameworkElement> クラスにより定義された位置決めプロパティにより、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内で要素配置の微調整が可能になります。 これで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を利用して効果的に要素を配置するための手法を理解できたことでしょう。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウトの詳細はその他の資料で確認できます。 「[パネルの概要](../controls/panels-overview.md)」というトピックでは、さまざまな <xref:System.Windows.Controls.Panel> 要素についてさらに詳しく説明しています。 「[チュートリアル:初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」というトピックでは、レイアウト要素を利用してコンポーネントを配置し、そのアクションをデータ ソースに結びつける高度な手法を紹介しています。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>
- <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>
- <xref:System.Windows.FrameworkElement.Margin%2A>
- [パネルの概要](../controls/panels-overview.md)
- [レイアウト](layout.md)
- [WPF レイアウト ギャラリー サンプル](https://go.microsoft.com/fwlink/?LinkID=160054)
