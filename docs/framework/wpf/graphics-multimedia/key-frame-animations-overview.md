---
title: キー フレーム アニメーションの概要
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], key-frame
- key frames [WPF], about key-frame animations
- multiple animation target values [WPF]
ms.assetid: 10028f97-bb63-41fc-b8ad-663dac7ea203
ms.openlocfilehash: 8eb590b07eae3b76b3a206b9731997a6bc2c90d7
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344900"
---
# <a name="key-frame-animations-overview"></a>キー フレーム アニメーションの概要
このトピックでは、キー フレーム アニメーションの概要を説明します。 キー フレーム アニメーションでは、3 つ以上のターゲット値を使用してアニメーション化することができ、アニメーションの補間方式を制御できます。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 この概要を理解するのには、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アニメーションとタイムラインを理解しておく必要があります。 アニメーションの概要については、「[アニメーションの概要](animation-overview.md)」を参照してください。 さらに、From/To/By アニメーションについて理解しておくと役に立ちます。 詳細については、「From/To/By アニメーションの概要」を参照してください。  
  
<a name="whatisakeyframeanimation"></a>
## <a name="what-is-a-key-frame-animation"></a>キー フレーム アニメーションとは  
 From/To/By アニメーションと同じように、キー フレーム アニメーションも、ターゲット プロパティの値をアニメーション化します。 これは、その <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 中にターゲット値の間に遷移を作成します。 ただし、From/To/By アニメーションは 2 つの値の間の遷移を作成しますが、キー フレーム アニメーションは、任意の数のターゲット値の間の遷移を作成できます。 From/To/By アニメーションとは異なり、キー フレーム アニメーションには、ターゲット値を設定する From、To、または By プロパティはありません。 キー フレーム アニメーションのターゲット値は、キー フレーム オブジェクトを使用して記述されます (このため、"キー フレーム アニメーション" という用語が使用されます)。 アニメーションのターゲット値を指定するには、キー フレーム オブジェクトを作成し、アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A> コレクションに追加します。 アニメーションを実行すると、アニメーションが指定したフレームの間で遷移します。  
  
 複数のターゲット値のサポートに加え、一部のキー フレーム メソッドでは、複数の補間方式もサポートします。 アニメーションの補間方式は、1 つの値から次の値にどのように遷移するかを定義します。 補間には、離散、線形、およびスプラインの 3 つの種類があります。  
  
 キー フレーム アニメーションをアニメーション化するには、次の手順を完了します。  
  
- From/To/By アニメーションの場合と同じように、アニメーションを宣言して、その <xref:System.Windows.Media.Animation.Timeline.Duration%2A> を指定します。  
  
- ターゲット値ごとに、適切な種類のキー フレームを作成し、その値と <xref:System.Windows.Media.Animation.KeyTime> を設定して、アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A> コレクションに追加します。  
  
- From/To/By アニメーションと同じように、アニメーションをプロパティに関連付けます。 ストーリーボードを使用したアニメーションのプロパティへの適用の詳細については、「[ストーリー ボードの概要](storyboards-overview.md)」を参照してください。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> を使用して、<xref:System.Windows.Shapes.Rectangle> 要素を 4 つの異なる場所にアニメーション化します。  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
 From/To/By アニメーションのように、キー フレーム アニメーションをプロパティに適用するには、マークアップとコード内で <xref:System.Windows.Media.Animation.Storyboard> を使用するか、コード内で <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用します。 キー フレーム アニメーションを使用して <xref:System.Windows.Media.Animation.AnimationClock> を作成し、それを 1 つ以上のプロパティに適用することもできます。 アニメーションを適用するためのさまざまなメソッドの詳細については、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」を参照してください。  
  
<a name="animation_types"></a>
## <a name="key-frame-animation-types"></a>キー フレーム アニメーションの種類  
 アニメーションはプロパティ値を生成するため、プロパティの型ごとに異なるアニメーションの種類があります。 <xref:System.Double> を受け取るプロパティ (要素の <xref:System.Windows.FrameworkElement.Width%2A> プロパティなど) をアニメーション化するには、<xref:System.Double> 値を生成するアニメーションを使用します。 <xref:System.Windows.Point> を受け取るプロパティをアニメーション化するには、<xref:System.Windows.Point> 値を生成するアニメーションを使用します。他も同様です。  
  
 キー フレーム アニメーション クラスは <xref:System.Windows.Media.Animation> 名前空間に属し、次の名前付け規則を使用します。  
  
 *\<Type>* `AnimationUsingKeyFrames`  
  
 ここで、 *\<Type>* は、クラスがアニメーション化する値の型です。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、次のキー フレーム アニメーション クラスを提供します。  
  
