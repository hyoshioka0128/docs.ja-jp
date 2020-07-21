---
title: パス アニメーションの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], paths
- path animations [WPF]
ms.assetid: 979c732c-df74-47a6-be96-8e07b3707d53
ms.openlocfilehash: 07628d26c8222c7c01f58826a36a15e13dc31ff4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181868"
---
# <a name="path-animations-overview"></a>パス アニメーションの概要
<a name="introduction"></a>このトピックでは、ジオメトリック パスを使用して出力値を生成できるパス アニメーションの概要を説明します。 パス アニメーションは、複雑なパスに沿ってオブジェクトを移動および回転させるときに便利です。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション機能を理解している必要があります。 アニメーションの機能の概要については、「[アニメーションの概要](animation-overview.md)」を参照してください。  
  
 <xref:System.Windows.Media.PathGeometry> オブジェクトを使用してパス アニメーションを定義するので、<xref:System.Windows.Media.PathGeometry> と各種の <xref:System.Windows.Media.PathSegment> オブジェクトについても理解している必要があります。 詳細については、「[ジオメトリの概要](geometry-overview.md)」を参照してください。  
  
<a name="what_is_a_path_animation"></a>
## <a name="what-is-a-path-animation"></a>パス アニメーションとは  
 パス アニメーションは、<xref:System.Windows.Media.PathGeometry> を入力として使用する <xref:System.Windows.Media.Animation.AnimationTimeline> の一種です。 From/To/By アニメーションのように From、To、または By プロパティを設定するか、キー フレーム アニメーションのようにキー フレームを使用する代わりに、ジオメトリック パスを定義し、それを使用してパス アニメーションの `PathGeometry` プロパティを設定します。 パス アニメーションが進むとき、パスから x、y、および角度情報を読み取り、その情報を使用して、出力を生成します。  
  
 パス アニメーションは、複雑なパスに沿ってオブジェクトをアニメーション化するのに便利です。 パスに沿ってオブジェクトを移動する 1 つの方法として、<xref:System.Windows.Media.MatrixTransform> と <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> を使用して、複雑なパスに沿ってオブジェクトを変換する方法があります。 次の例では、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> オブジェクトを使用して <xref:System.Windows.Media.MatrixTransform> の <xref:System.Windows.Media.MatrixTransform.Matrix%2A> プロパティをアニメーション化することで、この手法を示します。 <xref:System.Windows.Media.MatrixTransform> がボタンに適用され、曲線パスに沿って移動するようにします。 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> プロパティは `true` に設定されているため、四角形がパスの接線に沿って回転します。  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の例で使用されているパス構文の詳細については、「[パス マークアップ構文](path-markup-syntax.md)」の概要を参照してください。 サンプル全体については、「[パス アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/PathAnimations)」を参照してください。  
  
 パス アニメーションをプロパティに適用するには、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] とコード内で <xref:System.Windows.Media.Animation.Storyboard> を使用するか、コード内で <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用します。 パス アニメーションを使用して <xref:System.Windows.Media.Animation.AnimationClock> を作成し、それを 1 つ以上のプロパティに適用することもできます。 アニメーションを適用するためのさまざまなメソッドの詳細については、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」を参照してください。  
  
<a name="animation_types"></a>
## <a name="path-animation-types"></a>パス アニメーションの種類  
 アニメーションはプロパティ値を生成するため、プロパティの型ごとに異なるアニメーションの種類があります。 <xref:System.Double> (<xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティなど) を受け取るプロパティをアニメーション化するには、<xref:System.Double> 値を生成するアニメーションを使用します。 <xref:System.Windows.Point> を受け取るプロパティをアニメーション化するには、<xref:System.Windows.Point> 値を生成するアニメーションを使用します。他も同様です。  
  
 パス アニメーション クラスは <xref:System.Windows.Media.Animation> 名前空間に属し、次の名前付け規則を使用します。  
  
 *\<Type>* `AnimationUsingPath`  
  
 ここで、 *\<Type>* は、クラスがアニメーション化する値の型です。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、次のパス アニメーション クラスが用意されています。  
  
