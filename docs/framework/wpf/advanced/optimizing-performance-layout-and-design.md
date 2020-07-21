---
title: 'パフォーマンスの最適化: レイアウトとデザイン'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- layout [WPF], optimizing performance
- design considerations [WPF]
- layout pass [WPF]
ms.assetid: 005f4cda-a849-448b-916b-38d14d9a96fe
ms.openlocfilehash: a18cc364d625cc98f77e63b0f361980ef574e8a5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611891"
---
# <a name="optimizing-performance-layout-and-design"></a>パフォーマンスの最適化: レイアウトとデザイン
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの設計によっては、レイアウトの計算やオブジェクト参照の検証で不要なオーバーヘッドが発生して、パフォーマンスに影響が及ぶことがあります。 オブジェクトの作成 (特に実行時の作成) はアプリケーションのパフォーマンス特性に影響する可能性があります。  
  
 このトピックでは、このようなパフォーマンスに関する推奨事項について説明します。  
  
## <a name="layout"></a>レイアウト  
 "レイアウト パス" という用語は、<xref:System.Windows.Controls.Panel> 派生オブジェクトの子のコレクションのメンバーを測定および配置して、それらを画面上に描画するプロセスを表します。 レイアウト パスは数学的に増大するプロセスで、コレクション内の子の数が多くなれば、必要な計算の数も多くなります。 たとえば、コレクション内の子 <xref:System.Windows.UIElement> オブジェクトがその位置を変更するたびに、レイアウト システムによる新しいパスがトリガーされる可能性があります。 オブジェクトの特性とレイアウトの動作の間には密接な関係があるため、レイアウト システムを呼び出すことができるイベントの種類を把握することが重要です。 レイアウト パスの不要な呼び出しをできるだけ減らすことで、アプリケーションのパフォーマンスを向上させることができます。  
  
 レイアウト システムは、コレクションの子メンバーごとに、測定パスと配置パスという 2 つのパスを実行します。 それぞれの子オブジェクトでは、独自のレイアウト動作を提供するために、<xref:System.Windows.UIElement.Measure%2A> および <xref:System.Windows.UIElement.Arrange%2A> メソッドの独自のオーバーライドされた実装が提供されます。 簡単に言うと、レイアウトは、要素のサイズ測定、配置、画面上への描画を繰り返す再帰的なシステムです。  
  
- 子 <xref:System.Windows.UIElement> オブジェクトでは、最初にそのコア プロパティが測定され、レイアウト プロセスが開始されます。  
  
- <xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Margin%2A> など、サイズに関連するオブジェクトの <xref:System.Windows.FrameworkElement> のプロパティが評価されます。  
  
- <xref:System.Windows.Controls.Panel> 固有のロジックが適用されます。たとえば、<xref:System.Windows.Controls.DockPanel> の <xref:System.Windows.Controls.DockPanel.Dock%2A> プロパティや <xref:System.Windows.Controls.StackPanel> の <xref:System.Windows.Controls.StackPanel.Orientation%2A> プロパティなどです。  
  
- すべての子オブジェクトが測定された後、コンテンツが配置されます。  
  
- 子オブジェクトのコレクションが画面に描画されます。  
  
 以下のアクションが発生すると、再びレイアウト パス プロセスが呼び出されます。  
  
- 子オブジェクトがコレクションに追加された場合。  
  
- 子オブジェクトに <xref:System.Windows.FrameworkElement.LayoutTransform%2A> が適用されます。  
  
- 子オブジェクトに対して <xref:System.Windows.UIElement.UpdateLayout%2A> メソッドが呼び出されます。  
  
- 測定パスや配置パスに影響を与えるものとしてメタデータでマークされている依存関係プロパティの値が変更された場合。  
  
### <a name="use-the-most-efficient-panel-where-possible"></a>可能な場合は最も効率的なパネルを使用する  
 使用する <xref:System.Windows.Controls.Panel> 派生要素のレイアウト動作は、レイアウト プロセスの複雑さに直接基づいています。 たとえば、<xref:System.Windows.Controls.Grid> または <xref:System.Windows.Controls.StackPanel> コントロールでは <xref:System.Windows.Controls.Canvas> コントロールよりもはるかに多くの機能が提供されます。 はるかに多くの機能が用意されていますが、その代償として、パフォーマンスへの負荷も高くなります。 しかし、<xref:System.Windows.Controls.Grid> コントロールに用意されている機能が必要ない場合は、<xref:System.Windows.Controls.Canvas> やカスタム パネルなど、コストのかからない代替手段を使用してください。  
  
 詳細については、「[Panels Overview](../controls/panels-overview.md)」を参照してください。  
  
### <a name="update-rather-than-replace-a-rendertransform"></a>RenderTransform は置き換えずに更新する  
 <xref:System.Windows.Media.Transform> を <xref:System.Windows.UIElement.RenderTransform%2A> プロパティの値として置き換えずに、更新することができます。 アニメーションを含むシナリオでは特にこれが当てはまります。 既存の <xref:System.Windows.Media.Transform> を更新すると、不要なレイアウト計算が開始されないようにすることができます。  
  
### <a name="build-your-tree-top-down"></a>ツリーはトップダウンで作成する  
 論理ツリーのノードが追加または削除されると、ノードの親とそのすべての子でプロパティの無効化が行われます。 このため、常にトップダウンの作成パターンに従って、検証済みのノードで無駄に無効化が行われないようにする必要があります。 次の表に、ツリーをトップダウンで作成した場合とボトムアップで作成した場合の実行速度の違いを示します。このツリーには 150 のレベルがあり、各レベルに <xref:System.Windows.Controls.TextBlock> と <xref:System.Windows.Controls.DockPanel> が 1 つずつ含まれています。  
  
|**動作**|**ツリーの作成 (ミリ秒)**|**レンダリング-ツリーの作成を含む (ミリ秒)**|  
|----------------|---------------------------------|-------------------------------------------------|  
|ボトムアップ|366|454|  
|トップダウン|11|96|  
  
 ツリーをトップダウンで作成する方法を次のコード例に示します。  
  
 [!code-csharp[Performance#PerformanceSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet1)]
 [!code-vb[Performance#PerformanceSnippet1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet1)]  
  
 論理ツリーについて詳しくは、「[WPF のツリー](trees-in-wpf.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
- [レイアウト](layout.md)
