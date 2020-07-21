---
title: ジオメトリの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- geometry classes [WPF]
- graphics [WPF], geometry classes
ms.assetid: 9fba8934-98b7-4af6-82f6-f4ef887f963a
ms.openlocfilehash: ff42e59edd9d98b0b52dc3bdd3ace0c35df60878
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112376"
---
# <a name="geometry-overview"></a>ジオメトリの概要
この概要では、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の <xref:System.Windows.Media.Geometry> クラスを使用して図形を記述する方法を説明します。 このトピックでは、<xref:System.Windows.Media.Geometry> オブジェクトと <xref:System.Windows.Shapes.Shape> 要素の違いも示します。  

<a name="wcpsdk_graphics_geometry_introduction"></a>
## <a name="what-is-a-geometry"></a>ジオメトリとは  
 <xref:System.Windows.Media.Geometry> クラスとそれから派生するクラス (<xref:System.Windows.Media.EllipseGeometry>、<xref:System.Windows.Media.PathGeometry>、<xref:System.Windows.Media.CombinedGeometry> など) を使用すると、2D 図形のジオメトリを記述できます。 これらの幾何学的な記述には、画面を塗りつぶす図形を定義したり、ヒット テストやクリップ領域を定義するなど、多くの用途があります。 ジオメトリを使用して、アニメーション パスを定義することもできます。  
  
 <xref:System.Windows.Media.Geometry> オブジェクトは、四角形や円などの単純なものにすることも、2 つ以上のジオメトリ オブジェクトから作成された複合的なものにすることもできます。  円弧と曲線を記述できる <xref:System.Windows.Media.PathGeometry> および <xref:System.Windows.Media.StreamGeometry> クラスを使用すると、より複雑なジオメトリを作成できます。  
  
 <xref:System.Windows.Media.Geometry> は <xref:System.Windows.Freezable> オブジェクトの一種であるため、<xref:System.Windows.Media.Geometry> オブジェクトはいくつかの特殊な機能を備えています。つまり、それらのオブジェクトを[リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)として宣言すること、複数のオブジェクト間で共有すること、読み取り専用にしてパフォーマンスを高めること、複製すること、スレッド セーフにすることができます。 <xref:System.Windows.Freezable> オブジェクトで提供されるさまざまな機能について詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
<a name="wcpsdk_graphics_geometry_geometryandshapes"></a>
## <a name="geometries-vs-shapes"></a>ジオメトリと図形  
 <xref:System.Windows.Media.Geometry> と <xref:System.Windows.Shapes.Shape> クラスは、(たとえば、<xref:System.Windows.Media.EllipseGeometry> と <xref:System.Windows.Shapes.Ellipse> を比較した場合) 両方とも 2D 図形を記述するという点で似ているように見えますが、重要な違いがあります。  
  
 1 つには、<xref:System.Windows.Media.Geometry> クラスは <xref:System.Windows.Freezable> クラスを継承し、<xref:System.Windows.Shapes.Shape> クラスは <xref:System.Windows.FrameworkElement> を継承します。 これらは要素であるため、<xref:System.Windows.Shapes.Shape> オブジェクトは、それ自体をレンダリングしてレイアウト システムに加わることができますが、<xref:System.Windows.Media.Geometry> オブジェクトはできません。  
  
 <xref:System.Windows.Shapes.Shape> オブジェクトは <xref:System.Windows.Media.Geometry> オブジェクトよりも簡単に使用できますが、<xref:System.Windows.Media.Geometry> オブジェクトの方が汎用性があります。 <xref:System.Windows.Shapes.Shape> オブジェクトは 2D グラフィックスのレンダリングに使用されますが、<xref:System.Windows.Media.Geometry> オブジェクトは 2D グラフィックスの幾何学的領域の定義、クリッピング用の領域の定義、ヒット テスト用の領域の定義などに使用できます。  
  
