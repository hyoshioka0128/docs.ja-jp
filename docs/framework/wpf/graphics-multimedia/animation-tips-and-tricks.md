---
title: アニメーションのヒントとテクニック
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- troubleshooting [WPF], animation
- animations [WPF], FillBehavior property
- troubleshooting animation [WPF]
- animating objects [WPF], troubleshooting
- animation tips and tricks [WPF]
- tips and tricks [WPF], animation
- performance troubleshooting [WPF], animation
- animations [WPF], use of system resources
ms.assetid: e467796b-d5d4-45a6-a108-8c5d7ff69a0f
ms.openlocfilehash: 6b540448599c1e1083ed367a312ef60fceacd0d5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187647"
---
# <a name="animation-tips-and-tricks"></a>アニメーションのヒントとテクニック
WPF でアニメーションを扱うときに、アニメーションのパフォーマンスを向上させて不満を解消するためのヒントとテクニックがいくつかあります。  
  
<a name="generalissuessection"></a>
## <a name="general-issues"></a>一般的な問題  
  
### <a name="animating-the-position-of-a-scroll-bar-or-slider-freezes-it"></a>スクロール バーまたはスライダーの位置をアニメーション化するとフリーズする  
 <xref:System.Windows.Media.Animation.FillBehavior> が <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd> (既定値) であるアニメーションを使ってスクロール バーまたはスライダーの位置をアニメーション化すると、ユーザーはスクロール バーまたはスライダーを移動できなくなります。 原因は、アニメーションが終了しても、ターゲット プロパティの基底値をまだオーバーライドしているためです。 アニメーションによってプロパティの現在の値がオーバーライドされないようにするには、それを削除するか、<xref:System.Windows.Media.Animation.FillBehavior> を <xref:System.Windows.Media.Animation.FillBehavior.Stop> に指定します。 詳細と例については、「[ストーリーボードを使用してアニメーション化した後にプロパティを設定する](how-to-set-a-property-after-animating-it-with-a-storyboard.md)」をご覧ください。  
  
### <a name="animating-the-output-of-an-animation-has-no-effect"></a>アニメーションの出力のアニメーション化の効果がない  
 別のアニメーションの出力であるオブジェクトをアニメーション化することはできません。 たとえば、<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> を使用して <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A> を <xref:System.Windows.Media.RadialGradientBrush> から <xref:System.Windows.Media.SolidColorBrush> にアニメーション化する場合、<xref:System.Windows.Media.RadialGradientBrush> と <xref:System.Windows.Media.SolidColorBrush> のいずれのプロパティもアニメーション化することはできません。  
  
### <a name="cant-change-the-value-of-a-property-after-animating-it"></a>プロパティをアニメーション化した後にその値を変更できない  
 場合によっては、アニメーションが完了した後でも、アニメーション化の後にプロパティの値を変更できないように見えることがあります。 原因は、アニメーションが終了しても、プロパティの基底値をまだオーバーライドしているためです。 アニメーションによってプロパティの現在の値がオーバーライドされないようにするには、それを削除するか、<xref:System.Windows.Media.Animation.FillBehavior> を <xref:System.Windows.Media.Animation.FillBehavior.Stop> に指定します。 詳細と例については、「[ストーリーボードを使用してアニメーション化した後にプロパティを設定する](how-to-set-a-property-after-animating-it-with-a-storyboard.md)」をご覧ください。  
  
### <a name="changing-a-timeline-has-no-effect"></a>タイムラインを変更しても効果がない  
 ほとんどの <xref:System.Windows.Media.Animation.Timeline> プロパティはアニメーション化可能で、データ バインドできますが、アクティブな <xref:System.Windows.Media.Animation.Timeline> のプロパティ値を変更しても効果がないように見えます。 これは、<xref:System.Windows.Media.Animation.Timeline> が開始されると、タイミング システムが <xref:System.Windows.Media.Animation.Timeline> のコピーを作成し、それを使用して <xref:System.Windows.Media.Animation.Clock> オブジェクトを作成するためです。 元を変更しても、システムのコピーには影響しません。  
  
 <xref:System.Windows.Media.Animation.Timeline> に変更を反映させるには、クロックを再生成し、それを使って、以前に作成されたクロックを置き換える必要があります。 クロックは、自動的には再生成されません。 タイムラインの変更を適用するいくつかの方法を次に示します。  
  
- タイムラインが <xref:System.Windows.Media.Animation.Storyboard> であるか、それに属している場合は、<xref:System.Windows.Media.Animation.BeginStoryboard> または <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用してストーリーボードを再適用することで、変更を反映させることができます。 これには、アニメーションが再起動されるという副作用があります。 コードでは、<xref:System.Windows.Media.Animation.Storyboard.Seek%2A> メソッドを使用して、ストーリーボードを前の位置に戻すことができます。  
  
- <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用してプロパティにアニメーションを直接適用した場合は、もう一度 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを呼び出して、変更されたアニメーションを渡します。  
  
- クロック レベルで直接操作している場合は、新しいクロック セットを作成して適用し、それらを使って、生成されたクロックの以前のセットを置換します。  
  
 タイムラインとクロックについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。  
  
