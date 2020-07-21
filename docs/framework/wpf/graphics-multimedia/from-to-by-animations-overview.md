---
title: From/To/By アニメーションの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], From/to/by
- From/to/by animation
ms.assetid: 516fce0a-e7f8-49b8-b018-53b3d409a8a3
ms.openlocfilehash: 135f01823d374b30f8d4d41762d2267a254f98c9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186463"
---
# <a name="fromtoby-animations-overview"></a>From/To/By アニメーションの概要
このトピックでは、From/To/By アニメーションを使って依存関係プロパティをアニメーション化する方法を説明します。 From/To/By アニメーションでは、2 つの値の間の遷移が作成されます。  
  
<a name="prereq"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション機能を理解している必要があります。 アニメーションの機能の概要については、「[アニメーションの概要](animation-overview.md)」を参照してください。  
  
<a name="whatisanimation"></a>
## <a name="what-is-a-fromtoby-animation"></a>From/To/By アニメーションとは  
 From/To/By アニメーションは、開始値と終了値の間の遷移を作成する <xref:System.Windows.Media.Animation.AnimationTimeline> の一種です。 遷移が完了するまでにかかる時間は、そのアニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> によって決まります。  
  
 From/To/By アニメーションをプロパティに適用するには、マークアップとコード内で <xref:System.Windows.Media.Animation.Storyboard> を使用するか、コード内で <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用します。 From/To/By アニメーションを使用して <xref:System.Windows.Media.Animation.AnimationClock> を作成し、それを 1 つ以上のプロパティに適用することもできます。 アニメーションを適用するためのさまざまなメソッドの詳細については、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」を参照してください。  
  
 From/To/By アニメーションは、2 つのターゲット値以外の値を持つことはできません。 3 つ以上のターゲット値を持つアニメーションを必要とする場合は、キー フレーム アニメーションを使います。 キー フレーム アニメーションについては、「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」に説明があります。  
  
<a name="animation_types"></a>
## <a name="fromtoby-animation-types"></a>From/To/By アニメーションの種類  
 アニメーションはプロパティ値を生成するため、プロパティの型ごとに異なるアニメーションの種類があります。 要素の <xref:System.Windows.FrameworkElement.Width%2A> プロパティなど、<xref:System.Double> を受け取るプロパティをアニメーション化するには、<xref:System.Double> 値を生成するアニメーションを使用します。 <xref:System.Windows.Point> を受け取るプロパティをアニメーション化するには、<xref:System.Windows.Point> 値を生成するアニメーションを使用します。他も同様です。  
  
 From/To/By アニメーション クラスは <xref:System.Windows.Media.Animation> 名前空間に属し、次の名前付け規則を使用します。  
  
 *\<Type>* `Animation`  
  
 ここで、 *\<Type>* は、クラスがアニメーション化する値の型です。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、次の From/To/By アニメーション クラスが用意されています。  
  
|プロパティの型|対応する From/To/By アニメーションのクラス|  
|-------------------|------------------------------------------------|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimation>|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimation>|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16Animation>|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32Animation>|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64Animation>|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimation>|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimation>|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimation>|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimation>|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimation>|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimation>|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimation>|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimation>|  
  
<a name="anim_values"></a>
## <a name="target-values"></a>ターゲット値  
 From/To/By アニメーションでは、2 つのターゲット値の間の遷移が作成されます。 通常は、開始値 (<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを使用して設定) と終了値 (<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを使用して設定) を指定します。 ただし、開始値、終了値、またはオフセット値のみを指定することもできます。 これらの場合、アニメーションは不足しているターゲット値をアニメーション化するプロパティから取得します。 次の一覧では、アニメーションのターゲット値を指定する方法について説明します。  
  
- **開始値**  
  
     アニメーションの開始値を明示的に指定する場合は、<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを使用します。 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティは、単独で使用することも、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティまたは <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティと併用することもできます。 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティだけを指定した場合、アニメーションはその値から、アニメーション化されるプロパティの基本値まで遷移します。  
  
- **終了値**  
  
     アニメーションの終了値を指定するには、その <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを使用します。 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティだけを指定した場合、アニメーションは開始値を、アニメーション化するプロパティから、または同じプロパティに適用されている別のアニメーションの出力から取得します。 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティと共に <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを使用して、アニメーションの開始と終了の値を明示的に指定できます。  
  
- **オフセット値**  
  
     <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティを使用すると、アニメーションの明示的な開始値または終了値の代わりにオフセットを指定できます。 アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティでは、アニメーションがその期間中に値を変更する量を指定します。 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティは、単独で使用することも、<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティと共に使用することもできます。 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティだけを指定した場合、アニメーションは、プロパティの基本値または別のアニメーションの出力に、オフセット値を加算します。  
  
<a name="examples"></a>
## <a name="using-fromtoby-values"></a>From/To/By 値の使用  
 次のセクションでは、<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>、および <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> のプロパティを併用する方法、または個別に使用する方法について説明します。  
  
 このセクションの例ではそれぞれ、From/To/By アニメーションの一種である <xref:System.Windows.Media.Animation.DoubleAnimation> を使用して、デバイスに依存しないピクセルで高さ 10、幅 100 の <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> プロパティをアニメーション化します。  
  
 各例では <xref:System.Windows.Media.Animation.DoubleAnimation> を使用しますが、From/To/By アニメーションすべての From、To、By の各プロパティの動作は同じです。 また、これらの各例では <xref:System.Windows.Media.Animation.Storyboard> を使用しますが、他の方法でも From/To/By アニメーションを使用できます。 詳しくは、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」を参照してください。  
  
