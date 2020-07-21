---
title: フロー ドキュメントの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'documents [WPF], flow documents [WPF], , '
- ', '
- flow documents [WPF]
ms.assetid: ef236a50-d44f-43c8-ba7c-82b0c733c0b7
ms.openlocfilehash: 1dcba034dd934cb0e103cd131fcaa2088e2f93d3
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856151"
---
# <a name="flow-document-overview"></a>フロー ドキュメントの概要

フロー ドキュメントは、表示と読みやすさを最適化するように設計されたドキュメントです。 フロー ドキュメントは、1 つの定義済みのレイアウトに設定するのではなく、ウィンドウのサイズ、デバイスの解像度、省略可能なユーザー設定など、ランタイム変数に基づいてコンテンツを動的に調整したりリフローしたりします。 また、フロー ドキュメントは、改ページ位置の自動修正や列などの高度なドキュメント機能を提供します。 ここでは、フロー ドキュメントの概要およびフロー ドキュメントの作成方法について説明します。

<a name="what_is_a_flow_document"></a>

## <a name="what-is-a-flow-document"></a>フロー ドキュメントとは

フロー ドキュメントは、ウィンドウ サイズ、デバイスの解像度、およびその他の環境変数に応じて "コンテンツをリフロー" するために設計されています。 また、フロー ドキュメントには、検索、読みやすさを最適化するモードの表示、およびフォントのサイズと外観を変更する機能を含むさまざまな組み込み機能があります。 フロー ドキュメントは、主なドキュメントの使用シナリオが読みやすさである場合に最適です。 これに対し、固定ドキュメントは、静的なプレゼンテーションを行うように設計されています。 ソース コンテンツの再現性が重要である場合は、固定ドキュメントが便利です。 各種ドキュメントの詳細については、「[WPF のドキュメント](documents-in-wpf.md)」を参照してください。

さまざまなサイズの複数のウィンドウで表示されるサンプルのフロー ドキュメントを次の図に示します。 表示領域が変わると、コンテンツはスペースを最大限に利用できるようにリフローされます。

![フロー ドキュメントのコンテンツのリフロー](./media/edocs-flowdocument.png "eDocs_FlowDocument")

