---
title: ブラシの概要
description: Windows Presentation Foundation (WPF) でグラデーションとパターンを使用して、単純な純色で描画することによって、概念を示す方法を説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: 9bfd702d7a5a9d807e2b922874119c2bb2e68f39
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853715"
---
# <a name="wpf-brushes-overview"></a>WPF のブラシの概要
画面上に表示されるすべてのものが見えるのは、ブラシで描画されているからです。 たとえば、ボタンの背景、テキストの前景、図形の塗りつぶしを表現するためにブラシが使用されます。 このトピックでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ブラシを使用した塗りつぶしの概念を紹介し、いくつかの例を示します。 ブラシを使用すると、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] オブジェクトを単色で塗りつぶすことも、パターンとイメージの複雑な組み合わせで塗りつぶすこともできます。  
  
<a name="paintingwithbrush"></a>
## <a name="painting-with-a-brush"></a>ブラシによる塗りつぶし  
 <xref:System.Windows.Media.Brush> は、その出力によって領域を "塗りつぶし" ます。 ブラシが異なれば、出力の種類も異なります。 ブラシには、単色で領域を塗りつぶすものや、グラデーション、パターン、画像、または描画によって領域を塗りつぶすものがあります。 次の図は、各種の <xref:System.Windows.Media.Brush> の例を示しています。  
  
 ![ブラシの種類](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
ブラシの例  
  
 ほとんどのビジュアル オブジェクトで、その塗りつぶし方法を指定できます。 次の表に、<xref:System.Windows.Media.Brush> を使用できる一般的なオブジェクトとプロパティの一覧を示します。  
  
|クラス|ブラシのプロパティ|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>、<xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>、<xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 次のセクションでは、各種の <xref:System.Windows.Media.Brush> について説明し、それぞれの例を示します。  
  
<a name="paintwithsolidcolorbrush"></a>
## <a name="paint-with-a-solid-color"></a>単色で塗りつぶす  
 <xref:System.Windows.Media.SolidColorBrush> は、1 つの <xref:System.Windows.Media.Color> で領域を塗りつぶします。 <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> を指定する方法はさまざまです。たとえば、アルファ、赤、青、および緑のチャネルを指定することや、<xref:System.Windows.Media.Colors> クラスによって提供される定義済みの色のいずれかを使用できます。  
  
 次の例では、<xref:System.Windows.Media.SolidColorBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![SolidColorBrush を使用して塗りつぶされた四角形](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
SolidColorBrush を使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 <xref:System.Windows.Media.SolidColorBrush> クラスの詳細については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」をご覧ください。  
  
<a name="paintwithlineargradientbrush"></a>
## <a name="paint-with-a-linear-gradient"></a>線形グラデーションを使用して塗りつぶす  
 <xref:System.Windows.Media.LinearGradientBrush> は、線形グラデーションを使用して領域を塗りつぶします。 線形グラデーションは、直線 (グラデーション軸) に沿って 2 つ以上の色をブレンドします。 <xref:System.Windows.Media.GradientStop> オブジェクトを使用して、グラデーションの色とその位置を指定します。  
  
 次の例では、<xref:System.Windows.Media.LinearGradientBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![LinearGradientBrush を使用して塗りつぶされた四角形](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
LinearGradientBrush を使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 <xref:System.Windows.Media.LinearGradientBrush> クラスの詳細については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」を参照してください。  
  
<a name="paintwithradialgradientbrush"></a>
## <a name="paint-with-a-radial-gradient"></a>放射状グラデーションを使用して塗りつぶす  
 <xref:System.Windows.Media.RadialGradientBrush> は、放射状グラデーションを使用して領域を塗りつぶします。 放射状グラデーションは、円に沿って 2 つ以上の色をブレンドします。 <xref:System.Windows.Media.LinearGradientBrush> クラスと同様に、<xref:System.Windows.Media.GradientStop> オブジェクトを使用して、グラデーションの色とその位置を指定します。  
  
 次の例では、<xref:System.Windows.Media.RadialGradientBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![RadialGradientBrush を使用して塗りつぶされた四角形](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
RadialGradientBrush を使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 <xref:System.Windows.Media.RadialGradientBrush> クラスの詳細については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」を参照してください。  
  
<a name="paintwithimage"></a>
## <a name="paint-with-an-image"></a>イメージを使用して塗りつぶす  
 <xref:System.Windows.Media.ImageBrush> は、<xref:System.Windows.Media.ImageSource> を使用して領域を塗りつぶします。  
  
 次の例では、<xref:System.Windows.Media.ImageBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![ImageBrush によって塗りつぶされた四角形](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
イメージを使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 <xref:System.Windows.Media.ImageBrush> クラスの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。  
  
<a name="paintwithdrawing"></a>
## <a name="paint-with-a-drawing"></a>描画を使用して塗りつぶす  
 <xref:System.Windows.Media.DrawingBrush> は、<xref:System.Windows.Media.Drawing> を使用して領域を塗りつぶします。 <xref:System.Windows.Media.Drawing> には、図形、イメージ、テキスト、およびメディアを格納できます。  
  
 次の例では、<xref:System.Windows.Media.DrawingBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![DrawingBrush を使用して塗りつぶされた四角形](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
DrawingBrush を使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 <xref:System.Windows.Media.DrawingBrush> クラスの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」をご覧ください。  
  
<a name="paintwithvisual"></a>
## <a name="paint-with-a-visual"></a>ビジュアルを使用して塗りつぶす  
 <xref:System.Windows.Media.VisualBrush> は、<xref:System.Windows.Media.Visual> オブジェクトを使用して領域を塗りつぶします。 ビジュアル オブジェクトの例としては、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Controls.MediaElement> などがあります。 <xref:System.Windows.Media.VisualBrush> を使用すると、アプリケーションのある部分から別の領域にコンテンツを投影することもできます。これは、反射効果を作成する場合や、画面の一部を拡大する場合に非常に便利です。  
  
 次の例では、<xref:System.Windows.Media.VisualBrush> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 次の図は、塗りつぶされた四角形を示しています。  
  
 ![VisualBrush を使用して塗りつぶされた四角形](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
VisualBrush を使用して塗りつぶされた四角形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 <xref:System.Windows.Media.VisualBrush> クラスの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」をご覧ください。  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>
## <a name="paint-using-predefined-and-system-brushes"></a>定義済みブラシとシステム ブラシを使用して塗りつぶす  
 利便性のために、Windows Presentation Foundation (WPF) には、オブジェクトの塗りつぶしに使用できる一連の定義済みブラシとシステム ブラシが用意されています。  
  
- 使用できる定義済みブラシの一覧については、<xref:System.Windows.Media.Brushes> クラスをご覧ください。 定義済みブラシの使用方法を示す例については、「[純色で領域を塗りつぶす](how-to-paint-an-area-with-a-solid-color.md)」をご覧ください。  
  
- 使用できるシステム ブラシの一覧については、<xref:System.Windows.SystemColors> クラスをご覧ください。 例については、「[システム ブラシで領域を塗りつぶす](how-to-paint-an-area-with-a-system-brush.md)」をご覧ください。  
  
<a name="commonbrushfeatures"></a>
## <a name="common-brush-features"></a>ブラシの一般的な機能  
 <xref:System.Windows.Media.Brush> オブジェクトには、ブラシを透明または部分的に透明にするために使用できる <xref:System.Windows.Media.Brush.Opacity%2A> プロパティが用意されています。 <xref:System.Windows.Media.Brush.Opacity%2A> の値が 0 の場合、ブラシは完全に透明になります。一方、<xref:System.Windows.Media.Brush.Opacity%2A> の値が 1 の場合、ブラシは完全に不透明になります。 次の例では、<xref:System.Windows.Media.Brush.Opacity%2A> プロパティを使用して、<xref:System.Windows.Media.SolidColorBrush> を 25% 不透明にします。  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 ブラシに部分的に透明な色が含まれる場合、色の不透明度の値は、ブラシの不透明度の値を乗算して算出されます。 たとえば、ブラシの不透明度の値が 0.5 で、ブラシで使用される色の不透明度の値も 0.5 の場合、出力の色の不透明度の値は 0.25 になります。  
  
> [!NOTE]
> <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> プロパティを使用して、要素全体の不透明度を変更するよりも、ブラシの不透明度の値を変更する方が効率的です。  
  
 <xref:System.Windows.Media.Brush.Transform%2A> または <xref:System.Windows.Media.Brush.RelativeTransform%2A> プロパティを使用することで、ブラシのコンテンツを回転、拡大縮小、傾斜、および移動できます。 詳細については、「[ブラシの変換の概要](brush-transformation-overview.md)」を参照してください。  
  
 <xref:System.Windows.Media.Brush> オブジェクトは <xref:System.Windows.Media.Animation.Animatable> オブジェクトであるため、アニメーション化できます。 詳しくは、「 [アニメーションの概要](animation-overview.md)」をご覧ください。  
  
<a name="freezable_features"></a>
### <a name="freezable-features"></a>Freezable 機能  
 <xref:System.Windows.Media.Brush> クラスは <xref:System.Windows.Freezable> クラスを継承するため、いくつかの特殊な機能を備えています。つまり、<xref:System.Windows.Media.Brush> オブジェクトを[リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)として宣言すること、複数のオブジェクト間で共有すること、複製することができます。 さらに、<xref:System.Windows.Media.VisualBrush> を除くすべての種類の <xref:System.Windows.Media.Brush> を読み取り専用にして、パフォーマンスの向上とスレッドセーフを実現できます。  
  
 <xref:System.Windows.Freezable> オブジェクトで提供されるさまざまな機能について詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
 <xref:System.Windows.Media.VisualBrush> オブジェクトをフリーズできない理由について詳しくは、<xref:System.Windows.Media.VisualBrush> の種類に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
- [ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)
- [ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)
- [VisualBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)
- [方法トピック](brushes-how-to-topics.md)
- [パフォーマンスに関するその他の推奨事項](../advanced/optimizing-performance-other-recommendations.md)