### <a name="fillbehaviorstop-doesnt-work-as-expected"></a>FillBehavior.Stop が期待どおりに動作しない  
 あるアニメーションを別のアニメーションに "引き渡す" ときなどに、<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティを <xref:System.Windows.Media.Animation.FillBehavior.Stop> に設定しても効果がないように見える場合があります。これは、<xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> の設定が <xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace> になっているためです。  
  
 次の例では、<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Shapes.Rectangle>、および <xref:System.Windows.Media.TranslateTransform> を作成します。 <xref:System.Windows.Media.TranslateTransform> は、<xref:System.Windows.Shapes.Rectangle> が <xref:System.Windows.Controls.Canvas> の周りを移動するようにアニメーション化されます。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipAnimatedObject](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipanimatedobject)]  
  
 このセクションの例では、前のオブジェクトを使って、<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティが想定どおり動作しないケースをいくつか示します。  
  
#### <a name="fillbehaviorstop-and-handoffbehavior-with-multiple-animations"></a>複数のアニメーションでの FillBehavior="Stop" と HandoffBehavior  
 アニメーションが 2 番目のアニメーションで置き換えられるときに、<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティを無視するように見えることがあります。 次の例を見てみましょう。ここでは、2 つの <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを作成し、それらを使用して、前の例で示したものと同じ <xref:System.Windows.Media.TranslateTransform> をアニメーション化しています。  
  
 1 つ目の <xref:System.Windows.Media.Animation.Storyboard> である `B1` は、<xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティを 0 から 350 にアニメーション化します。これにより、四角形は 350 ピクセル右に移動します。 アニメーションが継続時間の最後に達し、再生が停止すると、<xref:System.Windows.Media.TranslateTransform.X%2A> プロパティは元の値である 0 に戻ります。 その結果、四角形は右に 350 ピクセル移動し、元の位置に移動します。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB1Button](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb1button)]  
  
 2 つ目の <xref:System.Windows.Media.Animation.Storyboard> である `B2` も、同じ <xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティをアニメーション化します。 この <xref:System.Windows.Media.Animation.Storyboard> では、アニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティのみが設定されているため、アニメーションは、アニメーション化するプロパティの現在の値を開始値として使用します。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB2Button](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb2button)]  
  
 最初の <xref:System.Windows.Media.Animation.Storyboard> の再生中に 2 番目のボタンをクリックすると、次の動作が想定されます。  
  
1. アニメーションでは <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> が <xref:System.Windows.Media.Animation.FillBehavior.Stop> に設定されているため、最初のストーリーボードが終了し、四角形は元の位置に戻されます。  
  
2. 2 つ目のストーリーボードが反映され、現在位置である 0 から 500 にアニメーション化します。  
  
 **しかし、これは行われません。** 代わりに、四角形は戻らずに、右に移動し続けます。 その理由は、2 番目のアニメーションは最初のアニメーションの現在の値を開始値として使い、その値から 500 までアニメーション化するためです。 <xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace><xref:System.Windows.Media.Animation.HandoffBehavior> が使用されているために 2 番目のアニメーションが 1 番目を置き換えるときは、1 番目のアニメーションの <xref:System.Windows.Media.Animation.FillBehavior> は関係ありません。  
  
