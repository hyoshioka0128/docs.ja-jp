---
title: プロパティ アニメーションの手法の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- animation [WPF], properties [WPF], methods for
- properties [WPF], methods for animating
ms.assetid: 74f61413-f8c0-4e75-bf04-951886426c8b
ms.openlocfilehash: 0b4bf6d4963f32ad83f762fce73c805197ff9c9b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181844"
---
# <a name="property-animation-techniques-overview"></a>プロパティ アニメーションの手法の概要
このトピックでは、ストーリーボード、ローカル アニメーション、クロック、フレームごとのアニメーションなど、プロパティをアニメーション化するさまざまなアプローチについて説明します。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、「[アニメーションの概要](animation-overview.md)」で説明されている基本のアニメーション機能に精通している必要があります。  
  
<a name="summary"></a>
## <a name="different-ways-to-animate"></a>さまざまなアニメーション化方法  
 プロパティをアニメーション化するには多数のシナリオがあるため、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ではプロパティをアニメーション化するいくつかの方法が提供されます。  
  
 それぞれの方法について、インスタンス単位、スタイル内、コントロール テンプレート内、またはデータ テンプレート内で使用できるかどうか、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で使用できるかどうか、およびアニメーションを対話的に制御できるかどうかを次の表に示します。  "インスタンス単位" とは、スタイル、コントロール テンプレート、またはデータ テンプレート内のインスタンスではなく、オブジェクトのインスタンスに直接アニメーションまたはストーリーボードを適用する方法のことです。  
  
|アニメーションの手法|シナリオ|XAML のサポート|対話的に制御可能|  
|-------------------------|---------------|-------------------|--------------------------------|  
|ストーリー ボード アニメーション|インスタンス単位、<xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate>、 <xref:System.Windows.DataTemplate>|はい|はい|  
|ローカル アニメーション|インスタンス単位|いいえ|いいえ|  
|クロック アニメーション|インスタンス単位|いいえ|はい|  
|フレーム単位のアニメーション|インスタンス単位|いいえ|N/A|  
  
<a name="storyboard_animations"></a>
## <a name="storyboard-animations"></a>ストーリー ボード アニメーション  
 <xref:System.Windows.Media.Animation.Storyboard> は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でアニメーションを定義および適用する場合、アニメーションを開始後に対話的に制御する場合、複雑なアニメーション ツリーを作成する場合、あるいは <xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate> または <xref:System.Windows.DataTemplate> でアニメーション化する場合に使用します。 <xref:System.Windows.Media.Animation.Storyboard> によってアニメーション化されるオブジェクトは、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> であるか、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> を設定するために使用される必要があります。 詳しくは、「[ストーリーボードの概要](storyboards-overview.md)」をご覧ください。  
  
 <xref:System.Windows.Media.Animation.Storyboard> は、特殊な種類のコンテナー <xref:System.Windows.Media.Animation.Timeline> であり、その中に含まれているアニメーションのターゲット情報を提供します。 <xref:System.Windows.Media.Animation.Storyboard> を使用してアニメーション化するには、次の 3 つのステップを実行します。  
  
1. <xref:System.Windows.Media.Animation.Storyboard> と 1 つ以上のアニメーションを宣言します。  
  
2. <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 添付プロパティおよび <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 添付プロパティを使用して、各アニメーションのターゲット オブジェクトおよびプロパティを指定します。  
  
3. (コードのみ) <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> の <xref:System.Windows.NameScope> を定義します。 <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> を使用してアニメーション化するオブジェクトの名前を登録します。  
  
