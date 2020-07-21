---
title: Drawing オブジェクトの概要
description: オブジェクトについて理解し、それらを使用して Windows Presentation Foundation (WPF) でシェイプ、ビットマップ、テキスト、メディアを効率的に描画する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- ImageDrawing objects [WPF]
- GlyphRunDrawing objects [WPF]
- GeometryDrawing objects [WPF]
- drawings [WPF], about drawings
- Drawing objects [WPF]
- DrawingGroup objects [WPF]
ms.assetid: 9b5ce5c0-e204-4320-a7a8-0b2210d62f88
ms.openlocfilehash: f00a59cd6e799e57f238c5f9b72ecc48e8445475
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853841"
---
# <a name="drawing-objects-overview"></a>Drawing オブジェクトの概要
このトピックでは、<xref:System.Windows.Media.Drawing> オブジェクトについて紹介し、それを使用して図形、ビットマップ、テキスト、メディアを効率的に描画する方法を説明します。 クリップアートを作成するとき、<xref:System.Windows.Media.DrawingBrush> で描画するとき、または <xref:System.Windows.Media.Visual> オブジェクトを使用するときは、<xref:System.Windows.Media.Drawing> オブジェクトを使用します。  

<a name="whatisadrawingsection"></a>
## <a name="what-is-a-drawing-object"></a>Drawing オブジェクトとは  
 <xref:System.Windows.Media.Drawing> オブジェクトでは、シェイプ、ビットマップ、ビデオ、テキスト行などの表示可能なコンテンツを記述します。 さまざまな種類の描画で、さまざまな種類のコンテンツを記述します。 次の一覧に、さまざまな種類の描画オブジェクトを示します。  
  
- <xref:System.Windows.Media.GeometryDrawing> - 図形を描画します。  
  
- <xref:System.Windows.Media.ImageDrawing> - イメージを描画します。  
  
- <xref:System.Windows.Media.GlyphRunDrawing> - テキストを描画します。  
  
- <xref:System.Windows.Media.VideoDrawing> - オーディオまたはビデオのファイルを再生します。  
  
- <xref:System.Windows.Media.DrawingGroup> - その他の描画を行います。 他の描画を 1 つの複合描画に結合するには、描画グループを使用します。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトは汎用的です。<xref:System.Windows.Media.Drawing> オブジェクトには多くの使用法があります。  
  
- <xref:System.Windows.Media.DrawingImage> および <xref:System.Windows.Controls.Image> コントロールを使用すると、イメージとして表示できます。  
  
- <xref:System.Windows.Media.DrawingBrush> と共に使用すると、<xref:System.Windows.Controls.Page> の <xref:System.Windows.Controls.Page.Background%2A> などのオブジェクトを描画できます。  
  
- <xref:System.Windows.Media.DrawingVisual> の外観の記述に使用できます。  
  
- <xref:System.Windows.Media.Visual> のコンテンツの列挙に使用できます。  
  
 WPF には、図形、ビットマップ、テキスト、メディアを描画できる他の型のオブジェクトが用意されています。 たとえば、<xref:System.Windows.Shapes.Shape> オブジェクトを使用して図形を描画することもできます。<xref:System.Windows.Controls.MediaElement> コントロールはアプリケーションにビデオを追加する別の方法を提供します。 それでは、どのようなときに <xref:System.Windows.Media.Drawing> オブジェクトを使用する必要があるのでしょうか。 フレームワーク レベルの機能を犠牲にしてパフォーマンス上の利点を得ることができる場合、または <xref:System.Windows.Freezable> の機能が必要な場合です。 <xref:System.Windows.Media.Drawing> オブジェクトは[レイアウト](../advanced/layout.md)、入力、フォーカスをサポートしていないため、背景の記述、クリップアート、<xref:System.Windows.Media.Visual> オブジェクトでの低レベルの描画に理想的なパフォーマンス上の利点を提供します。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトは、<xref:System.Windows.Freezable> オブジェクトの一種であるため、いくつかの特殊な機能があります。たとえば、[リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)としての宣言、複数オブジェクトでの共有、読み取り専用にすることによるパフォーマンスの向上、複製、スレッド セーフ化などです。 <xref:System.Windows.Freezable> オブジェクトで提供されるさまざまな機能について詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
