---
title: '方法: Inlines プロパティを介してフロー コンテンツ要素を操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flow content elements [WPF], manipulating through Inlines property
- documents [WPF], manipulating flow Content elements through Inlines property
- Inlines property [WPF], manipulating flow Content elements
- properties [WPF], Inlines [WPF], manipulating flow Content elements
ms.assetid: 510780d2-3da1-4360-8763-7054bda22ea3
ms.openlocfilehash: 92f23fbf44464eb7658f3382f873f3db63f7cb26
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614577"
---
# <a name="how-to-manipulate-flow-content-elements-through-the-inlines-property"></a>方法: Inlines プロパティを介してフロー コンテンツ要素を操作する
この例では、**Inlines** プロパティを介して、インライン フロー コンテンツ要素 (および <xref:System.Windows.Controls.TextBlock> などの、そのような要素のコンテナー) に対して実行できる一般的な操作をいくつか示します。 このプロパティは、<xref:System.Windows.Documents.InlineCollection> の項目を追加および削除するために使用されます。 **Inlines** プロパティを使用するフロー コンテンツ要素には、次のようなものがあります。  
  
- <xref:System.Windows.Documents.Bold>  
  
- <xref:System.Windows.Documents.Hyperlink>  
  
- <xref:System.Windows.Documents.Italic>  
  
- <xref:System.Windows.Documents.Paragraph>  
  
- <xref:System.Windows.Documents.Span>  
  
- <xref:System.Windows.Documents.Underline>  
  
 この例では、フロー コンテンツ要素として <xref:System.Windows.Documents.Span> が使用されることがありますが、これらの手法は、<xref:System.Windows.Documents.InlineCollection> コレクションをホストするすべての要素またはコントロールに適用できます。  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.Span> オブジェクトを作成し、**Add** メソッドを使用して、<xref:System.Windows.Documents.Span> のコンテンツの子として 2 つのテキスト実行を追加します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.Run> 要素を作成し、それを <xref:System.Windows.Documents.Span> の先頭に挿入します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Span> に含まれる最上位レベルの <xref:System.Windows.Documents.Inline> 要素の数を取得します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesCount](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinescount)]
 [!code-vb[SpanSnippets#_SpanInlinesCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinescount)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Span> 内の最後の <xref:System.Windows.Documents.Inline> 要素を削除します。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Span> からすべてのコンテンツ (<xref:System.Windows.Documents.Inline> 要素) をクリアします。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Documents.BlockCollection>
- <xref:System.Windows.Documents.InlineCollection>
- <xref:System.Windows.Documents.ListItemCollection>
- [フロー ドキュメントの概要](flow-document-overview.md)
- [Blocks プロパティを介して FlowDocument を操作する](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Columns プロパティによってテーブルの列を操作する](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