#### <a name="fillbehavior-and-the-completed-event"></a>FillBehavior と完了イベント  
 次の例では、<xref:System.Windows.Media.Animation.FillBehavior.Stop><xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> が効果がないと思われるもう 1 つのシナリオを示します。 ここでも、例はストーリーボードを使用して、<xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティを 0 から 350 へとアニメーション化します。 ただし、今回はこの例では <xref:System.Windows.Media.Animation.Timeline.Completed> イベントを登録します。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardCButton](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardcbutton)]  
  
 <xref:System.Windows.Media.Animation.Timeline.Completed> イベント ハンドラーは、同じプロパティを現在の値から 500 へとアニメーション化する別の <xref:System.Windows.Media.Animation.Storyboard> を開始します。  
  
 [!code-csharp[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml.cs#fillbehaviortipstoryboardc1completedhandler)]
 [!code-vb[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/VisualBasic/FillBehaviorTip.xaml.vb#fillbehaviortipstoryboardc1completedhandler)]  
  
 次に示すのは、2 番目の <xref:System.Windows.Media.Animation.Storyboard> をリソースとして定義するマークアップです。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipResources](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipresources)]  
  
 <xref:System.Windows.Media.Animation.Storyboard> を実行すると、<xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティは 0 から 350 へとアニメーション化され、完了すると 0 に戻り (<xref:System.Windows.Media.Animation.FillBehavior> 設定が <xref:System.Windows.Media.Animation.FillBehavior.Stop> になっているため)、その後、0 から 500 へとアニメーション化されると予測されます。 そうではなく、<xref:System.Windows.Media.TranslateTransform> は 0 から 350 へ、それから 500 へとアニメーション化します。  
  
 これは、WPF でのイベントの発生順序が原因です。また、プロパティ値がキャッシュされ、プロパティが無効にされない限り再計算されないことも原因です。 <xref:System.Windows.Media.Animation.Timeline.Completed> イベントはルート タイムライン (最初の <xref:System.Windows.Media.Animation.Storyboard>) によってトリガーされたため、最初に処理されます。 この時点で、<xref:System.Windows.Media.TranslateTransform.X%2A> プロパティはまだ無効になっていないため、アニメーション化された値を返します。 2 番目の <xref:System.Windows.Media.Animation.Storyboard> は、キャッシュされた値を開始値として使用してアニメーション化を開始します。  
  
<a name="performancesection"></a>
## <a name="performance"></a>パフォーマンス  
  
### <a name="animations-continue-to-run-after-navigating-away-from-a-page"></a>アニメーションがページからの移動後も実行され続ける  
 実行中のアニメーションを含む <xref:System.Windows.Controls.Page> から離れると、それらのアニメーションは <xref:System.Windows.Controls.Page> がガベージ コレクションされるまで再生を続けます。 使っているナビゲーション システムによっては、離れた後のページが無期限にメモリに残り、その間、そのアニメーションでリソースが消費されることがあります。 これは、ページに常時実行 ("アンビエント") アニメーションが含まれる場合に最も顕著です。  
  
 このため、<xref:System.Windows.FrameworkElement.Unloaded> イベントを使って、ページから離れるときにアニメーションを削除することをお勧めします。  
  
 アニメーションを削除する別の方法もあります。 次の手法を使って、<xref:System.Windows.Media.Animation.Storyboard> に属するアニメーションを削除できます。  
  
- イベント トリガーを使用して開始した <xref:System.Windows.Media.Animation.Storyboard> を削除するには、「[方法: ストーリーボードを削除する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms749412(v=vs.90))」を参照してください。  
  
- コードを使用して <xref:System.Windows.Media.Animation.Storyboard> を削除するには、<xref:System.Windows.Media.Animation.Storyboard.Remove%2A> メソッドを参照してください。  
  
 次の手法は、アニメーションの開始方法に関係なく使用できます。  
  
- 特定のプロパティからアニメーションを削除するには、<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> メソッドを使用します。 アニメーション化するプロパティを 1 番目のパラメーターとして指定し、`null` を 2 番目として指定します。 これにより、すべてのアニメーション クロックがプロパティから削除されます。  
  
 プロパティをアニメーション化するさまざまな方法について詳しくは、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」をご覧ください。  
  
### <a name="using-the-compose-handoffbehavior-consumes-system-resources"></a>HandoffBehavior を使うとシステム リソースが消費される  
 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose><xref:System.Windows.Media.Animation.HandoffBehavior> を使用してプロパティに <xref:System.Windows.Media.Animation.Storyboard>、<xref:System.Windows.Media.Animation.AnimationTimeline>、または <xref:System.Windows.Media.Animation.AnimationClock> を適用すると、そのプロパティに以前関連付けられていたすべての <xref:System.Windows.Media.Animation.Clock> オブジェクトがシステム リソースを消費し続けます。タイミング システムは、これらのクロックを自動的には削除しません。  
  
 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> を使って大量のクロックを適用するときのパフォーマンスの問題を回避するには、アニメーション化されたプロパティから、構成クロックを完了後に削除する必要があります。 クロックを削除する方法はいくつかあります。  
  
- プロパティからすべてのクロックを削除するには、アニメーション化されたオブジェクトの <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationClock%29> または <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> メソッドを使用します。 アニメーション化するプロパティを 1 番目のパラメーターとして指定し、`null` を 2 番目として指定します。 これにより、すべてのアニメーション クロックがプロパティから削除されます。  
  
- 特定の <xref:System.Windows.Media.Animation.AnimationClock> をクロックの一覧から削除するには、<xref:System.Windows.Media.Animation.AnimationClock> の <xref:System.Windows.Media.Animation.Clock.Controller%2A> プロパティを使用して <xref:System.Windows.Media.Animation.ClockController>を取得し、次に <xref:System.Windows.Media.Animation.ClockController.Remove%2A> の <xref:System.Windows.Media.Animation.ClockController> メソッドを呼び出します。 これは通常、クロックの <xref:System.Windows.Media.Animation.Clock.Completed> イベント ハンドラーで実行されます。 <xref:System.Windows.Media.Animation.ClockController> によって制御できるのはルート クロックのみであることに注意してください。子クロックの <xref:System.Windows.Media.Animation.Clock.Controller%2A> プロパティは `null` を返します。 クロックの有効期間が永久の場合は <xref:System.Windows.Media.Animation.Clock.Completed> イベントが呼び出されないことにも注意してください。  その場合は、ユーザーが <xref:System.Windows.Media.Animation.ClockController.Remove%2A> を呼び出すタイミングを決定する必要があります。  
  
 これは主に、有効期間が長いオブジェクトでのアニメーションの問題です。  オブジェクトがガベージ コレクションされる場合は、そのクロックも切断されて、ガベージ コレクションされます。  
  
 クロック オブジェクトについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
