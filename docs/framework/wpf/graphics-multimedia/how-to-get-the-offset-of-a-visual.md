---
title: '方法: ビジュアルのオフセットを取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting offset values from visual objects [WPF]
- offset values [WPF], retrieving from visual objects [WPF]
- visual objects [WPF], retrieving offset values from
- retrieving offset values from visual objects [WPF]
ms.assetid: 889a1dd6-1b11-445a-b351-fbb04c53ee34
ms.openlocfilehash: 4787b771c7e59a8b033b9267079c068a5845a1e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947494"
---
# <a name="how-to-get-the-offset-of-a-visual"></a>方法: ビジュアルのオフセットを取得する
これらの例では、ビジュアル オブジェクトの親、または先祖や子孫に対する相対的なオフセット値を取得する方法を示します。  
  
## <a name="example"></a>例  
 次のマークアップの例は、<xref:System.Windows.FrameworkElement.Margin%2A> 値 4 で定義されている <xref:System.Windows.Controls.TextBlock> を示しています。  
  
 [!code-xaml[VisualSnippets#VisualSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet1)]  
  
 次のコード例は、<xref:System.Windows.Media.VisualTreeHelper.GetOffset%2A> メソッドを使用して、<xref:System.Windows.Controls.TextBlock> のオフセットを取得する方法を示しています。 オフセット値は、返された <xref:System.Windows.Vector> 値内に含まれます。  
  
 [!code-csharp[VisualSnippets#VisualSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet2)]
 [!code-vb[VisualSnippets#VisualSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet2)]  
  
 オフセットでは、<xref:System.Windows.FrameworkElement.Margin%2A> 値が考慮されます。 この場合、<xref:System.Windows.Vector.X%2A> は 4 で、<xref:System.Windows.Vector.Y%2A> は 4 です。  
  
 返されるオフセット値は、<xref:System.Windows.Media.Visual> の親に対する相対値です。 <xref:System.Windows.Media.Visual> の親に対して相対的ではないオフセット値を返す場合は、<xref:System.Windows.Media.Visual.TransformToAncestor%2A> メソッドを使用します。  
  
## <a name="getting-the-offset-relative-to-an-ancestor"></a>先祖に対する相対的なオフセットの取得  
 次のマークアップの例は、2 つの <xref:System.Windows.Controls.StackPanel> オブジェクト内で入れ子になっている <xref:System.Windows.Controls.TextBlock> を示しています。  
  
 [!code-xaml[VisualSnippets#VisualSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window2.xaml#visualsnippet7)]  
  
 次の図は、マークアップの結果を示しています。  
  
 ![オブジェクトのオフセット値](./media/visualoffset-01.png "VisualOffset_01")  
2 つの StackPanels 内で入れ子になった TextBlock  
  
 次のコード例は、<xref:System.Windows.Media.Visual.TransformToAncestor%2A> メソッドを使用して、含まれている <xref:System.Windows.Window> に対する <xref:System.Windows.Controls.TextBlock> 相対的なオフセットを取得する方法を示しています。 オフセット値は、返された <xref:System.Windows.Media.GeneralTransform> 値内に含まれます。  
  
 [!code-csharp[VisualSnippets#VisualSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet5)]
 [!code-vb[VisualSnippets#VisualSnippet5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet5)]  
  
 オフセットでは、オブジェクトが含まれる <xref:System.Windows.Window> 内のすべてのオブジェクトの <xref:System.Windows.FrameworkElement.Margin%2A> 値が考慮されます。 この場合、<xref:System.Windows.Vector.X%2A> は 28 (16 + 8 + 4) で、<xref:System.Windows.Vector.Y%2A> は 28 です。  
  
 返されるオフセット値は、<xref:System.Windows.Media.Visual> の先祖に対する相対値です。 <xref:System.Windows.Media.Visual> の子孫に対して相対的なオフセット値を返す場合は、<xref:System.Windows.Media.Visual.TransformToDescendant%2A> メソッドを使用します。  
  
## <a name="getting-the-offset-relative-to-a-descendant"></a>子孫に対する相対的なオフセットの取得  
 次のマークアップの例は、<xref:System.Windows.Controls.StackPanel> オブジェクト内に含まれる <xref:System.Windows.Controls.TextBlock> を示しています。  
  
 [!code-xaml[VisualSnippets#VisualSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet4)]  
  
 次のコード例は、<xref:System.Windows.Media.Visual.TransformToDescendant%2A> メソッドを使用して、その子 <xref:System.Windows.Controls.TextBlock> に対する <xref:System.Windows.Controls.StackPanel> の相対的なオフセットを取得する方法を示します。 オフセット値は、返された <xref:System.Windows.Media.GeneralTransform> 値内に含まれます。  
  
 [!code-csharp[VisualSnippets#VisualSnippet9](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet9)]
 [!code-vb[VisualSnippets#VisualSnippet9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet9)]  
  
 オフセットでは、すべてのオブジェクトの <xref:System.Windows.FrameworkElement.Margin%2A> 値が考慮されます。 この場合、<xref:System.Windows.Vector.X%2A> は -4 で、<xref:System.Windows.Vector.Y%2A> は -4 です。 親オブジェクトはその子オブジェクトに対する相対的な負のオフセットであるため、オフセット値は負の値になります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
