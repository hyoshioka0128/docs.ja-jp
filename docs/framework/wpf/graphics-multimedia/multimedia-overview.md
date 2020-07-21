---
title: マルチメディアの概要
ms.date: 03/30/2017
helpviewer_keywords:
- multimedia [WPF]
- media [WPF]
ms.assetid: feb25b15-d741-4ac3-818f-1b19f63a3562
ms.openlocfilehash: d4abf4d9fd324ffbf2737dc686c02e50ca1a8a5a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181882"
---
# <a name="multimedia-overview"></a>マルチメディアの概要
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のマルチメディア機能を使用してアプリケーションにオーディオとビデオを統合することで、ユーザー エクスペリエンスを向上させることできます。 このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のマルチメディア機能の概要を説明します。  

<a name="mediaapi"></a>
## <a name="media-api"></a>メディア API  
 <xref:System.Windows.Controls.MediaElement> および <xref:System.Windows.Media.MediaPlayer> クラスは、オーディオまたはビデオのコンテンツを表示するために使用されます。 これらのクラスは、対話式またはクロックで制御できます。 これらのクラスは、Microsoft Windows Media Player 10 コントロールでメディアの再生に使用できます。 どちらのクラスを使用するかは、シナリオによって決まります。  
  
 <xref:System.Windows.Controls.MediaElement> は、[レイアウト](../advanced/layout.md)でサポートされている <xref:System.Windows.UIElement> であり、多くのコントロールのコンテンツとして利用できます。 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] でコードとして使用することもできます。 それに対し、<xref:System.Windows.Media.MediaPlayer> は <xref:System.Windows.Media.Drawing> オブジェクト向けに設計されていて、レイアウトではサポートされていません。 <xref:System.Windows.Media.MediaPlayer> を使用して読み込まれたメディアは、<xref:System.Windows.Media.VideoDrawing> を使用するか、<xref:System.Windows.Media.DrawingContext> を直接操作することでのみ表示できます。 <xref:System.Windows.Media.MediaPlayer> は XAML では使用できません。  
  
 描画オブジェクトと描画コンテキストの詳細については、「[描画オブジェクトの概要](drawing-objects-overview.md)」を参照してください。  
  
> [!NOTE]
> アプリケーションでメディアを配布するときに、プロジェクト リソースとしてメディア ファイルを使うことはできません。 プロジェクト ファイルで、メディアの種類を `Content` に設定し、`CopyToOutputDirectory` を `PreserveNewest` または `Always` に設定する必要があります。  
  
<a name="mediaplaybackmodes"></a>
## <a name="media-playback-modes"></a>メディア再生モード  
  
> [!NOTE]
> <xref:System.Windows.Controls.MediaElement> と <xref:System.Windows.Media.MediaPlayer> のどちらにも同様のメンバーが含まれています。 このセクションのリンクは、<xref:System.Windows.Controls.MediaElement> クラスのメンバーを示しています。 特に明記されていない限り、<xref:System.Windows.Controls.MediaElement> クラス内でリンクされているメンバーは、<xref:System.Windows.Media.MediaPlayer> クラスにも存在します。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でのメディアの再生を理解するには、メディアを再生できる複数のモードを理解しておく必要があります。 <xref:System.Windows.Controls.MediaElement> と <xref:System.Windows.Media.MediaPlayer> はどちらも、Independent モードと Clock モードの 2 つの異なるメディア モードで使用できます。 メディア モードは、<xref:System.Windows.Controls.MediaElement.Clock%2A> プロパティによって決まります。 <xref:System.Windows.Controls.MediaElement.Clock%2A> が `null` の場合、メディア オブジェクトは Independent モードになります。 <xref:System.Windows.Controls.MediaElement.Clock%2A> が null 以外の場合、メディア オブジェクトは Clock モードになります。 既定では、メディア オブジェクトは Independent モードになっています。  
  