<a name="drawinggeometriessection"></a>
## <a name="draw-a-shape"></a>図形の描画  
 図形を描画するには、<xref:System.Windows.Media.GeometryDrawing> を使用します。 ジオメトリ描画の <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> プロパティは描画する図形を記述し、<xref:System.Windows.Media.GeometryDrawing.Brush%2A> プロパティは図形の内部の描画方法を記述し、<xref:System.Windows.Media.GeometryDrawing.Pen%2A> プロパティはアウトラインの描画方法を記述します。  
  
 次の例では、<xref:System.Windows.Media.GeometryDrawing> を使用して図形を描画します。 この図形は 1 つの <xref:System.Windows.Media.GeometryGroup> オブジェクトと 2 つの <xref:System.Windows.Media.EllipseGeometry> オブジェクトによって記述されます。 図形の内側は <xref:System.Windows.Media.LinearGradientBrush> で塗りつぶされ、その枠線は <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen> で描画されます。  
  
 この例では、次の <xref:System.Windows.Media.GeometryDrawing> が作成されます。  
  
 ![2 つの楕円の GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexampleinline)]
 [!code-xaml[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexampleinline)]  
  
 完全な例については、「[GeometryDrawing を作成する](how-to-create-a-geometrydrawing.md)」をご覧ください。  
  
 <xref:System.Windows.Media.PathGeometry> などの他の <xref:System.Windows.Media.Geometry> クラスを使用すると、曲線や円弧を作成することでさらに複雑な図形を作成できます。 <xref:System.Windows.Media.Geometry> オブジェクトの詳細については、「[ジオメトリの概要](geometry-overview.md)」をご覧ください。  
  
 <xref:System.Windows.Media.Drawing> オブジェクトを使用しないで図形を描画する他の方法について詳しくは、「[WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)」をご覧ください。  
  
<a name="drawingimagessection"></a>
## <a name="draw-an-image"></a>イメージの描画  
 イメージを描画するには、<xref:System.Windows.Media.ImageDrawing> を使用します。 <xref:System.Windows.Media.ImageDrawing> オブジェクトの <xref:System.Windows.Media.ImageDrawing.ImageSource%2A> プロパティは描画するイメージを記述し、<xref:System.Windows.Media.ImageDrawing.Rect%2A> プロパティはイメージが描画される領域を定義します。  
  
 次の例では、(75,75) に存在する 100 x 100 ピクセルの四角形にイメージを描画します。 次の図は、この例で作成した <xref:System.Windows.Media.ImageDrawing> を示しています。 グレーの境界は、<xref:System.Windows.Media.ImageDrawing> の範囲を示すために追加したものです。  
  
 ![&#40;75,75&#41; に描画される 100 × 100 の ImageDrawing](./media/graphicsmm-simple-imagedrawing-offset.png "graphicsmm_simple_imagedrawing_offset")  
100×100 の ImageDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawing100by100inline)]
 [!code-xaml[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawing100by100inline)]  
  
 イメージについて詳しくは、「[イメージングの概要](imaging-overview.md)」をご覧ください。  
  
<a name="playmedia"></a>
## <a name="play-media-code-only"></a>メディアの再生 (コードのみ)  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で <xref:System.Windows.Media.VideoDrawing> を宣言することはできますが、メディアの読み込みと再生ができるのはコードを使用する場合のみです。 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] でビデオを再生するには、代わりに <xref:System.Windows.Controls.MediaElement> を使用します。  
  
 オーディオ ファイルまたはビデオ ファイルを再生するには、<xref:System.Windows.Media.VideoDrawing> と <xref:System.Windows.Media.MediaPlayer> を使用します。 メディアを読み込んで再生するには、2 つの方法があります。 1 つ目の方法は、<xref:System.Windows.Media.MediaPlayer> と <xref:System.Windows.Media.VideoDrawing> を単独で使用することです。2 つ目の方法は、<xref:System.Windows.Media.MediaPlayer> と <xref:System.Windows.Media.VideoDrawing> で使用する独自の <xref:System.Windows.Media.MediaTimeline> を作成することです。  
  
> [!NOTE]
> アプリケーションでメディアを配布するときは、イメージのようにプロジェクト リソースとしてメディア ファイルを使うことはできません。 プロジェクト ファイルで、メディアの種類を `Content` に設定し、`CopyToOutputDirectory` を `PreserveNewest` または `Always` に設定する必要があります。  
  
 独自の <xref:System.Windows.Media.MediaTimeline> を作成しないでメディアを再生するには、次の手順を実行します。  
  
1. <xref:System.Windows.Media.MediaPlayer> オブジェクトを作成します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline1)]  
  
2. <xref:System.Windows.Media.MediaPlayer.Open%2A> メソッドを使用して、メディア ファイルを読み込みます。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline2)]  
  
3. <xref:System.Windows.Media.VideoDrawing> を作成します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline3)]  
  