### <a name="fromto"></a>From/To  
 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> と <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> の値を両方とも設定すると、アニメーションは <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティによって指定された値から、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティによって指定された値まで進行します。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを 50 に、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを 300 に設定しています。 その結果、<xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> は 50 から 300 までアニメーション化されます。  
  
 [!code-csharp[basicvalues_snip#FromToAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromtoanimationinline)]
 [!code-vb[basicvalues_snip#FromToAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromtoanimationinline)]  
  
### <a name="to"></a>終了  
 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティだけを設定すると、アニメーションは、アニメーション化されるプロパティの基本値、または同じプロパティに以前に適用された合成アニメーションの出力から、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティによって指定された値まで進行します。  
  
 ("合成アニメーション" とは、現在のアニメーションが <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> ハンドオフ動作を使用して適用されていた場合に、引き続き有効である同じプロパティに以前に適用された <xref:System.Windows.Media.Animation.ClockState.Active> または <xref:System.Windows.Media.Animation.ClockState.Filling> のアニメーションを指します。)  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティのみを 300 に設定します。 開始値が指定されなかったため、<xref:System.Windows.Media.Animation.DoubleAnimation> は <xref:System.Windows.FrameworkElement.Width%2A> プロパティの基本値 (100) を開始値として使用します。 <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> は、100 から、アニメーションのターゲット値である 300 までアニメーション化されます。  
  
 [!code-csharp[basicvalues_snip#ToAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#toanimationinline)]
 [!code-vb[basicvalues_snip#ToAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#toanimationinline)]  
  
### <a name="by"></a>By  
 アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティだけを設定すると、アニメーションは、アニメーション化されるプロパティの基本値、または合成アニメーションの出力から、その値と <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティによって指定された値の合計まで進行します。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティのみを 300 に設定します。 この例では開始値が指定されていないため、<xref:System.Windows.Media.Animation.DoubleAnimation> は <xref:System.Windows.FrameworkElement.Width%2A> プロパティの基本値 100 を開始値として使用します。 終了値は、アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 値 300 をその開始値 100 に加算して算出されます。つまり、400 です。 その結果、<xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> は 100 から 400 までアニメーション化されます。  
  
 [!code-csharp[basicvalues_snip#ByAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#byanimationinline)]
 [!code-vb[basicvalues_snip#ByAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#byanimationinline)]  
  
### <a name="fromby"></a>From/By  
 アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティおよび <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティを設定すると、アニメーションは <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティで指定された値から、<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> と <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティの合計によって指定された値まで進行します。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを 50 に、その <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティを 300 に設定しています。 終了値は、アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 値 300 をその開始値 50 に加算して算出されます。つまり、350 です。 その結果、<xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> は 50 から 350 までアニメーション化されます。  
  
 [!code-csharp[basicvalues_snip#FromByAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#frombyanimationinline)]
 [!code-vb[basicvalues_snip#FromByAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#frombyanimationinline)]  
  
### <a name="from"></a>From  
 アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 値だけを指定すると、アニメーションは、<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティで指定された値から、アニメーション化されるプロパティの基本値、または合成アニメーションの出力まで進行します。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティのみを 50 に設定します。 終了値が指定されなかったため、<xref:System.Windows.Media.Animation.DoubleAnimation> は <xref:System.Windows.FrameworkElement.Width%2A> プロパティの基本値 100 を終了値として使用します。 <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.FrameworkElement.Width%2A> は、50 から、<xref:System.Windows.FrameworkElement.Width%2A> プロパティの基本値である 100 までアニメーション化されます。  
  
 [!code-csharp[basicvalues_snip#FromAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromanimationinline)]
 [!code-vb[basicvalues_snip#FromAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromanimationinline)]  
  
### <a name="toby"></a>To/By  
 アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> と <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> の両方のプロパティを設定した場合、<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> プロパティは無視されます。  
  
<a name="otheranimationtypes"></a>
## <a name="other-animation-types"></a>他のアニメーションの種類  
 From/To/By アニメーションは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって提供されるアニメーションの唯一の種類ではありません。キー フレーム アニメーションとパス アニメーションも提供されています。  
  
- キー フレーム アニメーションは、キー フレームを使って記述されている任意の数の目標値に沿ってアニメーション化します。 詳しくは、「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」を参照してください。  
  
- パス アニメーションは、<xref:System.Windows.Media.PathGeometry> から出力値を生成します。 詳しくは、「[パス アニメーションの概要](path-animations-overview.md)」を参照してください。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、独自のカスタム アニメーションの種類を作成することもできます。 詳しくは、「[カスタム アニメーションの概要](custom-animations-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.Timeline>
- <xref:System.Windows.Media.Animation.Storyboard>
- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [パス アニメーションの概要](path-animations-overview.md)
- [カスタム アニメーションの概要](custom-animations-overview.md)
- [アニメーションのターゲット値 (From、To、および By) のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/TargetValues)
