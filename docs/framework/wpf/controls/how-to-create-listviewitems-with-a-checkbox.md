---
title: '方法: CheckBox を持つ ListViewItem を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], ListView
- controls [WPF], CheckBox
- ListView controls [WPF], CheckBox controls
- CheckBox control [WPF], ListView control
ms.assetid: f6d66c7f-906c-4f65-a55a-0ede9d00e26a
ms.openlocfilehash: b09d5ad11b0961febf524cec1e19cb1e59832e44
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910781"
---
# <a name="how-to-create-listviewitems-with-a-checkbox"></a>方法: CheckBox を持つ ListViewItem を作成する
この例では、<xref:System.Windows.Controls.GridView> を使用する <xref:System.Windows.Controls.ListView> コントロールに <xref:System.Windows.Controls.CheckBox> コントロールの列を表示する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.ListView> に <xref:System.Windows.Controls.CheckBox> コントロールが含まれる列を作成するには、<xref:System.Windows.Controls.CheckBox> が含まれる <xref:System.Windows.DataTemplate> を作成します。 次に、<xref:System.Windows.Controls.GridViewColumn> の <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> を <xref:System.Windows.DataTemplate> に設定します。  
  
 次は、<xref:System.Windows.Controls.CheckBox> が含まれる <xref:System.Windows.DataTemplate> の例です。 この例では、<xref:System.Windows.Controls.CheckBox> の <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> プロパティを、それが含まれる <xref:System.Windows.Controls.ListViewItem> の <xref:System.Windows.Controls.ListBoxItem.IsSelected%2A> プロパティ値にバインドしています。 そのため、<xref:System.Windows.Controls.CheckBox> が含まれる <xref:System.Windows.Controls.ListViewItem> が選択されると、<xref:System.Windows.Controls.CheckBox> にチェックマークが入ります。  
  
 [!code-xaml[ListViewChkBox#CheckBoxDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#checkboxdatatemplate)]  
  
 次の例では、<xref:System.Windows.Controls.CheckBox> コントロールの列を作成する方法を示します。 列を作成するため、この例では、<xref:System.Windows.Controls.GridViewColumn> の <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> プロパティが <xref:System.Windows.DataTemplate> に設定されています。  
  
 [!code-xaml[ListViewChkBox#GridViewColumnCheckBox](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#gridviewcolumncheckbox)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Control>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [ListView の概要](listview-overview.md)
- [方法トピック](listview-how-to-topics.md)
- [GridView の概要](gridview-overview.md)