### <a name="the-path-shape"></a>パス図形  
 1 つの <xref:System.Windows.Shapes.Shape> である <xref:System.Windows.Shapes.Path> クラスは、実際には <xref:System.Windows.Media.Geometry> を使用してそのコンテンツを記述します。 <xref:System.Windows.Media.Geometry> を使用して <xref:System.Windows.Shapes.Path> の <xref:System.Windows.Shapes.Path.Data%2A> プロパティを設定し、その <xref:System.Windows.Shapes.Shape.Fill%2A> および <xref:System.Windows.Shapes.Shape.Stroke%2A> プロパティを設定することで、<xref:System.Windows.Media.Geometry> をレンダリングできます。  
  
<a name="commonproperties"></a>
## <a name="common-properties-that-take-a-geometry"></a>ジオメトリを使用する一般的なプロパティ  
 これまでのセクションでは、図形の描画、アニメーション、クリッピングなどのさまざまな目的で、ジオメトリ オブジェクトを他のオブジェクトと共に使用できることを説明しました。 次の表に、<xref:System.Windows.Media.Geometry> オブジェクトを受け取るプロパティを持つクラスをいくつか示します。  
  
|種類|プロパティ|  
|----------|--------------|  
|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|  
|<xref:System.Windows.Media.GeometryDrawing>|<xref:System.Windows.Media.GeometryDrawing.Geometry%2A>|  
|<xref:System.Windows.Shapes.Path>|<xref:System.Windows.Shapes.Path.Data%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.Clip%2A>|  
  
<a name="wcpsdk_graphics_geometry_geometrytypes"></a>
## <a name="simple-geometry-types"></a>単純なジオメトリの種類  
 すべてのジオメトリの基底クラスは、抽象クラスの <xref:System.Windows.Media.Geometry> です。  <xref:System.Windows.Media.Geometry> クラスから派生するクラスは、単純なジオメトリ、パス ジオメトリ、複合ジオメトリという 3 つのカテゴリに大まかに分類できます。  
  
 単純なジオメトリのクラスには、<xref:System.Windows.Media.LineGeometry>、<xref:System.Windows.Media.RectangleGeometry>、<xref:System.Windows.Media.EllipseGeometry> が含まれ、線、四角形、円などの基本的な幾何学図形を作成するために使用されます。  
  
- <xref:System.Windows.Media.LineGeometry> は、線の始点と終点を指定して定義します。  
  
- <xref:System.Windows.Media.RectangleGeometry> は、その相対位置、高さおよび幅を指定する <xref:System.Windows.Rect> 構造体で定義されます。 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> と <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> プロパティを設定して、角丸四角形を作成できます。  
  
- <xref:System.Windows.Media.EllipseGeometry> は、中心点、x 半径、および y 半径によって定義されます。  レンダリングとクリッピング用の単純ジオメトリの作成方法を次の例に示します。  
  
 <xref:System.Windows.Media.PathGeometry> を使用するか、ジオメトリ オブジェクトを結合する方法でも、これらと同じ図形や、さらに複雑な図形を作成できますが、これらのクラスを使用すると、このような基本的な幾何学図形をより簡単に生成できます。  
  
 次の例は、<xref:System.Windows.Media.LineGeometry> を作成してレンダリングする方法を示しています。  前述のように、<xref:System.Windows.Media.Geometry> オブジェクトはそれ自体を描画できないため、この例では <xref:System.Windows.Shapes.Path> 図形を使用して線をレンダリングします。  線には領域がないため、<xref:System.Windows.Shapes.Path> の <xref:System.Windows.Shapes.Shape.Fill%2A> プロパティを設定しても効果はありません。代わりに、<xref:System.Windows.Shapes.Shape.Stroke%2A> および <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> プロパティのみが指定されています。 この例からの出力を次の図に示します。  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
(10,20) から (100,130) まで描画された LineGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 次の例は、<xref:System.Windows.Media.EllipseGeometry> を作成してレンダリングする方法を示しています。  この例では、<xref:System.Windows.Media.EllipseGeometry> の <xref:System.Windows.Media.EllipseGeometry.Center%2A> をポイント `50,50` に設定し、x 半径と y 半径の両方を `50` に設定します。これにより、直径 100 の円が作成されます。  楕円の内部は、Path 要素の Fill プロパティに値 (この例では <xref:System.Windows.Media.Brushes.Gold%2A>) を割り当てることで塗りつぶします。 この例からの出力を次の図に示します。  
  
 ![EllipseGeometry](./media/graphicsmm-ellipse.gif "graphicsmm_ellipse")  
