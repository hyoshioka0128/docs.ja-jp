---
title: パフォーマンスの最適化:テキスト
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- rendering text [WPF]
- hyperlinks [WPF]
- formatted text [WPF]
- text [WPF], performance
- glyphs [WPF]
ms.assetid: 66b1b9a7-8618-48db-b616-c57ea4327b98
ms.openlocfilehash: 3e729458538353499f27f95ea2ca37fea1335238
ms.sourcegitcommit: 9a97c76e141333394676bc5d264c6624b6f45bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75740340"
---
# <a name="optimizing-performance-text"></a>パフォーマンスの最適化:テキスト

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、機能豊富な [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] コントロールを使用した、テキスト コンテンツ表示のサポートが含まれています。 一般にテキスト レンダリングは 3 つの階層に分けることができます。

1. <xref:System.Windows.Documents.Glyphs> オブジェクトと <xref:System.Windows.Media.GlyphRun> オブジェクトを直接使用する。

2. <xref:System.Windows.Media.FormattedText> オブジェクトを使用する。

3. <xref:System.Windows.Controls.TextBlock> オブジェクトや <xref:System.Windows.Documents.FlowDocument> オブジェクトなどの高レベルのコントロールを使用する。

このトピックでは、テキスト レンダリングのパフォーマンスに関する推奨事項を説明します。

<a name="Glyph_Level"></a>

## <a name="rendering-text-at-the-glyph-level"></a>グリフ レベルでのテキスト レンダリング

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、書式設定後のテキストをインターセプトして保存したいユーザーのために <xref:System.Windows.Documents.Glyphs> に直接アクセスするグリフ レベルのマークアップなど、高度なテキスト サポートが提供されています。 これらの機能は、下記のようなシナリオでのさまざまなテキスト レンダリング要件をサポートする不可欠なものです。

- 固定形式のドキュメントの画面表示。

