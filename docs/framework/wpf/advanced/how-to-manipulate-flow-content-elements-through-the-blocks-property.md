---
title: '方法: Blocks プロパティを介してフロー コンテンツ要素を操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], manipulating flow content elements through Blocks property
- flow content elements [WPF], manipulating through Blocks property
- properties [WPF], Blocks [WPF], manipulating flow content elements
- Blocks property [WPF], manipulating flow content elements
ms.assetid: aeda4ece-b979-4818-a093-ef938e908751
ms.openlocfilehash: 3ca05590bd1adf7f9c486382a08cb334b4731ac9
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614612"
---
# <a name="how-to-manipulate-flow-content-elements-through-the-blocks-property"></a>方法: Blocks プロパティを介してフロー コンテンツ要素を操作する
この例では、**Blocks** プロパティを介して、フロー コンテンツ要素に対して実行できる一般的な操作をいくつか示します。 このプロパティは、<xref:System.Windows.Documents.BlockCollection> の項目を追加および削除するために使用されます。 **Blocks** プロパティを使用するフロー コンテンツ要素には、次のようなものがあります。  
  
- <xref:System.Windows.Documents.Figure>  
  
- <xref:System.Windows.Documents.Floater>  
  
- <xref:System.Windows.Documents.ListItem>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.TableCell>  
  
 この例では、フロー コンテンツ要素として <xref:System.Windows.Documents.Section> が使用されることがありますが、これらの手法は、フロー コンテンツ要素コレクションをホストするすべての要素に適用できます。  
  
## <a name="example"></a>例  
 次の例では新しい <xref:System.Windows.Documents.Section> を作成してから、**Add** メソッドを使用して、新しい段落を **Section** コンテンツに追加します。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.Paragraph> 要素を作成し、それを <xref:System.Windows.Documents.Section> の先頭に挿入します。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksinsert)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksinsert)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Section> に含まれる最上位レベルの <xref:System.Windows.Documents.Block> 要素の数を取得します。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksCount](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblockscount)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblockscount)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Section> 内の最後の <xref:System.Windows.Documents.Block> 要素を削除します。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksremovelast)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksremovelast)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.Section> からすべてのコンテンツ (<xref:System.Windows.Documents.Block> 要素) をクリアします。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksClear](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksclear)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksclear)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Documents.BlockCollection>
- <xref:System.Windows.Documents.InlineCollection>
- <xref:System.Windows.Documents.ListItemCollection>
- [フロー ドキュメントの概要](flow-document-overview.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Columns プロパティによってテーブルの列を操作する](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