(50,50) に描画された EllipseGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmellipsegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmellipsegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmellipsegeometryexample)]  
  
 次の例は、<xref:System.Windows.Media.RectangleGeometry> を作成してレンダリングする方法を示しています。  四角形の位置と大きさは <xref:System.Windows.Rect> 構造体によって定義されます。 位置は `50,50`、高さと幅は両方とも `25` で、正方形が作成されます。 この例からの出力を次の図に示します。  
  
 ![RectangleGeometry](./media/graphicsmm-rectangle.gif "graphicsmm_rectangle")  
50,50 に描画された RectangleGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 次の例は、<xref:System.Windows.Media.EllipseGeometry> をイメージのクリップ領域として使用する方法を示しています。  <xref:System.Windows.Controls.Image> オブジェクトは、200 の <xref:System.Windows.FrameworkElement.Width%2A> と 150 の <xref:System.Windows.FrameworkElement.Height%2A> を指定して定義されています。  <xref:System.Windows.Media.EllipseGeometry.RadiusX%2A> 値が 100、<xref:System.Windows.Media.EllipseGeometry.RadiusY%2A> 値が 75、<xref:System.Windows.Media.EllipseGeometry.Center%2A> 値が 100,75 である <xref:System.Windows.Media.EllipseGeometry> が、イメージの <xref:System.Windows.UIElement.Clip%2A> プロパティに設定されています。  イメージの楕円の領域内の部分だけが表示されます。 この例からの出力を次の図に示します。  
  
 ![クリッピングを使用する (または使用しない) イメージ](./media/graphicsmm-clipexample.png "graphicsmm_clipexample")  
イメージ コントロールのクリップに使用される EllipseGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmimageclipgeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmimageclipgeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmimageclipgeometryexample)]  
  
<a name="wcpsdk_graphics_geometry_pathgeometry"></a>
## <a name="path-geometries"></a>パス ジオメトリ  
 <xref:System.Windows.Media.PathGeometry> クラスと、それと同等だが軽量である <xref:System.Windows.Media.StreamGeometry> クラスは、円弧、曲線、および線で構成される複数の複雑な図形を記述する手段を提供します。  
  
 <xref:System.Windows.Media.PathGeometry> の中核となるのは、<xref:System.Windows.Media.PathFigure> オブジェクトのコレクションです。各図形によって <xref:System.Windows.Media.PathGeometry> 内に個別の図形が記述されるので、このように呼ばれます。 各 <xref:System.Windows.Media.PathFigure> は、1 つ以上の <xref:System.Windows.Media.PathSegment> オブジェクトで構成され、このそれぞれで図形のセグメントが記述されます。  
  
 多くの種類のセグメントがあります。  
  
