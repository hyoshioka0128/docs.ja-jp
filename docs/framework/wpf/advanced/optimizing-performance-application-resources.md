---
title: 'パフォーマンスの最適化: アプリケーション リソース'
ms.date: 03/30/2017
helpviewer_keywords:
- application resources [WPF], performance
- resources [WPF], performance
- static resources [WPF]
- sharing resources [WPF]
- brushes [WPF], performance
- sharing brushes without copying [WPF]
ms.assetid: 62b88488-c08e-4804-b7de-a1c34fbe929c
ms.openlocfilehash: 59b124c28ade0a6c5119b651ff935d460bf4516d
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458559"
---
# <a name="optimizing-performance-application-resources"></a>パフォーマンスの最適化: アプリケーション リソース
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用すると、類似した型の要素全体で一貫した外観や動作をサポートできるように、アプリケーション リソースを共有できます。 このトピックでは、アプリケーションのパフォーマンスを向上させるために役立ついくつかの推奨事項について説明します。  
  
 リソースについて詳しくは、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」をご覧ください。  
  
## <a name="sharing-resources"></a>リソースを共有する  
 アプリケーションでカスタム コントロールを使用して、<xref:System.Windows.ResourceDictionary> (または XAML リソース ノード) 内のリソースを定義する場合は、<xref:System.Windows.Application> または <xref:System.Windows.Window> のオブジェクト レベルでリソースを定義するか、カスタム コントロールの既定のテーマでそれらを定義することをお勧めします。 カスタム コントロールの <xref:System.Windows.ResourceDictionary> にリソースを定義すると、そのコントロールのすべてのインスタンスのパフォーマンスに影響が生じます。 たとえば、カスタム コントロールのリソース定義の一部として定義されたパフォーマンス重視のブラシ操作と、カスタム コントロールの多数のインスタンスがある場合、アプリケーションのワーキング セットは大幅に増加します。  
  
 この点について説明するために、次のように考えてみます。 たとえば、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用してカード ゲームを開発しているとします。 ほとんどのカード ゲームでは、52 個の異なる表を持つ 52 枚のカードが必要です。 カードのカスタム コントロールを実装し、カードのカスタム コントロールのリソースに 52 個のブラシ (それぞれカードの表を表す) を定義します。 メイン アプリケーションでは、最初にこのカード カスタム コントロールのインスタンスを 52 個作成します。 カード カスタム コントロールの各インスタンスで、<xref:System.Windows.Media.Brush> オブジェクトのインスタンスが 52 個生成されます。これにより、アプリケーションで合計 52 * 52 個の <xref:System.Windows.Media.Brush> オブジェクトが得られます。 カード コントロールの 52 個のインスタンス間で 52 個のブラシを共有しているため、ブラシをカードのカスタム コントロール リソースから <xref:System.Windows.Application> または <xref:System.Windows.Window> オブジェクト レベルに移動するか、カスタム コントロールの既定のテーマで定義することで、アプリケーションのワーキング セットを減らすことができます。  
  
## <a name="sharing-a-brush-without-copying"></a>ブラシをコピーせずに共有する  
 同じ <xref:System.Windows.Media.Brush> オブジェクトを使用している複数の要素がある場合は、XAML でブラシをインラインで定義するのではなく、ブラシをリソースとして定義し、それを参照します。 この方法では、1 つのインスタンスを作成して再利用します。一方、XAML でブラシをインラインで定義すると、要素ごとに新しいインスタンスが作成されます。  
  
 次のマークアップ サンプルは、この点を示しています。  
  
 [!code-xaml[Performance#PerformanceSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/BrushResource.xaml#performancesnippet7)]  
  
## <a name="use-static-resources-when-possible"></a>可能な場合は静的リソースを使用する  
 静的リソースでは、既に定義されているリソースへの参照を検索することによって、任意の XAML プロパティ属性の値が提供されます。 そのリソース検索動作は、コンパイル時の検索に類似しています。  
  
 一方、動的リソースでは、初期コンパイル中に一時式が作成されます。そのため、オブジェクトを構築するために要求されたリソース値が実際に必要になるまで、リソースの検索が遅延されます。 そのリソース検索動作は、実行時の検索に類似しており、パフォーマンスに影響します。 アプリケーションでは、必要な場合にのみ動的リソースを使用して、可能な限り静的リソースを使用してください。  
  
 次のマークアップ サンプルは、両方の種類のリソースの使用方法を示しています。  
  
 [!code-xaml[Performance#PerformanceSnippet8](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/DynamicResource.xaml#performancesnippet8)]  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
