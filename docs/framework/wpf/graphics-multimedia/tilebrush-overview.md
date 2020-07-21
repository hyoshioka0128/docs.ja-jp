---
title: TileBrush の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF]
- brushes [WPF], TileBrush
ms.assetid: aa4a7b7e-d09d-44c2-8d61-310c50e08d68
ms.openlocfilehash: 99bcc8695206030a381d71df2dda495867d3e9c7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187107"
---
# <a name="tilebrush-overview"></a>TileBrush の概要
<xref:System.Windows.Media.TileBrush> オブジェクトを使用すると、イメージ、<xref:System.Windows.Media.Drawing>、または <xref:System.Windows.Media.Visual> で領域を塗りつぶす方法を細かく制御できます。 ここでは、<xref:System.Windows.Media.TileBrush> の機能を使用して、<xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、または <xref:System.Windows.Media.VisualBrush> で領域を塗りつぶす方法を詳細に制御する方法について説明します。  

<a name="prerequisite"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、<xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、または <xref:System.Windows.Media.VisualBrush> の各クラスの基本的な機能の使用方法について理解しておくと役立ちます。 これらの型の概要については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。  
  
<a name="tilebrush"></a>
## <a name="painting-an-area-with-tiles"></a>タイルで領域を塗りつぶす  
 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、および <xref:System.Windows.Media.VisualBrush> は、<xref:System.Windows.Media.TileBrush> オブジェクトの種類です。 タイル ブラシを使用すると、イメージ、描画、またはビジュアルで領域を塗りつぶす方法を細かく制御できます。 たとえば、単一のイメージを引き伸ばして領域を塗りつぶすだけではなく、一連のイメージ タイルでパターンを作って領域を塗りつぶすことができます。  
  
 タイル ブラシによる領域の塗りつぶしには、コンテンツ、基本タイル、および出力領域の 3 つのコンポーネントが含まれます。  
  
 ![TileBrush のコンポーネント](./media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk_mmgraphics_defaultcontentprojection2")  
1 つのタイルを使用する TileBrush のコンポーネント  
  
 ![タイル表示された TileBrush のコンポーネント](./media/graphicsmm-tiledprojection.png "graphicsmm_tiledprojection")  
Tile の TileMode を使用する TileBrush のコンポーネント  
  
 出力領域とは、<xref:System.Windows.Shapes.Ellipse> の <xref:System.Windows.Shapes.Shape.Fill%2A> や <xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> など、塗りつぶされる領域のことです。 次のセクションでは、<xref:System.Windows.Media.TileBrush> の他の 2 つのコンポーネントについて説明します。  
  
<a name="brushcontent"></a>
## <a name="brush-content"></a>ブラシのコンテンツ  
 <xref:System.Windows.Media.TileBrush> には 3 つの種類があり、それぞれが異なる種類のコンテンツを使用して塗りつぶしを行います。  
  
- ブラシが <xref:System.Windows.Media.ImageBrush> の場合、このコンテンツはイメージです。<xref:System.Windows.Media.ImageBrush.ImageSource%2A> プロパティで <xref:System.Windows.Media.ImageBrush> のコンテンツを指定します。  
  
- ブラシが <xref:System.Windows.Media.DrawingBrush> の場合、このコンテンツは描画です。 <xref:System.Windows.Media.DrawingBrush.Drawing%2A> プロパティで <xref:System.Windows.Media.DrawingBrush> のコンテンツを指定します。  
  
- ブラシが <xref:System.Windows.Media.VisualBrush> の場合、このコンテンツはビジュアルです。 <xref:System.Windows.Media.VisualBrush.Visual%2A> プロパティで <xref:System.Windows.Media.VisualBrush> のコンテンツを指定します。  
  
 <xref:System.Windows.Media.TileBrush.Viewbox%2A> プロパティを使用して、<xref:System.Windows.Media.TileBrush> のコンテンツの位置とサイズを指定できます。ただし、この <xref:System.Windows.Media.TileBrush.Viewbox%2A> は、通常は既定値のままにしておきます。 既定では、<xref:System.Windows.Media.TileBrush.Viewbox%2A> は、ブラシのコンテンツを完全に含むように構成されます。 <xref:System.Windows.Controls.Viewbox> の構成の詳細については、<xref:System.Windows.Controls.Viewbox> プロパティのページを参照してください。  
  
<a name="thebasetile"></a>
## <a name="the-base-tile"></a>基本タイル  
 <xref:System.Windows.Media.TileBrush> は、そのコンテンツを基本タイルに投影します。 <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティにより、<xref:System.Windows.Media.TileBrush> のコンテンツを引き伸ばして基本タイルを塗りつぶす方法を制御します。 <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティは、<xref:System.Windows.Media.Stretch> 列挙型によって定義される次の値を受け取ります。  
  
- <xref:System.Windows.Media.Stretch.None>:ブラシのコンテンツは、タイルを塗りつぶすために引き伸ばされません。  
  
- <xref:System.Windows.Media.Stretch.Fill>:ブラシのコンテンツは、タイルに合わせて拡大縮小されます。 コンテンツの高さと幅は別々にスケーリングされるため、コンテンツの元の縦横比が維持されない場合があります。 つまり、出力タイルを完全に塗りつぶすために、ブラシのコンテンツがいびつになることがあります。  
  
- <xref:System.Windows.Media.Stretch.Uniform>:ブラシのコンテンツは、タイル内に完全に収まるように拡大縮小されます。 コンテンツの縦横比は維持されます。  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>:ブラシのコンテンツは、コンテンツの元の縦横比を維持しながら、出力領域を完全に塗りつぶすように拡大縮小されます。  
  
 <xref:System.Windows.Media.TileBrush.Stretch%2A> のさまざまな設定を次のイメージに示します。  
  
 ![異なる TileBrush Stretch 設定](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
  
 次の例では、<xref:System.Windows.Media.ImageBrush> のコンテンツは、出力領域を塗りつぶすために引き伸ばされない設定になっています。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMNoStretchExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/StretchExample.xaml#graphicsmmnostretchexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/StretchExample.cs#graphicsmmnostretchexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/stretchexample.vb#graphicsmmnostretchexample)]  
  
 既定では、<xref:System.Windows.Media.TileBrush> は 1 つのタイル (基本タイル) を生成し、出力領域が完全に塗りつぶされるようにそのタイルを引き伸ばします。 基本タイルのサイズと位置は、<xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティおよび <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティを設定して変更できます。  
  
<a name="basetilesize"></a>
### <a name="base-tile-size"></a>基本タイルのサイズ  
 <xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティは基本タイルのサイズと位置を決定し、<xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティは <xref:System.Windows.Media.TileBrush.Viewport%2A> で絶対座標と相対座標のどちらを使用するかを決定します。 座標が相対的な場合、座標は出力領域のサイズに対して相対的になります。 点 (0,0) は出力領域の左上隅を表し、(1,1) は出力領域の右下隅を表します。 <xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティで絶対座標を使用するように指定するには、<xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティを <xref:System.Windows.Media.BrushMappingMode.Absolute> に設定します。  
  
 <xref:System.Windows.Media.TileBrush> の <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> で相対座標を指定した場合と絶対座標を指定した場合の出力の違いを次の図に示します。 どの図も、並べて表示するパターンを示しています。次のセクションでは、パターンの指定方法について説明します。  
  
 ![ビューポートの絶対単位と相対単位](./media/absolute-and-relative-viewports.png "absolute_and_relative_viewports")  
  
 次の例では、イメージを使用して幅と高さが 50% のタイルを作成しています。 基本タイルは、出力領域の (0,0) の位置にあります。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmrelativeviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmrelativeviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmrelativeviewportunitsexample1)]  
  
 次の例では、<xref:System.Windows.Media.ImageBrush> のタイルを 25 x 25 のデバイスに依存しないピクセルに設定します。 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> は絶対値であるため、<xref:System.Windows.Media.ImageBrush> のタイルは、塗りつぶす領域のサイズに関係なく常に 25 x 25 ピクセルになります。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmabsoluteviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmabsoluteviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmabsoluteviewportunitsexample1)]  
  