4. <xref:System.Windows.Media.Animation.Storyboard> を開始します。  
  
 <xref:System.Windows.Media.Animation.Storyboard> を開始すると、アニメーションが、アニメーション化されるプロパティに適用され、開始されます。 <xref:System.Windows.Media.Animation.Storyboard> を開始するには、2 つの方法があります。<xref:System.Windows.Media.Animation.Storyboard> クラスによって提供される <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用するか、<xref:System.Windows.Media.Animation.BeginStoryboard> アクションを使用します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でアニメーション化する唯一の方法は、<xref:System.Windows.Media.Animation.BeginStoryboard> アクションを使用することです。 <xref:System.Windows.Media.Animation.BeginStoryboard> アクションは、<xref:System.Windows.EventTrigger>、<xref:System.Windows.Trigger> プロパティ、または <xref:System.Windows.DataTrigger> で使用できます。  
  
 次の表は、<xref:System.Windows.Media.Animation.Storyboard> の開始方法それぞれがサポートされているさまざまな場所 (インスタンス単位、スタイル、コントロール テンプレート、データ テンプレート) を示しています。  
  
|ストーリーボードが開始される場所|インスタンス単位|スタイル|コントロール テンプレート|データ テンプレート|例|  
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> および <xref:System.Windows.EventTrigger>|はい|はい|はい|はい|[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> およびプロパティ <xref:System.Windows.Trigger>|いいえ|はい|はい|はい|[プロパティ値が変化したときにアニメーションをトリガーする](how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> および <xref:System.Windows.DataTrigger>|いいえ|はい|はい|はい|[方法: データが変化したときにアニメーションをトリガーする](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|  
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッド|はい|いいえ|いいえ|いいえ|[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトの詳細については、「[ストーリーボードの概要](storyboards-overview.md)」をご覧ください。  
  
## <a name="local-animations"></a>ローカル アニメーション  
 ローカル アニメーションは、任意の <xref:System.Windows.Media.Animation.Animatable> オブジェクトの依存関係プロパティをアニメーション化する場合に使用すると便利です。 プロパティに適用するアニメーションが 1 つだけであり、アニメーションを開始後に対話的に制御する必要がない場合は、ローカル アニメーションを使用します。 ローカル アニメーションは、<xref:System.Windows.Media.Animation.Storyboard> アニメーションとは異なり、<xref:System.Windows.FrameworkElement> にも <xref:System.Windows.FrameworkContentElement> にも関連付けられていないオブジェクトをアニメーション化できます。 また、この種類のアニメーションには <xref:System.Windows.NameScope> を定義する必要がありません。  
  
 ローカル アニメーションはコードだけで使用できます。スタイル、コントロール テンプレート、またはデータ テンプレート内では定義できません。 ローカル アニメーションは、開始後に対話的に制御できません。  
  
 ローカル アニメーションを使用してアニメーション化するには、次の手順を実行します。  
  
1. <xref:System.Windows.Media.Animation.AnimationTimeline> オブジェクトを作成します。  
  
2. アニメーション化するオブジェクトの <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用して、指定したプロパティに <xref:System.Windows.Media.Animation.AnimationTimeline> を適用します。  
  
 次の例は、<xref:System.Windows.Controls.Button> の幅と背景色をアニメーション化する方法を示しています。  
  
 [!code-cpp[animateproperty#11](~/samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](~/samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
## <a name="clock-animations"></a>クロック アニメーション  
 <xref:System.Windows.Media.MediaPlayer.Clock%2A> オブジェクトは、<xref:System.Windows.Media.Animation.Storyboard> を使用せずにアニメーション化するときに、複雑なタイミング ツリーを作成する場合またはアニメーションを開始後に対話的に制御する場合に使用します。 クロック オブジェクトを使用して、任意の <xref:System.Windows.Media.Animation.Animatable> オブジェクトの依存関係プロパティをアニメーション化できます。  
  
 <xref:System.Windows.Media.Animation.Clock> オブジェクトは、スタイル、コントロール テンプレート、またはデータ テンプレート内でアニメーション化するために直接使用することはできません。 (アニメーションとタイミング システムは、実際に <xref:System.Windows.Media.Animation.Clock> オブジェクトを使用してスタイル、コントロール テンプレート、およびデータ テンプレート内でアニメーション化しますが、このような <xref:System.Windows.Media.Animation.Clock> オブジェクトを <xref:System.Windows.Media.Animation.Storyboard> から作成する必要があります。 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトと <xref:System.Windows.Media.Animation.Clock> オブジェクトの間のリレーションシップについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。)  
  
 1 つの <xref:System.Windows.Media.Animation.Clock> をプロパティに適用するには、次の手順を実行します。  
  
1. <xref:System.Windows.Media.Animation.AnimationTimeline> オブジェクトを作成します。  
  
2. <xref:System.Windows.Media.Animation.AnimationTimeline> の <xref:System.Windows.Media.Animation.AnimationTimeline.CreateClock%2A> メソッドを使用して、<xref:System.Windows.Media.Animation.AnimationClock> を作成します。  
  
3. アニメーション化するオブジェクトの <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> メソッドを使用して、指定したプロパティに <xref:System.Windows.Media.Animation.AnimationClock> を適用します。  
  
 次の例は、<xref:System.Windows.Media.Animation.AnimationClock> を作成して、それを 2 つの類似したプロパティに適用する方法を示しています。  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 タイミング ツリーを作成し、これを使用してプロパティをアニメーション化するには、次の手順を実行します。  
  
1. <xref:System.Windows.Media.Animation.ParallelTimeline> オブジェクトおよび <xref:System.Windows.Media.Animation.AnimationTimeline> オブジェクトを使用して、タイミング ツリーを作成します。  
  
2. ルート <xref:System.Windows.Media.Animation.ParallelTimeline> の <xref:System.Windows.Media.Animation.TimelineGroup.CreateClock%2A> を使用して、<xref:System.Windows.Media.Animation.ClockGroup> を作成します。  
  
3. <xref:System.Windows.Media.Animation.ClockGroup> の <xref:System.Windows.Media.Animation.ClockGroup.Children%2A> を反復処理し、その子 <xref:System.Windows.Media.Animation.Clock> オブジェクトを適用します。 子 <xref:System.Windows.Media.Animation.AnimationClock> ごとに、アニメーション化するオブジェクトの <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> メソッドを使用して、指定したプロパティに <xref:System.Windows.Media.Animation.AnimationClock> を適用します  
  
 Clock オブジェクトについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。  
  
## <a name="per-frame-animation-bypass-the-animation-and-timing-system"></a>フレーム単位のアニメーション:アニメーションとタイミング システムをバイパスする  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーション システムを完全にバイパスする必要があるときは、この方法を使います。 この方法の 1 つのシナリオは、アニメーションの各ステップで、オブジェクトの最後の一連のやり取りに基づいてオブジェクトの再計算が必要になる物理アニメーションです。  
  
 フレーム単位アニメーションは、スタイル、コントロール テンプレート、またはデータ テンプレート内で定義できません。  
  
 フレームごとにアニメーション化するには、アニメーション化するオブジェクトを格納しているオブジェクトの <xref:System.Windows.Media.CompositionTarget.Rendering> イベントを登録します。 このイベント ハンドラー メソッドは、フレームごとに 1 回呼び出されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] がビジュアル ツリーの永続化されたレンダリング データを構成ツリーにマーシャリングするたびに、イベント ハンドラー メソッドが呼び出されます。  
  
 イベント ハンドラーでは、アニメーション効果に必要なあらゆる計算を実行し、これらの値を使用してアニメーション化するオブジェクトのプロパティを設定します。  
  
 現在のフレームの表現時間を取得するために、このイベントに関連付けられている <xref:System.EventArgs> を、<xref:System.Windows.Media.RenderingEventArgs> としてキャストできます。これにより、現在のフレームのレンダリング時間を取得するために使用できる <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> プロパティが提供されます。  
  
 詳細については、<xref:System.Windows.Media.CompositionTarget.Rendering> に関するページをご覧ください。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
- [アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)
- [依存関係プロパティの概要](../advanced/dependency-properties-overview.md)
