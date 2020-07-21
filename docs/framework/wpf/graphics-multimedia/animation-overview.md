---
title: アニメーションの概要
description: Windows Presentation Foundation (WPF) のドラマチックな画面切り替え効果や、鮮やかな視覚的刺激で、魅力的なユーザーインターフェイスをさらに豪華にすることができます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], animations
- animations [WPF], overview
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
ms.openlocfilehash: d761be0c95fb8aa7eb39cb26b57979185226b8fb
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853862"
---
# <a name="animation-overview"></a>アニメーションの概要

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、魅力的なユーザー インターフェイスや説得力のあるドキュメントを作成するためのグラフィックスとレイアウト機能の強力なセットを提供します。 アニメーションを使うと、魅力的なユーザー インターフェイスをさらに豪華で使いやすいものにすることができます。 単に背景色をアニメーション化するか、アニメーション化された <xref:System.Windows.Media.Transform> を適用するだけで、ドラマチックな画面切り替え効果を演出したり、効果的な視覚的刺激を提供したりできます。

この概要では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションおよびタイミング システムを紹介します。 ここでは、ストーリーボードを使用した [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] オブジェクトのアニメーションに焦点を当てます。

<a name="introducinganimations"></a>

## <a name="introducing-animations"></a>アニメーションの概要

アニメーションは、それぞれが直前のイメージと少しずつ異なる一連のイメージをすばやく繰り返すことで生み出される錯覚です。 脳は、イメージのグループを 1 つの変化するシーンとして認識します。 映画では、この錯覚は 1 秒あたりに多数の写真またはフレームを記録するカメラを使って生み出されます。 フレームを映写機で再生すると、見る人には動く画像として映ります。

コンピューター上のアニメーションも同様です。 たとえば、四角形の描画をビューからフェードアウトするプログラムは次のように動作する可能性があります。

- プログラムがタイマーを作成します。

- 設定された間隔でプログラムがタイマーをチェックして経過時間を確認します。

- プログラムは、タイマーをチェックするたびに、経過時間に基づいて四角形の現在の不透明度値を計算します。

- プログラムは、新しい値で四角形を更新し、再描画します。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] より前は、Microsoft Windows 開発者が独自のタイミング システムを作成して管理するか、特殊なカスタム ライブラリを使用する必要がありました。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、マネージド コードと [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を通じて公開され、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] フレームワークと密接に統合されている効率的なタイミング システムが含まれています。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションを使うと、コントロールやその他のグラフィカル オブジェクトを簡単にアニメーション化できます。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、タイミング システムの管理と画面の効率的な再描画をすべてバックグラウンドで処理します。 効果を実現するしくみではなく、作り出す効果に重点を置くことのできるタイミング クラスが提供されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、クラスが継承できるアニメーションの基底クラスを公開しているため、独自のアニメーションを簡単に作成して、カスタマイズされたアニメーションを生成することもできます。 これらのカスタム アニメーションは、標準のアニメーション クラスのパフォーマンス上のメリットの多くを得ます。

<a name="thewpftimingsystem"></a>

## <a name="wpf-property-animation-system"></a>WPF プロパティ アニメーション システム

タイミング システムに関するいくつかの重要な概念を理解すると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションを簡単に使用できます。 最も重要な点は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、個々のプロパティにアニメーションを適用してオブジェクトをアニメーション化することです。 たとえば、フレームワーク要素を拡張するには、その <xref:System.Windows.FrameworkElement.Width%2A> プロパティと <xref:System.Windows.FrameworkElement.Height%2A> プロパティをアニメーション化します。 オブジェクトを徐々に見えなくなるようにするには、その <xref:System.Windows.UIElement.Opacity%2A> プロパティをアニメーション化します。

プロパティにアニメーション機能を持たせるには、次の 3 つの要件を満たす必要があります。

- 依存関係プロパティである必要があります。

- <xref:System.Windows.DependencyObject> を継承し、<xref:System.Windows.Media.Animation.IAnimatable> インターフェイスを実装するクラスに属している必要があります。