4. <xref:System.Windows.Media.VideoDrawing> の <xref:System.Windows.Media.VideoDrawing.Rect%2A> プロパティを設定することで、メディアを描画するサイズと位置を指定します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline4](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline4)]  
  
5. <xref:System.Windows.Media.VideoDrawing> の <xref:System.Windows.Media.VideoDrawing.Player%2A> プロパティに、作成した <xref:System.Windows.Media.MediaPlayer> を設定します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline5](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline5)]  
  
6. <xref:System.Windows.Media.MediaPlayer> の <xref:System.Windows.Media.MediaPlayer.Play%2A> メソッドを使用して、メディアの再生を開始します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline6](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline6)]  
  
 次の例では、<xref:System.Windows.Media.VideoDrawing> と <xref:System.Windows.Media.MediaPlayer> を使用して、ビデオ ファイルを 1 回再生します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 メディアに対する追加のタイミング制御を取得するには、<xref:System.Windows.Media.MediaPlayer> と <xref:System.Windows.Media.VideoDrawing> オブジェクトで <xref:System.Windows.Media.MediaTimeline> を使用します。 <xref:System.Windows.Media.MediaTimeline> を使用すると、ビデオを繰り返す必要があるかどうかを指定できます。 <xref:System.Windows.Media.VideoDrawing> で <xref:System.Windows.Media.MediaTimeline> を使用するには、次の手順を実行します。  
  
1. <xref:System.Windows.Media.MediaTimeline> を宣言し、そのタイミング動作を設定します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline1)]  
  
2. <xref:System.Windows.Media.MediaTimeline> から <xref:System.Windows.Media.MediaClock> を作成します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline2)]  
  
3. <xref:System.Windows.Media.MediaPlayer> を作成し、<xref:System.Windows.Media.MediaClock> を使用してその <xref:System.Windows.Media.MediaPlayer.Clock%2A> プロパティを設定します。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline3)]  
  
4. <xref:System.Windows.Media.VideoDrawing> を作成し、<xref:System.Windows.Media.MediaPlayer> を <xref:System.Windows.Media.VideoDrawing> の <xref:System.Windows.Media.VideoDrawing.Player%2A> プロパティに割り当てます。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline4](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline4)]  
  
 次の例では、<xref:System.Windows.Media.MediaPlayer> および <xref:System.Windows.Media.VideoDrawing> と共に <xref:System.Windows.Media.MediaTimeline> を使用して、ビデオを繰り返し再生します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 <xref:System.Windows.Media.MediaTimeline> を使用する場合は、<xref:System.Windows.Media.MediaPlayer> の対話型メソッドではなく、<xref:System.Windows.Media.MediaClock> の <xref:System.Windows.Media.Animation.Clock.Controller%2A> プロパティから返された対話型の <xref:System.Windows.Media.Animation.ClockController> を使用して、メディアの再生を制御します。  
  
