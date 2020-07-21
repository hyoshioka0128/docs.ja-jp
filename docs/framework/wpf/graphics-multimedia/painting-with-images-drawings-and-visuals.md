---
title: イメージ、描画、およびビジュアルによる塗りつぶし
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with drawings
- painting [WPF], with drawings
- painting [WPF], with images
- painting with visuals [WPF]
- brushes [WPF], painting with images
- brushes [WPF], painting with visuals
ms.assetid: 779aac3f-8d41-49d8-8130-768244aa2240
ms.openlocfilehash: e0e5e386b32425c87502d18a24e758193c14a5b6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186919"
---
# <a name="painting-with-images-drawings-and-visuals"></a>イメージ、描画、およびビジュアルによる塗りつぶし
このトピックでは、<xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、および <xref:System.Windows.Media.VisualBrush> の各オブジェクトを使用して、イメージ、<xref:System.Windows.Media.Drawing>、または <xref:System.Windows.Media.Visual> で領域を塗りつぶす方法について説明します。  

<a name="prereqs"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] に用意されているさまざまな種類のブラシとその基本的な機能を理解している必要があります。 概要については、「[WPF のブラシの概要](wpf-brushes-overview.md)」を参照してください。  
  
<a name="image"></a>
## <a name="paint-an-area-with-an-image"></a>イメージで領域を塗りつぶす  
 <xref:System.Windows.Media.ImageBrush> は、<xref:System.Windows.Media.ImageSource> を使用して領域を塗りつぶします。 <xref:System.Windows.Media.ImageBrush> と共に使用する最も一般的な <xref:System.Windows.Media.ImageSource> の種類は、ビットマップ グラフィックを記述する <xref:System.Windows.Media.Imaging.BitmapImage> です。 <xref:System.Windows.Media.Drawing> オブジェクトを使って塗りつぶすのに <xref:System.Windows.Media.DrawingImage> を使用できますが、代わりに <xref:System.Windows.Media.DrawingBrush> を使用する方が簡単です。 <xref:System.Windows.Media.ImageSource> オブジェクトの詳細については、「[イメージングの概要](imaging-overview.md)」を参照してください。  
  
 <xref:System.Windows.Media.ImageBrush> を使用して塗りつぶすには、<xref:System.Windows.Media.Imaging.BitmapImage> を作成し、それを使用してビットマップ コンテンツを読み込みます。 次に、<xref:System.Windows.Media.Imaging.BitmapImage> を使用して、<xref:System.Windows.Media.ImageBrush> の <xref:System.Windows.Media.ImageBrush.ImageSource%2A> プロパティを設定します。 最後に、塗りつぶすオブジェクトに <xref:System.Windows.Media.ImageBrush> を適用します。  [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、単に <xref:System.Windows.Media.ImageBrush> の <xref:System.Windows.Media.ImageBrush.ImageSource%2A> プロパティを、読み込むイメージのパスを含めて設定することもできます。  
  
 すべての <xref:System.Windows.Media.Brush> オブジェクトと同様に、<xref:System.Windows.Media.ImageBrush> を使用して、図形、パネル、コントロール、テキストなどのオブジェクトを塗りつぶすことができます。 次の図は、<xref:System.Windows.Media.ImageBrush> を使用して実現できる効果をいくつか示しています。  
  
 ![ImageBrush の出力例](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
ImageBrush で描画されたオブジェクト  
  
 既定では、<xref:System.Windows.Media.ImageBrush> は、塗りつぶされる領域を完全に埋めるようにイメージを引き伸ばします。このため、塗りつぶされる領域の縦横比がイメージの縦横比と異なる場合は、イメージがゆがむ可能性があります。 この動作を変更するには、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを既定値の <xref:System.Windows.Media.Stretch.Fill> から <xref:System.Windows.Media.Stretch.None>、<xref:System.Windows.Media.Stretch.Uniform>、または <xref:System.Windows.Media.Stretch.UniformToFill> に変更します。 <xref:System.Windows.Media.ImageBrush> は <xref:System.Windows.Media.TileBrush> の一種であるため、イメージ ブラシが出力領域を塗りつぶす方法を正確に指定し、さらにパターンを作成することもできます。 高度な <xref:System.Windows.Media.TileBrush> 機能の詳細については、「[TileBrush の概要](tilebrush-overview.md)」を参照してください。  
  
<a name="fillingpanelwithimage"></a>
## <a name="example-paint-an-object-with-a-bitmap-image"></a>例:ビットマップ イメージによるオブジェクトの塗りつぶし  
 次の例では、<xref:System.Windows.Media.ImageBrush> を使用して <xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Panel.Background%2A> を塗りつぶします。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/ImageBrushExample.xaml#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/ImageBrushExample.cs#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/imagebrushexample.vb#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
<a name="drawingbrushintro"></a>
## <a name="paint-an-area-with-a-drawing"></a>描画を使用して領域を塗りつぶす  
 <xref:System.Windows.Media.DrawingBrush> を使用すると、図形、テキスト、イメージ、およびビデオで領域を塗りつぶすことができます。 描画ブラシ内の図形そのものを、純色、グラデーション、イメージ、または別の <xref:System.Windows.Media.DrawingBrush> で塗りつぶすこともできます。 次の図は、<xref:System.Windows.Media.DrawingBrush> の使用法をいくつか示しています。  
  
 ![DrawingBrush の出力例](./media/wcpsdk-mmgraphics-drawingbrushexamples.png "wcpsdk_mmgraphics_drawingbrushexamples")  
DrawingBrush で塗りつぶされたオブジェクト  
  
 <xref:System.Windows.Media.DrawingBrush> は、<xref:System.Windows.Media.Drawing> オブジェクトを使用して領域を塗りつぶします。 <xref:System.Windows.Media.Drawing> オブジェクトでは、図形、ビットマップ、ビデオ、テキスト行などの表示可能なコンテンツを記述します。 さまざまな種類の描画で、さまざまな種類のコンテンツを記述します。 次の一覧に、さまざまな種類の描画オブジェクトを示します。  
  
- <xref:System.Windows.Media.GeometryDrawing> - 図形を描画します。  
  
- <xref:System.Windows.Media.ImageDrawing> - イメージを描画します。  
  
- <xref:System.Windows.Media.GlyphRunDrawing> - テキストを描画します。  
  
- <xref:System.Windows.Media.VideoDrawing> - オーディオまたはビデオのファイルを再生します。  
  
- <xref:System.Windows.Media.DrawingGroup> - その他の描画を描きます。 他の描画を 1 つの複合描画に結合するには、描画グループを使用します。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトの詳細については、「[Drawing オブジェクトの概要](drawing-objects-overview.md)」を参照してください。  
  
 <xref:System.Windows.Media.DrawingBrush> は、<xref:System.Windows.Media.ImageBrush> と同様に、その <xref:System.Windows.Media.DrawingBrush.Drawing%2A> を引き伸ばして出力領域を塗りつぶします。 この動作をオーバーライドするには、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを既定の設定の<xref:System.Windows.Media.Stretch.Fill> から変更します。 詳細については、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを参照してください。  
  
<a name="fillingareawithdrawingbrushexample"></a>
## <a name="example-paint-an-object-with-a-drawing"></a>例:描画によるオブジェクトの塗りつぶし  
 次の例は、3 つの楕円の描画によってオブジェクトを塗りつぶす方法を示しています。 楕円を記述するには、<xref:System.Windows.Media.GeometryDrawing> を使用します。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/DrawingBrushExample.xaml#graphicsmmdrawingbrushasbuttonbackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/DrawingBrushExample.cs#graphicsmmdrawingbrushasbuttonbackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/drawingbrushexample.vb#graphicsmmdrawingbrushasbuttonbackgroundexample1)]  
  
<a name="visualbrushsection"></a>
## <a name="paint-an-area-with-a-visual"></a>ビジュアルで領域を塗りつぶす  
 すべてのブラシの中で最も汎用性が高く強力な <xref:System.Windows.Media.VisualBrush> は <xref:System.Windows.Media.Visual> を使用して領域を塗りつぶします。 <xref:System.Windows.Media.Visual> は多くの便利なグラフィカル コンポーネントの上位クラスとして機能する低レベルのグラフィカルの種類です。 たとえば、<xref:System.Windows.Window>、<xref:System.Windows.FrameworkElement>、および <xref:System.Windows.Controls.Control> クラスは、すべて <xref:System.Windows.Media.Visual> オブジェクトの種類です。 <xref:System.Windows.Media.VisualBrush> を使用すると、ほとんどすべての [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] グラフィカル オブジェクトで領域を塗りつぶすことができます。  
  
> [!NOTE]
> <xref:System.Windows.Media.VisualBrush> は <xref:System.Windows.Freezable> オブジェクトの一種ですが、<xref:System.Windows.Media.VisualBrush.Visual%2A> プロパティが `null` 以外の値に設定されている場合は、固定 (読み取り専用に) することはできません。  
  
 <xref:System.Windows.Media.VisualBrush> の <xref:System.Windows.Media.VisualBrush.Visual%2A> コンテンツを指定する方法は 2 つあります。  
  
- 新しい <xref:System.Windows.Media.Visual> を作成し、それを使用して <xref:System.Windows.Media.VisualBrush> の <xref:System.Windows.Media.VisualBrush.Visual%2A> プロパティを設定する。 例については、「[例: ビジュアルによるオブジェクトの塗りつぶし](#examplevisualbrush1)」という後続のセクションを参照してください。  
  
- ターゲットの <xref:System.Windows.Media.Visual> の複製イメージを作成する既存の <xref:System.Windows.Media.Visual> を使用する。 その後、<xref:System.Windows.Media.VisualBrush> を使用して、反射や拡大などの面白い効果を作り出すことができます。 例については、「[例: 反射を作成する](#examplevisualbrush2)」セクションを参照してください。  
  
 <xref:System.Windows.Media.VisualBrush> の新しい <xref:System.Windows.Media.VisualBrush.Visual%2A> を定義し、その <xref:System.Windows.Media.Visual> が <xref:System.Windows.UIElement> (パネルやコントロールなど) である場合、<xref:System.Windows.Media.VisualBrush.AutoLayoutContent%2A> プロパティが `true` に設定されていると、レイアウト システムは <xref:System.Windows.UIElement> とその子要素に対して実行されます。 ただし、ルートの <xref:System.Windows.UIElement> が基本的にシステムの残りの部分 (スタイル) から分離されているため、外部レイアウトはこの境界を超えられません。 ルートの <xref:System.Windows.UIElement> は、唯一の親が <xref:System.Windows.Media.VisualBrush> であるために塗りつぶす領域に合わせて自動的にそれ自体のサイズを調整できないので、そのサイズを明示的に指定する必要があります。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でのレイアウトの詳細については、「[レイアウト](../advanced/layout.md)」を参照してください。  
  
 <xref:System.Windows.Media.ImageBrush> や <xref:System.Windows.Media.DrawingBrush> と同様に、<xref:System.Windows.Media.VisualBrush> はそのコンテンツを引き伸ばして出力領域を塗りつぶします。 この動作をオーバーライドするには、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを既定の設定の<xref:System.Windows.Media.Stretch.Fill> から変更します。 詳細については、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを参照してください。  
  
<a name="examplevisualbrush1"></a>
## <a name="example-paint-an-object-with-a-visual"></a>例:ビジュアルによるオブジェクトの塗りつぶし  
 次の例では、さまざまなコントロールとパネルを使用して四角形を塗りつぶします。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/VisualBrushExample.xaml#graphicsmmvisualbrushasrectanglebackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/VisualBrushExample.cs#graphicsmmvisualbrushasrectanglebackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/visualbrushexample.vb#graphicsmmvisualbrushasrectanglebackgroundexample1)]  
  
<a name="examplevisualbrush2"></a>
## <a name="example-create-a-reflection"></a>例:反射を作成する  
 前の例では、背景として使用する新しい <xref:System.Windows.Media.Visual> を作成する方法を示しました。 <xref:System.Windows.Media.VisualBrush> は、既存のビジュアルを表示するために使用することもできます。この機能により、反射や拡大などの興味深い視覚効果を生み出すことができます。 次の例では、<xref:System.Windows.Media.VisualBrush> を使用して、複数の要素を含む <xref:System.Windows.Controls.Border> の反射を作成します。 次の図は、この例で生成される出力を示しています。  
  
 ![反映された Visual オブジェクト](./media/graphicsmm-visualbrush-reflection-small.jpg "graphicsmm_visualbrush_reflection_small")  
反映された Visual オブジェクト  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xaml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 画面の一部を引き伸ばす方法と反射を作成する方法のその他の例については、「[VisualBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)」を参照してください。  
  
<a name="tilebrush"></a>
## <a name="tilebrush-features"></a>TileBrush の機能  
 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、および <xref:System.Windows.Media.VisualBrush> は、<xref:System.Windows.Media.TileBrush> オブジェクトの種類です。 <xref:System.Windows.Media.TileBrush> オブジェクトを使用すると、イメージ、描画、またはビジュアルで領域を塗りつぶす方法を細かく制御できます。 たとえば、1 つのイメージを引き伸ばして領域を塗りつぶす代わりに、一連のイメージ タイルでパターンを作って領域を塗りつぶすことができます。  
  
 <xref:System.Windows.Media.TileBrush> には、コンテンツ、タイル、および出力領域という 3 つの主要コンポーネントがあります。  
  
 ![TileBrush コンポーネント](./media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk_mmgraphics_defaultcontentprojection2")  
1 つのタイルを使用する TileBrush のコンポーネント  
  
 ![タイル表示された TileBrush のコンポーネント](./media/graphicsmm-tiledprojection.png "graphicsmm_tiledprojection")  
複数のタイルを使用する TileBrush のコンポーネント  
  
 <xref:System.Windows.Media.TileBrush> オブジェクトの並べて表示する機能の詳細については、「[TileBrush の概要](tilebrush-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.VisualBrush>
- <xref:System.Windows.Media.TileBrush>
- [TileBrush の概要](tilebrush-overview.md)
- [WPF のブラシの概要](wpf-brushes-overview.md)
- [イメージングの概要](imaging-overview.md)
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [不透明度マスクの概要](opacity-masks-overview.md)
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
- [ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)
- [VisualBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)