- 互換性のあるアニメーションの種類が使用可能である必要があります。 ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で提供されていない場合は、独自に作成することができます。 「[カスタム アニメーションの概要](custom-animations-overview.md)」をご覧ください。)

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、<xref:System.Windows.Media.Animation.IAnimatable> プロパティを持つ多数のオブジェクトが含まれています。 <xref:System.Windows.Controls.Button> や <xref:System.Windows.Controls.TabControl> などのコントロール、<xref:System.Windows.Controls.Panel> オブジェクトや <xref:System.Windows.Shapes.Shape> オブジェクトは、<xref:System.Windows.DependencyObject> を継承します。 これらのプロパティの大部分は依存関係プロパティです。

アニメーションは、スタイルやコントロール テンプレートなど、ほぼ任意の場所で使用できます。 アニメーションはビジュアルである必要はありません。このセクションで説明している条件を満たしていれば、ユーザー インターフェイスの一部ではないオブジェクトをアニメーション化できます。

<a name="storyboardwalkthrough"></a>

## <a name="example-make-an-element-fade-in-and-out-of-view"></a>例:要素の表示のフェードインとフェードアウトを行う

この例では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションを使用して依存関係プロパティの値をアニメーション化する方法を示します。 <xref:System.Double> 値を生成するアニメーションの一種である <xref:System.Windows.Media.Animation.DoubleAnimation> を使用して、<xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.UIElement.Opacity%2A> プロパティをアニメーション化します。 結果として、<xref:System.Windows.Shapes.Rectangle> の表示がフェードインおよびフェードアウトします。

この例の最初の部分では、<xref:System.Windows.Shapes.Rectangle> 要素を作成します。 その後のステップは、アニメーションを作成して四角形の <xref:System.Windows.UIElement.Opacity%2A> プロパティに適用する方法を示しています。

XAML で <xref:System.Windows.Controls.StackPanel> に <xref:System.Windows.Shapes.Rectangle> 要素を作成する方法を次に示します。

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]

コードで <xref:System.Windows.Controls.StackPanel> に <xref:System.Windows.Shapes.Rectangle> 要素を作成する方法を次に示します。

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]

<a name="opacity_animation_step1"></a>

### <a name="part-1-create-a-doubleanimation"></a>第 1 部:DoubleAnimation を作成する

要素の表示をフェードインおよびフェードアウトする 1 つの方法は、その <xref:System.Windows.UIElement.Opacity%2A> プロパティをアニメーション化することです。 <xref:System.Windows.UIElement.Opacity%2A> プロパティの型は <xref:System.Double> であるため、double 値を生成するアニメーションが必要です。 これに該当するアニメーションの 1 つが <xref:System.Windows.Media.Animation.DoubleAnimation> です。 <xref:System.Windows.Media.Animation.DoubleAnimation> は、2 つの double 値の間の遷移を作成します。 開始値を指定するには、その <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを設定します。 終了値を指定するには、その <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを設定します。

1. 不透明度の値 `1.0` を指定すると、オブジェクトが完全に不透明になり、不透明度の値 `0.0` を指定すると、完全に非表示になります。 アニメーションを `1.0` から `0.0` に遷移させるには、その <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> プロパティを `1.0` に、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> プロパティを `0.0` に設定します。 XAML で <xref:System.Windows.Media.Animation.DoubleAnimation> を作成する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]

    コードで <xref:System.Windows.Media.Animation.DoubleAnimation> を作成する方法を次に示します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]

2. 次に、<xref:System.Windows.Media.Animation.Timeline.Duration%2A> を指定する必要があります。 アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> は、開始値から到達値への移動にかかる時間を指定します。 XAML で <xref:System.Windows.Media.Animation.Timeline.Duration%2A> を 5 秒に設定する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]

    コードで <xref:System.Windows.Media.Animation.Timeline.Duration%2A> を 5 秒に設定する方法を次に示します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]

