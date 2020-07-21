---
title: '方法: ScrollChanged イベントの処理'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ScrollViewer control [WPF], raising ScrollChanged events
- ScrollChanged events [WPF]
ms.assetid: 42c695d8-ee28-49d4-80fd-fc71e9be7f29
ms.openlocfilehash: 54f20a4b8c6e6fcc190257fcf5de4374415d68b4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771060"
---
# <a name="how-to-handle-the-scrollchanged-event"></a>方法: ScrollChanged イベントの処理
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Controls.ScrollViewer> の <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> イベントを処理する方法を示します。  
  
 <xref:System.Windows.Documents.Paragraph> パーツを持つ <xref:System.Windows.Documents.FlowDocument> 要素は [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で定義されます。 ユーザーの操作によって <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> イベントが発生すると、ハンドラーが呼び出され、イベントが発生したことを示すテキストが <xref:System.Windows.Controls.TextBlock> に書き込まれます。  
  
 [!code-xaml[scrollchangedeventargsLayout#1](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#1)]  
[!code-xaml[scrollchangedeventargsLayout#2](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[scrollchangedeventargsLayout#3](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml.cs#3)]
 [!code-vb[scrollchangedeventargsLayout#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/scrollchangedeventargsLayout/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.ScrollViewer.ScrollChanged>
- <xref:System.Windows.Controls.ScrollChangedEventHandler>
- <xref:System.Windows.Controls.ScrollChangedEventArgs>