|プロパティの型|対応するFrom/To/By アニメーションのクラス|サポートされる補間方式|  
|-------------------|------------------------------------------------|-------------------------------------|  
|<xref:System.Boolean>|<xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>|離散|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16AnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32AnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64AnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames>|離散|  
|<xref:System.Object>|<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>|離散|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.String>|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|離散|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames>|離散、線形、スプライン|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimationUsingKeyFrames>|離散、線形、スプライン|  
  
<a name="animation_target_values"></a>
## <a name="target-values-key-frames-and-key-times"></a>ターゲット値 (キー フレーム) とキー時刻  
 さまざまな種類のプロパティをアニメーション化するための多様な種類のキー フレーム アニメーションがあるように、さまざまな種類のキー フレーム オブジェクトがあります (アニメーション化される値の型とサポートされる補間方式ごとに 1 種類のオブジェクト)。 キー フレームの種類は、次の名前付け規則に従います。  
  
 *\<InterpolationMethod>\<Type>* `KeyFrame`  
  
 ここで、 *\<InterpolationMethod>* は、キー フレームで使用される補間方式であり、 *\<Type>* は、クラスがアニメーション化する値の型です。 3 つの補間方式のすべてをサポートするキー フレーム アニメーションでは、3 種類のキー フレームを使用できます。 たとえば、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> では、<xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>、<xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>、<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> の 3 種類のキー フレームを使用できます。 (補間方式については、後のセクションで詳しく説明します)。  
  
 キー フレームの主な目的は、<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> と <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>を指定することです。 すべての種類のキー フレームには、次の 2 つのプロパティがあります。  
  
- <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> プロパティは、そのキー フレームのターゲット値を指定します。  
  
- <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> プロパティは、キー フレームの <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> に達するタイミング (アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 内で) を指定します。  
  
 キー フレーム アニメーションが開始されると、<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> プロパティによって定義された順序でキー フレームが反復処理されます。  
  
- 時刻 0 にキー フレームがない場合は、ターゲット プロパティの現在の値と最初のキー フレームの <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> の間を遷移するアニメーションが作成されます。それ以外の場合は、アニメーションの出力値が最初のキー フレームの値になります。  
  
- 2 つ目のキーフレームに指定された補間方式を使用して、1 つ目と 2 つ目のキー フレームの <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> の間を遷移するアニメーションが作成されます。 遷移は最初のキー フレームの <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> から開始し、2 番目のキーフレームの <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> に達すると終了します。  
  
- アニメーションは、前後のキー フレームの間の遷移を作成しながら続行されます。  
  
- 最終的に、アニメーションは、最も大きなキー時刻 (アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 以下) を持つキー フレームの値になるまで遷移します。  
  
 アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> が <xref:System.Windows.Duration.Automatic%2A> か、その <xref:System.Windows.Media.Animation.Timeline.Duration%2A> が最後のキー フレームの時間と同じ場合、アニメーションは終了します。 それ以外の場合、アニメーションの <xref:System.Windows.Duration> が最後のキー フレームのキー時刻よりも大きいと、<xref:System.Windows.Duration> の終わりに達するまで、アニメーションでキー フレーム値が保持されます。 すべてのアニメーションと同じように、キー フレーム アニメーションでは、<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティを使用して、アクティブ期間の終わりに達したときに最終値を保持するかどうかを決定します。 詳細については、「[タイミング動作の概要](timing-behaviors-overview.md)」を参照してください。  
  
 次の例では、前の例で定義した <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> オブジェクトを使用して、<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> プロパティと <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> プロパティがどのように機能するかを示しています。  
  
- 最初のキー フレームは、アニメーションの出力値をただちに 0 に設定します。  
  
- 2 番目のキー フレームは、0 から 350 までアニメーション化されます。 最初のキー フレームが終わった時点で開始され (時刻 = 0 秒)、2 秒間再生され、時刻 = 0:0:2 で終わります。  
  
