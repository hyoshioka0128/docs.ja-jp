---
title: '方法: ScrollViewer のコンテンツ スクロール メソッドを使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IScrollInfo interface [WPF]
- scrolling methods [WPF]
- ScrollViewer control [WPF], scrolling methods
ms.assetid: 4708cc65-6510-45f8-82e6-30b0d3e30045
ms.openlocfilehash: e81c63de16d09de8435d5ec49a013bf8dc5927cd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61697306"
---
# <a name="how-to-use-the-content-scrolling-methods-of-scrollviewer"></a>方法: ScrollViewer のコンテンツ スクロール メソッドを使用する
この例は、<xref:System.Windows.Controls.ScrollViewer> 要素のスクロール メソッドを使用する方法を示します。 これらのメソッドにより、<xref:System.Windows.Controls.ScrollViewer> での、行またはページごとのコンテンツの増分スクロールが可能になります。  
  
## <a name="example"></a>例  
 次の例は、子 <xref:System.Windows.Controls.TextBlock> 要素をホストする `sv1` という名前の <xref:System.Windows.Controls.ScrollViewer> を作成しています。 <xref:System.Windows.Controls.TextBlock> が親 <xref:System.Windows.Controls.ScrollViewer> より大きいため、スクロールを有効にするためのスクロール バーが表示されます。 さまざまなスクロール メソッドを表す <xref:System.Windows.Controls.Button> 要素は、左側に個別の <xref:System.Windows.Controls.StackPanel> としてドッキングされます。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル内の各 <xref:System.Windows.Controls.Button> は、<xref:System.Windows.Controls.ScrollViewer> のスクロール動作を制御する、関連のカスタム メソッドを呼び出します。  
  
 [!code-xaml[ScrollViewerMethods#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml#1)]  
  
 次の例では、<xref:System.Windows.Controls.ScrollViewer.LineUp%2A> メソッドと <xref:System.Windows.Controls.ScrollViewer.LineDown%2A> メソッドを使用しています。  
  
 [!code-csharp[ScrollViewerMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ScrollViewerMethods#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewerMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.StackPanel>