3. 前のコードでは、`1.0` から `0.0` に遷移するアニメーションを示しました。これにより、ターゲット要素が完全な不透明から完全な非表示に徐々に変化します。 要素が見えなくなった後にそれを再び見えるようにするには、アニメーションの <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティを `true` に設定します。 アニメーションを無限に繰り返すには、その <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A> に設定します。 XAML で <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティおよび <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを設定する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]

    コードで <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティおよび <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを設定する方法を次に示します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]

<a name="opacity_animation_step2"></a>

### <a name="part-2-create-a-storyboard"></a>第 2 部: ストーリーボードを作成する

オブジェクトにアニメーションを適用するには、<xref:System.Windows.Media.Animation.Storyboard> を作成し、<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 添付プロパティおよび <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 添付プロパティを使用して、アニメーション化するオブジェクトおよびプロパティを指定します。

1. <xref:System.Windows.Media.Animation.Storyboard> を作成し、アニメーションをその子として追加します。 XAML で <xref:System.Windows.Media.Animation.Storyboard> を作成する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]

    コードで <xref:System.Windows.Media.Animation.Storyboard> を作成するには、クラス レベルで <xref:System.Windows.Media.Animation.Storyboard> 変数を宣言します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]

    次に、<xref:System.Windows.Media.Animation.Storyboard> を初期化し、アニメーションをその子として追加します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]

2. <xref:System.Windows.Media.Animation.Storyboard> は、アニメーションを適用する場所を認識している必要があります。 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 添付プロパティを使用して、アニメーション化するオブジェクトを指定します。 XAML で <xref:System.Windows.Media.Animation.DoubleAnimation> のターゲット名を `MyRectangle` に設定する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]

    コードで <xref:System.Windows.Media.Animation.DoubleAnimation> のターゲット名を `MyRectangle` に設定する方法を次に示します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]

3. <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 添付プロパティを使用して、アニメーション化するプロパティを指定します。 XAML で <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.UIElement.Opacity%2A> プロパティをターゲットとするようにアニメーションを構成する方法を次に示します。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]

    コードで <xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.UIElement.Opacity%2A> プロパティをターゲットとするようにアニメーションを構成する方法を次に示します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]

<xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 構文とその他の例について詳しくは、「[ストーリーボードの概要](storyboards-overview.md)」をご覧ください。

<a name="opacity_animation_step3"></a>

### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>第 3 部 (XAML):ストーリーボードをトリガーに関連付ける

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で <xref:System.Windows.Media.Animation.Storyboard> を適用して開始する最も簡単な方法は、イベント トリガーを使用することです。 このセクションでは、XAML で <xref:System.Windows.Media.Animation.Storyboard> をトリガーに関連付ける方法を示します。

1. <xref:System.Windows.Media.Animation.BeginStoryboard> オブジェクトを作成し、それにストーリーボードを関連付けます。 <xref:System.Windows.Media.Animation.BeginStoryboard> は、<xref:System.Windows.Media.Animation.Storyboard> の一種であり、<xref:System.Windows.TriggerAction> を適用して開始します。

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]

2. <xref:System.Windows.EventTrigger> を作成し、その <xref:System.Windows.EventTrigger.Actions%2A> コレクションに <xref:System.Windows.Media.Animation.BeginStoryboard> を追加します。 <xref:System.Windows.EventTrigger> の <xref:System.Windows.EventTrigger.RoutedEvent%2A> プロパティを、<xref:System.Windows.Media.Animation.Storyboard> を開始するルーティング イベントに設定します。 (ルーティング イベントについて詳しくは、「[ルーティング イベントの概要](../advanced/routed-events-overview.md)」をご覧ください。)

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]

3. 四角形の <xref:System.Windows.FrameworkElement.Triggers%2A> コレクションに <xref:System.Windows.EventTrigger> を追加します。

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]

<a name="opacity_animation_step3code"></a>

### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>第 3 部 (コード):ストーリーボードをイベント ハンドラーに関連付ける

コードで <xref:System.Windows.Media.Animation.Storyboard> を適用して開始する最も簡単な方法は、イベント ハンドラーを使用することです。 このセクションでは、コードで <xref:System.Windows.Media.Animation.Storyboard> をイベント ハンドラーに関連付ける方法を示します。