|セグメントの種類|説明|例|  
|------------------|-----------------|-------------|  
|<xref:System.Windows.Media.ArcSegment>|2 つの点を結ぶ楕円の円弧を作成します。|[楕円の円弧を作成する](how-to-create-an-elliptical-arc.md)。|  
|<xref:System.Windows.Media.BezierSegment>|2 つの点を結ぶ 3 次ベジエ曲線を作成します。|[3 次ベジエ曲線を作成する](how-to-create-a-cubic-bezier-curve.md)。|  
|<xref:System.Windows.Media.LineSegment>|2 つの点を結ぶ直性を作成します。|[PathGeometry で LineSegment を作成する](how-to-create-a-linesegment-in-a-pathgeometry.md)|  
|<xref:System.Windows.Media.PolyBezierSegment>|一続きの 3 次ベジエ曲線を作成します。|<xref:System.Windows.Media.PolyBezierSegment> の種類のページを参照してください。|  
|<xref:System.Windows.Media.PolyLineSegment>|一続きの直線を作成します。|<xref:System.Windows.Media.PolyLineSegment> の種類のページを参照してください。|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|一続きの 2 次ベジエ曲線を作成します。|<xref:System.Windows.Media.PolyQuadraticBezierSegment> のページを参照してください。|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|2 次ベジエ曲線を作成します。|[2 次ベジエ曲線を作成する](how-to-create-a-quadratic-bezier-curve.md)。|  
  
 <xref:System.Windows.Media.PathFigure> 内のセグメントは 1 つの幾何学図形に結合されて、各セグメントの終点が次のセグメントの始点になります。 <xref:System.Windows.Media.PathFigure> の <xref:System.Windows.Media.PathFigure.StartPoint%2A> プロパティでは、最初のセグメントが描画される開始点を指定します。 後続の各セグメントは、前のセグメントの終点から始まります。 たとえば、`10,50` から `10,150` までの縦線を定義するには、<xref:System.Windows.Media.PathFigure.StartPoint%2A> プロパティを `10,50` に設定し、<xref:System.Windows.Media.LineSegment.Point%2A> プロパティを `10,150` に設定して <xref:System.Windows.Media.LineSegment> を作成します。  
  
 次の例では、<xref:System.Windows.Media.LineSegment> を含む単一の <xref:System.Windows.Media.PathFigure> で構成される単純な <xref:System.Windows.Media.PathGeometry> を作成し、<xref:System.Windows.Shapes.Path> 要素を使用してそれを表示します。 <xref:System.Windows.Media.PathFigure> オブジェクトの <xref:System.Windows.Media.PathFigure.StartPoint%2A> は `10,20` に設定され、<xref:System.Windows.Media.LineSegment> は終点の `100,130` を指定して定義されています。 次の図は、この例で作成した <xref:System.Windows.Media.PathGeometry> を示しています。  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
単一の LineSegment を含む PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrylineexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrylineexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrylineexample)]  
  
 この例を前の <xref:System.Windows.Media.LineGeometry> 例と対比することは価値があります。  <xref:System.Windows.Media.PathGeometry> に使用される構文は、単純な <xref:System.Windows.Media.LineGeometry> に使用されるものよりもはるかに詳細であり、この場合は <xref:System.Windows.Media.LineGeometry> クラスを使用する方が理にかなっているかもしれませんが、<xref:System.Windows.Media.PathGeometry> の詳細な構文では非常に難解で複雑な幾何学的領域を実現できます。  
  
 より複雑なジオメトリは、 <xref:System.Windows.Media.PathSegment> オブジェクトの組み合わせを使用して作成できます。  
  
 次の例では、図形を作成するために、<xref:System.Windows.Media.BezierSegment>、<xref:System.Windows.Media.LineSegment>、および <xref:System.Windows.Media.ArcSegment> を使用します。 この例ではまず、始点 (前のセグメントの終点)、終点 (<xref:System.Windows.Media.BezierSegment.Point3%2A>)、2 つの制御点 (<xref:System.Windows.Media.BezierSegment.Point1%2A> と <xref:System.Windows.Media.BezierSegment.Point2%2A>) の 4 つの点を定義して、3 次ベジエ曲線を作成します。  3 次ベジエ曲線の 2 つの制御点は磁石のように動作し、本来は直線になる部分を制御点の方へ引き寄せ、曲線を生成します。 最初の制御点である <xref:System.Windows.Media.BezierSegment.Point1%2A> は曲線の開始部分に影響し、2 つ目の制御点である <xref:System.Windows.Media.BezierSegment.Point2%2A> は曲線の終了部分に影響します。  
  
 次に、この例では <xref:System.Windows.Media.LineSegment> を追加します。これは、その前にある <xref:System.Windows.Media.BezierSegment> の終点から <xref:System.Windows.Media.LineSegment> プロパティで指定された点までの間で描画されます。  
  
 そして、例では <xref:System.Windows.Media.ArcSegment> を追加します。これは、その前の <xref:System.Windows.Media.LineSegment> の終点から <xref:System.Windows.Media.ArcSegment.Point%2A> プロパティで指定された点まで描画されます。 さらに、例では円弧の x および y 半径 (<xref:System.Windows.Media.ArcSegment.Size%2A>)、回転角度 (<xref:System.Windows.Media.ArcSegment.RotationAngle%2A>)、結果の円弧の角度の大きさを示すフラグ (<xref:System.Windows.Media.ArcSegment.IsLargeArc%2A>)、および円弧が描画される方向を示す値 (<xref:System.Windows.Media.ArcSegment.SweepDirection%2A>) も指定します。 この例で作成した図形を次の図に示します。  
  
 ![PathGeometry](./media/graphicsmm-path2.gif "graphicsmm_path2")  
PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexexample)]  
  
 さらに複雑なジオメトリは、<xref:System.Windows.Media.PathGeometry> 内で複数の <xref:System.Windows.Media.PathFigure> オブジェクトを使用して作成できます。  
  
 次の例では、2 つの <xref:System.Windows.Media.PathFigure> オブジェクトを持つ <xref:System.Windows.Media.PathGeometry> を作成し、それぞれに複数の <xref:System.Windows.Media.PathSegment> オブジェクトが含まれます。  上の例の <xref:System.Windows.Media.PathFigure> と、<xref:System.Windows.Media.PolyLineSegment> と <xref:System.Windows.Media.QuadraticBezierSegment> を含む <xref:System.Windows.Media.PathFigure> が使用されます。  <xref:System.Windows.Media.PolyLineSegment> は点の配列を指定して定義され、<xref:System.Windows.Media.QuadraticBezierSegment> は制御点と終点を指定して定義されます。 この例で作成した図形を次の図に示します。  
  
 ![PathGeometry](./media/graphicsmm-path.gif "graphicsmm_path")  
複数の図形を使用する PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexmultiexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexmultiexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexmultiexample)]  
  
### <a name="streamgeometry"></a>StreamGeometry  
 <xref:System.Windows.Media.StreamGeometry> は、<xref:System.Windows.Media.PathGeometry> クラスと同様に、曲線、円弧、直線を含めることができる複雑な幾何学図形を定義します。 <xref:System.Windows.Media.PathGeometry> とは異なり、<xref:System.Windows.Media.StreamGeometry> のコンテンツは、データ バインディング、アニメーション、変更をサポートしていません。 複雑なジオメトリを記述する必要があるが、データ バインディング、アニメーション、または変更をサポートするオーバーヘッドが望ましくない場合は、<xref:System.Windows.Media.StreamGeometry> を使用します。 <xref:System.Windows.Media.StreamGeometry> クラスは効率的であるため、装飾の記述に適しています。  
  
 例については、「[方法 : StreamGeometry を使用して図形を作成する](how-to-create-a-shape-using-a-streamgeometry.md)」をご覧ください。  
  