### <a name="independent-mode"></a>Independent モード  
 Independent モードでは、メディア コンテンツがメディアの再生を行います。 Independent モードには、次のオプションがあります。  
  
- メディアの <xref:System.Uri> は直接指定できます。  
  
- メディアの再生を直接制御できます。  
  
- メディアの <xref:System.Windows.Controls.MediaElement.Position%2A> および <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> プロパティは変更できます。  
  
 メディアを読み込むには、<xref:System.Windows.Controls.MediaElement> オブジェクトの <xref:System.Windows.Controls.MediaElement.Source%2A> プロパティを設定するか、<xref:System.Windows.Media.MediaPlayer> オブジェクトの <xref:System.Windows.Media.MediaPlayer.Open%2A> メソッドを呼び出します。  
  
 Independent モードでメディアの再生を制御するには、メディア オブジェクトの制御メソッドを使用できます。 使用できる制御メソッドは、<xref:System.Windows.Controls.MediaElement.Play%2A>、<xref:System.Windows.Controls.MediaElement.Pause%2A>、<xref:System.Windows.Controls.MediaElement.Close%2A>、<xref:System.Windows.Controls.MediaElement.Stop%2A> です。 <xref:System.Windows.Controls.MediaElement> の場合、これらのメソッドを使用した対話型コントロールは、<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> が <xref:System.Windows.Controls.MediaState.Manual> に設定されている場合にのみ使用できます。 メディア オブジェクトが Clock モードの場合、これらのメソッドは使用できません。  
  
 Independent モードの例については、「[MediaElement (再生、一時停止、停止、ボリューム、および速度) を制御する](how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)」を参照してください。  
  
### <a name="clock-mode"></a>Clock モード  
 Clock モードでは、<xref:System.Windows.Media.MediaTimeline> によってメディアが再生されます。 Clock モードには次の特徴があります。  
  
- メディアの <xref:System.Uri> は、<xref:System.Windows.Media.MediaTimeline> を使用して間接的に設定されます。  
  
- メディアの再生は、クロックによって制御できます。 メディア オブジェクトの制御メソッドは使用できません。  
  
- メディアを読み込むには、<xref:System.Windows.Media.MediaTimeline> オブジェクトの <xref:System.Windows.Media.MediaTimeline.Source%2A> プロパティを設定し、タイムラインからクロックを作成し、メディア オブジェクトにクロックを割り当てます。 <xref:System.Windows.Media.Animation.Storyboard> 内の <xref:System.Windows.Media.MediaTimeline> が <xref:System.Windows.Controls.MediaElement> を対象としている場合も、この方法でメディアが読み込まれます。  
  
 Clock モードでメディアの再生を制御するには、<xref:System.Windows.Media.Animation.ClockController> 制御メソッドを使用する必要があります。 <xref:System.Windows.Media.Animation.ClockController> は <xref:System.Windows.Media.MediaClock> の <xref:System.Windows.Media.Animation.ClockController> プロパティから取得されます。 Clock モードで <xref:System.Windows.Controls.MediaElement> または <xref:System.Windows.Media.MediaPlayer> のいずれかのオブジェクトの制御メソッドを使用しようとすると、<xref:System.InvalidOperationException> がスローされます。  
  
 クロックとタイムラインの詳細については、「[アニメーションの概要](animation-overview.md)」を参照してください。  
  
 Clock モードの例については、「[ストーリーボードを使用して MediaElement を制御する](how-to-control-a-mediaelement-by-using-a-storyboard.md)」を参照してください。  
  
