---
title: ScrollViewer の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], ScrollViewer
- ScrollViewer control [WPF], about ScrollViewer control
ms.assetid: 94a13b94-cfdf-4b12-a1aa-90cb50c6e9b9
ms.openlocfilehash: 2ff0f134ea3174f7f034d47446aab782e2141916
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186985"
---
# <a name="scrollviewer-overview"></a>ScrollViewer の概要
ユーザー インターフェイス内のコンテンツは、多くの場合、コンピューター画面の表示領域よりも大きいです。 <xref:System.Windows.Controls.ScrollViewer> コントロールでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーション内のコンテンツのスクロールを有効にする便利な手段が提供されます。 このトピックでは、<xref:System.Windows.Controls.ScrollViewer> 要素について説明し、いくつかの使用例を示します。  
  
<a name="what_is_a_scrollviewer_element"></a>
## <a name="the-scrollviewer-control"></a>ScrollViewer コントロール  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでのスクロールを有効にする 2 つの定義済みの要素 <xref:System.Windows.Controls.Primitives.ScrollBar> と <xref:System.Windows.Controls.ScrollViewer> があります。 <xref:System.Windows.Controls.ScrollViewer> コントロールには、水平方向および垂直方向の <xref:System.Windows.Controls.Primitives.ScrollBar> 要素と、スクロール可能領域内に他の表示可能要素を表示するためのコンテンツ コンテナー (<xref:System.Windows.Controls.Panel> 要素など) がカプセル化されています。 コンテンツのスクロールに <xref:System.Windows.Controls.Primitives.ScrollBar> 要素を使用するには、カスタム オブジェクトを作成する必要があります。 ただし、<xref:System.Windows.Controls.ScrollViewer> 要素は、<xref:System.Windows.Controls.Primitives.ScrollBar> の機能をカプセル化する複合コントロールであるため、単独で使用できます。  
  
 <xref:System.Windows.Controls.ScrollViewer> コントロールはマウスとキーボードの両方のコマンドに応答し、このコントロールでは事前に決められた増分でコンテンツをスクロールするためのさまざまなメソッドが定義されています。 <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> イベントを使用して、<xref:System.Windows.Controls.ScrollViewer> の状態の変化を検出できます。  
  
 <xref:System.Windows.Controls.ScrollViewer> で保持できる子は 1 つだけであり、通常は、要素の <xref:System.Windows.Controls.Panel.Children%2A> コレクションをホストできる <xref:System.Windows.Controls.Panel> 要素です。 <xref:System.Windows.Controls.ContentPresenter.Content%2A> プロパティでは、<xref:System.Windows.Controls.ScrollViewer> の唯一の子を定義します。  
  
<a name="scrollviewer_physical_vs_logical"></a>
## <a name="physical-vs-logical-scrolling"></a>物理スクロールと論理スクロール  
 物理スクロールは、定義済みの物理インクリメント(通常ピクセル単位で宣言されている値) でコンテンツをスクロールするために使用します。 論理スクロールは、論理ツリーの次の項目にスクロールするために使用します。 物理スクロールは、ほとんどの <xref:System.Windows.Controls.Panel> 要素で既定のスクロール動作です。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]は両方の種類のスクロールをサポートしています。  
  
