---
title: '方法: ScrollViewer を持つエキスパンダーを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Expander
- ScrollViewer control [WPF], with Expander control
- Expander control [WPF], creating
- controls [WPF], ScrollViewer
ms.assetid: 2ad124d2-2406-4157-aaf2-64e067298f01
ms.openlocfilehash: ef0bc5d344f7d465de9209708430d3e61d40d4f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910794"
---
# <a name="how-to-create-an-expander-with-a-scrollviewer"></a>方法: ScrollViewer を持つエキスパンダーを作成する
この例では、画像やテキストなど、複雑なコンテンツが含まれる <xref:System.Windows.Controls.Expander> コントロールを作成する方法を示します。 この例ではまた、<xref:System.Windows.Controls.Expander> のコンテンツが <xref:System.Windows.Controls.ScrollViewer> コントロールに入ります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Expander> を作成する方法を次のコード サンプルに示します。 この例では、<xref:System.Windows.Controls.HeaderedContentControl.Header%2A> を定義する目的で、画像とテキストが含まれる <xref:System.Windows.Controls.Primitives.BulletDecorator> コントロールが使用されます。 <xref:System.Windows.Controls.ScrollViewer> コントロールからは、展開したコンテンツをスクロールする手段が与えられます。  
  
 この例では、コンテンツではなく <xref:System.Windows.Controls.ScrollViewer> で <xref:System.Windows.FrameworkElement.Height%2A> プロパティが設定されることに注目してください。 <xref:System.Windows.FrameworkElement.Height%2A> がコンテンツで設定される場合、ユーザーがコンテンツをスクロールすることが <xref:System.Windows.Controls.ScrollViewer> で許可されることはありません。 <xref:System.Windows.FrameworkElement.Width%2A> プロパティは <xref:System.Windows.Controls.Expander> コントロールに設定され、この設定が <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> と展開されたコンテンツに適用されます。  
  
 [!code-xaml[ExpanderRichContent#CreateExpander](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#createexpander)]  
  
 [!code-csharp[ExpanderRichContent#CreateExpanderCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#createexpandercode)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Expander>
- [エキスパンダーの概要](expander-overview.md)
- [方法トピック](expander-how-to-topics.md)