1. 四角形の <xref:System.Windows.FrameworkElement.Loaded> イベントを登録します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]

2. イベント ハンドラーを宣言します。 イベント ハンドラーで、<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用してストーリーボードを適用します。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]

### <a name="complete-example"></a>コード例全体

ビューでフェードインおよびフェードアウトする四角形を XAML で作成する方法を次に示します。

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]

ビューでフェードインおよびフェードアウトする四角形をコードで作成する方法を次に示します。

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]

<a name="animationtypes"></a>

## <a name="animation-types"></a>アニメーションの種類

アニメーションはプロパティの値を生成するため、異なるプロパティの型ごとに異なるアニメーションの種類が存在します。 要素の <xref:System.Windows.FrameworkElement.Width%2A> プロパティなど、<xref:System.Double> を受け取るプロパティをアニメーション化するには、<xref:System.Double> 値を生成するアニメーションを使用します。 <xref:System.Windows.Point> を受け取るプロパティをアニメーション化するには、<xref:System.Windows.Point> 値を生成するアニメーションを使用します。他も同様です。 プロパティの型は複数あるため、<xref:System.Windows.Media.Animation> 名前空間には複数のアニメーション クラスがあります。 幸いにも、それらは厳密な名前付け規則に従っているため、簡単に区別できます。

- \<*Type*>Animation

  これらは "From/To/By" または "基本" アニメーションと呼ばれ、開始値と宛先値の間をアニメーション化するか、開始値にオフセット値を加算することでアニメーション化します。

  - 開始値を指定するには、アニメーションの From プロパティを設定します。

  - 終了値を指定するには、アニメーションの To プロパティを設定します。

  - オフセット値を指定するには、アニメーションの By プロパティを設定します。

  これらのアニメーションは最も簡単に使用できるため、この概要の例ではこれらを使っています。 From/To/By アニメーションについては「From/To/By アニメーションの概要」で詳しく説明しています。

- \<*Type*>AnimationUsingKeyFrames

  キー フレーム アニメーションは、任意の数のターゲット値を指定でき、補間方法も制御できるため、From/To/By アニメーションよりも強力です。 一部の型は、キー フレーム アニメーションでのみアニメーション化できます。 キー フレーム アニメーションについては 「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」で詳しく説明しています。

- \<*Type*>AnimationUsingPath

  パス アニメーションでは、アニメーション値を生成するためにジオメトリック パスを使用できます。

- \<*Type*>AnimationBase

  抽象クラスを実装すると、\<*Type*> 値がアニメーション化されます。 このクラスは、\<*Type*>Animation と \<*Type*>AnimationUsingKeyFrames のクラスの基底クラスとして機能します。 これらのクラスは、ユーザー独自のカスタム アニメーションを作成する場合にのみ直接扱う必要があります。 それ以外の場合は、\<*Type*>Animation または KeyFrame\<*Type*>Animation を使います。

ほとんどの場合、<xref:System.Windows.Media.Animation.DoubleAnimation> や <xref:System.Windows.Media.Animation.ColorAnimation> などの \<*Type*>Animation クラスを使用します。

次の表は、いくつかの一般的なアニメーションの種類と、そこで使われるいくつかのプロパティを示しています。

|プロパティの型|対応する基本 (From/To/By) アニメーション|対応するキー フレーム アニメーション|対応するパス アニメーション|使用例|
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|None|<xref:System.Windows.Media.SolidColorBrush> または <xref:System.Windows.Media.GradientStop> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> をアニメーション化します。|
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|<xref:System.Windows.Controls.DockPanel> の <xref:System.Windows.FrameworkElement.Width%2A>、または <xref:System.Windows.Controls.Button> の <xref:System.Windows.FrameworkElement.Height%2A> をアニメーション化します。|
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|<xref:System.Windows.Media.EllipseGeometry>の <xref:System.Windows.Media.EllipseGeometry.Center%2A> 位置をアニメーション化します。|
|<xref:System.String>|None|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|None|<xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Text%2A>、または <xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.ContentControl.Content%2A> をアニメーション化します。|

