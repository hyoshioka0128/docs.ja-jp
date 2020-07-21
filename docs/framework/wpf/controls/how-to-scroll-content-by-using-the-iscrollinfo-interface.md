---
title: '方法: IScrollInfo インターフェイスを使用してコンテンツをスクロールする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ScrollViewer control [WPF], scrolling content
- scrolling content [WPF]
- IScrollInfo interface [WPF]
ms.assetid: d8700bef-a3f8-4c12-9de2-fc3b79f32cd3
ms.openlocfilehash: 6ebd8268e1358b45709885c07e6b096d5f806ebb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051248"
---
# <a name="how-to-scroll-content-by-using-the-iscrollinfo-interface"></a>方法: IScrollInfo インターフェイスを使用してコンテンツをスクロールする
この例では、<xref:System.Windows.Controls.Primitives.IScrollInfo> インターフェイスを使用し、コンテンツをスクロールする方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.Primitives.IScrollInfo> インターフェイスの機能を示します。 この例では、親 <xref:System.Windows.Controls.ScrollViewer> で入れ子になっている [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で <xref:System.Windows.Controls.StackPanel> 要素が作成されます。 <xref:System.Windows.Controls.StackPanel> の子要素は、<xref:System.Windows.Controls.Primitives.IScrollInfo> インターフェイスで定義されているメソッドを利用することで論理的にスクロールできます。また、コードで <xref:System.Windows.Controls.StackPanel> のインスタンスにキャストされます (`sp1`)。  
  
 [!code-xaml[IScrollInfoMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml#2)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル内の各 <xref:System.Windows.Controls.Button> によって、<xref:System.Windows.Controls.StackPanel> のスクロール動作を制御する関連カスタム メソッドがトリガーされます。 次の例では、<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> メソッドと <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A> メソッドの使用方法を示します。<xref:System.Windows.Controls.Primitives.IScrollInfo> クラスによって定義されるあらゆる配置メソッドの一般的な使用方法もわかります。  
  
 [!code-csharp[IScrollInfoMethods#3](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.Primitives.IScrollInfo>
- <xref:System.Windows.Controls.StackPanel>
- [ScrollViewer の概要](scrollviewer-overview.md)
- [方法トピック](scrollviewer-how-to-topics.md)
- [パネルの概要](panels-overview.md)
