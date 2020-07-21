---
title: 図形と基本描画の概要
description: Windows Presentation Foundation (WPF) で、すぐに使用できるシェイプと複数レイヤーのレンダリング サービスを使用して、ユーザー インターフェイスを強化します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- shapes [WPF], about shapes
- basic drawing [WPF]
- vector drawing [WPF], overview
- vectors [WPF], drawing
- Shape objects [WPF]
ms.assetid: 66d7a6d6-e3b6-47bc-8dfe-8a1b26f7d901
ms.openlocfilehash: 41d8f2b87232740c8945bd6a6099aa86dbe77bc6
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853694"
---
# <a name="shapes-and-basic-drawing-in-wpf-overview"></a>WPF での図形と基本描画の概要
このトピックでは、<xref:System.Windows.Shapes.Shape> オブジェクトを使用して描画する方法の概要について説明します。 <xref:System.Windows.Shapes.Shape> は <xref:System.Windows.UIElement> の一種であり、これを使用すると、画面に図形を描画できます。 <xref:System.Windows.Shapes.Shape> オブジェクトは UI 要素であるため、<xref:System.Windows.Controls.Panel> 要素やほとんどのコントロール内で使用できます。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、グラフィックス サービスやレンダリング サービスへのアクセスのレイヤーがいくつか用意されています。 最上位レイヤーにある <xref:System.Windows.Shapes.Shape> オブジェクトは使いやすく、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] イベント システムへの参加やレイアウトなど、多くの便利な機能を提供します。  

<a name="shapes"></a>
## <a name="shape-objects"></a>図形オブジェクト  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、すぐに使用できるさまざまな <xref:System.Windows.Shapes.Shape> オブジェクトが用意されています。  すべての図形オブジェクトは <xref:System.Windows.Shapes.Shape> クラスを継承します。 使用可能な図形オブジェクトには <xref:System.Windows.Shapes.Ellipse>、<xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline>、<xref:System.Windows.Shapes.Rectangle> があります。 <xref:System.Windows.Shapes.Shape> オブジェクトは、次の共通プロパティを共有します。  
  
- <xref:System.Windows.Shapes.Shape.Stroke%2A>:図形の枠線を描画する方法を示します。  
  
- <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>:図形の枠線の太さを示します。  
  
- <xref:System.Windows.Shapes.Shape.Fill%2A>:図形の内部を描画する方法を示します。  
  
