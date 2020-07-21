---
title: TextElement コンテンツ モデルの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], flow documents
- TextElement content model [WPF]
- flow content elements [WPF], TextElement content model
ms.assetid: d0a7791c-b090-438c-812f-b9d009d83ee9
ms.openlocfilehash: ddb2613dc924424b5f4b9d90f06d44b45b7b5e77
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186905"
---
# <a name="textelement-content-model-overview"></a>TextElement コンテンツ モデルの概要
このコンテンツ モデルの概要では、<xref:System.Windows.Documents.TextElement> でサポートされるコンテンツについて説明します。 <xref:System.Windows.Documents.Paragraph> クラスは <xref:System.Windows.Documents.TextElement> 型です。 コンテンツ モデルは、他のオブジェクトや要素に含めることのできるオブジェクトや要素を記述します。 ここでは、<xref:System.Windows.Documents.TextElement> から派生したオブジェクトに対して使用されるコンテンツ モデルの概要を示します。 詳細については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください。  

<a name="text_element_classes"></a>
## <a name="content-model-diagram"></a>コンテンツ モデルの図  
 <xref:System.Windows.Documents.TextElement> から派生したクラスのコンテンツ モデルと、このモデルにその他の `TextElement` 以外のクラスがどのように適用されるかについてまとめたものを、次の図に示します。  
  
 ![図:フロー コンテンツ コンテインメント スキーマ](./media/flow-content-schema.png "Flow_Content_Schema")  
  
 上の図からわかるように、要素で許容される子は、必ずしもクラスが <xref:System.Windows.Documents.Block> クラスと <xref:System.Windows.Documents.Inline> クラスのどちらから派生したかによって決まるわけではありません。 たとえば、<xref:System.Windows.Documents.Span> (<xref:System.Windows.Documents.Inline> の派生クラス) は <xref:System.Windows.Documents.Inline> 子要素だけを持つことができるのに対し、<xref:System.Windows.Documents.Figure> (同じく <xref:System.Windows.Documents.Inline> の派生クラス) は <xref:System.Windows.Documents.Block> 子要素だけを持つことができます。 そのため、どの要素を別の要素に含めることができるかをすばやく判断するには、図が役立ちます。 例として、図を使用して、<xref:System.Windows.Controls.RichTextBox> のフロー コンテンツを構築する方法を判断してみましょう。  
  
1. <xref:System.Windows.Controls.RichTextBox> には <xref:System.Windows.Documents.FlowDocument> が含まれている必要があり、さらにこれには <xref:System.Windows.Documents.Block> の派生オブジェクトが含まれている必要があります。 上の図に対応するセグメントを次に示します。  
  
     ![図:RichTextBox コンテインメント規則](./media/flow-ovw-schemawalkthrough1.png "Flow_Ovw_SchemaWalkThrough1")  
  
     この段階では、マークアップは次のようになります。  
  
     [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough1](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]  
  