#### <a name="the-iscrollinfo-interface"></a>IScrollInfo インターフェイス  
 <xref:System.Windows.Controls.Primitives.IScrollInfo> インターフェイスは、<xref:System.Windows.Controls.ScrollViewer> または派生コントロール内のメインのスクロール領域を表します。 このインターフェイスでは、物理インクリメントではなく、論理単位でのスクロールを必要する <xref:System.Windows.Controls.Panel> 要素で実装できる、スクロールのプロパティとメソッドが定義されています。 <xref:System.Windows.Controls.Primitives.IScrollInfo> のインスタンスを派生した <xref:System.Windows.Controls.Panel> にキャストしてそのスクロール メソッドを使用することで、ピクセル インクリメントではなく、子コレクションの次の論理単位までスクロールする便利な方法が提供されます。 既定の <xref:System.Windows.Controls.ScrollViewer> コントロールでは、物理単位でのスクロールがサポートされています。  
  
 <xref:System.Windows.Controls.StackPanel> と <xref:System.Windows.Controls.VirtualizingStackPanel> のどちらでも、<xref:System.Windows.Controls.Primitives.IScrollInfo> が実装されており、論理スクロールがネイティブにサポートされます。 論理スクロールをネイティブにサポートするレイアウト コントロールの場合でも、ホスト <xref:System.Windows.Controls.Panel> 要素を <xref:System.Windows.Controls.ScrollViewer> 内にラップし、<xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> プロパティを `false` に設定することによって、物理スクロールを実現できます。  
  
 次のコード例では、<xref:System.Windows.Controls.Primitives.IScrollInfo> のインスタンスを <xref:System.Windows.Controls.StackPanel> にキャストし、インターフェイスで定義されているコンテンツ スクロール メソッド (<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> と <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A>) を使用する方法を示します。  
  
 [!code-csharp[IScrollInfoMethods#3](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
<a name="scrollviewer_markup_syntax_and_sample"></a>
## <a name="defining-and-using-a-scrollviewer-element"></a>ScrollViewer 要素の定義と使用  
 次の例では、いくつかのテキストと四角形を含む <xref:System.Windows.Controls.ScrollViewer> をウィンドウ内に作成します。 <xref:System.Windows.Controls.Primitives.ScrollBar> 要素は、必要なときにだけ表示されます。 ウィンドウのサイズを変更すると、<xref:System.Windows.Controls.ScrollViewer.ComputedHorizontalScrollBarVisibility%2A> プロパティと <xref:System.Windows.Controls.ScrollViewer.ComputedVerticalScrollBarVisibility%2A> プロパティの更新された値によって、<xref:System.Windows.Controls.Primitives.ScrollBar> 要素が表示されたり、表示されなくなったりします。  
  
 [!code-cpp[ScrollViewer#1](~/samples/snippets/cpp/VS_Snippets_Wpf/ScrollViewer/CPP/ScrollViewer_wcp.cpp#1)]
 [!code-csharp[ScrollViewer#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewer/CSharp/ScrollViewer_wcp.cs#1)]
 [!code-vb[ScrollViewer#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewer/VisualBasic/ScrollViewer.vb#1)]
 [!code-xaml[ScrollViewer#1](~/samples/snippets/xaml/VS_Snippets_Wpf/ScrollViewer/XAML/Pane1.xaml#1)]  
  
<a name="scrollviewer_styling_scrollviewer"></a>
## <a name="styling-a-scrollviewer"></a>ScrollViewer のスタイル設定  
 Windows Presentation Foundation のすべてのコントロールと同様に、<xref:System.Windows.Controls.ScrollViewer> のスタイルを設定して、コントロールの既定のレンダリング動作を変更できます。 コントロールのスタイル設定の詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。  
  
<a name="scrollviewer_scroll_vs_paginate"></a>
## <a name="paginating-documents"></a>ドキュメントの改ページ調整  
 ドキュメントのコンテンツでは、スクロールする代わりに、改ページ調整をサポートするドキュメントのコンテナーを選択します。 <xref:System.Windows.Documents.FlowDocument> は、<xref:System.Windows.Controls.FlowDocumentPageViewer> などの表示コントロール内でホストされるように設計されたドキュメント用であり、複数のページにわたるコンテンツの改ページ調整がサポートされており、スクロールの必要がなくなります。 <xref:System.Windows.Controls.DocumentViewer> では、<xref:System.Windows.Documents.FixedDocument> コンテンツを表示するためのソリューションが提供されており、表示領域外のコンテンツを表示するには従来のスクロールが使用されます。  
  
 ドキュメント形式とプレゼンテーション オプションの詳細については、「[WPF のドキュメント](../advanced/documents-in-wpf.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.Primitives.ScrollBar>
- <xref:System.Windows.Controls.Primitives.IScrollInfo>
- [方法: スクロール ビューアーを作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752352(v=vs.90))
- [WPF のドキュメント](../advanced/documents-in-wpf.md)
- [ScrollBar のスタイルとテンプレート](scrollbar-styles-and-templates.md)
- [コントロール](../advanced/optimizing-performance-controls.md)
