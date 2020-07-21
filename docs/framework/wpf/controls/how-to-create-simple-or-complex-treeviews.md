---
title: '方法: 単純または複雑な TreeView を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], creating
- Control class [WPF], TreeView [WPF], creating
ms.assetid: 1defbb78-b8e7-4c0e-b650-576453ac828d
ms.openlocfilehash: 7edb4933ebcc0f0d2cb02754238c2342ee9dd4a2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62031916"
---
# <a name="how-to-create-simple-or-complex-treeviews"></a>方法: 単純または複雑な TreeView を作成する
この例では、単純または複雑な <xref:System.Windows.Controls.TreeView> コントロールを作成する方法を示します。  
  
 <xref:System.Windows.Controls.TreeView> は <xref:System.Windows.Controls.TreeViewItem> コントロールの階層から構成されます。このコントロールには、単純なテキスト文字列が含まれることもあれば、<xref:System.Windows.Controls.Button> コントロールやコンテンツが埋め込まれた <xref:System.Windows.Controls.StackPanel> など、もっと複雑なコンテンツが含まれることもあります。 <xref:System.Windows.Controls.TreeView> コンテンツは明示的に定義できます。あるいは、データ ソースからコンテンツを提供できます。 このトピックではこうした概念の例を提供します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.TreeViewItem> の <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> プロパティには、その項目に対して <xref:System.Windows.Controls.TreeView> で表示されるコンテンツが含まれます。 <xref:System.Windows.Controls.TreeViewItem> には、その子要素として <xref:System.Windows.Controls.TreeViewItem> コントロールが与えられることもあります。また、これらの子要素は <xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティを利用して定義できます。  
  
 次の例では、<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> プロパティをテキスト文字列に設定することで <xref:System.Windows.Controls.TreeViewItem> コンテンツを明示的に定義する方法を示します。  
  
 [!code-xaml[TreeViewSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#1)]  
  
 次の例では、<xref:System.Windows.Controls.Button> コントロールである <xref:System.Windows.Controls.ItemsControl.Items%2A> を定義することで <xref:System.Windows.Controls.TreeViewItem> の子要素を定義する方法を示します。  
  
 [!code-xaml[TreeViewSimple#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#3)]  
  
 次の例では、<xref:System.Windows.Data.XmlDataProvider> によって <xref:System.Windows.Controls.TreeViewItem> コンテンツが提供され、<xref:System.Windows.HierarchicalDataTemplate> によってコンテンツの外観が定義される <xref:System.Windows.Controls.TreeView> を作成する方法を示します。  
  
 [!code-xaml[TreeViewSimple#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#6)]  
  
 [!code-xaml[TreeViewSimple#7](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#7)]  
  
 [!code-xaml[TreeViewSimple#5](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#5)]  
  
 次の例では、<xref:System.Windows.Controls.TreeViewItem> コンテンツには、コンテンツが埋め込まれている <xref:System.Windows.Controls.DockPanel> コントロールが含まれる <xref:System.Windows.Controls.TreeView> を作成する方法を示します。  
  
 [!code-xaml[TreeViewSimple#9](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#9)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [TreeView の概要](treeview-overview.md)
- [方法トピック](treeview-how-to-topics.md)
