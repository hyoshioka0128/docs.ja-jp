---
title: 'パフォーマンスの最適化: 2D グラフィックスとイメージング'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], performance
- drawing [WPF], optimizing performance
- imaging [WPF], optimizing performance
- shapes [WPF], optimizing performance
- 2D graphics [WPF]
- images [WPF], optimizing performance
ms.assetid: e335601e-28c8-4d64-ba27-778fffd55f72
ms.openlocfilehash: eb3686367873276587572addda436471cd1abf27
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291803"
---
# <a name="optimizing-performance-2d-graphics-and-imaging"></a>パフォーマンスの最適化: 2D グラフィックスとイメージング
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、アプリケーションの要件に合わせて最適化できる広範な 2D グラフィックス機能とイメージング機能が用意されています。 このトピックでは、この領域でのパフォーマンスの最適化に関する情報を提供します。  

<a name="Drawing_and_Shapes"></a>
## <a name="drawing-and-shapes"></a>描画と図形  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、グラフィカルな描画コンテンツを表現するために <xref:System.Windows.Media.Drawing> と <xref:System.Windows.Shapes.Shape> の両方のオブジェクトが用意されています。 ただし、<xref:System.Windows.Media.Drawing> オブジェクトの方が <xref:System.Windows.Shapes.Shape> オブジェクトよりコンストラクトが簡単であり、パフォーマンス特性に優れています。  
  
 <xref:System.Windows.Shapes.Shape> を使用すると、画面にグラフィカルな図形を描画できます。 <xref:System.Windows.FrameworkElement> オブジェクトは <xref:System.Windows.Shapes.Shape> クラスから派生するため、パネルおよびほとんどのコントロール内で使用できます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、グラフィックス サービスやレンダリング サービスへのアクセスのレイヤーがいくつか用意されています。 <xref:System.Windows.Shapes.Shape> オブジェクトは最上位レイヤーで使いやすく、レイアウトやイベント処理などの便利な機能が多数提供されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、すぐに使用できるさまざまな図形オブジェクトが用意されています。 すべての図形オブジェクトは <xref:System.Windows.Shapes.Shape> クラスから継承されます。 使用可能な図形オブジェクトには <xref:System.Windows.Shapes.Ellipse>、<xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline>、<xref:System.Windows.Shapes.Rectangle> があります。  
  
 一方、<xref:System.Windows.Media.Drawing> オブジェクトは <xref:System.Windows.FrameworkElement> クラスから派生せず、図形、イメージ、テキストを描画するためのより軽量な実装が提供されます。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトには、次の 4 種類があります。  
  
- <xref:System.Windows.Media.GeometryDrawing> 図形が描画されます。  
  
- <xref:System.Windows.Media.ImageDrawing> 画像が描画されます。  
  
- <xref:System.Windows.Media.GlyphRunDrawing> テキストが描画されます。  
  