- デバイス非依存ピクセル単位で計測される座標と頂点を指定するデータ プロパティ。  
  
 図形オブジェクトは <xref:System.Windows.UIElement> から派生するため、パネルおよびほとんどのコントロール内で使用できます。 <xref:System.Windows.Controls.Canvas> パネルは子オブジェクトの絶対配置をサポートするため、複雑な描画の作成に特に適しています。  
  
 <xref:System.Windows.Shapes.Line> クラスを使用すると、2 つの点の間の線を描画できます。 直線の座標およびストローク プロパティを指定するいくつかの方法を次の例に示します。  
  
 [!code-xaml[drawingwithshapeelements#LineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 [!code-cpp[shapesprocedural#ShapesProceduralLine](~/samples/snippets/cpp/VS_Snippets_Wpf/ShapesProcedural/CPP/ShapesProcedural.cpp#shapesproceduralline)]
 [!code-csharp[shapesprocedural#ShapesProceduralLine](~/samples/snippets/csharp/VS_Snippets_Wpf/ShapesProcedural/Csharp/ShapesProcedural.cs#shapesproceduralline)]
 [!code-vb[shapesprocedural#ShapesProceduralLine](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ShapesProcedural/VisualBasic/ShapesProceduralVB.vb#shapesproceduralline)]  
  
 次の図は、レンダリングされた <xref:System.Windows.Shapes.Line> を示しています。  
  
 ![線の図](./media/shape-ovw-line2.gif "shape_ovw_line2")  
  
 <xref:System.Windows.Shapes.Line> クラスは <xref:System.Windows.Shapes.Shape.Fill%2A> プロパティを備えていますが、<xref:System.Windows.Shapes.Line> には領域がないため、このプロパティを設定しても効果はありません。  
  
 もう 1 つの一般的な図形は <xref:System.Windows.Shapes.Ellipse> です。  <xref:System.Windows.Shapes.Ellipse> を作成するには、この図形の <xref:System.Windows.FrameworkElement.Width%2A> プロパティと <xref:System.Windows.FrameworkElement.Height%2A> プロパティを定義します。 円を描画するには、<xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> の値が等しい <xref:System.Windows.Shapes.Ellipse> を指定します。  
  
 [!code-xaml[ShapeOverviews#ShapesOVW1](~/samples/snippets/csharp/VS_Snippets_Wpf/ShapeOverviews/CS/Window1.xaml#shapesovw1)]  
  
 [!code-csharp[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/CSharp/SetBackgroundColorOfShapeExample.cs#setbackgroundcolorofshapecodeexamplewholepage)]
 [!code-vb[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/visualbasic/setbackgroundcolorofshapeexample.vb#setbackgroundcolorofshapecodeexamplewholepage)]  
  
 次の図は、レンダリングされた <xref:System.Windows.Shapes.Ellipse> の例を示しています。  
  
 ![楕円の図](./media/shape-ovw-ellipse2.png "shape_ovw_ellipse2")  
  
<a name="paths"></a>
## <a name="using-paths-and-geometries"></a>パスとジオメトリの使用  
 <xref:System.Windows.Shapes.Path> クラスを使用すると、曲線や複雑な図形を描画できます。 これらの曲線と図形は、<xref:System.Windows.Media.Geometry> オブジェクトを使用して記述します。 <xref:System.Windows.Shapes.Path> を使用するには、<xref:System.Windows.Media.Geometry> を作成し、それを使用して <xref:System.Windows.Shapes.Path> オブジェクトの <xref:System.Windows.Shapes.Path.Data%2A> プロパティを設定します。  
  
 さまざまな <xref:System.Windows.Media.Geometry> オブジェクトから選択できます。 <xref:System.Windows.Media.LineGeometry>、<xref:System.Windows.Media.RectangleGeometry>、<xref:System.Windows.Media.EllipseGeometry> の各クラスは、比較的単純な図形を記述します。 より複雑な図形を作成したり、曲線を作成したりするには、<xref:System.Windows.Media.PathGeometry> を使用します。  
  
<a name="pathgeometry"></a>
### <a name="pathgeometry-and-pathsegments"></a>PathGeometry と PathSegment  
 <xref:System.Windows.Media.PathGeometry> オブジェクトは、1 つまたは複数の <xref:System.Windows.Media.PathFigure> オブジェクトで構成されます。各 <xref:System.Windows.Media.PathFigure> は、異なる "図" または図形を表します。 各 <xref:System.Windows.Media.PathFigure> は、それぞれが図または図形の結合部分を表す 1 つ以上の <xref:System.Windows.Media.PathSegment> オブジェクトで構成されています。 セグメントの種類には <xref:System.Windows.Media.LineSegment>、<xref:System.Windows.Media.BezierSegment>、 <xref:System.Windows.Media.ArcSegment> があります。  
  
 次の例では、<xref:System.Windows.Shapes.Path> を使用して 2 次ベジエ曲線を描画します。  
  
 [!code-xaml[geometrysample#34](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 レンダリングされた図形を次の図に示します。  
  
 ![パスの図](./media/shape-ovw-path2.gif "shape_ovw_path2")  
  
 <xref:System.Windows.Media.PathGeometry> クラスおよび他の <xref:System.Windows.Media.Geometry> クラスの詳細については、「[ジオメトリの概要](geometry-overview.md)」をご覧ください。  
  
<a name="pathdatastring"></a>
### <a name="xaml-abbreviated-syntax"></a>省略された XAML 構文  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、省略された特殊な構文を使用して <xref:System.Windows.Shapes.Path> を記述することもできます。 次の例では、省略された構文を使用して複雑な図形を描画します。  
  
```xaml  
      <Path Stroke="DarkGoldenRod" StrokeThickness="3"
Data="M 100,200 C 100,25 400,350 400,175 H 280" />  
```  
  
 次の図は、レンダリングされた <xref:System.Windows.Shapes.Path> を示しています。  
  
 ![パスの図](./media/shape-ovw-path.PNG "shape_ovw_path")  
  
 <xref:System.Windows.Shapes.Path.Data%2A> 属性文字列は、M で示される "moveto" コマンドで始まります。このコマンドは、<xref:System.Windows.Controls.Canvas> の座標系のパスの始点を設定します。 <xref:System.Windows.Shapes.Path> データ パラメーターの大文字と小文字は区別されます。 大文字の M は、現在の新しい点の絶対位置を示します。 小文字の m は、相対座標を示します。 最初のセグメントは、2 つの制御点 (100,25) と (400,350) を使用して描画される、始点が (100,200) で終点が (400,175) の 3 次ベジエ曲線です。 このセグメントは、<xref:System.Windows.Shapes.Path.Data%2A> 属性文字列の C コマンドによって示されます。 ここでも、大文字の C は絶対パスを示し、小文字の c は相対パスを示します。  
  
 2 番目のセグメントは、絶対水平 "lineto" コマンド H で始まります。このコマンドは、前のサブパスの終点 (400,175) から新しい終点 (280,175) まで描画される直線を指定します。 水平 "lineto" コマンドであるため、指定される値は *x* 座標です。  
  
 パス構文全体については、<xref:System.Windows.Shapes.Path.Data%2A> のリファレンスと「[PathGeometry を使用して図形を作成する](how-to-create-a-shape-by-using-a-pathgeometry.md)」をご覧ください。  
  
<a name="fillpaint"></a>
## <a name="painting-shapes"></a>図形の塗りつぶし  
 <xref:System.Windows.Media.Brush> オブジェクトは、図形の <xref:System.Windows.Shapes.Shape.Stroke%2A> と <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶすために使用します。 次の例では、<xref:System.Windows.Shapes.Ellipse> のストロークおよび塗りつぶしを指定します。 ブラシ プロパティの有効な入力は、キーワードまたは 16 進数のカラー値のいずれかです。 使用可能な色のキーワードの詳細については、<xref:System.Windows.Media> 名前空間の <xref:System.Windows.Media.Colors> クラスのプロパティをご覧ください。  
  
```xaml
<Canvas Background="LightGray">
   <Ellipse  
      Canvas.Top="50"  
      Canvas.Left="50"  
      Fill="#FFFFFF00"  
      Height="75"  
      Width="75"  
      StrokeThickness="5"  
      Stroke="#FF0000FF"/>  
</Canvas>  
```  
  
 次の図は、レンダリングされた <xref:System.Windows.Shapes.Ellipse> を示しています。  
  
 ![楕円](./media/shape-ovw-ellipsefill.PNG "shape_ovw_ellipsefill")  
  
 あるいは、プロパティ要素構文を使用して <xref:System.Windows.Media.SolidColorBrush> オブジェクトを明示的に作成し、純色で図形を塗りつぶすこともできます。  
  
```xaml
<!-- This polygon shape uses pre-defined color values for its Stroke and  
     Fill properties.   
     The SolidColorBrush's Opacity property affects the fill color in   
     this case by making it slightly transparent (opacity of 0.4) so   
     that it blends with any underlying color. -->  
  
<Polygon  
    Points="300,200 400,125 400,275 300,200"  
    Stroke="Purple"
    StrokeThickness="2">  
    <Polygon.Fill>  
       <SolidColorBrush Color="Blue" Opacity="0.4"/>  
    </Polygon.Fill>  
</Polygon>  
```  
  
 レンダリングされた図形を次の図に示します。  
  
 ![SolidColorBrush の図](./media/shape-ovw-solidcolorbrush.PNG "shape_ovw_solidcolorbrush")  
  
 図形のストロークまたは塗りつぶしをグラデーション、イメージ、パターンなどで塗りつぶすこともできます。 詳細については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」をご覧ください。  
  
<a name="stretchableshapessection"></a>
## <a name="stretchable-shapes"></a>伸縮可能な図形  
 <xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline>、<xref:System.Windows.Shapes.Rectangle> の各クラスには、すべて <xref:System.Windows.Shapes.Shape.Stretch%2A> プロパティがあります。 このプロパティにより、<xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツ (描画される図形) がどのように引き伸ばされて <xref:System.Windows.Shapes.Shape> オブジェクトのレイアウト空間を埋めるかが決まります。 <xref:System.Windows.Shapes.Shape> オブジェクトのレイアウト空間とは、レイアウト システムによって <xref:System.Windows.Shapes.Shape> に割り当てられる空間の大きさであり、<xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> の明示的な設定または <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> と <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> の設定によって決まります。 Windows Presentation Foundation のレイアウトの詳細については、「[レイアウト](../advanced/layout.md)」をご覧ください。  
  
 プロパティには、次のいずれかの値を指定します。  
  
- <xref:System.Windows.Media.Stretch.None>:<xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツは引き伸ばされません。  
  
- <xref:System.Windows.Media.Stretch.Fill>:<xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツは、レイアウト空間を塗りつぶすように引き伸ばされます。  縦横比は維持されません。  
  
- <xref:System.Windows.Media.Stretch.Uniform>:<xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツは、元の縦横比を維持しながら、レイアウト空間を塗りつぶすように可能な限り引き伸ばされます。  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>:<xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツは、元の縦横比を維持しながら、レイアウト空間を完全に塗りつぶすように引き伸ばされます。  
  
 <xref:System.Windows.Shapes.Shape> オブジェクトのコンテンツが引き伸ばされると、<xref:System.Windows.Shapes.Shape> オブジェクトの枠線は、引き伸ばし後に塗りつぶされることに注意してください。  
  
 次の例では、<xref:System.Windows.Shapes.Polygon> を使用して、頂点が (0,0)、(0,1)、および (1,1) の非常に小さい三角形を描画します。 <xref:System.Windows.Shapes.Polygon> オブジェクトの <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> が 100 に設定され、その Stretch プロパティが Fill に設定されています。 その結果、<xref:System.Windows.Shapes.Polygon> オブジェクトのコンテンツ (三角形) は、より大きい空間を塗りつぶすように引き伸ばされます。  
  
```xaml
<Polygon  
  Points="0,0 0,1 1,1"  
  Fill="Blue"  
  Width="100"  
  Height="100"  
  Stretch="Fill"  
  Stroke="Black"  
  StrokeThickness="2" />  
```

```csharp
PointCollection myPointCollection = new PointCollection();  
myPointCollection.Add(new Point(0,0));  
myPointCollection.Add(new Point(0,1));  
myPointCollection.Add(new Point(1,1));  
  
Polygon myPolygon = new Polygon();  
myPolygon.Points = myPointCollection;  
myPolygon.Fill = Brushes.Blue;  
myPolygon.Width = 100;  
myPolygon.Height = 100;  
myPolygon.Stretch = Stretch.Fill;  
myPolygon.Stroke = Brushes.Black;  
myPolygon.StrokeThickness = 2;  
```

<a name="transforms"></a>
## <a name="transforming-shapes"></a>図形の変換  
 <xref:System.Windows.Media.Transform> クラスは、2 次元の平面で図形を変換する手段を提供します。  変換には、回転 (<xref:System.Windows.Media.RotateTransform>)、スケール (<xref:System.Windows.Media.ScaleTransform>)、傾斜 (<xref:System.Windows.Media.SkewTransform>)、平行移動 (<xref:System.Windows.Media.TranslateTransform>) など、さまざまな種類があります。  
  
 図形に適用される一般的な変換は回転です。  図形を回転させるには、<xref:System.Windows.Media.RotateTransform> を作成して、その <xref:System.Windows.Media.RotateTransform.Angle%2A>を指定します。 たとえば、<xref:System.Windows.Media.RotateTransform.Angle%2A> が 45 の場合は要素が時計回りに 45 度回転し、90 の場合は要素が時計回りに 90 度回転します。 要素を回転させるときの中心点を制御する場合は、<xref:System.Windows.Media.RotateTransform.CenterX%2A> プロパティと <xref:System.Windows.Media.RotateTransform.CenterY%2A> プロパティを設定します。 これらのプロパティ値は、変換する要素の座標空間で表します。 <xref:System.Windows.Media.RotateTransform.CenterX%2A> と <xref:System.Windows.Media.RotateTransform.CenterY%2A> の既定値は 0 です。 最後に、要素に <xref:System.Windows.Media.RotateTransform> を適用します。 変換がレイアウトに影響しないようにするには、図形の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティを設定します。  
  
 次の例では、<xref:System.Windows.Media.RotateTransform> を使用して、図形をその左上隅 (0,0) を中心に 45 度回転しています。  
  
 [!code-xaml[transformssample#14](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#14)]  
  
 次の例では、別の図形を 45 度回転していますが、この場合は (25,50) が回転の中心です。  
  
 [!code-xaml[transformssample#15](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#15)]  
  
 上記 2 つの変換を適用すると、結果は次の図のようになります。  
  
 ![中心点が異なる 45 度の回転](./media/wcpsdk-graphicsmm-rotatetransform45degrees.gif "wcpsdk_graphicsmm_rotatetransform45degrees")  
  
 前の例では、単一の変換を各図形オブジェクトに適用しました。 1 つの図形 (またはその他の UI 要素) に複数の変換を適用するには、<xref:System.Windows.Media.TransformGroup> を使用します。  
  
## <a name="see-also"></a>関連項目

- [2D グラフィックスとイメージング](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)
- [ジオメトリの概要](geometry-overview.md)
- [チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [アニメーションの概要](animation-overview.md)
