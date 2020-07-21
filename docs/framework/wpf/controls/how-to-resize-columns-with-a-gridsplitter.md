---
title: '方法: GridSplitter を使用して列のサイズを変更する'
ms.date: 03/30/2017
helpviewer_keywords:
- grid columns [WPF], resizing
- GridSplitter control [WPF], resizing grid columns
- resizing grid columns [WPF]
ms.assetid: 47b20fe6-7adc-4aa6-9693-b4e184eef74b
ms.openlocfilehash: f743e9ccf8a984a646a4b8f05ee99162e5bc73ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770696"
---
# <a name="how-to-resize-columns-with-a-gridsplitter"></a>方法: GridSplitter を使用して列のサイズを変更する
この例からは、垂直 <xref:System.Windows.Controls.GridSplitter> を正しく作成することで、<xref:System.Windows.Controls.Grid> の寸法を変更することなく、<xref:System.Windows.Controls.Grid> 内の 2 つの列間のスペースを再配分する方法がわかります。  
  
## <a name="example"></a>例  
 **列の端に重なって表示される GridSplitter を作成する方法**  
  
 <xref:System.Windows.Controls.Grid> 内で隣接する列のサイズを変更する <xref:System.Windows.Controls.GridSplitter> を指定するには、サイズを変更する列の 1 つに <xref:System.Windows.Controls.Grid.Column%2A> 添付プロパティを設定します。 <xref:System.Windows.Controls.Grid> に複数の行がある場合、<xref:System.Windows.Controls.Grid.RowSpan%2A> 添付プロパティを行の数に設定します。 次に、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティを <xref:System.Windows.HorizontalAlignment.Left> または <xref:System.Windows.HorizontalAlignment.Right> に設定します (どちらの配置にするかは、サイズを変更する 2 つの列によって決まります)。 最後に、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティを <xref:System.Windows.VerticalAlignment.Stretch> に設定します。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterColumnOverlay](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplittercolumnoverlay)]  
  
 その独自の列がない <xref:System.Windows.Controls.GridSplitter> は、<xref:System.Windows.Controls.Grid> 内の他のコントロールによって隠されることがあります。 この問題の詳しい回避方法については、[GridSplitter を表示されるようにする](how-to-make-sure-that-a-gridsplitter-is-visible.md)を参照してください。  
  
 **列を占有する GridSplitter を作成する方法**  
  
 <xref:System.Windows.Controls.Grid> 内の列を占有する <xref:System.Windows.Controls.GridSplitter> を指定するには、サイズを変更する列の 1 つに <xref:System.Windows.Controls.Grid.Column%2A> 添付プロパティを設定します。 Grid に複数の行がある場合、<xref:System.Windows.Controls.Grid.RowSpan%2A> 添付プロパティを行の数に設定します。 次に <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> を <xref:System.Windows.HorizontalAlignment.Center> に設定し、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> プロパティを <xref:System.Windows.VerticalAlignment.Stretch> に設定し、<xref:System.Windows.Controls.GridSplitter> が含まれる列の <xref:System.Windows.Controls.ColumnDefinition.Width%2A> を <xref:System.Windows.GridLength.Auto%2A> に設定します。  
  
 次の例では、ある列を占有し、その両側の列のサイズを変更する垂直 <xref:System.Windows.Controls.GridSplitter> を定義する方法を示します。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart1)]  
[!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart2](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GridSplitter>
- [方法トピック](gridsplitter-how-to-topics.md)
