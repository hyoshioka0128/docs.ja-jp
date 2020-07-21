---
title: コントロールのパフォーマンスを最適化する
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], improving performance
- container recycling [WPF]
- user interface virtualization [WPF]
ms.assetid: 45a31c43-ea8a-4546-96c8-0631b9934179
ms.openlocfilehash: d02fde7076cd6a24fdfb171ed54161b20f3d465e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76746730"
---
# <a name="optimizing-performance-controls"></a>パフォーマンスの最適化:コントロール

Windows Presentation Foundation (WPF) には、ほとんどの Windows アプリケーションで使用される一般的なユーザーインターフェイス (UI) コンポーネントの多くが含まれています。 このトピックでは、UI のパフォーマンスを向上させる方法について説明します。

## <a name="displaying-large-data-sets"></a>大容量のデータ セットの表示

<xref:System.Windows.Controls.ListView> や <xref:System.Windows.Controls.ComboBox> などの WPF コントロールは、アプリケーションで項目のリストを表示するために使用されます。 表示するリストが大きい場合、アプリケーションのパフォーマンスに影響する可能性があります。 これは、標準的なレイアウト システムでは、リスト コントロールに関連付けられた項目ごとにレイアウト コンテナーを作成した後、コンテナーのレイアウト サイズと位置を計算するためです。 通常、すべての項目を同時に表示する必要はありません。その代わりに項目のサブセットが表示され、ユーザーはリストをスクロールすることで、すべての項目を確認します。 このような場合は、UI の*仮想化*が役に立ちます。これは、項目に対する項目コンテナーの生成、および関連するレイアウトの計算を、項目が表示されるまで遅らせることを意味します。

UI の仮想化は、リスト コントロールにとって重要な処理です。 UI の仮想化とデータの仮想化を混同しないでください。 UI の仮想化では、表示される項目だけをメモリに格納しますが、データのバインディングがある場合はデータ構造体のすべてがメモリに格納されます。 これに対し、データの仮想化では、画面上に表示されているデータ項目だけがメモリに格納されます。

リスト項目がデータにバインドされている場合、既定では、<xref:System.Windows.Controls.ListView> および <xref:System.Windows.Controls.ListBox> コントロールの UI 仮想化が有効です。 <xref:System.Windows.Controls.TreeView> の仮想化は、<xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=nameWithType> 添付プロパティを `true` に設定することで有効にすることができます。 <xref:System.Windows.Controls.ItemsControl> から派生するカスタム コントロールまたは <xref:System.Windows.Controls.ComboBox> などの <xref:System.Windows.Controls.StackPanel> クラスを使用する既存の項目コントロールに対して UI 仮想化を有効にする場合は、<xref:System.Windows.Controls.ItemsControl.ItemsPanel%2A> を <xref:System.Windows.Controls.VirtualizingStackPanel> に設定し、<xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizing%2A> を `true` に設定することができます。 残念ながら、これらのコントロールに対する UI の仮想化を知らずに無効にすることがあります。 UI の仮想化が無効になる条件を一覧で示します。

- 項目コンテナーは、<xref:System.Windows.Controls.ItemsControl> に直接追加されます。 たとえば、アプリケーションによって明示的に <xref:System.Windows.Controls.ListBoxItem> オブジェクトが <xref:System.Windows.Controls.ListBox> に追加された場合、<xref:System.Windows.Controls.ListBox> では <xref:System.Windows.Controls.ListBoxItem> オブジェクトが仮想化されません。

- <xref:System.Windows.Controls.ItemsControl> の項目コンテナーにはさまざまな種類があります。 たとえば、<xref:System.Windows.Controls.Separator> オブジェクトを使用する <xref:System.Windows.Controls.Menu> では項目のリサイクルを実装できません。これは、<xref:System.Windows.Controls.Menu> に <xref:System.Windows.Controls.Separator> および <xref:System.Windows.Controls.MenuItem> という種類のオブジェクトが含まれているためです。

- <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> を `false` に設定します。

- <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A> を `false` に設定します。

コンテナー項目を仮想化する際の重要な考慮事項は項目が属する項目コンテナーに関連付けられた追加の状態情報があるかどうかです。 その場合は、追加状態を保存する必要があります。 たとえば、項目が <xref:System.Windows.Controls.Expander> コントロールに含まれていて、<xref:System.Windows.Controls.Expander.IsExpanded%2A> 状態が項目自体ではなく項目のコンテナーにバインドされているとします。 コンテナーを新しい項目に再利用すると場合、<xref:System.Windows.Controls.Expander.IsExpanded%2A> の現在の値が新しい項目に使用されます。 さらに、古い項目は正しい <xref:System.Windows.Controls.Expander.IsExpanded%2A> 値を失います。

現時点では、データの仮想化のサポートが組み込まれている WPF コントロールはありません。

## <a name="container-recycling"></a>コンテナーのリサイクル

