---
title: '方法: 段落間の間隔を調整する'
ms.date: 03/30/2017
helpviewer_keywords:
- spacing between paragraphs [WPF]
- paragraphs [WPF], spacing between
- documents [WPF], adjusting spacing between paragraphs
ms.assetid: 7cd2f2ac-0e19-4587-bfb6-7f5b18c9536e
ms.openlocfilehash: e2a6ba34e3ab15eb316671fef7c11bea03d53c73
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777014"
---
# <a name="how-to-adjust-spacing-between-paragraphs"></a>方法: 段落間の間隔を調整する
この例では、フロー コンテンツ内の段落間の間隔を調整または削除する方法を示しています。  
  
 フロー コンテンツでは、段落に設定した余白に応じて、段落間に余分なスペースが表示されます。つまり、それらの段落間の間隔を調整することで、段落間の間隔を制御できます。  2 つの段落間の余分なスペースを全体でなくすには、段落の余白を **0** に設定します。  <xref:System.Windows.Documents.FlowDocument> 全体で段落間の間隔を同じにするには、スタイルを使用して、<xref:System.Windows.Documents.FlowDocument> 内のすべての段落に同じ余白値を設定します。  
  
 2 つの隣接する段落の余白は、倍になるのではなく、2 つの余白の大きい方に "折りたたまれる" という点にご注意ください。 つまり、2 つの隣接する段落の余白がそれぞれ 20 ピクセルと 40 ピクセルであった場合、段落間の間隔は 2 つの余白の大きい方の 40 ピクセルになります。  
  
## <a name="example"></a>例  
 次の例では、スタイルを使用して、<xref:System.Windows.Documents.FlowDocument> 内のすべての <xref:System.Windows.Documents.Paragraph> 要素の余白を **0** に設定しています。これにより、<xref:System.Windows.Documents.FlowDocument> の段落間の余分な間隔は実質的になくなります。  
  
 [!code-xaml[BlockSnippets#_ParagraphSpacingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/BlockSnippets/CSharp/Window1.xaml#_paragraphspacingxaml)]