### <a name="path-markup-syntax"></a>パス マークアップ構文  
 <xref:System.Windows.Media.PathGeometry> および <xref:System.Windows.Media.StreamGeometry> の種類では、一連の特殊な移動および描画コマンドを使用して [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 属性構文がサポートされています。 詳しくは、「[パス マークアップ構文](path-markup-syntax.md)」をご覧ください。  
  
<a name="wcpsdk_graphics_geometry_introduction2"></a>
## <a name="composite-geometries"></a>複合ジオメトリ  
 複合ジオメトリ オブジェクトは、<xref:System.Windows.Media.GeometryGroup> または <xref:System.Windows.Media.CombinedGeometry> を使用するか、静的 <xref:System.Windows.Media.Geometry> メソッド <xref:System.Windows.Media.Geometry.Combine%2A> を呼び出すことで作成できます。  
  
- <xref:System.Windows.Media.CombinedGeometry> オブジェクトと <xref:System.Windows.Media.Geometry.Combine%2A> メソッドは、2 つのジオメトリによって定義された領域を結合するブール演算を実行します。 領域がない <xref:System.Windows.Media.Geometry> オブジェクトは破棄されます。 結合できるのは、2 つの <xref:System.Windows.Media.Geometry> オブジェクトだけです (ただし、この 2 つのジオメトリは複合ジオメトリにすることもできます)。  
  
- <xref:System.Windows.Media.GeometryGroup> クラスは、含まれている <xref:System.Windows.Media.Geometry> オブジェクトの混合を、それらの領域を結合することなく作成します。 任意の数の <xref:System.Windows.Media.Geometry> オブジェクトを <xref:System.Windows.Media.GeometryGroup> に追加できます。 例については、「[方法 : 複合図形を作成する](how-to-create-a-composite-shape.md)」をご覧ください。  
  
 <xref:System.Windows.Media.GeometryGroup> オブジェクトは結合操作を実行しないため、これらを使用すると、<xref:System.Windows.Media.CombinedGeometry> オブジェクトまたは <xref:System.Windows.Media.Geometry.Combine%2A> メソッドを使用するよりもパフォーマンスが向上します。  
  
<a name="combindgeometriessection"></a>
## <a name="combined-geometries"></a>結合したジオメトリ  
 前のセクションでは、<xref:System.Windows.Media.CombinedGeometry> オブジェクトと <xref:System.Windows.Media.Geometry.Combine%2A> メソッドが、それらに含まれているジオメトリによって定義された領域を結合することを説明しました。 <xref:System.Windows.Media.GeometryCombineMode> 列挙型は、ジオメトリの結合方法を指定します。 <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> プロパティに指定できる値は、<xref:System.Windows.Media.GeometryCombineMode.Union>、<xref:System.Windows.Media.GeometryCombineMode.Intersect>、<xref:System.Windows.Media.GeometryCombineMode.Exclude>、および <xref:System.Windows.Media.GeometryCombineMode.Xor> です。  
  
 次の例では、<xref:System.Windows.Media.CombinedGeometry> が Union の結合モードを指定して定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#23](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Union 結合モードの結果](./media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
  
 次の例では、<xref:System.Windows.Media.CombinedGeometry> が <xref:System.Windows.Media.GeometryCombineMode.Xor> の結合モードを指定して定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#24](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 結合モードの結果](./media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_xor")  
  
 その他の例については、「[方法 : 複合図形を作成する](how-to-create-a-composite-shape.md)」と「[方法 : 結合したジオメトリを作成する](how-to-create-a-combined-geometry.md)」をご覧ください。  
  
<a name="freezable_features"></a>
## <a name="freezable-features"></a>Freezable 機能  
 <xref:System.Windows.Media.Geometry> クラスは <xref:System.Windows.Freezable> クラスを継承するため、いくつかの特殊な機能を備えています。つまり、<xref:System.Windows.Media.Geometry> オブジェクトを [XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)として宣言すること、複数のオブジェクト間で共有すること、読み取り専用にしてパフォーマンスを高めること、複製すること、スレッド セーフにすることができます。 <xref:System.Windows.Freezable> オブジェクトで提供されるさまざまな機能について詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
<a name="othergeometryfeatures"></a>
## <a name="other-geometry-features"></a>その他のジオメトリ機能  
 <xref:System.Windows.Media.Geometry> クラスには、次のような便利なユーティリティ メソッドも用意されています。  
  
- <xref:System.Windows.Media.Geometry.GetArea%2A> - <xref:System.Windows.Media.Geometry> の領域を取得します。  
  
- <xref:System.Windows.Media.Geometry.FillContains%2A> - ジオメトリに別の <xref:System.Windows.Media.Geometry> が含まれているかどうかを判断します。  
  
- <xref:System.Windows.Media.Geometry.StrokeContains%2A> - 指定された点が <xref:System.Windows.Media.Geometry> のストロークに含まれているかどうかを判断します。  
  
 メソッドの完全な一覧については、<xref:System.Windows.Media.Geometry> クラスを参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Geometry>
- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.GeometryDrawing>
- [2D グラフィックスとイメージング](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [パス マークアップ構文](path-markup-syntax.md)
- [方法トピック](geometries-how-to-topics.md)
- [アニメーションの概要](animation-overview.md)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