- 3 番目のキー フレームは、350 から 50 までアニメーション化されます。 2 番目のキー フレームが終わった時点で開始され (時刻 = 2 秒)、5 秒間再生され、時刻 = 0:0:7 で終わります。  
  
- 4 番目のキー フレームは、50 から 200 までアニメーション化されます。 3 番目のキー フレームが終わった時点で開始され (時刻 = 7 秒)、1 秒間再生され、時刻 = 0:0:8 で終わります。  
  
- アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティが 10 秒に設定されていたため、このアニメーションは、終了時刻 = 0:0:10 になる前の 2 秒間、最終値を保持します。  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
<a name="interpolationmethods"></a>
## <a name="interpolation-methods"></a>補間方式  
 前のセクションで、一部のキー フレーム アニメーションでは複数の補間方式がサポートされることに言及しました。 アニメーションの補間は、その継続時間中にアニメーションがどのように遷移するかを表します。 アニメーションで使用するキー フレームの種類を選択することで、そのキー フレーム セグメントの補間方式を定義できます。 補間方式には、線形、離散、およびスプラインの 3 つの種類があります。  
  
### <a name="linear-interpolation"></a>線形補間  
 線形補間では、アニメーションは、セグメントの継続期間中、一定の率で進行します。 たとえば、キー フレーム セグメントが 5 秒間で 0 から 10 に遷移する場合、アニメーションは、指定された時間に次の値を出力します。  
  
|時刻|出力値|  
|----------|------------------|  
|0|0|  
|1|2|  
|2|4|  
|3|6|  
|4|8|  
|4.25|8.5|  
|4.5|9|  
|5|10|  
  
### <a name="discrete-interpolation"></a>離散補間  
 離散補間では、アニメーション関数は、1 つの値から次の値に補間なしでジャンプします。 キー フレーム セグメントが 5 秒間で 0 から 10 に遷移する場合、アニメーションは、指定された時間で次の値を出力します。  
  
|時間|出力値|  
|----------|------------------|  
|0|0|  
|1|0|  
|2|0|  
|3|0|  
|4|0|  
|4.25|0|  
|4.5|0|  
|5|10|  
  
 アニメーションの出力値は、セグメント期間の最後の最後に達するまで変化しないことに注意してください。  
  
 スプライン補間はさらに複雑です。 次のセクションで説明します。  
  
<a name="anim_spline"></a>
### <a name="splined-interpolation"></a>スプライン補間  
 スプライン補間を使用して、リアルなタイミング効果を実現できます。 アニメーションは現実世界で起こる効果を模倣するために使用されることが多いため、開発者は、オブジェクトの加速と減速を細かく制御し、タイミング セグメントを緻密に操作することが必要になる場合があります。 スプライン キーフレームでは、スプライン補間を使用してアニメーション化できます。 その他のキー フレームでは、<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> と <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> を指定します。 スプライン キー フレームでは、<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A> も指定します。 次の例に、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> の 1 つのスプライン キー フレームを示します。 <xref:System.Windows.Media.Animation.KeySpline> プロパティに注目してください。このプロパティが、スプライン キー フレームを他の種類のキー フレームとは異なるものにしています。  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 3 次ベジエ曲線は、開始点、終点、および 2 つの制御点によって定義されます。 スプライン キー フレームの <xref:System.Windows.Media.Animation.KeySpline> プロパティは、(0, 0) から (1, 1) を結ぶベジエ曲線の 2 つの制御点を定義します。 最初の制御点は、ベジエ曲線の前半分の曲率を制御し、2 つ目の制御点は、後半分の曲率を制御します。 結果として得られる曲線は、そのスプライン キー フレームの変化率を表します。 曲線が急であればあるほど、キー フレームの値は急激に変化します。 曲線が平坦になると、キー フレームの値は緩やかに変化します。  
  
 <xref:System.Windows.Media.Animation.KeySpline> を使用して、流れ落ちる水や跳ねるボールなどの物理的な軌道をシミュレートしたり、モーション アニメーションに対して他の "イーズイン" 効果と "イーズアウト" 効果を適用したりできます。 背景のフェードやコントロール ボタンの復帰などのユーザー操作効果では、スプライン補間を適用して、アニメーションの変化率を特定の方法で加速したり減速したりできます。  
  
 次の例では、0,1 1,0 の <xref:System.Windows.Media.Animation.KeySpline> を指定して、以下のベジエ曲線を作成します。  
  
 ![ベジエ曲線](./media/graphicsmm-keyspline-0-1-1-0.png "graphicsmm_keyspline_0_1_1_0")  