上のイメージに示すように、フロー コンテンツには、段落、リスト、イメージなどの多くのコンポーネントを含めることができます。 これらのコンポーネントは、マークアップでの要素と手続き型コードでのオブジェクトに対応します。 これらのクラスについては、この概要の「[フロー関連のクラス](#flow_related_classes)」セクションで後ほど詳しく説明します。 ここでは、太字テキストと一覧が含まれている段落で構成されているフロー ドキュメントを作成する、シンプルなコード例を示します。

[!code-xaml[FlowOvwSnippets_snip#SimpleFlowExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SimpleFlowExample.xaml#simpleflowexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SimpleFlowExample.cs#simpleflowcodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SimpleFlowExample.vb#simpleflowcodeonlyexamplewholepage)]

次の図は、このコード スニペットの結果を示したものです。

![スクリーンショット: レンダリングされた FlowDocument の例](./media/flow-ovw-first-example.png "Flow_Ovw_First_Example")

この例では、フロー コンテンツをホストするために <xref:System.Windows.Controls.FlowDocumentReader> コントロールが使用されています。 コントロールをホストするフロー コンテンツの詳細については、「[フロー ドキュメントの種類](#flow_document_types)」を参照してください。 <xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.List>、<xref:System.Windows.Documents.ListItem>、<xref:System.Windows.Documents.Bold> 要素は、マークアップの順序に基づいて、コンテンツの書式設定を制御するために使用されます。 たとえば、<xref:System.Windows.Documents.Bold> 要素は、段落内のテキストの部分のみにまたがっています。結果として、テキストのその部分のみが太字となります。 HTML を使用したことがある場合、これは慣れ親しまれているでしょう。

フロー ドキュメントには、上の図で強調表示されているいくつかの機能が組み込まれています。

- 検索: ユーザーがドキュメント全体のフル テキスト検索を実行できるようにします。

- 表示モード: ユーザーは、単一ページ (一度に 1 ページ) 表示モード、一度に 2 ページ (読書形式) 表示モード、連続したスクロール (ボトムレス) 表示モードなど、各自に適切な表示モードを選択できます。  これらの表示モードの詳細については、「<xref:System.Windows.Controls.FlowDocumentReaderViewingMode>」を参照してください。

- ページ ナビゲーション コントロール: ドキュメントの表示モードでページを使用する場合、ページ ナビゲーション コントロールには、次のページへのジャンプ用ボタン (下向き矢印)、前のページへのジャンプ用ボタン (上向き矢印)、現在のページ番号と総ページ数のインジケーターが含まれます。 ページ間の移動は、キーボードの方向キーを使用して行うこともできます。

- ズーム: ズーム コントロールでは、ユーザーはプラスまたはマイナス ボタンをそれぞれクリックして、ズーム レベルを上げたり下げたりすることができます。 ズーム コントロールには、ズーム レベルの調整用スライダーも含まれます。 詳細については、「<xref:System.Windows.Controls.FlowDocumentReader.Zoom%2A>」を参照してください。

これらの機能は、フロー コンテンツをホストするために使用されるコントロールに基づいて変更できます。 次のセクションでは、さまざまなコントロールについて説明します。

<a name="flow_document_types"></a>

## <a name="flow-document-types"></a>フロー ドキュメントの種類

フロー ドキュメント コンテンツの表示、およびそれがどのように表示されるかは、どのようなオブジェクトがフロー コンテンツをホストするために使用されるかに依存します。 フロー コンテンツの表示をサポートするコントロールには、<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、<xref:System.Windows.Controls.RichTextBox>、<xref:System.Windows.Controls.FlowDocumentScrollViewer> の 4 つがあります。 これらのコントロールについて、以下に簡単に説明します。

> [!NOTE]
> <xref:System.Windows.Documents.FlowDocument> はフロー コンテンツを直接ホストするために必要です。したがって、これらの表示コントロールではすべて、フロー コンテンツ ホスティングを有効にするために <xref:System.Windows.Documents.FlowDocument> を使用します。

### <a name="flowdocumentreader"></a>FlowDocumentReader

<xref:System.Windows.Controls.FlowDocumentReader> には、単一ページ (一度に 1 ページ) 表示モード、一度に 2 ページ (読書形式) 表示モード、連続スクロール (ボトムレス) 表示モードなど、さまざまな表示モードをユーザーが動的に選択できるようにする機能が含まれます。 これらの表示モードの詳細については、「<xref:System.Windows.Controls.FlowDocumentReaderViewingMode>」を参照してください。 さまざまな表示モードを動的に切り替える必要がない場合、<xref:System.Windows.Controls.FlowDocumentPageViewer> および <xref:System.Windows.Controls.FlowDocumentScrollViewer> で、特定の表示モードに固定された軽量のフロー コンテンツ ビューアーが提供されます。

### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer と FlowDocumentScrollViewer

<xref:System.Windows.Controls.FlowDocumentPageViewer> では、コンテンツを一度に 1 ページの表示モードで表示しますが、<xref:System.Windows.Controls.FlowDocumentScrollViewer> では、コンテンツを連続したスクロール モードで表示します。 <xref:System.Windows.Controls.FlowDocumentPageViewer> と <xref:System.Windows.Controls.FlowDocumentScrollViewer> は両方とも、特定の表示モードに固定されています。 <xref:System.Windows.Controls.FlowDocumentReader> と比較してください。これには、ユーザーが (<xref:System.Windows.Controls.FlowDocumentReaderViewingMode> 列挙体で提供される) 各種表示モードから動的に選ぶことができる機能が含まれていますが、<xref:System.Windows.Controls.FlowDocumentPageViewer> や <xref:System.Windows.Controls.FlowDocumentScrollViewer> よりも多くのリソースを消費します。

既定では、垂直スクロール バーは常に表示され、水平スクロール バーは必要に応じて表示されます。 <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> の既定の UI にはツール バーが含まれませんが、<xref:System.Windows.Controls.FlowDocumentScrollViewer> プロパティを使用して組み込みツール バーを有効にできます。

### <a name="richtextbox"></a>RichTextBox

ユーザーがフロー コンテンツを編集できるようにする場合は、<xref:System.Windows.Controls.RichTextBox> を使用します。 たとえば、テーブル、斜体や太字の書式設定などをユーザーが操作できるようにするエディターを作成する必要がある場合は、<xref:System.Windows.Controls.RichTextBox> を使用します。 詳細については、「[RichTextBox の概要](../controls/richtextbox-overview.md)」を参照してください。

> [!NOTE]
> <xref:System.Windows.Controls.RichTextBox> 内のフロー コンテンツは、他のコントロールに含まれているフロー コンテンツと一部異なる動作をします。 たとえば、<xref:System.Windows.Controls.RichTextBox> に列がないと、自動サイズ変更動作は行われません。 また、検索、表示モード、ページ ナビゲーション、ズームなどのフロー コンテンツの通常の組み込み機能は、<xref:System.Windows.Controls.RichTextBox> 内では利用できません。

<a name="creating_flow_content"></a>

## <a name="creating-flow-content"></a>フロー コンテンツの作成

フロー コンテンツは、テキスト、イメージ、テーブル、コントロールのような <xref:System.Windows.UIElement> 派生クラスを含むさまざまな要素で構成された複雑なものにすることができます。 複雑なフロー コンテンツを作成する方法を理解するには、次の点が重要です。

- **フロー関連のクラス**: フロー コンテンツで使用される各クラスには特定の目的があります。 また、フロー クラス間の階層型の関係により、それらがどのように使用されるかが理解しやすくなっています。 たとえば、<xref:System.Windows.Documents.Block> から派生したクラスは他のオブジェクトを含めるために使用されますが、<xref:System.Windows.Documents.Inline> クラスから派生したクラスには、表示されるオブジェクトが含まれます。

- **コンテンツ スキーマ**: フロー ドキュメントには、多くの入れ子になった要素が必要になる場合があります。 コンテンツ スキーマは、使用可能な要素間の親/子リレーションシップを指定します。

以下のセクションでは、これらの各領域について詳しく説明します。

<a name="flow_related_classes"></a>

## <a name="flow-related-classes"></a>フロー関連のクラス

次の図は、フロー コンテンツで最も一般的に使用されるオブジェクトを示します。

![図:フロー コンテンツ要素クラス階層](./media/flow-class-hierarchy.png "Flow_Class_Hierarchy")

フロー コンテンツのために、次の 2 つの重要なカテゴリがあります。

1. **Block の派生クラス**: "Block コンテンツ要素" または単に "Block 要素" とも呼ばれます。 <xref:System.Windows.Documents.Block> から継承する要素は、要素を共通の親の下にグループ化したり、共通の属性をグループに適用したりするために使用できます。

2. **Inline の派生クラス**: "Inline コンテンツ要素" または単に "Inline 要素" とも呼ばれます。 <xref:System.Windows.Documents.Inline> から継承する要素は、Block 要素または別の Inline 要素内に格納されます。 Inline 要素は、多くの場合、画面にレンダリングされるコンテンツの直接のコンテナーとして使用されます。 たとえば、<xref:System.Windows.Documents.Paragraph> (Block 要素) には <xref:System.Windows.Documents.Run> (Inline 要素) を含めることができますが、<xref:System.Windows.Documents.Run> には実際には、画面にレンダリングされるテキストが含まれます。

これらの 2 つのカテゴリの各クラスについて、以下に簡単に説明します。

### <a name="block-derived-classes"></a>Block の派生クラス

**Paragraph**

<xref:System.Windows.Documents.Paragraph> は、通常、コンテンツを段落にグループ化するために使用されます。 Paragraph の最も単純かつ一般的な用途は、テキストの段落の作成です。

[!code-xaml[FlowOvwSnippets_snip#ParagraphExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ParagraphExample.xaml#paragraphexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ParagraphExample.cs#paragraphcodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ParagraphExample.vb#paragraphcodeonlyexamplewholepage)]

しかし、次に示すように、他の Inline の派生要素を含めることもできます。

**セクション**

<xref:System.Windows.Documents.Section> は、他の <xref:System.Windows.Documents.Block> 派生要素を含めるためにのみ使用されます。 格納している要素に対して、既定の書式設定を適用することはありません。 しかし、<xref:System.Windows.Documents.Section> に設定されたプロパティ値はすべて、その子要素に適用されます。 セクションでは、プログラムで子コレクションを反復処理することもできます。 <xref:System.Windows.Documents.Section> は、HTML の \<DIV> タグと同様の方法で使用されます。

以下の例では、3 つの段落が 1 つの <xref:System.Windows.Documents.Section> で定義されます。 このセクションには、<xref:System.Windows.Documents.TextElement.Background%2A> プロパティ値である Red があるため、段落の背景色も赤になります。

[!code-xaml[FlowOvwSnippets_snip#SectionExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SectionExample.xaml#sectionexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SectionExample.cs#sectioncodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SectionExample.vb#sectioncodeonlyexamplewholepage)]

**BlockUIContainer**

<xref:System.Windows.Documents.BlockUIContainer> では、Block の派生フロー コンテンツに <xref:System.Windows.UIElement> 要素 (つまり、<xref:System.Windows.Controls.Button>) を埋め込めるようにします。 <xref:System.Windows.Documents.InlineUIContainer> (下記参照) は、Inline の派生フロー コンテンツに <xref:System.Windows.UIElement> 要素を埋め込むために使用されます。 <xref:System.Windows.Documents.BlockUIContainer> と <xref:System.Windows.Documents.InlineUIContainer> は重要です。これら 2 つの要素のいずれかに含まれない限り、フロー コンテンツで <xref:System.Windows.UIElement> を使用する方法は他にないためです。

次の例では、<xref:System.Windows.Documents.BlockUIContainer> 要素を使用して、フロー コンテンツ内の <xref:System.Windows.UIElement> オブジェクトをホストする方法を示しています。

[!code-xaml[SpanSnippets#_BlockUIXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml#_blockuixaml)]

次の図には、この例がどのようにレンダリングされるかが示されています。

![フロー コンテンツに埋め込まれた UIElement を示すスクリーンショット。](./media/flow-document-overview/embedded-blockuicontainer.png)

**List**

<xref:System.Windows.Documents.List> は、箇条書きまたは数値リストを作成するために使用されます。 <xref:System.Windows.Documents.List.MarkerStyle%2A> プロパティを <xref:System.Windows.TextMarkerStyle> 列挙値に設定して、リストのスタイルを決定します。 簡単なリストを作成する方法を次の例に示します。

[!code-xaml[FlowOvwSnippets_snip#ListExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ListExample.xaml#listexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ListExample.cs#listcodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ListExample.vb#listcodeonlyexamplewholepage)]

> [!NOTE]
> <xref:System.Windows.Documents.List> は、<xref:System.Windows.Documents.ListItemCollection> を使用して子要素を管理する唯一のフロー要素です。

**テーブル**

<xref:System.Windows.Documents.Table> は、テーブルを作成するために使用されます。 <xref:System.Windows.Documents.Table> は <xref:System.Windows.Controls.Grid> 要素に似ていますが、より多くの機能を備えているため、さらに多くのリソース オーバーヘッドが必要になります。 <xref:System.Windows.Controls.Grid> は <xref:System.Windows.UIElement> であるため、<xref:System.Windows.Documents.BlockUIContainer> または <xref:System.Windows.Documents.InlineUIContainer> に含まれている場合を除き、フロー コンテンツで使用することはできません。 <xref:System.Windows.Documents.Table> の詳細については、「[テーブルの概要](table-overview.md)」を参照してください。

### <a name="inline-derived-classes"></a>Inline の派生クラス

**実行**

<xref:System.Windows.Documents.Run> は、書式設定されていないテキストを含めるために使用されます。 フロー コンテンツでは、<xref:System.Windows.Documents.Run> オブジェクトを広範に使用することを想定している場合があります。 しかし、マークアップでは、<xref:System.Windows.Documents.Run> 要素を明示的に使用する必要はありません。 <xref:System.Windows.Documents.Run> は、コードを使用してフロー ドキュメントを作成または操作するときに使用する必要があります。 たとえば、以下のマークアップでは、最初の <xref:System.Windows.Documents.Paragraph> で <xref:System.Windows.Documents.Run> 要素が明示的に指定されますが、2 番目では指定されません。 両方の段落は、同じ出力を生成します。

[!code-xaml[FlowOvwSnippets_snip#RunExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/RunSnippetsExample.xaml#runexample1)]

> [!NOTE]
> .NET Framework 4 以降では、<xref:System.Windows.Documents.Run> オブジェクトの <xref:System.Windows.Documents.Run.Text%2A> プロパティは依存関係プロパティです。 <xref:System.Windows.Controls.TextBlock> などのデータ ソースに、<xref:System.Windows.Documents.Run.Text%2A> プロパティをバインドすることができます。 <xref:System.Windows.Documents.Run.Text%2A> プロパティでは、一方向のバインドが完全にサポートされます。 <xref:System.Windows.Documents.Run.Text%2A> プロパティでは、<xref:System.Windows.Controls.RichTextBox> を除き、双方向のバインドもサポートされます。 例については、「<xref:System.Windows.Documents.Run.Text%2A?displayProperty=nameWithType>」を参照してください。

**Span**

<xref:System.Windows.Documents.Span> では、他のインライン コンテンツ要素をまとめてグループ化します。 <xref:System.Windows.Documents.Span> 要素内のコンテンツには、固有のレンダリングは適用されません。 しかし、<xref:System.Windows.Documents.Hyperlink>、<xref:System.Windows.Documents.Bold>、<xref:System.Windows.Documents.Italic>、<xref:System.Windows.Documents.Underline> を含め、<xref:System.Windows.Documents.Span> から継承する要素では、書式設定がテキストに適用されます。

テキスト、<xref:System.Windows.Documents.Bold> 要素、<xref:System.Windows.Controls.Button> を含む、インライン コンテンツを含めるために使用されている <xref:System.Windows.Documents.Span> の例を以下に示します。

[!code-xaml[FlowOvwSnippets_snip#SpanExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SpanExample.xaml#spanexamplewholepage)]

次のスクリーンショットは、この例がどのように表示されるかを示しています。

![スクリーンショット: レンダリングされた Span の例](./media/flow-spanexample.gif "Flow_SpanExample")

**InlineUIContainer**

<xref:System.Windows.Documents.InlineUIContainer> では、<xref:System.Windows.UIElement> 要素 (つまり、<xref:System.Windows.Controls.Button> などのコントロール) を <xref:System.Windows.Documents.Inline> コンテンツ要素に埋め込めるようにします。 この要素は、前述の <xref:System.Windows.Documents.BlockUIContainer> に相当するインラインです。 <xref:System.Windows.Documents.InlineUIContainer> を使用して、<xref:System.Windows.Documents.Paragraph> に <xref:System.Windows.Controls.Button> インラインを挿入する例を以下に示します。

[!code-xaml[FlowOvwSnippets_snip#InlineUIContainerExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/InlineUIContainerExample.xaml#inlineuicontainerexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/InlineUIContainerExample.cs#inlineuicontainercodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/InlineUIContainerExample.vb#inlineuicontainercodeonlyexamplewholepage)]

> [!NOTE]
> <xref:System.Windows.Documents.InlineUIContainer> は、マークアップでは明示的に使用する必要はありません。 これを省略しても、コードがコンパイルされると <xref:System.Windows.Documents.InlineUIContainer> が作成されます。

**Figure および Floater**

<xref:System.Windows.Documents.Figure> と <xref:System.Windows.Documents.Floater> は、主要コンテンツ フローとは別にカスタマイズできる配置プロパティを持つフロー ドキュメント内にコンテンツを埋め込むために使用されます。 多くの場合、<xref:System.Windows.Documents.Figure> または <xref:System.Windows.Documents.Floater> 要素は、コンテンツの一部を強調表示したり、目立たせたりするため、メイン コンテンツ フロー内のサポート イメージや他のコンテンツをホストするため、または広告などの関連の薄いコンテンツを挿入するために使用されます。

次の例では、テキストの段落に <xref:System.Windows.Documents.Figure> を埋め込む方法を示します。

[!code-xaml[FlowOvwSnippets_snip#FigureExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/FigureExample.xaml#figureexamplewholepage)]

[!code-csharp[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/FigureExample.cs#figurecodeonlyexamplewholepage)]
[!code-vb[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/FigureExample.vb#figurecodeonlyexamplewholepage)]

この例がどのように表示されるかを次の図に示します。

![スクリーンショット: Figure の例](./media/flow-ovw-figure-example.png "Flow_Ovw_Figure_Example")

<xref:System.Windows.Documents.Figure> と <xref:System.Windows.Documents.Floater> はいくつかの点で異なり、異なるシナリオで使用されます。

**Figure:**

- 配置可能です。水平方向および垂直方向のアンカーを設定することによって、ページ、コンテンツ、列または段落に対して相対的にドッキングできます。 また、<xref:System.Windows.Documents.Figure.HorizontalOffset%2A> および <xref:System.Windows.Documents.Figure.VerticalOffset%2A> プロパティを使用して、任意のオフセットを指定することもできます。

- 複数の列にサイズを設定できます。<xref:System.Windows.Documents.Figure> の高さと幅は、ページ、コンテンツ、または列の高さや幅の倍数に設定できます。 ページおよびコンテンツの場合は、1 より大きい倍数は指定できない点に注意してください。 たとえば、<xref:System.Windows.Documents.Figure> の幅を "0.5 ページ"、"0.25 コンテンツ" または "2 列" に設定できます。 高さと幅は、絶対ピクセル値で指定することもできます。

- ページ割り付けは行いません。<xref:System.Windows.Documents.Figure> 内のコンテンツが <xref:System.Windows.Documents.Figure> 内に収まらない場合は、収まるコンテンツがすべてレンダリングされ、残りのコンテンツは失われます

**Floater:**

- 配置できません。必要なスペースを確保できる場所に描画されます。 <xref:System.Windows.Documents.Floater> のオフセットやアンカーを設定することはできません。

- 複数の列にサイズを設定することはできません。既定では、<xref:System.Windows.Documents.Floater> のサイズは 1 列になります。 絶対ピクセル値に設定できる <xref:System.Windows.Documents.Floater.Width%2A> プロパティがありますが、この値が 1 列の幅より大きい場合は無視され、浮遊要素のサイズは 1 列になります。 正しいピクセル幅を設定することによってサイズを 1 列未満にすることはできますが、列を基準とした相対的なサイズ指定はできないため、<xref:System.Windows.Documents.Floater> の幅に関しては "0.5 列" という表現は有効ではありません。 <xref:System.Windows.Documents.Floater> には高さのプロパティはなく、高さを設定することはできません。高さはコンテンツに依存します

- <xref:System.Windows.Documents.Floater> ではページ割り付けを行います。指定された幅のコンテンツが複数列の高さまで拡張されると、浮遊要素は分割されて、次の列、次のページなどにページ割り付けが行われます

 <xref:System.Windows.Documents.Figure> は、サイズや配置の制御を必要とし、指定サイズにコンテンツが収まることが確実なスタンドアロン コンテンツを配置する場合に適しています。 <xref:System.Windows.Documents.Floater> は、メイン ページのコンテンツと同様にフローするものの、それとは分離される、流動性の高いコンテンツを配置する場合に適しています。

**LineBreak**

<xref:System.Windows.Documents.LineBreak> を使用すると、フロー コンテンツで改行が行われます。 次の例は、<xref:System.Windows.Documents.LineBreak> の使い方を示しています。

[!code-xaml[FlowOvwSnippets_snip#LineBreakExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/LineBreakExample.xaml#linebreakexamplewholepage)]

次のスクリーンショットは、この例がどのように表示されるかを示しています。

![スクリーンショット: LineBreak の例](./media/flow-ovw-linebreakexample.png "Flow_Ovw_LineBreakExample")

### <a name="flow-collection-elements"></a>フロー コレクションの要素

上記の例の多くでは、プログラムでフロー コンテンツを構築するために、<xref:System.Windows.Documents.BlockCollection> と <xref:System.Windows.Documents.InlineCollection> が使用されています。 たとえば、<xref:System.Windows.Documents.Paragraph> に要素を追加する場合は、次の構文を使用できます。

```csharp
myParagraph.Inlines.Add(new Run("Some text"));
```

これにより、<xref:System.Windows.Documents.Run> が <xref:System.Windows.Documents.Paragraph> の <xref:System.Windows.Documents.InlineCollection> に追加されます。  これは、マークアップの <xref:System.Windows.Documents.Paragraph> の内部にある暗黙の <xref:System.Windows.Documents.Run> と同じです。

```xml
<Paragraph>
Some Text
</Paragraph>
```

<xref:System.Windows.Documents.BlockCollection> の使用例として、次の例では新しい <xref:System.Windows.Documents.Section> を作成してから、**Add** メソッドを使用して、新しい <xref:System.Windows.Documents.Paragraph> を <xref:System.Windows.Documents.Section> コンテンツに追加します。

[!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
[!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]

フロー コレクションに項目を追加できるだけでなく、項目を削除することもできます。  次の例では、<xref:System.Windows.Documents.Span> 内の最後の <xref:System.Windows.Documents.Inline> 要素を削除します。

[!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
[!code-vb[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]

次の例では、<xref:System.Windows.Documents.Span> からすべてのコンテンツ (<xref:System.Windows.Documents.Inline>) をクリアします。

[!code-csharp[SpanSnippets#_SpanInlinesClear](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
[!code-vb[SpanSnippets#_SpanInlinesClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]

フロー コンテンツをプログラムで操作する場合、これらのコレクションを広く活用する可能性があります。

フロー要素で、その子要素を含めるために <xref:System.Windows.Documents.InlineCollection> (インライン) と <xref:System.Windows.Documents.BlockCollection> (ブロック) のどちらを使用するかは、親で含めることができる子要素の種類 (<xref:System.Windows.Documents.Block> または <xref:System.Windows.Documents.Inline>) によって異なります。 フロー コンテンツ要素のコンテインメイト規則については、次のセクションのコンテンツ スキーマにまとめます。

> [!NOTE]
> フロー コンテンツで使用されるコレクションの 3 つ目の種類として <xref:System.Windows.Documents.ListItemCollection> がありますが、このコレクションは <xref:System.Windows.Documents.List> でのみ使用されます。 さらに、<xref:System.Windows.Documents.Table> で使用されるコレクションがいくつかあります。 詳細については、「[テーブルの概要](table-overview.md)」を参照してください。

<a name="content_schema"></a>

## <a name="content-schema"></a>コンテンツ スキーマ

多数のさまざまなフロー コンテンツ要素が指定されると、要素が格納できる子要素の種類を追跡できなくなる可能性があります。 フロー要素のコンテインメイト規則をまとめたものを次の図に示します。 矢印は、使用可能な親/子リレーションシップを表します。

![図:フロー コンテンツ コンテインメント スキーマ](./media/flow-content-schema.png "Flow_Content_Schema")

上の図からわかるように、要素で許容される子は、必ずしもそれが <xref:System.Windows.Documents.Block> 要素と <xref:System.Windows.Documents.Inline> 要素のどちらであるかによって決まるわけではありません。 たとえば、<xref:System.Windows.Documents.Span> (<xref:System.Windows.Documents.Inline> 要素) では <xref:System.Windows.Documents.Inline> 子要素のみを持つことができるのに対して、<xref:System.Windows.Documents.Figure> (同じく <xref:System.Windows.Documents.Inline> 要素) では <xref:System.Windows.Documents.Block> 子要素のみを持つことができます。 そのため、どの要素を別の要素に含めることができるかをすばやく判断するには、図が役立ちます。 例として、図を使用して、<xref:System.Windows.Controls.RichTextBox> のフロー コンテンツを構築する方法を判断してみましょう。

**1.** <xref:System.Windows.Controls.RichTextBox> には <xref:System.Windows.Documents.FlowDocument> が含まれている必要があり、さらにこれには <xref:System.Windows.Documents.Block> の派生オブジェクトが含まれている必要があります。 上の図でこれに対応する部分を次に示します。

![図:RichTextBox コンテインメント規則](./media/flow-ovw-schemawalkthrough1.png "Flow_Ovw_SchemaWalkThrough1")

この段階では、マークアップは次のようになります。

[!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough1](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]

**2.** 図によると、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.Table>、<xref:System.Windows.Documents.List>、<xref:System.Windows.Documents.BlockUIContainer> など、選択できる <xref:System.Windows.Documents.Block> 要素がいくつかあります (上記の Block の派生クラスを参照)。 たとえば、<xref:System.Windows.Documents.Table> が必要だとします。 上の図によると、<xref:System.Windows.Documents.Table> には <xref:System.Windows.Documents.TableRowGroup> が含まれており、それには <xref:System.Windows.Documents.TableRow> 要素が含まれています。さらにこれには <xref:System.Windows.Documents.TableCell> 要素が含まれており、それには <xref:System.Windows.Documents.Block> の派生オブジェクトが含まれています。 上の図で <xref:System.Windows.Documents.Table> に対応するセグメントを、以下に示します。

![図:Table の親/子のスキーマ](./media/flow-ovw-schemawalkthrough2.png "Flow_Ovw_SchemaWalkThrough2")

以下は、これに対応するマークアップです。

[!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough2](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]

**3.** ここでも、<xref:System.Windows.Documents.TableCell> の下に 1 つまたは複数の <xref:System.Windows.Documents.Block> 要素が必要です。 簡単にするために、セル内にいくつかのテキストを配置することにします。 これは、<xref:System.Windows.Documents.Paragraph> を <xref:System.Windows.Documents.Run> 要素と共に使用することで行うことができます。 <xref:System.Windows.Documents.Paragraph> で <xref:System.Windows.Documents.Inline> 要素を受け取ることができ、<xref:System.Windows.Documents.Run> (<xref:System.Windows.Documents.Inline> 要素) でプレーンテキストのみを受け取れることを示す図の対応するセグメントを以下に示します。

![図:Paragraph の親/子スキーマ](./media/flow-ovw-schemawalkthrough3.png "Flow_Ovw_SchemaWalkThrough3")

![図:Run の親/子スキーマ](./media/flow-ovw-schemawalkthrough4.png "Flow_Ovw_SchemaWalkThrough4")

以下は、マークアップでの例の全体です。

[!code-xaml[FlowOvwSnippets_snip#SchemaExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]

<a name="customizing_text"></a>

## <a name="customizing-text"></a>テキストのカスタマイズ

通常、テキストは、フロー ドキュメントで最も一般的なコンテンツの種類です。 上で導入されたオブジェクトは、テキストをレンダリングする方法のほとんどの側面を制御するために使用できますが、このセクションで説明されるテキストのカスタマイズ用にその他のメソッドがいくつか存在します。

### <a name="text-decorations"></a>文字装飾

文字装飾によって、下線、上線、ベースライン、および取り消し線の効果をテキストに適用できます (下図参照)。 これらの装飾は、<xref:System.Windows.Documents.Inline>、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Controls.TextBlock>、<xref:System.Windows.Controls.TextBox> を含む多数のオブジェクトによって公開される、<xref:System.Windows.Documents.Inline.TextDecorations%2A> プロパティを使用して追加されます。

<xref:System.Windows.Documents.Paragraph.TextDecorations%2A> の <xref:System.Windows.Documents.Paragraph> プロパティを設定する方法を次の例に示します。

[!code-xaml[InlineSnippets#_Paragraph_TextDecXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml#_paragraph_textdecxaml)]

[!code-csharp[InlineSnippets#_Paragraph_TextDec](~/samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml.cs#_paragraph_textdec)]
[!code-vb[InlineSnippets#_Paragraph_TextDec](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InlineSnippets/visualbasic/window1.xaml.vb#_paragraph_textdec)]

この例の表示結果を次の図に示します。

![スクリーンショット: 既定の取り消し線効果が適用されたテキスト](./media/inline-textdec-strike.png "Inline_TextDec_Strike")

次の図には、それぞれ**上線**、**ベースライン**、**下線**の各装飾がどのようにレンダリングされるかが示されています。

![スクリーンショット: TextDecorator の上に線を引く](./media/inline-textdec-over.png "Inline_TextDec_Over")

![スクリーンショット: テキストに対する既定のベースライン効果](./media/inline-textdec-base.png "Inline_TextDec_Base")

![スクリーンショット: 既定の下線効果が適用されたテキスト](./media/inline-textdec-under.png "Inline_TextDec_Under")

### <a name="typography"></a>タイポグラフィ

<xref:System.Windows.Documents.TextElement.Typography%2A> プロパティは、<xref:System.Windows.Documents.TextElement>、<xref:System.Windows.Documents.FlowDocument>、<xref:System.Windows.Controls.TextBlock>、<xref:System.Windows.Controls.TextBox> を含むほとんどのフロー関連のコンテンツによって公開されます。 このプロパティは、テキストの文字体裁の特性またはバリエーション (つまり、小さい大文字か大きい大文字か、上付き文字と下付き文字の作成など) を制御するために使用されます。

次の例では、<xref:System.Windows.Documents.Paragraph> を例の要素として使用して、<xref:System.Windows.Documents.TextElement.Typography%2A> 属性を設定する方法が示されています。

[!code-xaml[TextElementSnippets#_TextElement_TypogXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]

この例の表示結果を次の図に示します。

![スクリーンショット: 文字体裁に変更があるテキスト](./media/textelement-typog.png "TextElement_Typog")

これに対し、既定の文字体裁プロパティを設定した同様の例がどのように表示されるかを次の図に示します。

![スクリーンショット: 文字体裁に変更があるテキスト](./media/textelement-typog-default.png "TextElement_Typog_Default")

次の例では、<xref:System.Windows.Controls.TextBox.Typography%2A> プロパティをプログラムで設定する方法が示されています。

[!code-csharp[TextElementSnippets#_TextElement_Typog](~/samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
[!code-vb[TextElementSnippets#_TextElement_Typog](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]

文字体裁の詳細については、「[WPF のタイポグラフィ](typography-in-wpf.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [[テキスト]](optimizing-performance-text.md)
- [WPF のタイポグラフィ](typography-in-wpf.md)
- [方法トピック](flow-content-elements-how-to-topics.md)
- [TextElement コンテンツ モデルの概要](textelement-content-model-overview.md)
- [RichTextBox の概要](../controls/richtextbox-overview.md)
- [WPF のドキュメント](documents-in-wpf.md)
- [テーブルの概要](table-overview.md)
- [注釈の概要](annotations-overview.md)
