---
title: 'パフォーマンスの最適化: 他の推奨事項'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Terminal Services rendering [WPF]
- opacity [WPF]
- hit-test objects [WPF]
- ScrollBarVisibility enumeration [WPF]
- brushes [WPF], performance
ms.assetid: d028cc65-7e97-4a4f-9859-929734eaf40d
ms.openlocfilehash: 727331adb41251460209f157d1804ff455bcf473
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186302"
---
# <a name="optimizing-performance-other-recommendations"></a>パフォーマンスの最適化: 他の推奨事項
<a name="introduction"></a> このトピックでは、「[WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)」セクションのトピックで説明されている推奨事項を補足するパフォーマンスに関する推奨事項について取り上げます。  
  
 このトピックは、次のセクションで構成されています。  
  
- [ブラシの Opacity と要素の Opacity](#Opacity)  
  
- [オブジェクトへの移動](#Navigation_Objects)  
  
- [大きな 3D サーフェイスのヒット テスト](#Hit_Testing)  
  
- [CompositionTarget.Rendering イベント](#CompositionTarget_Rendering_Event)  
  
- [ScrollBarVisibility=Auto は使用しない](#Avoid_Using_ScrollBarVisibility)  
  
- [Font Cache サービスの構成による起動時間の短縮](#FontCache)  
  
<a name="Opacity"></a>
## <a name="opacity-on-brushes-versus-opacity-on-elements"></a>ブラシの Opacity と要素の Opacity  
 <xref:System.Windows.Media.Brush> を使用して要素の <xref:System.Windows.Shapes.Shape.Fill%2A> や <xref:System.Windows.Shapes.Shape.Stroke%2A> を設定するときには、要素の <xref:System.Windows.UIElement.Opacity%2A> プロパティを設定するのではなく、<xref:System.Windows.Media.Brush.Opacity%2A?displayProperty=nameWithType> の値を設定することをお勧めします。 要素の <xref:System.Windows.UIElement.Opacity%2A> プロパティを変更すると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって一時的なサーフェイスが作成される可能性があります。  
  
<a name="Navigation_Objects"></a>
## <a name="navigation-to-object"></a>オブジェクトへの移動  
 <xref:System.Windows.Navigation.NavigationWindow> オブジェクトは<xref:System.Windows.Window> から派生し、コンテンツ ナビゲーションのサポートで Window を拡張します。この拡張は、主に <xref:System.Windows.Navigation.NavigationService> と履歴を統合することによって行われます。 <xref:System.Windows.Navigation.NavigationWindow> のクライアント領域は、Uniform Resource Identifier (URI) またはオブジェクトを指定することで更新できます。 この両方の方法を次のサンプルに示します。  
  
 [!code-csharp[Performance#PerformanceSnippet14](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/TestNavigation.xaml.cs#performancesnippet14)]
 [!code-vb[Performance#PerformanceSnippet14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/testnavigation.xaml.vb#performancesnippet14)]  
  
 各 <xref:System.Windows.Navigation.NavigationWindow> オブジェクトには、そのウィンドウのユーザーのナビゲーションを記録する履歴があります。 履歴の目的の 1 つは、ユーザーが自分の来た道を戻れるようにすることです。  
  
 Uniform Resource Identifier (URI) を使用して移動した場合、履歴には Uniform Resource Identifier (URI) の参照のみが格納されます。 したがって、ページに戻るたびにそのページが動的に再構築されることになり、ページの複雑さによってはかなりの時間がかかることもあります。 この場合、履歴の格納の負荷は低い反面、ページの再構築にかかる時間が長くなる可能性があります。  
  
 オブジェクトを使用して移動した場合は、オブジェクトのビジュアル ツリー全体が履歴に格納されます。 したがって、ページに戻るたびにページを再構築する必要はなく、ページがすぐに描画されます。 この場合、履歴の格納の負荷は高くなりますが、ページの再構築にかかる時間は短くて済みます。  
  
 <xref:System.Windows.Navigation.NavigationWindow> オブジェクトを使用するときは、履歴のサポートがアプリケーションのパフォーマンスにどのように影響するのかを念頭に置いておく必要があります。 詳細については、「[ナビゲーションの概要](../app-development/navigation-overview.md)」を参照してください。  
  
<a name="Hit_Testing"></a>
## <a name="hit-testing-on-large-3d-surfaces"></a>大きな 3D サーフェイスのヒット テスト  
 大きな 3D サーフェイスのヒット テストは、CPU 消費の面でパフォーマンスへの影響が非常に大きくなります。 3D サーフェイスがアニメーション化されている場合には特にその傾向が強くなります。 そのようなサーフェイスでヒット テストを行う必要がない場合は、ヒット テストを無効にしてください。 <xref:System.Windows.UIElement> から派生したオブジェクトでは、<xref:System.Windows.UIElement.IsHitTestVisible%2A> プロパティを `false` に設定することでヒット テストを無効にできます。  
  
<a name="CompositionTarget_Rendering_Event"></a>
## <a name="compositiontargetrendering-event"></a>CompositionTarget.Rendering イベント  
 <xref:System.Windows.Media.CompositionTarget.Rendering?displayProperty=nameWithType> イベントにより、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は常にアニメーション化されます。 このイベントを使用する場合は、毎回デタッチしてください。  
  
<a name="Avoid_Using_ScrollBarVisibility"></a>
## <a name="avoid-using-scrollbarvisibilityauto"></a>ScrollBarVisibility=Auto は使用しない  
 `HorizontalScrollBarVisibility` プロパティと `VerticalScrollBarVisibility` プロパティには、できる限り <xref:System.Windows.Controls.ScrollBarVisibility.Auto?displayProperty=nameWithType> 値を使用しないでください。 これらのプロパティは、<xref:System.Windows.Controls.RichTextBox>、<xref:System.Windows.Controls.ScrollViewer>、<xref:System.Windows.Controls.TextBox> の各オブジェクトと、<xref:System.Windows.Controls.ListBox> オブジェクトの添付プロパティのために定義されています。 代わりに、<xref:System.Windows.Controls.ScrollBarVisibility> は <xref:System.Windows.Controls.ScrollBarVisibility.Disabled>、<xref:System.Windows.Controls.ScrollBarVisibility.Hidden>、または <xref:System.Windows.Controls.ScrollBarVisibility.Visible> に設定します。  
  
 <xref:System.Windows.Controls.ScrollBarVisibility.Auto> 値は、スペースが限られていて、スクロール バーを必要なときにだけ表示する場合に使用するための値です。 <xref:System.Windows.Controls.ScrollBarVisibility> 値は、たとえば、数百行のテキストが含まれる <xref:System.Windows.Controls.TextBox> ではなく、30 項目の <xref:System.Windows.Controls.ListBox> で使用するときに役に立ちます。  
  
<a name="FontCache"></a>
## <a name="configure-font-cache-service-to-reduce-start-up-time"></a>Font Cache サービスの構成による起動時間の短縮  
 WPF Font Cache サービスでは、WPF アプリケーション間でフォント データが共有されます。 このサービスがまだ実行されていない場合は、実行する最初の WPF アプリケーションによって開始されます。 Windows Vista を使用している場合は、"Windows Presentation Foundation (WPF) Font Cache 3.0.0.0" サービスの設定を [手動] (既定) から [自動 (遅延開始)] に変更することで、WPF アプリケーションの最初の起動時間を短縮できます。  
  
## <a name="see-also"></a>関連項目

- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [アニメーションのヒントとテクニック](../graphics-multimedia/animation-tips-and-tricks.md)
