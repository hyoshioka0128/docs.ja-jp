---
title: '方法: GridSplitter を使用して行のサイズを変更する'
ms.date: 03/30/2017
helpviewer_keywords:
- resizing grid rows [WPF]
- grid rows [WPF], resizing
- GridSplitter control [WPF], resizing grid rows
ms.assetid: 2413a9f2-1d81-46ed-95cb-95ec8233eea2
ms.openlocfilehash: 6760a7a691af4f666294556cae3bc95a4299730a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770709"
---
# <a name="how-to-resize-rows-with-a-gridsplitter"></a>方法: GridSplitter を使用して行のサイズを変更する
この例からは、水平 <xref:System.Windows.Controls.GridSplitter> を使用することで、<xref:System.Windows.Controls.Grid> の寸法を変更することなく、<xref:System.Windows.Controls.Grid> 内の 2 つの行間のスペースを再配分する方法がわかります。  
  
## <a name="example"></a>例  
 **行の端に重なって表示される GridSplitter を作成する方法**  
  
 <xref:System.Windows.Controls.Grid> 内で隣接する行のサイズを変更する <xref:System.Windows.Controls.GridSplitter> を指定するには、サイズを変更する行の 1 つに <xref:System.Windows.Controls.Grid.Row%2A> 添付プロパティを設定します。 <xref:System.Windows.Controls.Grid> に複数の列がある場合は、<xref:System.Windows.Controls.Grid.ColumnSpan%2A> 添付プロパティを設定して列の数を指定します。 次に、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> を <xref:System.Windows.VerticalAlignment.Top> または <xref:System.Windows.VerticalAlignment.Bottom> に設定します (どちらの配置にするかは、サイズを変更する 2 つの行によって決まります)。 最後に、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティを <xref:System.Windows.HorizontalAlignment.Stretch> に設定します。  
  
 次の例では、隣接する行のサイズを変更する水平 <xref:System.Windows.Controls.GridSplitter> を定義する方法を示します。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterRowOverlay](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterrowoverlay)]  
  
 その独自の行を占有しない <xref:System.Windows.Controls.GridSplitter> は、<xref:System.Windows.Controls.Grid> 内の他のコントロールによって隠されることがあります。 この問題の詳しい回避方法については、[GridSplitter を表示されるようにする](how-to-make-sure-that-a-gridsplitter-is-visible.md)を参照してください。  
  
 **行を占有する GridSplitter を作成する方法**  
  
 <xref:System.Windows.Controls.Grid> 内の行を占有する <xref:System.Windows.Controls.GridSplitter> を指定するには、サイズを変更する行の 1 つに <xref:System.Windows.Controls.Grid.Row%2A> 添付プロパティを設定します。 <xref:System.Windows.Controls.Grid> に複数の列がある場合、<xref:System.Windows.Controls.Grid.ColumnSpan%2A> 添付プロパティを列の数に設定します。 次に <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> を <xref:System.Windows.VerticalAlignment.Center> に設定し、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティを <xref:System.Windows.HorizontalAlignment.Stretch> に設定し、<xref:System.Windows.Controls.GridSplitter> が含まれる行の <xref:System.Windows.Controls.RowDefinition.Height%2A> を <xref:System.Windows.GridLength.Auto%2A> に設定します。  
  
 次の例では、ある行を占有し、その両側の行のサイズを変更する水平 <xref:System.Windows.Controls.GridSplitter> を定義する方法を示します。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterEntireRowPart1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart1)]  
[!code-xaml[GridSplitterRowColumn#GridSplitterEntireRowPart2](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GridSplitter>
- [方法トピック](gridsplitter-how-to-topics.md)