<a name="drawtext"></a>
## <a name="draw-text"></a>テキストの描画  
 テキストを描画するには、<xref:System.Windows.Media.GlyphRunDrawing> と <xref:System.Windows.Media.GlyphRun> を使用します。 次の例では、<xref:System.Windows.Media.GlyphRunDrawing> を使用して "Hello World" というテキストを描画します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GlyphRunDrawingExample.cs#glyphrundrawingexampleinline)]
 [!code-xaml[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GlyphRunExample.xaml#glyphrundrawingexampleinline)]  
  
 <xref:System.Windows.Media.GlyphRun> は、固定形式のドキュメント プレゼンテーションと印刷のシナリオで使用することを意図された低レベルのオブジェクトです。 画面にテキストを描画する簡単な方法は、<xref:System.Windows.Controls.Label> または <xref:System.Windows.Controls.TextBlock> を使用する方法です。 <xref:System.Windows.Media.GlyphRun> について詳しくは、「[GlyphRun オブジェクトと Glyphs 要素の概要](../advanced/introduction-to-the-glyphrun-object-and-glyphs-element.md)」をご覧ください。  
  
<a name="compositedrawingssection"></a>
## <a name="composite-drawings"></a>複合描画  
 <xref:System.Windows.Media.DrawingGroup> を使用すると、複数の描画を 1 つの複合描画に結合できます。 <xref:System.Windows.Media.DrawingGroup> を使用すると、図形、イメージ、テキストを 1 つの <xref:System.Windows.Media.Drawing> オブジェクトに結合できます。  
  
 次の例では、<xref:System.Windows.Media.DrawingGroup> を使用して、2 つの <xref:System.Windows.Media.GeometryDrawing> オブジェクトと <xref:System.Windows.Media.ImageDrawing> オブジェクトを結合します。 この例を実行すると、次の出力が生成されます。  
  
 ![複数の描画を含む DrawingGroup](./media/graphicsmm-simple.jpg "graphicsmm_simple")  
複合描画  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 また、<xref:System.Windows.Media.DrawingGroup> を使用すると、不透明マスク、変換、ビットマップ効果などの操作をコンテンツに適用することもできます。 <xref:System.Windows.Media.DrawingGroup> 操作は、<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>、<xref:System.Windows.Media.DrawingGroup.Opacity%2A>、<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>、<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>、<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>、<xref:System.Windows.Media.DrawingGroup.Transform%2A> の順に適用されます。  
  
 次の図は、<xref:System.Windows.Media.DrawingGroup> 操作が適用される順序を示したものです。  
  
 ![DrawingGroup の操作の順序](./media/graphcismm-drawinggroup-order.png "graphcismm_drawinggroup_order")  
DrawingGroup の操作の順序  
  
 次の表では、<xref:System.Windows.Media.DrawingGroup> オブジェクトの内容の操作に使用できるプロパティを説明します。  
  
|プロパティ|説明|図|  
|--------------|-----------------|------------------|  
|<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>|<xref:System.Windows.Media.DrawingGroup> の内容の選択した部分の不透明度を変更します。 例については、「[方法: 描画の不透明度を制御する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748242(v=vs.90))」をご覧ください。|![不透明度マスクを使用した DrawingGroup](./media/graphicsmm-opmask.png "graphicsmm_opmask")|  
|<xref:System.Windows.Media.DrawingGroup.Opacity%2A>|<xref:System.Windows.Media.DrawingGroup> の内容の不透明度を一様に変更します。 <xref:System.Windows.Media.Drawing> を透明または半透明にするには、このプロパティを使用します。 例については、「[方法: 不透明マスクを描画に適用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms753195(v=vs.90))」をご覧ください。|![不透明度の設定が異なる DrawingGroups](./media/graphicsmm-opacity.png "graphicsmm_opacity")|  
|<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>|<xref:System.Windows.Media.DrawingGroup> の内容に <xref:System.Windows.Media.Effects.BitmapEffect> を適用します。 例については、「[方法: BitmapEffect を描画に適用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752341(v=vs.90))」をご覧ください。|![BlurBitmapEffect を使用した DrawingGroup](./media/graphicsmm-bitmap.png "graphicsmm_bitmap")|  
|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|<xref:System.Windows.Media.Geometry> を使用して記述した領域に <xref:System.Windows.Media.DrawingGroup> の内容をクリッピングします。 例については、「[方法: 描画をクリッピングする](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms743068(v=vs.90))」をご覧ください。|![クリップ領域が定義された DrawingGroup](./media/graphicsmm-clipgeom.png "graphicsmm_clipgeom")|  
|<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>|デバイスに依存しないピクセルを、指定したガイドラインに沿ったデバイス ピクセルにスナップします。 このプロパティは、低解像度ディスプレイで、非常に詳細なグラフィックスがはっきりとレンダリングされるようにするのに便利です。 例については、「[方法 : 描画に GuidelineSet を適用する](how-to-apply-a-guidelineset-to-a-drawing.md)」をご覧ください。|![GuidelineSet がある (またはない) DrawingGroup](./media/graphicsmm-drawinggroup-guidelineset.png "graphicsmm_drawinggroup_guidelineset")|  
|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|<xref:System.Windows.Media.DrawingGroup> の内容を変換します。 例については、「[方法: 変換を描画に適用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms742304(v=vs.90))」をご覧ください。|![回転した DrawingGroup](./media/graphicsmm-rotate.png "graphicsmm_rotate")|  
  
<a name="usingimagedrawing"></a>
## <a name="display-a-drawing-as-an-image"></a>描画をイメージとして表示する  
 <xref:System.Windows.Controls.Image> コントロールで <xref:System.Windows.Media.Drawing> を表示するには、<xref:System.Windows.Controls.Image> コントロールの <xref:System.Windows.Controls.Image.Source%2A> として <xref:System.Windows.Media.DrawingImage> を使用し、表示する描画に <xref:System.Windows.Media.DrawingImage> オブジェクトの <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=nameWithType> プロパティを設定します。  
  
 次の例では、<xref:System.Windows.Media.DrawingImage> と <xref:System.Windows.Controls.Image> コントロールを使用して <xref:System.Windows.Media.GeometryDrawing> を表示します。 この例を実行すると、次の出力が生成されます。  
  
 ![2 つの楕円の GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
<a name="renderingwithdrawingbrushsection"></a>
## <a name="paint-an-object-with-a-drawing"></a>描画によるオブジェクトの塗りつぶし  
 <xref:System.Windows.Media.DrawingBrush> は、描画オブジェクトで領域を塗りつぶすブラシの一種です。 描画でほとんどすべてのグラフィカル オブジェクトを塗りつぶすために使うことができます。 <xref:System.Windows.Media.DrawingBrush> の <xref:System.Windows.Media.Drawing> プロパティは、<xref:System.Windows.Media.DrawingBrush.Drawing%2A> を記述します。 <xref:System.Windows.Media.DrawingBrush> で <xref:System.Windows.Media.Drawing> をレンダリングするには、ブラシの <xref:System.Windows.Media.Drawing> プロパティを使用してブラシにこれを追加し、ブラシを使用してコントロールやパネルなどのグラフィカル オブジェクトを塗りつぶします。  
  
 次の例では、<xref:System.Windows.Media.DrawingBrush> を使用して、<xref:System.Windows.Media.GeometryDrawing> から作成されたパターンで <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を塗りつぶします。 この例を実行すると、次の出力が生成されます。  
  
 ![並べて表示される DrawingBrush](./media/graphicsmm-drawingbrush-geometrydrawing.png "graphicsmm_drawingbrush_geometrydrawing")  
DrawingBrush で使われる GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 <xref:System.Windows.Media.DrawingBrush> クラスには、内容を拡大したり並べて表示したりするためのさまざまなオプションが用意されています。 <xref:System.Windows.Media.DrawingBrush> の詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」の概要をご覧ください。  
  
<a name="renderingwithvisualsection"></a>
## <a name="render-a-drawing-with-a-visual"></a>ビジュアルで描画をレンダリングする  
 <xref:System.Windows.Media.DrawingVisual> は、描画をレンダリングするために設計されたビジュアル オブジェクトの一種です。 高度にカスタマイズされたグラフィカル環境を構築したい開発者は、ビジュアル レイヤーを直接操作できますが、この概要ではそれについては説明しません。 詳しくは、「[DrawingVisual オブジェクトの使用](using-drawingvisual-objects.md)」をご覧ください。  
  
<a name="drawingcontextobjects"></a>
## <a name="drawingcontext-objects"></a>DrawingContext オブジェクト  
 <xref:System.Windows.Media.DrawingContext> クラスを使用すると、<xref:System.Windows.Media.Visual> または <xref:System.Windows.Media.Drawing> にビジュアル コンテンツを設定できます。 このような低レベルのグラフィックス オブジェクトの多くは、グラフィカル コンテンツを非常に効率よく記述できるため、<xref:System.Windows.Media.DrawingContext> を使用します。  
  
 <xref:System.Windows.Media.DrawingContext> の描画メソッドは <xref:System.Drawing.Graphics?displayProperty=nameWithType> 型の描画メソッドと見た目は似ていますが、実際にはかなり異なります。 <xref:System.Windows.Media.DrawingContext> は保持モードのグラフィックス システムで使用されますが、<xref:System.Drawing.Graphics?displayProperty=nameWithType> 型はイミディエイト モードのグラフィックス システムで使用されます。 <xref:System.Windows.Media.DrawingContext> オブジェクトの描画コマンドを使用すると、実際には、レンダリング命令のセットが保存され (ただし、厳密な格納メカニズムは <xref:System.Windows.Media.DrawingContext> を提供するオブジェクトの型に依存します)、後でグラフィックス システムによって使用されます。画面にリアルタイムで描画されることはありません。 Windows Presentation Foundation (WPF) グラフィックス システムの動作方法について詳しくは、「[WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)」をご覧ください。  
  
 <xref:System.Windows.Media.DrawingContext> を直接インスタンス化することはできません。ただし、描画コンテキストは、特定のメソッド (<xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> や <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType> など) から取得できます。  
  
<a name="enumeratevisualcontents"></a>
## <a name="enumerate-the-contents-of-a-visual"></a>ビジュアルの内容の列挙  
 他の用途に加えて、<xref:System.Windows.Media.Drawing> オブジェクトでは、<xref:System.Windows.Media.Visual> の内容を列挙するためのオブジェクト モデルも提供されます。  
  
 次の例では、<xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> メソッドを使用して <xref:System.Windows.Media.Visual> の <xref:System.Windows.Media.DrawingGroup> 値を取得し、それを列挙します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Drawing>
- <xref:System.Windows.Media.DrawingGroup>
- [2D グラフィックスとイメージング](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [ジオメトリの概要](geometry-overview.md)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
- [方法トピック](drawings-how-to-topics.md)