<a name="tilingbehavior"></a>
### <a name="tiling-behavior"></a>並べて表示する動作  
 <xref:System.Windows.Media.TileBrush> が並べて表示するパターンを生成するのは、基本タイルが出力領域を完全に塗りつぶさず、並べて表示するモードが <xref:System.Windows.Media.TileMode.None> 以外に設定されている場合です。 タイル ブラシのタイルが出力領域を完全に塗りつぶさない場合、<xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティにより、出力領域を塗りつぶすために基本タイルを繰り返すかどうかを指定します。繰り返す場合は、繰り返し方法も指定します。 <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティは、<xref:System.Windows.Media.TileMode> 列挙型によって定義される次の値を受け取ります。  
  
- <xref:System.Windows.Media.TileMode.None>:基本タイルのみが描画されます。  
  
- <xref:System.Windows.Media.TileMode.Tile>:基本タイルが描画され、残りの領域は基本タイルの繰り返しによって塗りつぶされます。つまり、1 つのタイルの右端が次のタイルの左端に隣接し、同様に上端と下端も隣接します。  
  
- <xref:System.Windows.Media.TileMode.FlipX>:タイルが 1 列おきに左右に反転することを除き、<xref:System.Windows.Media.TileMode.Tile> と同じです。  
  
- <xref:System.Windows.Media.TileMode.FlipY>:タイルが 1 行おきに上下に反転することを除き、<xref:System.Windows.Media.TileMode.Tile> と同じです。  
  
- <xref:System.Windows.Media.TileMode.FlipXY>:<xref:System.Windows.Media.TileMode.FlipX> と <xref:System.Windows.Media.TileMode.FlipY> の組み合わせです。  
  
 並べて表示するさまざまなモードを次のイメージに示します。  
  
 ![TileBrush の TileMode のさまざまな設定](./media/img-mmgraphics-tilemodes.gif "img_mmgraphics_tilemodes")  
  
 次の例では、幅と高さが 100 ピクセルの四角形がイメージを使用して塗りつぶされます。 ブラシの <xref:System.Windows.Media.TileBrush.Viewport%2A> を 0,0,0.25,0.25 に設定することにより、ブラシの基本タイルは出力領域の 1/4 のサイズになります。 ブラシの <xref:System.Windows.Media.TileBrush.TileMode%2A> は <xref:System.Windows.Media.TileMode.FlipXY> に設定されます。 そのため、四角形はタイルの行で塗りつぶされます。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMFlipXYExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TilingExample.xaml#graphicsmmflipxyexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TilingExample.cs#graphicsmmflipxyexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilingexample.vb#graphicsmmflipxyexample)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.VisualBrush>
- <xref:System.Windows.Media.TileBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [方法トピック](brushes-how-to-topics.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
- [ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)
- [VisualBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)