- 印刷シナリオ。

  - デバイス プリンター言語としての [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。

  - Microsoft XPS Document Writer。

  - 以前のプリンター ドライバー、Win32 アプリケーションから固定形式への出力。

  - 印刷スプール形式。

- 以前のバージョンの Windows のクライアントおよびその他のコンピューティング デバイスを含む、固定形式のドキュメント表示。

> [!NOTE]
> <xref:System.Windows.Documents.Glyphs> および <xref:System.Windows.Media.GlyphRun> は、固定形式のドキュメント表示と印刷シナリオ向けに設計されています。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、一般的なレイアウトおよび <xref:System.Windows.Controls.Label> や <xref:System.Windows.Controls.TextBlock> などの [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] シナリオのための要素が提供されています。 レイアウトと [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] シナリオの詳細については、[WPF のタイポグラフィ](typography-in-wpf.md)を参照してください。

次の例は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の <xref:System.Windows.Documents.Glyphs> オブジェクトのプロパティを定義する方法を示しています。 <xref:System.Windows.Documents.Glyphs> オブジェクトによって、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.Media.GlyphRun> の出力を表します。 この例では、Arial、Courier New、Times New Roman フォントがローカル コンピューターの **C:\WINDOWS\Fonts** フォルダーにインストールされていると想定しています。

[!code-xaml[GlyphsOvwSample1#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]

### <a name="using-drawglyphrun"></a>DrawGlyphRun を使用する

カスタム コントロールがあり、グリフをレンダリングする場合は、<xref:System.Windows.Media.DrawingContext.DrawGlyphRun%2A> メソッドを使用します。

また、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、<xref:System.Windows.Media.FormattedText> オブジェクトを使用してカスタム テキストの書式を設定するための下位レベルのサービスも提供します。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でテキストをレンダリングする最も効率的な方法は、<xref:System.Windows.Documents.Glyphs> と <xref:System.Windows.Media.GlyphRun> を使用してグリフ レベルでテキスト コンテンツを生成することです。 ただし、この効率の代償として、<xref:System.Windows.Controls.TextBlock> や <xref:System.Windows.Documents.FlowDocument> などの [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コントロールの組み込み機能である使いやすいリッチ テキストの書式設定が失われます。

<a name="FormattedText_Object"></a>

## <a name="formattedtext-object"></a>FormattedText オブジェクト

<xref:System.Windows.Media.FormattedText> オブジェクトを使用すると、複数行のテキストを描画できます。このテキストでは、テキスト内の各文字を個々に書式設定できます。 詳細については、「[書式設定されたテキストの描画](drawing-formatted-text.md)」を参照してください。

書式設定されたテキストを作成するには、<xref:System.Windows.Media.FormattedText.%23ctor%2A> コンストラクターを呼び出して <xref:System.Windows.Media.FormattedText> オブジェクトを作成します。 最初の書式設定済みテキスト文字列を作成したら、書式スタイルの範囲を適用できます。 アプリケーションで独自のレイアウトを実装する場合は、<xref:System.Windows.Controls.TextBlock> などのコントロールを使用するよりも、<xref:System.Windows.Media.FormattedText>オブジェクトの方が適しています。 <xref:System.Windows.Media.FormattedText> オブジェクトの詳細については、「[書式設定されたテキストの描画](drawing-formatted-text.md)」を参照してください。

<xref:System.Windows.Media.FormattedText> オブジェクトには、低レベルのテキスト書式設定機能が用意されています。 複数の書式スタイルを 1 つ以上の文字に適用できます。 たとえば、<xref:System.Windows.Media.FormattedText.SetFontSize%2A> メソッドと <xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A> メソッドの両方を呼び出して、テキストの最初の 5 文字の書式設定を変更できます。

次のコード例では、<xref:System.Windows.Media.FormattedText> オブジェクトを作成し、レンダリングします。

[!code-csharp[formattedtextsnippets#FormattedTextSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
[!code-vb[formattedtextsnippets#FormattedTextSnippets1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]

<a name="FlowDocument_TextBlock_Label"></a>

## <a name="flowdocument-textblock-and-label-controls"></a>FlowDocument、TextBlock、ラベル コントロール

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には画面にテキストを描画するための複数のコントロールが含まれています。 各コントロールは異なるシナリオを対象にしており、それぞれに一連の機能と制限があります。

### <a name="flowdocument-impacts-performance-more-than-textblock-or-label"></a>FlowDocument は TextBlock やラベルよりもパフォーマンスへの影響が大きい

一般的に、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] で短い文を使用するなど限定的なテキストのサポートが必要な場合は、<xref:System.Windows.Controls.TextBlock> 要素を使用するべきです。 最小限のテキスト サポートが必要な場合には、<xref:System.Windows.Controls.Label> を使用します。 <xref:System.Windows.Documents.FlowDocument> 要素は、コンテンツのリッチな表示をサポートする再フロー可能なドキュメントのコンテナーなので、<xref:System.Windows.Controls.TextBlock> コントロールや <xref:System.Windows.Controls.Label> コントロールを使用するのに比べてパフォーマンスに大きく影響します。

<xref:System.Windows.Documents.FlowDocument> の詳細については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください。

### <a name="avoid-using-textblock-in-flowdocument"></a>FlowDocument での TextBlock の使用を避ける

<xref:System.Windows.Controls.TextBlock> 要素は <xref:System.Windows.UIElement> から派生します。 <xref:System.Windows.Documents.Run> 要素は <xref:System.Windows.Documents.TextElement> から派生します。これは、<xref:System.Windows.UIElement> 派生オブジェクトよりも使用コストが低くなります。 テキスト コンテンツを <xref:System.Windows.Documents.FlowDocument> で表示する場合は、可能であれば <xref:System.Windows.Controls.TextBlock> ではなく <xref:System.Windows.Documents.Run> を使用します。

次のマークアップ サンプルは、<xref:System.Windows.Documents.FlowDocument> 内でテキスト コンテンツを設定する 2 つの方法を示しています。

[!code-xaml[Performance#PerformanceSnippet13](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/FlowDocument.xaml#performancesnippet13)]

### <a name="avoid-using-run-to-set-text-properties"></a>テキスト プロパティの設定に Run は使用しない

一般に、<xref:System.Windows.Controls.TextBlock> 内で <xref:System.Windows.Documents.Run> を使用すると、明示的な <xref:System.Windows.Documents.Run> オブジェクトをまったく使用しない場合よりもパフォーマンス負荷が高くなります。 テキストのプロパティを設定するために <xref:System.Windows.Documents.Run> を使用している場合は、代わりにそれらのプロパティを <xref:System.Windows.Controls.TextBlock> に直接設定してください。

次のマークアップ サンプルは、テキスト プロパティ (この例では <xref:System.Windows.Controls.TextBlock.FontWeight%2A> プロパティ) を設定するこれらの 2 つの方法を示しています。

[!code-xaml[Performance#PerformanceSnippet12](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml#performancesnippet12)]

次の表は、明示的な <xref:System.Windows.Documents.Run> がある場合とない場合の 1000 個の <xref:System.Windows.Controls.TextBlock>オブジェクトを表示するコストを示しています。

|**TextBlock 型**|**作成時間 (ミリ秒)**|**レンダリング時間 (ミリ秒)**|
|------------------------|------------------------------|----------------------------|
|Run によるテキスト プロパティ設定|146|540|
|TextBlock によるテキスト プロパティ設定|43|453|

### <a name="avoid-databinding-to-the-labelcontent-property"></a>Label.Content プロパティへのデータ バインドを避ける

<xref:System.String> ソースから頻繁に更新される <xref:System.Windows.Controls.Label> オブジェクトがあるシナリオを考えてみましょう。 <xref:System.Windows.Controls.Label> 要素の <xref:System.Windows.Controls.ContentControl.Content%2A> プロパティを <xref:System.String> ソース オブジェクトにデータ バインドすると、パフォーマンスが低下する可能性があります。 ソース <xref:System.String> が更新されるたびに、古い <xref:System.String> オブジェクトは破棄され、新しい <xref:System.String> が再作成されます。<xref:System.String> オブジェクトは不変であるため、変更できません。 その結果、<xref:System.Windows.Controls.Label> オブジェクトの <xref:System.Windows.Controls.ContentPresenter> によって古いコンテンツは破棄され、新しいコンテンツが再生成され、新しい <xref:System.String> が表示されます。

この問題の解決策は単純です。 <xref:System.Windows.Controls.Label> がカスタムの <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 値に設定されていない場合は、<xref:System.Windows.Controls.Label> を <xref:System.Windows.Controls.TextBlock> に置き換え、その <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティをソース文字列にデータ バインドします。

|**データ バインドされたプロパティ**|**更新時間 (ミリ秒)**|
|-----------------------------|----------------------------|
|Label.Content|835|
|TextBlock.Text|242|

<a name="Hyperlink"></a>

## <a name="hyperlink"></a>ハイパーリンク

<xref:System.Windows.Documents.Hyperlink> オブジェクトは、インライン レベルのフロー コンテンツ要素であり、フロー コンテンツ内のハイパーリンクをホストすることができます。

### <a name="combine-hyperlinks-in-one-textblock-object"></a>1 つの TextBlock オブジェクト内でハイパーリンクを結合

複数の <xref:System.Windows.Documents.Hyperlink>要素の使用を最適化するには、同じ <xref:System.Windows.Controls.TextBlock> 内にグループ化します。 こうすると、アプリケーション内で作成するオブジェクトの数を最小限に抑えるのに役立ちます。 たとえば、次のように複数のハイパーリンクを表示するとします。

MSN Home &#124; My MSN

次のマークアップの例は、ハイパーリンクの表示に使用される複数の <xref:System.Windows.Controls.TextBlock> 要素を示しています。

[!code-xaml[Performance#PerformanceSnippet9](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet9)]

次のマークアップの例は、ハイパーリンクをより効率的に表示する方法を示しています。今回は 1 つの <xref:System.Windows.Controls.TextBlock> を使用しています。

[!code-xaml[Performance#PerformanceSnippet10](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet10)]

### <a name="showing-underlines-on-hyperlinks-only-on-mouseenter-events"></a>MouseEnter イベントでのみハイパーリンクに下線を表示

<xref:System.Windows.TextDecoration> オブジェクトは、テキストに追加できるビジュアル装飾です。ただし、インスタンス化するにはパフォーマンスの負荷が高くなります。 <xref:System.Windows.Documents.Hyperlink> 要素を広範に使用する場合は、<xref:System.Windows.ContentElement.MouseEnter> イベントなどのイベントをトリガーするときにのみ下線を表示することを検討してください。 詳細については、「[方法: ハイパーリンクに下線を引くかどうかを指定する](how-to-specify-whether-a-hyperlink-is-underlined.md)」を参照してください。

MouseEnter イベントで下線付きのハイパーリンクをトリガーする方法を次の図に示します。

![TextDecorations を表示するハイパーリンク](./media/how-to-specify-whether-a-hyperlink-is-underlined/text-decorations-hyperlinks.png)

次のマークアップ サンプルは、下線ありとなしで定義された <xref:System.Windows.Documents.Hyperlink> を示しています。

[!code-xaml[Performance#PerformanceSnippet11](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]

下線ありとなしの 1000 個の <xref:System.Windows.Documents.Hyperlink> 要素を表示する場合のパフォーマンス コストを次の表に示します。

|**ハイパーリンク**|**作成時間 (ミリ秒)**|**レンダリング時間 (ミリ秒)**|
|-------------------|------------------------------|----------------------------|
|下線あり|289|1130|
|下線なし|299|776|

<a name="Text_Formatting_Features"></a>

## <a name="text-formatting-features"></a>テキスト書式設定機能

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、自動ハイフネーションなどのリッチ テキスト書式設定サービスを提供します。 これらのサービスはアプリケーションのパフォーマンスに影響を与える可能性があり、必要な場合のみ使用すべきです。

### <a name="avoid-unnecessary-use-of-hyphenation"></a>ハイフネーションの不要な使用を避ける

自動ハイフネーションを使用すると、テキスト行のハイフン ブレークポイントを検出し、<xref:System.Windows.Controls.TextBlock> オブジェクトと <xref:System.Windows.Documents.FlowDocument> オブジェクトの行にブレーク位置を追加できます。 既定では、これらのオブジェクトでは自動ハイフネーション機能は無効です。 この機能は、オブジェクトの IsHyphenationEnabled プロパティを `true` に設定することで有効にできます。 ただし、この機能を有効にすると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によってコンポーネント オブジェクト モデル (COM) の相互運用機能が開始されます。これは、アプリケーションのパフォーマンスに影響する可能性があります。 必要でない限り、自動ハイフネーションを使用しないことをお勧めします。

### <a name="use-figures-carefully"></a>図表を慎重に使用する

<xref:System.Windows.Documents.Figure> 要素は、コンテンツのページ内に絶対的に配置できるフロー コンテンツの一部を表します。 位置が既にレイアウトされているコンテンツと競合する場合、<xref:System.Windows.Documents.Figure> によってページ全体が自動的に再フォーマットされることがあります。不要な再フォーマットの可能性を最小限に抑えるには、隣り合う <xref:System.Windows.Documents.Figure> 要素をグループ化するか、固定ページ サイズの場合はコンテンツの最上部で宣言します。

### <a name="optimal-paragraph"></a>適切な段落

<xref:System.Windows.Documents.FlowDocument> オブジェクトの適切な段落の機能は、空白ができる限り均等に分散されるように段落をレイアウトします。 既定では、適切な段落の機能は無効です。 この機能を有効にするには、オブジェクトの <xref:System.Windows.Documents.FlowDocument.IsOptimalParagraphEnabled%2A> プロパティを `true` に設定します。 ただし、この機能を有効にするとアプリケーションのパフォーマンスに影響します。 必要でない限り、適切な段落の機能を使用しないことをお勧めします。

## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