<a name="animationsaretimelines"></a>

### <a name="animations-are-timelines"></a>アニメーションはタイムラインである

すべての種類のアニメーションは <xref:System.Windows.Media.Animation.Timeline> クラスを継承するため、すべてのアニメーションは特殊な種類のタイムラインです。 <xref:System.Windows.Media.Animation.Timeline> は時間のセグメントを定義します。 タイムラインの "*タイミング動作*" (その <xref:System.Windows.Media.Animation.Timeline.Duration%2A>、繰り返す回数、進行速度) を指定できます。

アニメーションは <xref:System.Windows.Media.Animation.Timeline> であるため、時間のセグメントも表します。 また、アニメーションは、指定された時間のセグメント (つまり <xref:System.Windows.Media.Animation.Timeline.Duration%2A>) の経過に伴って進行しながら、出力値を計算します。 アニメーションは、進行時、つまり "再生" 時に、関連付けられているプロパティを更新します。

よく使用される 3 つのタイミング プロパティは、<xref:System.Windows.Media.Animation.Timeline.Duration%2A>、<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>、<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> です。

#### <a name="the-duration-property"></a>Duration プロパティ

既に述べたように、タイムラインは時間のセグメントを表します。 そのセグメントの長さは、タイムラインの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> によって決まります。これは通常、<xref:System.Windows.Duration.TimeSpan%2A> 値を使用して指定されます。 タイムラインがその期間の最後に達すると、イテレーションが完了します。

アニメーションは、その <xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティを使用して、現在の値を割り出します。 アニメーションの <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 値を指定しなかった場合は、既定値の 1 秒が使用されます。

