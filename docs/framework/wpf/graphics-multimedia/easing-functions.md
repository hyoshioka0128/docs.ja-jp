---
title: イージング関数
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applying mathematical formulas to animations [WPF]
- applying easing functions to animations [WPF]
- mathematical formulas [WPF], applying to animations
- animations [WPF], realistic movement
- easing functions [WPF]
- customizing easing functions [WPF]
- easing functions [WPF], definition
- easing functions [WPF], customizing
- animations [WPF], applying
ms.assetid: 075b9c2b-82c4-43fa-b3cd-de0b6236eb38
ms.openlocfilehash: a25bde5098af853c3906a174a189fc35f33f0525
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186500"
---
# <a name="easing-functions"></a>イージング関数
イージング関数を使うと、独自の数式をアニメーションに適用することができます。 たとえば、オブジェクトをリアルにバウンドさせたり、バネに乗っているように動作させたりすることができます。 キー フレーム アニメーションや From/To/By アニメーションを使ってこれらの効果を近似することもできますが、大量の作業が必要であり、アニメーションは数式を使うほど正確ではありません。  
  
 <xref:System.Windows.Media.Animation.EasingFunctionBase> から継承することによって独自のカスタム イージング関数を作成するだけでなく、ランタイムによって提供されるいくつかのイージング関数の 1 つを使用して一般的な効果を作成できます。  
  
- <xref:System.Windows.Media.Animation.BackEase>:示されているパスでアニメーション化を開始する直前に、アニメーションの動作を逆行させます。  
  
- <xref:System.Windows.Media.Animation.BounceEase>:バウンス効果を作成します。  
  
- <xref:System.Windows.Media.Animation.CircleEase>:円関数を使って加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.CubicEase>:数式 *f*(*t*) = *t*<sup>3</sup> を使用して、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.ElasticEase>:静止するまで前後に振れるバネのようなアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.ExponentialEase>:指数式を使って、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.PowerEase>:数式 *f*(*t*) = *t*<sup>p</sup> (この場合、p は <xref:System.Windows.Media.Animation.PowerEase.Power%2A> プロパティと等しい) を使用して、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.QuadraticEase>:数式 *f*(*t*) = *t*<sup>2</sup> を使用して、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.QuarticEase>:数式 *f*(*t*) = *t*<sup>4</sup> を使用して、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.QuinticEase>:数式 *f*(*t*) = *t*<sup>5</sup> を使用して、加速や減速するアニメーションを作成します。  
  
- <xref:System.Windows.Media.Animation.SineEase>:正弦公式を使用して、加速または減速するアニメーションを作成します。  
  
 アニメーションにイージング関数を適用するには、アニメーションの `EasingFunction` プロパティを使って、アニメーションに適用するイージング関数を指定します。 次の例は、<xref:System.Windows.Media.Animation.BounceEase> イージング関数を <xref:System.Windows.Media.Animation.DoubleAnimation> に適用して、バウンス効果を作成します。  
  
 [!code-xaml[BounceEase_snippet#BounceEase](~/samples/snippets/csharp/VS_Snippets_Wpf/bounceease_snippet/CS/window1.xaml#bounceease)]  
  
 前の例では、イージング関数を From/To/By アニメーションに適用しました。 キー フレーム アニメーションにこれらのイージング関数を適用することもできます。 次の例では、キー フレームとそれらに関連付けられたイージング関数を使って、四角形が上方に縮まり、遅くなり、下方に延び (落下するように)、停止するアニメーションを作成します。  
  
 [!code-xaml[EasingFunctionDoubleKeyFrame_snippet#EasingFunctionDoubleKeyFrame](~/samples/snippets/csharp/VS_Snippets_Wpf/easingfunctiondoublekeyframe_snippet/CS/window1.xaml#easingfunctiondoublekeyframe)]  
  
 <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> プロパティを使用して、イージング関数の動作を変更する、つまり、アニメーションの補間方法を変更することができます。 <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> に指定できる値は次の 3 つです。  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseIn>:補間は、イージング関数に関連付けられている数式に従います。  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseOut>:補間は、100% の補間から、イージング関数に関連付けられている数式の出力を引いた値に従います。  
  
- <xref:System.Windows.Media.Animation.EasingMode.EaseInOut>:補間は、アニメーションの最初の半分には <xref:System.Windows.Media.Animation.EasingMode.EaseIn> を使用し、残りの半分には <xref:System.Windows.Media.Animation.EasingMode.EaseOut> を使用します。  
  
 次のグラフは、<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> のさまざまな値を示しています。*f*(*x*) はアニメーションの進行状況を表し、*t* は時間を表します。  
  
 <xref:System.Windows.Media.Animation.BackEase>  
  
 ![BackEase EasingMode のグラフ。](./media/backease-graph.png "BackEase_Graph")  
  
 <xref:System.Windows.Media.Animation.BounceEase>  
  
 ![BounceEase EasingMode のグラフ。](./media/bounceease-graph.png "BounceEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CircleEase>  
  
 ![CircleEase EasingMode のグラフ。](./media/circleease-graph.png "CircleEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CubicEase>  
  
 ![CubicEase EasingMode のグラフ。](./media/cubicease-graph.png "CubicEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ElasticEase>  
  
 ![さまざまな easingmode のグラフでの ElasticEase。](./media/elasticease-graph.png "ElasticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ExponentialEase>  
  
 ![さまざまな easingmode のグラフでの ExponentialEase。](./media/exponentialease-graph.png "ExponentialEase_Graph")  
  
 <xref:System.Windows.Media.Animation.PowerEase>  
  
 ![さまざまな easingmode のグラフでの QuarticEase。](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuadraticEase>  
  
 ![さまざまな easingmode のグラフでの QuadraticEase](./media/quadraticease-graph.png "QuadraticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuarticEase>  
  
 ![さまざまな easingmode のグラフでの QuarticEase。](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuinticEase>  
  
 ![さまざまな easingmode のグラフでの QuinticEase。](./media/quinticease-graph.png "QuinticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.SineEase>  
  
 ![さまざまな EasingMode 値での SineEase](./media/sineease-graph.png "SineEase_Graph")  
  
> [!NOTE]
> <xref:System.Windows.Media.Animation.PowerEase> を使用すると、<xref:System.Windows.Media.Animation.PowerEase.Power%2A> プロパティを使って <xref:System.Windows.Media.Animation.CubicEase>、<xref:System.Windows.Media.Animation.QuadraticEase>、<xref:System.Windows.Media.Animation.QuarticEase>、および <xref:System.Windows.Media.Animation.QuinticEase> と同じ動作を作成できます。 たとえば、<xref:System.Windows.Media.Animation.PowerEase> を使用して <xref:System.Windows.Media.Animation.CubicEase> を置き換える場合は、<xref:System.Windows.Media.Animation.PowerEase.Power%2A> 値 3 を指定します。  
  
 ランタイムに含まれるイージング関数を使うだけでなく、<xref:System.Windows.Media.Animation.EasingFunctionBase> から継承することによって独自のイージング関数を作成できます。 次の例では、簡単なカスタム イージング関数を作成する方法を示します。 <xref:System.Windows.Media.Animation.EasingFunctionBase.EaseInCore%2A> メソッドをオーバーライドすることにより、イージング関数の動作について独自の数学ロジックを追加できます。
  
 [!code-csharp[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/customlog10easingfunction.cs#customeasingfunction)]
 [!code-vb[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/visualbasic/VS_Snippets_Wpf/customeasingfunction/visualbasic/customlog10easingfunction.vb#customeasingfunction)]
 [!code-xaml[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/window1.xaml#customeasingfunction)]
