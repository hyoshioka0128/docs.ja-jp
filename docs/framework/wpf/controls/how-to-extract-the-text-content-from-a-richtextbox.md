---
title: '方法: RichTextBox からテキスト コンテンツを抽出する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text content [WPF], extracting
- RichTextBox control [WPF], extracting text content
- content [WPF], extracting
- extracting text content [WPF]
ms.assetid: f13c093f-1a05-45b3-ac8f-c9ea5e4a11c5
ms.openlocfilehash: 220da59ec893528c99014e9ec95fb185c461b291
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001703"
---
# <a name="how-to-extract-the-text-content-from-a-richtextbox"></a>方法: RichTextBox からテキスト コンテンツを抽出する
この例では、<xref:System.Windows.Controls.RichTextBox> のコンテンツをプレーンテキストとして抽出する方法を示します。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] コードでは、単純コンテンツが含まれる名前付き <xref:System.Windows.Controls.RichTextBox> コントロールについて説明します。  
  
 [!code-xaml[RichTextBoxSnippets#_RTB_XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml#_rtb_xaml)]  
  
## <a name="example"></a>例  
 次のコードでは、引数として <xref:System.Windows.Controls.RichTextBox> を受け取り、<xref:System.Windows.Controls.RichTextBox> のプレーンテキスト コンテンツを表す文字列を返すメソッドを実装します。  
  
 このメソッドでは、<xref:System.Windows.Controls.RichTextBox> のコンテンツから新しい <xref:System.Windows.Documents.TextRange> を作成し、<xref:System.Windows.Documents.FlowDocument.ContentStart%2A> と <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> を使用して、抽出するコンテンツの範囲を示します。  <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> プロパティと <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> プロパティはそれぞれ <xref:System.Windows.Documents.TextPointer> を返し、<xref:System.Windows.Controls.RichTextBox> のコンテンツを表す、基になる FlowDocument からアクセスできます。  <xref:System.Windows.Documents.TextRange> は、Text プロパティを提供し、これにより、<xref:System.Windows.Documents.TextRange> のプレーンテキスト部分が文字列として返されます。  
  
 [!code-csharp[RichTextBoxSnippets#_RTB_StringFrom](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml.cs#_rtb_stringfrom)]
 [!code-vb[RichTextBoxSnippets#_RTB_StringFrom](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxSnippets/visualbasic/window1.xaml.vb#_rtb_stringfrom)]  
  
## <a name="see-also"></a>関連項目

- [RichTextBox の概要](richtextbox-overview.md)
- [TextBox の概要](textbox-overview.md)