- <xref:System.Windows.Media.DrawingGroup> その他の図が描画されます。 他の描画を 1 つの複合描画に結合するには、描画グループを使用します。  
  
 <xref:System.Windows.Media.GeometryDrawing> オブジェクトは、ジオメトリ コンテンツをレンダリングするために使用されます。 <xref:System.Windows.Media.Geometry> クラスと、それから派生する具象クラス (<xref:System.Windows.Media.CombinedGeometry>、<xref:System.Windows.Media.EllipseGeometry>、<xref:System.Windows.Media.PathGeometry> など) では、2D グラフィックスをレンダリングするための手段と、ヒット テストやクリッピングのサポートが提供されています。 ジオメトリ オブジェクトを使用すると、たとえば、コントロールの領域を定義したり、イメージに適用するクリップ領域を定義したりすることができます。 ジオメトリ オブジェクトは、四角形や円などの単純な領域にすることも、2 つ以上のジオメトリ オブジェクトから作成された複合的な領域にすることもできます。 さらに複雑な幾何学領域を作成するには、<xref:System.Windows.Media.PathSegment> 派生オブジェクト (<xref:System.Windows.Media.ArcSegment>、<xref:System.Windows.Media.BezierSegment>、<xref:System.Windows.Media.QuadraticBezierSegment> など) の組み合わせを使用します。  
  
 表面的には、<xref:System.Windows.Media.Geometry> クラスと <xref:System.Windows.Shapes.Shape> クラスは似ています。 いずれのクラスも 2D グラフィックスのレンダリングに使用され、それぞれのクラスから派生する具象クラスも似ています (<xref:System.Windows.Media.EllipseGeometry>、<xref:System.Windows.Shapes.Ellipse> など)。 ただし、この 2 つのクラスのセットの間には重要な違いがいくつかあります。 その 1 つとして、<xref:System.Windows.Media.Geometry> クラスには、<xref:System.Windows.Shapes.Shape> クラスの一部の機能 (図形そのものを描画する機能など) がありません。 ジオメトリ オブジェクトを描画するには、DrawingContext、Drawing、Path (Path が Shape であることは注目に値します) などの別のクラスを使用して描画操作を実行する必要があります。 塗りつぶし、ストローク、ストロークの太さなどの描画プロパティは、ジオメトリ オブジェクトを描画するクラスにあります。一方、図形オブジェクトにはこれらのプロパティが含まれています。 この違いは、ジオメトリ オブジェクトでは円などの領域が定義されるのに対し、図形オブジェクトでは領域が定義されるとともに、その領域の塗りつぶしやアウトラインも定義され、レイアウト システムに参加する、と考えることができます。  
  
 <xref:System.Windows.Shapes.Shape> オブジェクトは <xref:System.Windows.FrameworkElement> クラスから派生するため、Shape オブジェクトを使用するとアプリケーションのメモリ消費が大幅に増加する可能性があります。 グラフィカル コンテンツで <xref:System.Windows.FrameworkElement> の機能がまったく必要ない場合は、より軽量な <xref:System.Windows.Media.Drawing> オブジェクトを使用することを検討します。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトの詳細については、「[Drawing オブジェクトの概要](../graphics-multimedia/drawing-objects-overview.md)」を参照してください。  
  
<a name="StreamGeometry_Objects"></a>
## <a name="streamgeometry-objects"></a>StreamGeometry オブジェクト  
 <xref:System.Windows.Media.StreamGeometry> オブジェクトは、幾何学図形を作成するための <xref:System.Windows.Media.PathGeometry> の代替となる軽量なものです。 <xref:System.Windows.Media.StreamGeometry> は、複雑なジオメトリを作成する必要がある場合に使用します。 <xref:System.Windows.Media.StreamGeometry> は、多数の <xref:System.Windows.Media.PathGeometry> オブジェクトを処理することを想定して最適化されているため、多数の <xref:System.Windows.Media.PathGeometry> オブジェクトを個別に使用する場合に比べてパフォーマンスが向上します。  
  
 次の例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で属性構文の使用によって三角形の <xref:System.Windows.Media.StreamGeometry> が作成されます。  
  
 [!code-xaml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 <xref:System.Windows.Media.StreamGeometry> オブジェクトの詳細については、「[StreamGeometry を使用して図形を作成する](../graphics-multimedia/how-to-create-a-shape-using-a-streamgeometry.md)」を参照してください。  
  
<a name="DrawingVisual_Objects"></a>
## <a name="drawingvisual-objects"></a>DrawingVisual オブジェクト  
 <xref:System.Windows.Media.DrawingVisual> オブジェクトは、図形、画像、またはテキストのレンダリングに使用する軽量の描画クラスです。 このクラスが軽量と見なされる理由は、レイアウトやイベントの処理を行わないことで、パフォーマンスが向上するからです。 そのため、背景やクリップ アートの描画に適しています。 詳しくは、「[DrawingVisual オブジェクトの使用](../graphics-multimedia/using-drawingvisual-objects.md)」を参照してください。  
  
<a name="Images"></a>
## <a name="images"></a>イメージ  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のイメージング機能は、以前のバージョンの Windows のイメージング機能から大幅に強化されています。 イメージング機能 (ビットマップの表示や一般的なコントロール上でのイメージの使用など) は、以前は主に Microsoft Windows Graphics Device Interface (GDI) または Microsoft Windows GDI+ のアプリケーション プログラミング インターフェイス (API) によって処理されていました。 これらの API では、基本的なイメージング機能は提供されていましたが、コーデック拡張機能のサポートや高品質なイメージのサポートなどの機能が不足していました。 WPF Imaging API は、GDI および GDI+ の欠点を克服し、アプリケーション内でイメージを表示および使用するための新しい API のセットを提供するために再設計されています。  
  
 イメージを使用する際には、パフォーマンスを向上させるために以下の推奨事項をご検討ください。  
  
- アプリケーションでサムネイル イメージを表示する必要がある場合は、縮小版のイメージを作成することをご検討ください。 既定では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]は読み込んだイメージを本来のサイズにデコードします。 サムネイル バージョンのイメージのみが必要な場合は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] がイメージを本来のサイズにデコードしてからサムネイル サイズに縮小するという無駄が生じます。 この不要なオーバーヘッドを回避するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に対してイメージをサムネイル サイズにデコードするように要求するか、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] にサムネイル サイズのイメージを読み込むように要求します。  
  