<xref:System.Windows.Controls.ItemsControl> から継承されたコントロールに対して .NET Framework 3.5 SP1 で追加された UI 仮想化の最適化は "*コンテナーのリサイクル*" です。これにより、スクロールのパフォーマンスを向上させることもできます。 UI 仮想化を使用する <xref:System.Windows.Controls.ItemsControl> が入力されると、スクロールして表示される各項目の項目コンテナーが作成され、スクロールされて表示されない各項目の項目コンテナーが破棄されます。 *コンテナーのリサイクル*では、異なるデータ項目用の既存の項目コンテナーをコントロールが再利用できるので、ユーザーが <xref:System.Windows.Controls.ItemsControl> をスクロールするたびに項目コンテナーの作成と破棄が常に行われることはありません。 <xref:System.Windows.Controls.VirtualizingPanel.VirtualizationMode%2A> 添付プロパティを <xref:System.Windows.Controls.VirtualizationMode.Recycling> に設定することにより、項目のリサイクルを有効にすることができます。

仮想化をサポートする <xref:System.Windows.Controls.ItemsControl> では、コンテナーのリサイクルを使用できます。 <xref:System.Windows.Controls.ListBox> 上でコンテナーのリサイクルを有効にする方法の例については、「[ListBox のスクロール速度を向上させる](../controls/how-to-improve-the-scrolling-performance-of-a-listbox.md)」を参照してください。

## <a name="supporting-bidirectional-virtualization"></a>双方向仮想化のサポート

<xref:System.Windows.Controls.VirtualizingStackPanel> には、水平方向または垂直方向の一方向の UI 仮想化のサポートが組み込まれています。 コントロールに双方向仮想化を使用する場合は、<xref:System.Windows.Controls.VirtualizingStackPanel> クラスを拡張するカスタム パネルを実装する必要があります。 <xref:System.Windows.Controls.VirtualizingStackPanel> クラスでは、<xref:System.Windows.Controls.VirtualizingStackPanel.OnViewportSizeChanged%2A>、<xref:System.Windows.Controls.VirtualizingStackPanel.LineUp%2A>、<xref:System.Windows.Controls.VirtualizingStackPanel.PageUp%2A>、<xref:System.Windows.Controls.VirtualizingStackPanel.MouseWheelUp%2A> などの仮想メソッドが公開されています。これらの仮想メソッドを使用すると、リストの可視部分の変更を検出し、それに応じて処理することができます。

## <a name="optimizing-templates"></a>テンプレートの最適化

ビジュアル ツリーには、アプリケーションのすべてのビジュアル要素が含まれます。 直接的に作成されたオブジェクトに加え、テンプレートの拡張によって追加されたオブジェクトも含まれます。 たとえば、<xref:System.Windows.Controls.Button> を作成すると、ビジュアル ツリーに <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> および <xref:System.Windows.Controls.ContentPresenter> オブジェクトも取得されます。 コントロール テンプレートを最適化していない場合、必要のない余分なオブジェクトがビジュアル ツリーの中に多数作成される可能性があります。 ビジュアル ツリーの詳細については、「[WPF グラフィックス レンダリングの概要](../graphics-multimedia/wpf-graphics-rendering-overview.md)」を参照してください。

## <a name="deferred-scrolling"></a>遅延スクロール

既定では、ユーザーがスクロールバーのつまみをドラッグすると、コンテンツ ビューが連続的に更新されます。 コントロールのスクロールが遅い場合は、遅延スクロールの使用をご検討ください。 遅延スクロールでは、コンテンツは、ユーザーがつまみを離したときにのみ更新されます。

遅延スクロールを実装するには、<xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> プロパティを `true` に設定します。 <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> は添付プロパティであり、<xref:System.Windows.Controls.ScrollViewer> と、コントロール テンプレートに <xref:System.Windows.Controls.ScrollViewer> がある任意のコントロールに設定できます。

## <a name="controls-that-implement-performance-features"></a>パフォーマンス機能を実装するコントロール

次の表は、データを表示するための一般的なコントロールと、各コントロールのパフォーマンス機能に対するサポートを示しています。 これらの機能を有効にする方法については、前のセクションを参照してください。

|Control|仮想化|コンテナーのリサイクル|遅延スクロール|
|-------------|--------------------|-------------------------|------------------------|
|<xref:System.Windows.Controls.ComboBox>|有効にできます|有効にできます|有効にできます|
|<xref:System.Windows.Controls.ContextMenu>|有効にできます|有効にできます|有効にできます|
|<xref:System.Windows.Controls.DocumentViewer>|使用できません|使用できません|有効にできます|
|<xref:System.Windows.Controls.ListBox>|Default|有効にできます|有効にできます|
|<xref:System.Windows.Controls.ListView>|Default|有効にできます|有効にできます|
|<xref:System.Windows.Controls.TreeView>|有効にできます|有効にできます|有効にできます|
|<xref:System.Windows.Controls.ToolBar>|使用できません|使用できません|有効にできます|

> [!NOTE]
> <xref:System.Windows.Controls.TreeView> で仮想化とコンテナーのリサイクルを有効にする方法の例については、「[TreeView のパフォーマンスを改善する](../controls/how-to-improve-the-performance-of-a-treeview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [レイアウト](layout.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [コントロール](../controls/index.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [チュートリアル: WPF アプリケーション内のアプリケーション データのキャッシュ](walkthrough-caching-application-data-in-a-wpf-application.md)
