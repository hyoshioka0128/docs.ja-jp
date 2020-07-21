---
title: '方法: SelectedValue、SelectedValuePath、および SelectedItem を使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], SelectedValue properties
- Control class [WPF], SelectedItem properties
- Control class [WPF], TreeView properties
- Control class [WPF], SelectedValue properties
- TreeView control [WPF], SelectedItem properties
- SelectedValue [WPF], SelectedValuePath properties
- TreeView control [WPF], SelectedValuePath properties
- Control class [WPF], SelectedValuePath properties
- SelectedValue [WPF], SelectedItem properties
ms.assetid: 2fc92ad4-f02c-4f89-bbe9-d4978a7af0db
ms.openlocfilehash: d9f7a8f04f53b7d38a49dfef2c947dfa1c2d263d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699137"
---
# <a name="how-to-use-selectedvalue-selectedvaluepath-and-selecteditem"></a>方法: SelectedValue、SelectedValuePath、および SelectedItem を使用する
この例からは、<xref:System.Windows.Controls.TreeView.SelectedValue%2A> プロパティと <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> プロパティを使用し、<xref:System.Windows.Controls.TreeView> の <xref:System.Windows.Controls.TreeView.SelectedItem%2A> に値を指定する方法がわかります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> プロパティからは、<xref:System.Windows.Controls.TreeView> 内の <xref:System.Windows.Controls.TreeView.SelectedValue%2A> に <xref:System.Windows.Controls.TreeView.SelectedItem%2A> を指定する方法が与えられます。 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> は <xref:System.Windows.Controls.ItemsControl.Items%2A> コレクション内のオブジェクトです。<xref:System.Windows.Controls.TreeView> には、選択した項目の単一プロパティの値が表示されます。 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> プロパティによって、<xref:System.Windows.Controls.TreeView.SelectedValue%2A> プロパティの値を決定する目的で使用されるプロパティのパスが指定されます。 このトピックの例はこの概念を説明するものです。  
  
 次の例では、社員情報が含まれる <xref:System.Windows.Data.XmlDataProvider> を示します。  
  
 [!code-xaml[TreeViewSelectedValue#XMLDataProvider](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#xmldataprovider)]  
  
 次の例では、`Employee` の `EmployeeName` と `EmployeeWorkDay` を表示する <xref:System.Windows.HierarchicalDataTemplate> が定義されます。 <xref:System.Windows.HierarchicalDataTemplate> ではテンプレートの一部として `EmployeeNumber` が指定されないことにご留意ください。  
  
 [!code-xaml[TreeViewSelectedValue#HierarchicalDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#hierarchicaldatatemplate)]  
  
 次の例では、前に定義した <xref:System.Windows.HierarchicalDataTemplate> を使用し、<xref:System.Windows.Controls.TreeView.SelectedValue%2A> プロパティを `EmployeeNumber` に設定する <xref:System.Windows.Controls.TreeView> を示します。 <xref:System.Windows.Controls.TreeView> で `EmployeeName` を選択すると、<xref:System.Windows.Controls.TreeView.SelectedItem%2A> プロパティから、選択した `EmployeeName` に対応する `EmployeeInfo` データ項目が返されます。 ただし、この <xref:System.Windows.Controls.TreeView> の <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> が `EmployeeNumber` に設定されているため、<xref:System.Windows.Controls.TreeView.SelectedValue%2A> は `EmployeeNumber` に設定されます。  
  
 [!code-xaml[TreeViewSelectedValue#SelectedValuePath](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#selectedvaluepath)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [TreeView の概要](treeview-overview.md)
- [方法トピック](treeview-how-to-topics.md)