|プロパティの型|対応するパス アニメーション クラス|例|  
|-------------------|----------------------------------------|-------------|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|[パスに沿ってオブジェクトをアニメーション化する (ダブル アニメーション)](how-to-animate-an-object-along-a-path-double-animation.md)|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>|[パスに沿ってオブジェクトをアニメーション化する (行列アニメーション)](how-to-animate-an-object-along-a-path-matrix-animation.md)|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|[パスに沿ってオブジェクトをアニメーション化する (ポイント アニメーション)](how-to-animate-an-object-along-a-path-point-animation.md)|  
  
 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> では、その <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.PathGeometry%2A> から <xref:System.Windows.Media.Matrix> 値が生成されます。 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> を <xref:System.Windows.Media.MatrixTransform> と共に使用すると、パスに沿ってオブジェクトを移動できます。 また、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> の <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> プロパティを `true` に設定すると、パスの曲線に沿ってオブジェクトが回転します。  
  
 <xref:System.Windows.Media.Animation.PointAnimationUsingPath> では、その <xref:System.Windows.Media.Animation.PointAnimationUsingPath.PathGeometry%2A> の x と y の座標から <xref:System.Windows.Point> 値が生成されます。 <xref:System.Windows.Media.Animation.PointAnimationUsingPath> を使用して <xref:System.Windows.Point> 値を受け取るプロパティをアニメーション化すると、パスに沿ってオブジェクトを移動できます。 <xref:System.Windows.Media.Animation.PointAnimationUsingPath> ではオブジェクトを回転できません。  
  
 <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> では、その <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A> から <xref:System.Double> 値が生成されます。 <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.Source%2A> プロパティを設定すると、<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> で、パスの x 座標、y 座標、角度のどれを出力として使用するかを指定できます。 <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> を使用すると、オブジェクトを回転したり、x 軸または y 軸に沿って移動したりすることができます。  
  
<a name="pathanimationinput"></a>
## <a name="path-animation-input"></a>パス アニメーションの入力  
 各パス アニメーション クラスには、その入力を指定するための <xref:System.Windows.Media.PathGeometry> プロパティが用意されています。 パス アニメーションでは、<xref:System.Windows.Media.PathGeometry> を使用してその出力値が生成されます。 <xref:System.Windows.Media.PathGeometry> クラスを使用すると、円弧、曲線、直線で構成される複数の複雑な図形を記述できます。  
  
 <xref:System.Windows.Media.PathGeometry> の中核となるのは、<xref:System.Windows.Media.PathFigure> オブジェクトのコレクションです。これらのオブジェクトがこのような名前である理由は、各図形によって、<xref:System.Windows.Media.PathGeometry> 内に個別の形状が記述されることです。 各 <xref:System.Windows.Media.PathFigure> は 1 つ以上の <xref:System.Windows.Media.PathSegment> オブジェクトで構成され、このそれぞれで図形のセグメントが記述されます。  
  
 多くの種類のセグメントがあります。  
  
|セグメントの種類|説明|  
|------------------|-----------------|  
|<xref:System.Windows.Media.ArcSegment>|2 つの点を結ぶ楕円の円弧を作成します。|  
|<xref:System.Windows.Media.BezierSegment>|2 つの点を結ぶ 3 次ベジエ曲線を作成します。|  
|<xref:System.Windows.Media.LineSegment>|2 つの点を結ぶ直性を作成します。|  
|<xref:System.Windows.Media.PolyBezierSegment>|一続きの 3 次ベジエ曲線を作成します。|  
|<xref:System.Windows.Media.PolyLineSegment>|一続きの直線を作成します。|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|一続きの 2 次ベジエ曲線を作成します。|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|2 次ベジエ曲線を作成します。|  
  
 <xref:System.Windows.Media.PathFigure> 内のセグメントは 1 つの幾何学図形に結合され、各セグメントの終点が次のセグメントの始点として使用されます。 <xref:System.Windows.Media.PathFigure> の <xref:System.Windows.Media.PathFigure.StartPoint%2A> プロパティでは、最初のセグメントが描画されるときの開始地点を指定します。 後続の各セグメントは、前のセグメントの終点から始まります。 たとえば、`10,50` から `10,150` までの垂直線を定義するには、<xref:System.Windows.Media.PathFigure.StartPoint%2A> プロパティを `10,50` に設定し、<xref:System.Windows.Media.LineSegment.Point%2A> プロパティを `10,150` に設定して <xref:System.Windows.Media.LineSegment> を作成します。  
  
 <xref:System.Windows.Media.PathGeometry> オブジェクトの詳細については、「[ジオメトリの概要](geometry-overview.md)」を参照してください。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、特殊な省略構文を使用して <xref:System.Windows.Media.PathGeometry> の <xref:System.Windows.Media.PathGeometry.Figures%2A> プロパティを設定することもできます。 詳細については、「[パス マークアップ構文](path-markup-syntax.md)」の概要を参照してください。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の例で使用されているパス構文の詳細については、「[パス マークアップ構文](path-markup-syntax.md)」の概要を参照してください。  
  
## <a name="see-also"></a>関連項目

- [パス アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/PathAnimations)
- [パス マークアップ構文](path-markup-syntax.md)
- [パス アニメーションに関する「方法」トピック](path-animation-how-to-topics.md)
- [アニメーションの概要](animation-overview.md)
- [プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)
