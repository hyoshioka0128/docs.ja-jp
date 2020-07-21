---
title: TextBlock の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], TextBlock
- TextBlock control [WPF]
ms.assetid: 24720bca-341a-4b03-8a6b-7a678023b10a
ms.openlocfilehash: ce7da2b9c9c8e2a3a24d3acf18396ca447ac3f27
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61791015"
---
# <a name="textblock-overview"></a>TextBlock の概要
<xref:System.Windows.Controls.TextBlock> コントロールは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでより柔軟にテキストを使用できるようにします。 この要素は、主として、複数段落のテキストを必要としない、基本的な [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] シナリオを対象にしています。 これでは、<xref:System.Windows.Controls.TextBlock.FontFamily%2A>、<xref:System.Windows.Controls.TextBlock.FontSize%2A>、<xref:System.Windows.Controls.TextBlock.FontWeight%2A>、<xref:System.Windows.Controls.TextBlock.TextEffects%2A>、<xref:System.Windows.Controls.TextBlock.TextWrapping%2A> など、表示を細かく制御できるプロパティが多数サポートされています。 テキスト コンテンツを追加するには、<xref:System.Windows.Controls.TextBlock.Text%2A> プロパティを使用します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で使用すると、オープン タグとクローズ タグの間の内容は、要素のテキストとして暗黙的に追加されます。  
  
 <xref:System.Windows.Controls.TextBlock> 要素は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して非常に簡単にインスタンス化できます。  
  
 [!code-xaml[TextBlockSnip_XAML#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBlockSnip_XAML/CS/default.xaml#2)]  
  
 同様にコードで <xref:System.Windows.Controls.TextBlock> 要素も比較的簡単に使用できます。  
  
 [!code-csharp[TextBlockSnip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBlockSnip/CSharp/TextBlockSnips.cs#1)]
 [!code-vb[TextBlockSnip#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBlockSnip/VisualBasic/TextBlockSnips.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Label>