制御点が (0.0, 1.0) および (1.0, 0.0) のキー スプライン  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 このキー フレームは、開始されると速いスピードでアニメーション化され、その後スピードが低下し、終了前に再びスピードが上がります。  
  
 次の例では、0.5,0.25 0.75,1.0 の <xref:System.Windows.Media.Animation.KeySpline> を指定して、以下のベジエ曲線を作成します。  
  
 ![ベジエ曲線](./media/graphicsmm-keyspline-025-050-075-10.png "graphicsmm_keyspline_025_050_075_10")  
制御点が (0.25, 0.5) および (0.75, 1.0) のキー スプライン  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexampleinline3)]  
  
 ベジエ曲線の曲率がほとんど変化しないため、このキー フレームは、ほぼ一定の率でアニメーション化され、最後の最後にわずかに減速します。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> を使用して、四角形の位置をアニメーション化します。 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> は <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> オブジェクトを使用するため、各キー フレーム値の間の遷移では、スプライン補間が使用されます。  
  
 [!code-xaml[keyframes_ovw_snippet#SplinedInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#splinedinterpolationexample)]  
  
 スプライン補間は理解するのが難しいことがあります。さまざまな設定で実験すると理解しやすくなります。 [キー スプライン アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/KeySplineAnimations)を使用して、キー スプライン値を変更し、その結果をアニメーションで確認することができます。  
  
<a name="combininginterpolationmethods"></a>
### <a name="combining-interpolation-methods"></a>補間方式の組み合わせ  
 補間の種類が異なるキー フレームを 1 つのキー フレーム アニメーションで使用できます。 補間の種類が異なる 2 つのキー フレーム アニメーションが連続する場合は、2 番目のキー フレームの補間方式を使用して、最初の値から 2 番目の値への遷移が作成されます。  
  
 次の例では、線形、スプライン、離散の補間を使用する <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> が作成されます。  
  
 [!code-xaml[keyframes_ovw_snippet#ComboInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#combointerpolationexample)]  
  
<a name="keytimes"></a>
## <a name="more-about-duration-and-key-times"></a>継続時間とキー時刻の詳細  
 他のアニメーションと同様に、キー フレーム アニメーションには <xref:System.Windows.Duration> プロパティがあります。 アニメーションの <xref:System.Windows.Duration> を指定するだけでなく、その継続時間のどの部分を各キー フレームに与えるかを指定する必要があります。 これを行うには、アニメーションの各キー フレームに <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> を指定します。 各キー フレームの <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> は、そのキー フレームの終了時刻を指定します。  
  
 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> プロパティは、キー時刻の再生時間は指定しません。 キー フレームが再生される時間の長さは、そのキー フレームの終了時刻、前のキー フレームの終了時刻、およびアニメーションの継続時間によって決まります。 キー時刻は、時刻値、パーセント、または特殊な値 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> または <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> として指定できます。  
  
 次の一覧で、キー時刻を指定するさまざまな方法について説明します。  
  
### <a name="timespan-values"></a>TimeSpan 値  
 <xref:System.TimeSpan> 値を使用して <xref:System.Windows.Media.Animation.KeyTime> を指定できます。 値は、0 以上、アニメーションの継続時間以下にする必要があります。 次の例は、継続時間が 10 秒で、キー時刻が時刻値として指定されている 4 つのキー フレームがあるアニメーションを示しています。  
  
- 最初のキー フレームは、最初の 3 秒間で基準値から 100 までアニメーション化され、時刻 = 0:0:03 で終わります。  
  
- 2 番目のキー フレームは、100 から 200 までアニメーション化されます。 最初のキー フレームが終わった時点で開始され (時刻 = 3 秒)、5 秒間再生され、時刻 = 0:0:8 で終わります。  
  
- 3 番目のキー フレームは、200 から 500 までアニメーション化されます。 2 番目のキー フレームが終わった時点で開始され (時刻 = 8 秒)、1 秒間再生され、時刻 = 0:0:9 で終わります。  
  
- 4 番目のキー フレームは、500 から 600 までアニメーション化されます。 3 番目のキー フレームが終わった時点で開始され (時刻 = 9 秒)、1 秒間再生され、時刻 = 0:0:10 で終わります。  
  
 [!code-xaml[keyframes_ovw_snippet#TimeSpanKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#timespankeytimeexample)]  
  
### <a name="percentage-values"></a>パーセント値  
 パーセント値は、アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> の特定のパーセントが経過した時点でキー フレームが終了することを指定します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、後ろに `%` 記号が付いた数値として指定します。 コードでは、<xref:System.Windows.Media.Animation.KeyTime.FromPercent%2A> メソッドを使用し、パーセントを示す <xref:System.Double> を渡します。 値は、0 以上、100 パーセント以下にする必要があります。 次の例は、継続時間が 10 秒で、キー時刻がパーセントとして指定されている 4 つのキー フレームがあるアニメーションを示しています。  
  
- 最初のキー フレームは、最初の 3 秒間で基準値から 100 までアニメーション化され、時刻 = 0:0:3 で終わります。  
  
- 2 番目のキー フレームは、100 から 200 までアニメーション化されます。 最初のキー フレームが終わった時点で開始され (時刻 = 3 秒)、5 秒間再生され、時刻 = 0:0:8 (0.8 * 10 = 8) で終わります。  
  
- 3 番目のキー フレームは、200 から 500 までアニメーション化されます。 2 番目のキー フレームが終わった時点で開始され (時刻 = 8 秒)、1 秒間再生され、時刻 = 0:0:9 (0.9 * 10 = 9) で終わります。  
  
- 4 番目のキー フレームは、500 から 600 までアニメーション化されます。 3 番目のキー フレームが終わった時点で開始され (時刻 = 9 秒)、1 秒間再生され、時刻 = 0:0:10 (1 * 10 = 10)で終わります。  
  
 [!code-xaml[keyframes_ovw_snippet#PercentageKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#percentagekeytimeexample)]  
  
### <a name="special-value-uniform"></a>特殊な値 Uniform  
 各キー フレームの時間を均等にするには、タイミングとして <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> を使用します。  
  
 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> キー時刻は、使用可能な時間をキー フレームの数で均等に除算して、各キー フレームの終了時刻を決定します。 次の例は、継続時間が 10 秒で、キー時刻が <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> として指定されている 4 つのキー フレームがあるアニメーションを示しています。  
  
- 最初のキー フレームは、最初の 2.5 秒間で基準値から 100 までアニメーション化され、時刻 = 0:0:2.5 で終わります。  
  
- 2 番目のキー フレームは、100 から 200 までアニメーション化されます。 最初のキー フレームが終わった時点で開始され (時刻 = 0:0:2.5 秒)、2.5 秒間再生され、時刻 = 0:0:5 で終わります。  
  
- 3 番目のキー フレームは、200 から 500 までアニメーション化されます。 2 番目のキー フレームが終わった時点で開始され (時刻 = 5 秒)、2.5 秒間再生され、時刻 = 0:0:7.5 で終わります。  
  
- 4 番目のキー フレームは、500 から 600 までアニメーション化されます。 2 番目のキー フレームが終わった時点で開始され (時刻 = 7.5 秒)、2.5 秒間再生され、時刻 = 0:0:10 で終わります。  
  
 [!code-xaml[keyframes_ovw_snippet#UniformKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#uniformkeytimeexample)]  
  
### <a name="special-value-paced"></a>特殊な値 Paced  
 一定の割合でアニメーション化する場合は、タイミングとして <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> を使用します。  
  
 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> キー時刻は、各キー フレームの長さに応じて使用可能な時間を割り当てて、各フレームの継続時間を決定します。  これにより、アニメーションの速さ (ペース) を一定に保つ動作が提供されます。  次の例は、継続時間が 10 秒で、キー時刻が <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> として指定されている 3 つのキー フレームがあるアニメーションを示しています。  
  
 [!code-xaml[keyframes_ovw_snippet#PacedKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#pacedkeytimeexample)]  
  
 最後のキーフレームのキー時刻が <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> または <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> の場合、解決されるキー時刻は 100% に設定されることに注意してください。 マルチ フレーム アニメーションの最初のキー フレームが Paced の場合、解決されたキー時刻は 0 に設定されます (キー フレーム コレクションにキー フレームが 1 つだけ含まれているときに、それが Paced が設定されたキー フレームの場合は、解決されたキー時刻は 100% に設定されます)。  
  
 1 つのキー フレーム アニメーション内の異なるキー フレームで異なるキー時刻を使用できます。  
  
<a name="combiningkeytimes"></a>
## <a name="combining-key-times-out-of-order-key-frames"></a>キー時刻と順不同のキー フレームの組み合わせ  
 同じアニメーションで <xref:System.Windows.Media.Animation.KeyTime> 値の型が異なるキー フレームを使用できます。 さらに、キー フレームは再生する順序で追加することをお勧めしますが、それは必須ではありません。 アニメーションとタイミング システムは、順不同のキー フレームを解決できます。 キー時刻が無効なキー フレームは無視されます。  
  
 キー フレーム アニメーションのキー フレームのキー時刻が解決される手順を次に示します。  
  
1. <xref:System.TimeSpan> <xref:System.Windows.Media.Animation.KeyTime> の値を解決します。  
  
2. アニメーションの*合計補間時間*を決定します。これは、キー フレーム アニメーションが順方向の反復を完了するまでにかかる合計時間です。  
  
    1. アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> が <xref:System.Windows.Duration.Automatic%2A> でも <xref:System.Windows.Duration.Forever%2A> でもない場合、合計補間時間は、アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティの値になります。  
  
    2. そうでない場合、合計補間時間は、そのキー フレームに指定されている最大 <xref:System.TimeSpan> <xref:System.Windows.Media.Animation.KeyTime> 値 (存在する場合) です。  
  
    3. それ以外の場合、合計補間時間は 1 秒間です。  
  
3. 合計補間時間の値を使用して、<xref:System.Windows.Media.Animation.KeyTimeType.Percent> <xref:System.Windows.Media.Animation.KeyTime> 値を解決します。  
  
4. 前の手順で解決されていなければ、最後のキー フレームを解決します。 最後のキー フレームの <xref:System.Windows.Media.Animation.KeyTime> が <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> または <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> の場合、解決される時間は、合計補間時間と同じになります。  
  
     最初のキー フレームの <xref:System.Windows.Media.Animation.KeyTime> が <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> で、そのアニメーションに複数のキー フレームがある場合は、<xref:System.Windows.Media.Animation.KeyTime> 値を 0 に解決します。キー フレームが 1 つしかなく、その <xref:System.Windows.Media.Animation.KeyTime> 値が <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> の場合は、前の手順で説明したように、合計補間時間に解決されます。  
  
5. 残りの <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> <xref:System.Windows.Media.Animation.KeyTime> 値を解決します。これらには、使用可能な時間がそれぞれ均等に割り当てられます。  このプロセス中に、未解決の <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 値は <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> <xref:System.Windows.Media.Animation.KeyTime> 値 として一時的に処理され、一時的に解決された時刻を取得します。  
  
6. キー時刻が未指定のキー フレームの <xref:System.Windows.Media.Animation.KeyTime> 値を、解決された <xref:System.Windows.Media.Animation.KeyTime> 値を持つ、最近隣と宣言されたキー フレームを使用して解決します。  
  
7. 残りの <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 値を解決します。 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> は、隣接するキー フレームの <xref:System.Windows.Media.Animation.KeyTime> 値を使用して、解決時間を決定します。  目標は、アニメーションの速度がこのキー フレームの解決時間近くで一定であることを保証することです。  
  
8. キー フレームを、解決時間 (主キー) の順序と宣言 (セカンダリ キー) の順序で並べ替えます。つまり、解決されたキー フレームの <xref:System.Windows.Media.Animation.KeyTime> 値に基づく安定した並べ替えを使用します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.KeyTime>
- <xref:System.Windows.Media.Animation.KeySpline>
- <xref:System.Windows.Media.Animation.Timeline>
- [キー スプライン アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/KeySplineAnimations)
- [キー フレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)
- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
- [タイミング動作の概要](timing-behaviors-overview.md)