次の構文は、<xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティの [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 属性構文の簡略版を示しています。

"*時間*" `:` "*分*" `:` "*秒*"

次の表に、<xref:System.Windows.Duration> 設定とその結果の値をいくつか示します。

|設定|結果の値|
|-------------|---------------------|
|0:0:5.5|5.5 秒。|
|0:30:5.5|30 分 5.5 秒。|
|1:30:5.5|1 時間 30 分 5.5 秒。|

コードで <xref:System.Windows.Duration> を指定する方法の 1 つは、<xref:System.TimeSpan.FromSeconds%2A> メソッドを使用して <xref:System.TimeSpan> を作成し、その <xref:System.TimeSpan> を使用して新しい <xref:System.Windows.Duration> 構造体を宣言することです。

<xref:System.Windows.Duration> 値と [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 構文の詳細については、<xref:System.Windows.Duration> 構造体に関する記事をご覧ください。

#### <a name="autoreverse"></a>AutoReverse

<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティは、タイムラインが <xref:System.Windows.Media.Animation.Timeline.Duration%2A> の終わりに達した後に逆再生するかどうかを指定します。 このアニメーション プロパティを `true` に設定すると、アニメーションは <xref:System.Windows.Media.Animation.Timeline.Duration%2A> の終わりに達した後で反転し、終了値から開始値に向かって再生されます。 既定では、このプロパティは `false` です。

#### <a name="repeatbehavior"></a>RepeatBehavior

<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティは、タイムラインの再生回数を指定します。 既定では、タイムラインの反復回数は `1.0` です。これは、再生が 1 回だけで、繰り返されないことを意味します。

これらのプロパティとその他について詳しくは、「[タイミング動作の概要](timing-behaviors-overview.md)」をご覧ください。

<a name="applyanimationstoproperty"></a>

## <a name="applying-an-animation-to-a-property"></a>プロパティにアニメーションを適用する

これまでのセクションでは、さまざまな種類のアニメーションとそれらのタイミング プロパティについて説明しました。 このセクションでは、アニメーション化するプロパティにアニメーションを適用する方法を示します。 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトは、アニメーションをプロパティに適用する方法の 1 つを提供します。 <xref:System.Windows.Media.Animation.Storyboard> は "*コンテナー タイムライン*" であり、その中に含まれているアニメーションのターゲット情報を提供します。

### <a name="targeting-objects-and-properties"></a>ターゲットとするオブジェクトとプロパティ

<xref:System.Windows.Media.Animation.Storyboard> クラスでは、<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 添付プロパティおよび <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 添付プロパティが提供されます。 アニメーションでこれらのプロパティを設定して、アニメーション化する内容をアニメーションに指示します。 ただし、アニメーションがオブジェクトをターゲット指定するには、通常その前にオブジェクの名前を指定する必要があります。

<xref:System.Windows.FrameworkElement> への名前の割り当ては、<xref:System.Windows.Freezable> オブジェクトへの名前の割り当てとは異なります。 ほとんどのコントロールとパネルはフレームワーク要素ですが、ブラシ、変換、ジオメトリなどのほとんどの純粋なグラフィカル オブジェクトは Freezable オブジェクトです。 型が <xref:System.Windows.FrameworkElement> と <xref:System.Windows.Freezable> のどちらであるかが不明な場合は、そのリファレンス ドキュメントの**継承階層**のセクションを参照してください。

- <xref:System.Windows.FrameworkElement> をアニメーションのターゲットにするには、<xref:System.Windows.FrameworkElement.Name%2A> プロパティを設定して名前を付けます。 コードでは、<xref:System.Windows.FrameworkElement.RegisterName%2A> メソッドを使用して、要素名をその所属ページに登録する必要もあります。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で <xref:System.Windows.Freezable> オブジェクトをアニメーションのターゲットにするには、[x:Name Directive](../../../desktop-wpf/xaml-services/xname-directive.md) を使用して名前を割り当てます。 コードでは、<xref:System.Windows.FrameworkElement.RegisterName%2A> メソッドを使用して、オブジェクトをその所属ページに登録するだけです。

以降のセクションでは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] およびコードで要素に名前を付ける例を示します。 名前付けとターゲット設定について詳しくは、「[ストーリーボードの概要](storyboards-overview.md)」をご覧ください。

### <a name="applying-and-starting-storyboards"></a>ストーリーボードの適用と開始

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でストーリーボードを開始するには、<xref:System.Windows.EventTrigger> に関連付けます。 <xref:System.Windows.EventTrigger> は、指定したイベントが発生したときに実行するアクションを記述するオブジェクトです。 これらのアクションのいずれかを、ストーリーボードを開始するために使用する <xref:System.Windows.Media.Animation.BeginStoryboard> アクションにすることができます。 イベント トリガーは、アプリケーションが特定のイベントに応答する方法を指定できるようにするため、概念はイベント ハンドラーに似ています。 イベント ハンドラーとは異なり、イベント トリガーは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で的確に記述でき、他のコードは必要ありません。

コードで <xref:System.Windows.Media.Animation.Storyboard> を開始するには、<xref:System.Windows.EventTrigger> を使用するか、<xref:System.Windows.Media.Animation.Storyboard> クラスの <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用します。

<a name="controllingstoryboards"></a>

## <a name="interactively-control-a-storyboard"></a>ストーリーボードを対話的に制御する

前の例では、イベントの発生時に <xref:System.Windows.Media.Animation.Storyboard> を開始する方法を示しました。 開始後に <xref:System.Windows.Media.Animation.Storyboard> を対話形式で制御することもできます。つまり、<xref:System.Windows.Media.Animation.Storyboard> を一時停止、再開、停止、その期間の終わりまで前進、シーク、削除できます。 <xref:System.Windows.Media.Animation.Storyboard> を対話的に制御する方法の詳細と例については、「[ストーリーボードの概要](storyboards-overview.md)」をご覧ください。

<a name="fillbehaviorsection"></a>

## <a name="what-happens-after-an-animation-ends"></a>アニメーションの終了後の動作

<xref:System.Windows.Media.Animation.FillBehavior> プロパティは、タイムラインの終了時の動作を指定します。 既定では、タイムラインは終了時に <xref:System.Windows.Media.Animation.ClockState.Filling> を開始します。 <xref:System.Windows.Media.Animation.ClockState.Filling> であるアニメーションは、最終的な出力値を保持しています。

前の例の <xref:System.Windows.Media.Animation.DoubleAnimation> は、その <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティが <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A> に設定されているため、終了しません。 次の例では、類似のアニメーションを使って四角形をアニメーション化します。 前の例とは異なり、このアニメーションの <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティおよび <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティは既定値のままです。 したがって、アニメーションは 5 秒間で 1 から 0 まで進行し、停止します。

[!code-xaml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]

[!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
[!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]

<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> が既定値の <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd> から変更されなかったため、アニメーションは終了時に最終値 0 を保持します。 したがって、四角形の <xref:System.Windows.UIElement.Opacity%2A> は、アニメーションの終了後も 0 のままです。 四角形の <xref:System.Windows.UIElement.Opacity%2A> を別の値に設定した場合、アニメーションは依然として <xref:System.Windows.UIElement.Opacity%2A> プロパティに影響を与えているため、コードの効果はないように見えます。

コードでアニメーション化されたプロパティを再び制御する方法の 1 つは、<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用し、<xref:System.Windows.Media.Animation.AnimationTimeline> パラメーターに null 値を指定することです。 詳細と例については、「[ストーリーボードを使用してアニメーション化した後にプロパティを設定する](how-to-set-a-property-after-animating-it-with-a-storyboard.md)」をご覧ください。

<xref:System.Windows.Media.Animation.ClockState.Active> または <xref:System.Windows.Media.Animation.ClockState.Filling> のアニメーションを持つプロパティ値を設定しても効果がないように見えますが、プロパティ値は変更されるということに注意してください。 詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。

<a name="databindingAndAnimatingAnimationsSection"></a>

## <a name="data-binding-and-animating-animations"></a>アニメーションのデータ バインディングとアニメーション化

ほとんどのアニメーション プロパティは、データ バインドまたはアニメーション化できます。たとえば、<xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティをアニメーション化できます。 ただし、タイミング システムの動作が原因で、データ バインドまたはアニメーション化されたアニメーションは他のデータ バインドまたはアニメーション化されたオブジェクトと同様には動作しません。 その動作を理解するには、アニメーションをプロパティに適用する意味を理解することが役立ちます。

四角形の <xref:System.Windows.UIElement.Opacity%2A> をアニメーション化する方法を示した前のセクションの例を参照してください。 前の例の四角形が読み込まれると、そのイベント トリガーよって <xref:System.Windows.Media.Animation.Storyboard> が適用されます。 タイミング システムは、<xref:System.Windows.Media.Animation.Storyboard> とそのアニメーションのコピーを作成します。 これらのコピーは固定され (読み取り専用になります)、それらから <xref:System.Windows.Media.Animation.Clock> オブジェクトが作成されます。 これらのクロックは、ターゲット プロパティをアニメーション化する実際の作業を実行します。

タイミング システムは <xref:System.Windows.Media.Animation.DoubleAnimation> のクロックを作成し、それを <xref:System.Windows.Media.Animation.DoubleAnimation> の <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> および <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> によって指定されたオブジェクトおよびプロパティに適用します。 この場合、タイミング システムは "MyRectangle" という名前のオブジェクトの <xref:System.Windows.UIElement.Opacity%2A> プロパティにクロックを適用します。

クロックは <xref:System.Windows.Media.Animation.Storyboard> に対しても作成されますが、このクロックはどのプロパティにも適用されません。 その目的は、<xref:System.Windows.Media.Animation.DoubleAnimation> に対して作成されるクロックである子クロックを制御することです。

アニメーションがデータ バインディングまたはアニメーションの変更を反映するためには、そのクロックを再生成する必要があります。 クロックは、自動的には再生成されません。 アニメーションに変更を反映させるには、<xref:System.Windows.Media.Animation.BeginStoryboard> または <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用して、そのストーリーボードを再適用します。 これらのメソッドのいずれかを使うと、アニメーションが再起動されます。 コードでは、<xref:System.Windows.Media.Animation.Storyboard.Seek%2A> メソッドを使用して、ストーリーボードを前の位置に戻すことができます。

データ バインドされたアニメーションの例については、「[キー スプライン アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/KeySplineAnimations)」をご覧ください。 アニメーションとタイミング システムのしくみについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。

<a name="otherWaysToAnimateSection"></a>

## <a name="other-ways-to-animate"></a>その他のアニメーション化方法

この概要の例では、ストーリーボードを使ってアニメーション化する方法を示します。 コードを使う場合は、その他のいくつかの方法でアニメーション化できます。 詳しくは、「[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)」をご覧ください。

<a name="animation_samples"></a>

## <a name="animation-samples"></a>アニメーションのサンプル

以下のサンプルは、アプリケーションへのアニメーションの追加を開始するのに役立つ場合があります。

- [アニメーションのターゲット値 (From、To、および By) のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/TargetValues)

  さまざまな From/To/By 設定を示します。

- [アニメーションのタイミング動作のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationTiming)

  アニメーションのタイミング動作を制御するさまざまな方法を示します。 このサンプルは、アニメーションの宛先値をデータ バインドする方法も示しています。

<a name="related_topics"></a>

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)|タイミング システムが <xref:System.Windows.Media.Animation.Timeline> クラスおよび <xref:System.Windows.Media.Animation.Clock> クラスを使用してアニメーションを作成する方法について説明します。|
|[アニメーションのヒントとテクニック](animation-tips-and-tricks.md)|パフォーマンスなど、アニメーションでの問題を解決するための役に立つヒントの一覧を示します。|
|[カスタム アニメーションの概要](custom-animations-overview.md)|アニメーション システムをキー フレーム、アニメーション クラス、またはフレームごとのコールバックで拡張する方法について説明します。|
|[From/To/By アニメーションの概要](from-to-by-animations-overview.md)|2 つの値の間を遷移するアニメーションを作成する方法について説明します。|
|[キー フレーム アニメーションの概要](key-frame-animations-overview.md)|補間メソッドを制御する機能など、複数のターゲット値を持つアニメーションを作成する方法について説明します。|
|[イージング関数](easing-functions.md)|数式をアニメーションに適用してバウンスなどの現実的な動作を実現する方法について説明します。|
|[パス アニメーションの概要](path-animations-overview.md)|複雑なパスに沿ってオブジェクトを移動または回転する方法について説明します。|
|[プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)|ストーリーボード、ローカル アニメーション、クロック、フレームごとのアニメーションを使ったプロパティのアニメーションについて説明します。|
|[ストーリーボードの概要](storyboards-overview.md)|複数のタイムラインを持つストーリーボードを使って複雑なアニメーションを作成する方法について説明します。|
|[タイミング動作の概要](timing-behaviors-overview.md)|アニメーションで使用される <xref:System.Windows.Media.Animation.Timeline> の種類とプロパティについて説明します。|
|[タイミング イベントの概要](timing-events-overview.md)|開始、一時停止、再開、スキップ、停止など、タイムラインのポイントでコードを実行するために <xref:System.Windows.Media.Animation.Timeline> オブジェクトおよび <xref:System.Windows.Media.Animation.Clock> オブジェクトで使用できるイベントについて説明します。|
|[方法トピック](animation-and-timing-how-to-topics.md)|アプリケーションでアニメーションとタイムラインを使うためのコード例を示します。|
|[クロックに関する「方法」トピック](clocks-how-to-topics.md)|アプリケーションで <xref:System.Windows.Media.Animation.Clock> オブジェクトを使うためのコード例を示します。|
|[キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)|アプリケーションでキー フレーム アニメーションを使うためのコード例を示します。|
|[パス アニメーションに関する「方法」トピック](path-animation-how-to-topics.md)|アプリケーションでパス アニメーションを使うためのコード例を示します。|

<a name="reference"></a>

## <a name="reference"></a>関連項目

- <xref:System.Windows.Media.Animation.Timeline>

- <xref:System.Windows.Media.Animation.Storyboard>

- <xref:System.Windows.Media.Animation.BeginStoryboard>

- <xref:System.Windows.Media.Animation.Clock>