<a name="mediaelement"></a>
## <a name="mediaelement-class"></a>MediaElement クラス  
 アプリケーションへのメディアの追加は簡単であり、<xref:System.Windows.Controls.MediaElement> コントロールをアプリケーションの[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] に追加し、含めるメディアに <xref:System.Uri> を指定するだけです。 Microsoft Windows Media Player 10 でサポートされているメディアの種類はすべて、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でサポートされます。 次の例は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] での <xref:System.Windows.Controls.MediaElement> の簡単な使用法を示しています。  
  
 [!code-xaml[MediaElement_snip#SimpleMediaElementUsageWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaElement_snip/CSharp/SimpleUsage.xaml#simplemediaelementusagewholepage)]  
  
 このサンプルでは、メディアは、読み込まれるとすぐに自動的に再生されます。 メディアの再生が終了すると、メディアが閉じられ、すべてのメディア リソースが解放されます (ビデオ メモリを含みます)。 これは <xref:System.Windows.Controls.MediaElement> オブジェクトの既定の動作であり、<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> および <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> プロパティによって制御されます。  
  
### <a name="controlling-a-mediaelement"></a>MediaElement の制御  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> および <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> プロパティでは、<xref:System.Windows.FrameworkElement.IsLoaded%2A> がそれぞれ `true` または `false` である場合の <xref:System.Windows.Controls.MediaElement> の動作を制御します。 <xref:System.Windows.Controls.MediaState> では、メディアの再生動作に影響を与えるようにプロパティが設定されます。 たとえば、既定の <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> は <xref:System.Windows.Controls.MediaState.Play>、既定の <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> は <xref:System.Windows.Controls.MediaState.Close> です。 つまり、<xref:System.Windows.Controls.MediaElement> が読み込まれ、プリロールが完了するとすぐに、メディアの再生が開始されます。 再生が完了すると、メディアが閉じられ、すべてのメディア リソースが解放されます。  
  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> および <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> プロパティだけが、メディアの再生を制御する方法ではありません。 Clock モードでは、クロックが <xref:System.Windows.Controls.MediaElement> を制御でき、また、<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> が <xref:System.Windows.Controls.MediaState.Manual> の場合は対話型制御メソッドが制御を行います。 この制御の競合は、<xref:System.Windows.Controls.MediaElement> が次の優先順位を評価することによって処理されます。  
  
1. <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>。 メディアがアンロードされているときに有効です。 これにより、<xref:System.Windows.Media.MediaClock> が <xref:System.Windows.Controls.MediaElement> に関連付けられている場合でも、既定ですべてのメディア リソースが解放されます。  
  
2. <xref:System.Windows.Media.MediaClock>。 メディアに<xref:System.Windows.Controls.MediaElement.Clock%2A>があるときに有効です。 メディアがアンロードされると、<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> が <xref:System.Windows.Controls.MediaState.Manual> である限り、<xref:System.Windows.Media.MediaClock> が有効になります。 Clock モードは常に、<xref:System.Windows.Controls.MediaElement> の読み込み動作より優先されます。  
  
3. <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>。 メディアが読み込まれているときに有効です。  
  
4. 対話型の制御メソッド。 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> が <xref:System.Windows.Controls.MediaState.Manual> の場合に有効です。 使用できる制御メソッドは、<xref:System.Windows.Controls.MediaElement.Play%2A>、<xref:System.Windows.Controls.MediaElement.Pause%2A>、<xref:System.Windows.Controls.MediaElement.Close%2A>、<xref:System.Windows.Controls.MediaElement.Stop%2A> です。  
  
### <a name="displaying-a-mediaelement"></a>MediaElement の表示  
 <xref:System.Windows.Controls.MediaElement> を表示するには、表示するコンテンツが必要です。また、コンテンツが読み込まれるまで、<xref:System.Windows.FrameworkElement.ActualWidth%2A> および <xref:System.Windows.FrameworkElement.ActualHeight%2A> プロパティは 0 に設定されます。 オーディオのみのコンテンツでは、これらのプロパティは常に 0 です。 ビデオ コンテンツの場合、<xref:System.Windows.Controls.MediaElement.MediaOpened> イベントが発生すると、<xref:System.Windows.FrameworkElement.ActualWidth%2A> と <xref:System.Windows.FrameworkElement.ActualHeight%2A> が、読み込まれたメディアのサイズを報告します。 つまり、メディアが読み込まれるまでは、<xref:System.Windows.FrameworkElement.Width%2A> または <xref:System.Windows.FrameworkElement.Height%2A> プロパティが設定されていない限り、<xref:System.Windows.Controls.MediaElement> によって [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 内の物理的な領域は占有されることはありません。  
  
 <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> の両方のプロパティを設定すると、メディアが拡張され、<xref:System.Windows.Controls.MediaElement> 用に用意された領域がいっぱいになります。 メディアの元の縦横比を維持するには、<xref:System.Windows.FrameworkElement.Width%2A> または <xref:System.Windows.FrameworkElement.Height%2A> のいずれか一方 (両方ではなく) のプロパティを設定します。 <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> の両方のプロパティを設定すると、メディアが固定した要素サイズで表示されることになり、これは望ましくない場合があります。  
  
 要素のサイズが固定されることを避けるために、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、メディアをプリロールすることができます。 これを行うには、<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> を <xref:System.Windows.Controls.MediaState.Play> または <xref:System.Windows.Controls.MediaState.Pause> に設定します。 <xref:System.Windows.Controls.MediaState.Pause> 状態では、メディアがプリロールされ、最初のフレームが表示されます。 <xref:System.Windows.Controls.MediaState.Play> 状態では、メディアがプリロールされ、再生が開始されます。  
  
<a name="mediaplayer"></a>
## <a name="mediaplayer-class"></a>MediaPlayer クラス  
 <xref:System.Windows.Controls.MediaElement> クラスがフレームワーク要素の場合、<xref:System.Windows.Media.MediaPlayer> クラスは <xref:System.Windows.Media.Drawing> オブジェクトで使用されるように設計されています。 描画オブジェクトは、パフォーマンス上の利点を得るためにフレームワーク レベルの機能を犠牲にできる場合、または <xref:System.Windows.Freezable> の機能が必要な場合に使用されます。 <xref:System.Windows.Media.MediaPlayer> を使用すると、アプリケーションにメディア コンテンツを提供すると同時に、これらの機能を利用できます。 <xref:System.Windows.Controls.MediaElement> と同様に、<xref:System.Windows.Media.MediaPlayer> は Independent または Clock モードで使用できますが、<xref:System.Windows.Controls.MediaElement> オブジェクトのアンロード状態と読み込み状態はありません。 これにより、<xref:System.Windows.Media.MediaPlayer> の再生制御の複雑さが軽減されます。  
  
### <a name="controlling-mediaplayer"></a>Media Player の制御  
 <xref:System.Windows.Media.MediaPlayer> はステートレスであるため、メディアの再生を制御する方法は 2 つのみです。  
  
1. 対話型の制御メソッド。 Independent モード (`null`<xref:System.Windows.Media.MediaPlayer.Clock%2A> プロパティ) のときに有効です。  
  
2. <xref:System.Windows.Media.MediaClock>。 メディアに<xref:System.Windows.Media.MediaPlayer.Clock%2A>があるときに有効です。  
  
### <a name="displaying-a-mediaplayer"></a>MediaPlayer の表示  
 技術的には、<xref:System.Windows.Media.MediaPlayer> には物理表現がないため、表示することはできません。 ただし、これを使用すると、<xref:System.Windows.Media.VideoDrawing> クラスを使用して <xref:System.Windows.Media.Drawing> でメディアを表示できます。 次の例は、<xref:System.Windows.Media.VideoDrawing> を使用してメディアを表示する方法を示しています。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 <xref:System.Windows.Media.Drawing> オブジェクトの詳細については、「[Drawing オブジェクトの概要](drawing-objects-overview.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingGroup>
- [レイアウト](../advanced/layout.md)
- [方法トピック](audio-and-video-how-to-topics.md)
