---
title: '方法: トリガーを使用して、ListView で選択された項目のスタイルを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 1e2bdce0-afe8-4507-9b18-f33de43de25a
ms.openlocfilehash: ad64382b871bae9114a1e63257de3f8595376923
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61696199"
---
# <a name="how-to-use-triggers-to-style-selected-items-in-a-listview"></a>方法: トリガーを使用して、ListView で選択された項目のスタイルを設定する
この例は、<xref:System.Windows.Controls.ListViewItem> コントロールの <xref:System.Windows.Style.Triggers%2A> を定義して、<xref:System.Windows.Controls.ListViewItem> のプロパティ値の変更に応じて <xref:System.Windows.Controls.ListViewItem> の <xref:System.Windows.Style> が変更されるようにする方法を示します。  
  
## <a name="example"></a>例  
 プロパティの変更に応じて <xref:System.Windows.Controls.ListViewItem> の <xref:System.Windows.Style> を変更する場合は、<xref:System.Windows.Style> の変更に対して <xref:System.Windows.Style.Triggers%2A> を定義します。  
  
 次の例では、<xref:System.Windows.Controls.Control.Foreground%2A> プロパティを <xref:System.Windows.Media.Brushes.Blue%2A> に設定し、<xref:System.Windows.UIElement.IsMouseOver%2A> プロパティが `true` に変更されたときに <xref:System.Windows.Input.CursorType.Hand> を表示するように <xref:System.Windows.FrameworkElement.Cursor%2A> を変更する <xref:System.Windows.Trigger> を定義しています。  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#Trigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#trigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
 次の例では、<xref:System.Windows.Controls.ListViewItem> が選択された項目で、キーボード フォーカスがある場合に、<xref:System.Windows.Controls.ListViewItem> の <xref:System.Windows.Controls.Control.Foreground%2A> プロパティを <xref:System.Windows.Media.Brushes.Yellow%2A> に設定する <xref:System.Windows.MultiTrigger> を定義しています。  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#MultiTrigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#multitrigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Control>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