- イメージは常に、既定のサイズではなく必要なサイズにデコードするようにしてください。 前述のように、既定の実際のサイズではなく必要なサイズにイメージをデコードするように [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に要求します。 これにより、アプリケーションの作業セットを縮小できるだけでなく、実行速度も向上します。  
  
- 可能であれば、複数のイメージを 1 つに結合します (複数のイメージから成るフィルム ストリップなど)。  
  
- 詳しくは、「 [イメージングの概要](../graphics-multimedia/imaging-overview.md)」をご覧ください。  
  
### <a name="bitmapscalingmode"></a>BitmapScalingMode  
 ビットマップのスケーリングをアニメーション化する場合、既定の高品質イメージの再サンプリング アルゴリズムは、フレーム レートを低下させるほどシステム リソースを消費する場合があり、実際にはアニメーションの動きが滑らかでなくなることがあります。 <xref:System.Windows.Media.RenderOptions> オブジェクトの <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A> プロパティを <xref:System.Windows.Media.BitmapScalingMode.LowQuality> に設定することで、ビットマップをスケーリングするときに、より滑らかなアニメーションを作成できます。 <xref:System.Windows.Media.BitmapScalingMode.LowQuality> モードでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のレンダリング エンジンに対し、イメージを処理するときに品質重視のアルゴリズムから速度重視のアルゴリズムに切り替えるように指示されます。  
  
 イメージ オブジェクトの <xref:System.Windows.Media.BitmapScalingMode> を設定する方法の例を次に示します。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet2)]
 [!code-vb[RenderOptions#RenderOptionsSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet2)]  
  
### <a name="cachinghint"></a>CachingHint  
 既定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、<xref:System.Windows.Media.TileBrush> オブジェクト (<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.VisualBrush> など) のレンダリングされた内容はキャッシュされません。 シーンで <xref:System.Windows.Media.TileBrush> の内容も使用も変化しない静的なシナリオでは、ビデオ メモリが節約されるため、これには意味があります。 静的な内容の <xref:System.Windows.Media.TileBrush> を静的でない方法で使用する場合には、あまり意味はありません。たとえば、静的な <xref:System.Windows.Media.DrawingBrush> や <xref:System.Windows.Media.VisualBrush> が回転する 3D オブジェクトのサーフェイスにマップされている場合などです。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の既定の動作では、内容が変化しない場合でも、<xref:System.Windows.Media.DrawingBrush> または <xref:System.Windows.Media.VisualBrush> のすべてのフレームの内容全体が再レンダリングされます。  
  
 <xref:System.Windows.Media.RenderOptions> オブジェクトの <xref:System.Windows.Media.RenderOptions.CachingHint%2A> プロパティを <xref:System.Windows.Media.CachingHint.Cache> に設定すると、並べて表示されたブラシ オブジェクトのキャッシュ バージョンを使用してパフォーマンスを向上させることができます。  
  
 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> プロパティと <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> プロパティの値は、スケールの変化に伴って <xref:System.Windows.Media.TileBrush> オブジェクトをいつ再生成する必要があるかを決定する相対的なサイズ値です。 たとえば、<xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> プロパティを 2.0 に設定すると、<xref:System.Windows.Media.TileBrush> のキャッシュ サイズが現在のキャッシュ サイズの倍を超えた場合にだけ、キャッシュを再生成すれば済みます。  
  
 <xref:System.Windows.Media.DrawingBrush> のキャッシュ ヒント オプションの使用方法の例を次に示します。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet3)]
 [!code-vb[RenderOptions#RenderOptionsSnippet3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet3)]  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
- [アニメーションのヒントとテクニック](../graphics-multimedia/animation-tips-and-tricks.md)
