---
title: '方法: Blocks プロパティを介して FlowDocument を操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'documents [WPF], manipulating FlowDocuments through Blocks property [WPF], , '
- ', '
ms.assetid: cbb7291e-3f1b-433e-9e16-f4d93ced14e8
ms.openlocfilehash: c307d85bf24e2d8a20226856181e0758758d40c0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051508"
---
# <a name="how-to-manipulate-a-flowdocument-through-the-blocks-property"></a>方法: Blocks プロパティを介して FlowDocument を操作する
この例では、<xref:System.Windows.Documents.FlowDocument.Blocks%2A> プロパティを介して <xref:System.Windows.Documents.FlowDocument> に対して実行できる一般的な操作をいくつか示します。  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.FlowDocument> が作成され、新しい <xref:System.Windows.Documents.Paragraph> 要素が <xref:System.Windows.Documents.FlowDocument> に追加されます。  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksadd)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksadd)]  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.Paragraph> 要素を作成し、それを <xref:System.Windows.Documents.FlowDocument> の先頭に挿入します。  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksinsert)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksinsert)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.FlowDocument> に含まれる最上位レベルの <xref:System.Windows.Documents.Block> 要素の数を取得します。  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksCount](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblockscount)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblockscount)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.FlowDocument> 内の最後の <xref:System.Windows.Documents.Block> 要素を削除します。  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksremovelast)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksremovelast)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.FlowDocument> からすべてのコンテンツ (<xref:System.Windows.Documents.Block> 要素) をクリアします。  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksClear](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksclear)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksclear)]  
  
## <a name="see-also"></a>関連項目

- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Columns プロパティによってテーブルの列を操作する](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