2. 上の図によると、<xref:System.Windows.Documents.Block> 要素には、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.Table>、<xref:System.Windows.Documents.List>、<xref:System.Windows.Documents.BlockUIContainer> など、いくつかの選択肢があります (上の図の Block の派生クラスを参照)。 たとえば、<xref:System.Windows.Documents.Table> が必要だとします。 上の図によると、<xref:System.Windows.Documents.Table> には <xref:System.Windows.Documents.TableRowGroup> が含まれ、それには <xref:System.Windows.Documents.TableRow> が含まれ、それには <xref:System.Windows.Documents.TableCell> が含まれ、それには<xref:System.Windows.Documents.Block> 派生オブジェクトが含まれています。 上の図の <xref:System.Windows.Documents.Table> に対応する部分を次に示します。  
  
     ![図:テーブルの親&#47;子スキーマ](./media/flow-ovw-schemawalkthrough2.png "Flow_Ovw_SchemaWalkThrough2")  
  
     対応するマークアップは次のとおりです。  
  
     [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough2](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]  
  
3. ここでも、<xref:System.Windows.Documents.TableCell> の下には 1 つまたは複数の <xref:System.Windows.Documents.Block> 要素が必要です。 簡単にするために、セル内にいくつかのテキストを配置することにします。 これは、<xref:System.Windows.Documents.Paragraph> を <xref:System.Windows.Documents.Run> 要素と共に使用することで行うことができます。 上の図でこれに対応する部分を次に示します。<xref:System.Windows.Documents.Paragraph> は <xref:System.Windows.Documents.Inline> 要素を取ることができ、<xref:System.Windows.Documents.Run> (<xref:System.Windows.Documents.Inline> 要素) はプレーンテキストのみを取ることができることが示されています。  
  
     ![図:段落の親&#47;子スキーマ](./media/flow-ovw-schemawalkthrough3.png "Flow_Ovw_SchemaWalkThrough3")  
  
     ![図:実行の親&#47;子スキーマ](./media/flow-ovw-schemawalkthrough4.png "Flow_Ovw_SchemaWalkThrough4")  
  
 例全体をマークアップで次に示します。  
  
 [!code-xaml[FlowOvwSnippets_snip#SchemaExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]  
  
<a name="Using_the_Content_Property"></a>
## <a name="working-with-textelement-content-programmatically"></a>TextElement のコンテンツをプログラムで操作する  
 <xref:System.Windows.Documents.TextElement> のコンテンツはコレクションで構成されているため、<xref:System.Windows.Documents.TextElement> オブジェクトのコンテンツをプログラムで操作するには、これらのコレクションを操作します。 <xref:System.Windows.Documents.TextElement> の派生クラスで使用されるコレクションには、次の 3 種類があります。  
  
- <xref:System.Windows.Documents.InlineCollection>:<xref:System.Windows.Documents.Inline> 要素のコレクションを表します。 <xref:System.Windows.Documents.InlineCollection> は、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Span>、<xref:System.Windows.Controls.TextBlock> の要素の使用できる子コンテンツを定義します。  
  
- <xref:System.Windows.Documents.BlockCollection>:<xref:System.Windows.Documents.Block> 要素のコレクションを表します。 <xref:System.Windows.Documents.BlockCollection> は <xref:System.Windows.Documents.FlowDocument>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.ListItem>、<xref:System.Windows.Documents.TableCell>、<xref:System.Windows.Documents.Floater>、<xref:System.Windows.Documents.Figure> 要素で許容される子コンテンツを定義します。  
  
- <xref:System.Windows.Documents.ListItemCollection>:順序付きの、または順序付きでない <xref:System.Windows.Documents.List> 内の特定のコンテンツ項目を表すフロー コンテンツ要素。  
  
 これらのコレクションを操作 (項目を追加または削除) するには、**Inlines**、**Blocks**、**ListItems** のそれぞれのプロパティを使用します。 Span のコンテンツを **Inlines** プロパティを使用して操作する方法を次の例に示します。  
  
> [!NOTE]
> Table では、コンテンツの操作にいくつかのコレクションが使用されますが、これらのコレクションについてはここでは取り上げません。 詳細については、「[テーブルの概要](table-overview.md)」を参照してください。  
  
 次の例では、新しい <xref:System.Windows.Documents.Span> オブジェクトを作成した後、`Add` メソッドを使用して、2 つのテキスト ランを <xref:System.Windows.Documents.Span> のコンテンツの子として追加します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
 次の例では、新しい <xref:System.Windows.Documents.Run> 要素を作成し、それを <xref:System.Windows.Documents.Span> の先頭に挿入します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
 次の例では、<xref:System.Windows.Documents.Span> 内の最後の <xref:System.Windows.Documents.Inline> 要素を削除します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
 次の例では、<xref:System.Windows.Documents.Span> からすべてのコンテンツ (<xref:System.Windows.Documents.Inline> 要素) をクリアします。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
<a name="Types_that_Share_this_Content_Model"></a>
## <a name="types-that-share-this-content-model"></a>このコンテンツ モデルを共有する種類  
 次に示す型は、<xref:System.Windows.Documents.TextElement> クラスから継承され、この概要で説明したコンテンツを表示するために使用できます。  
  
 <xref:System.Windows.Documents.Bold>、<xref:System.Windows.Documents.Figure>、<xref:System.Windows.Documents.Floater>、<xref:System.Windows.Documents.Hyperlink>、<xref:System.Windows.Documents.InlineUIContainer>、<xref:System.Windows.Documents.Italic>、<xref:System.Windows.Documents.LineBreak>、<xref:System.Windows.Documents.List>、<xref:System.Windows.Documents.ListItem>、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Run>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.Span>、<xref:System.Windows.Documents.Table>、<xref:System.Windows.Documents.Underline>。  
  
 この一覧には、Windows SDK と共に配布される非抽象型しか含まれていません。 <xref:System.Windows.Documents.TextElement> を継承するその他の種類も使用できます。  
  
<a name="Types_that_Can_Contain_ContentControl_Objects"></a>
## <a name="types-that-can-contain-textelement-objects"></a>TextElement オブジェクトを含むことのできる型  
 「[WPF のコンテンツ モデル](../controls/wpf-content-model.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Blocks プロパティを介して FlowDocument を操作する](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Blocks プロパティを介してフロー コンテンツ要素を操作する](how-to-manipulate-flow-content-elements-through-the-blocks-property.md)
- [Blocks プロパティを介して FlowDocument を操作する](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Columns プロパティによってテーブルの列を操作する](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
