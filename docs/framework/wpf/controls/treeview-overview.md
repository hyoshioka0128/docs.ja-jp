---
title: TreeView の概要
ms.date: 03/30/2017
helpviewer_keywords:
- expanding node [WPF]
- TreeView control [WPF], about TreeView control
- Control class [WPF], TreeView
ms.assetid: 62212512-5a5c-4864-949e-b6a6a3a52c02
ms.openlocfilehash: 267e870e13d26439e4fbcbba3c5741ff84cabe3c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187380"
---
# <a name="treeview-overview"></a>TreeView の概要
<xref:System.Windows.Controls.TreeView> コントロールには、折りたたみ可能なノードを使用して、階層構造で情報を表示する方法が用意されています。 このトピックでは、<xref:System.Windows.Controls.TreeView> コントロールと <xref:System.Windows.Controls.TreeViewItem> コントロールについて説明し、その使用法の簡単な例を示します。  

<a name="Simple_TreeView_Control"></a>
## <a name="what-is-a-treeview"></a>TreeViewとは  
 <xref:System.Windows.Controls.TreeView> は、<xref:System.Windows.Controls.TreeViewItem> コントロールを使用することによって項目を入れ子にする <xref:System.Windows.Controls.ItemsControl> です。 <xref:System.Windows.Controls.TreeView> を作成する例を次に示します。  
  
 [!code-xaml[TreeViewSnips#EmbeddedTVIs](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#embeddedtvis)]  
  
<a name="Creating_a_TreeView"></a>
## <a name="creating-a-treeview"></a>TreeView の作成  
 <xref:System.Windows.Controls.TreeView> コントロールには、<xref:System.Windows.Controls.TreeViewItem> コントロールの階層が含まれています。 <xref:System.Windows.Controls.TreeViewItem> コントロールは、<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> と <xref:System.Windows.Controls.ItemsControl.Items%2A> コレクションが含まれる <xref:System.Windows.Controls.HeaderedItemsControl> です。  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用することによって <xref:System.Windows.Controls.TreeView> を定義する場合、<xref:System.Windows.Controls.TreeViewItem> コントロールの <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> の内容およびそのコレクションを構成する項目を明示的に定義できます。 前の図では、この方法を示しています。  
  
 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> をデータ ソースとして指定してから <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> と <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> を指定して、<xref:System.Windows.Controls.TreeViewItem> の内容を定義することもできます。  
  
 <xref:System.Windows.Controls.TreeViewItem> コントロールのレイアウトを定義するには、<xref:System.Windows.HierarchicalDataTemplate> オブジェクトも使用できます。 詳細と例については、「[Use SelectedValue, SelectedValuePath, and SelectedItem](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)」を参照してください。  
  
 項目が <xref:System.Windows.Controls.TreeViewItem> コントロールでない場合は、<xref:System.Windows.Controls.TreeView> コントロールが表示されるときに、項目が <xref:System.Windows.Controls.TreeViewItem> コントロールによって自動的に囲まれます。  
  
<a name="Expanding_and_Collapsing_a_TreeViewItem"></a>
## <a name="expanding-and-collapsing-a-treeviewitem"></a>TreeViewItem の展開と折りたたみ  
 ユーザーが <xref:System.Windows.Controls.TreeViewItem> を展開すると、<xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> プロパティは `true` に設定されます。 ユーザーが直接操作しなくても、<xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> プロパティを `true` (展開) または `false` (折りたたみ) に設定することによって、<xref:System.Windows.Controls.TreeViewItem> を展開したり折りたたんだりすることができます。 このプロパティが変更されると、<xref:System.Windows.Controls.TreeViewItem.Expanded> または <xref:System.Windows.Controls.TreeViewItem.Collapsed> イベントが発生します。  
  
 <xref:System.Windows.Controls.TreeViewItem> コントロールで <xref:System.Windows.FrameworkElement.BringIntoView%2A> メソッドが呼び出されると、<xref:System.Windows.Controls.TreeViewItem> とその親の <xref:System.Windows.Controls.TreeViewItem> コントロールが展開されます。 <xref:System.Windows.Controls.TreeViewItem> が非表示または部分的な表示になっている場合は、表示されるように <xref:System.Windows.Controls.TreeView> がスクロールします。  
  
<a name="TreeViewItem_Selection"></a>
## <a name="treeviewitem-selection"></a>TreeViewItem の選択  
 ユーザーが <xref:System.Windows.Controls.TreeViewItem> コントロールをクリックしてそれを選択すると、<xref:System.Windows.Controls.TreeViewItem.Selected> イベントが発生し、その <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> プロパティが `true` に設定されます。 また、<xref:System.Windows.Controls.TreeViewItem> は、<xref:System.Windows.Controls.TreeView> コントロールの <xref:System.Windows.Controls.TreeView.SelectedItem%2A> になります。 逆に、選択が <xref:System.Windows.Controls.TreeViewItem> コントロールから変更されると、その <xref:System.Windows.Controls.TreeViewItem.Unselected> イベントが発生し、その <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> プロパティが `false` に設定されます。  
  
 <xref:System.Windows.Controls.TreeView> コントロールの <xref:System.Windows.Controls.TreeView.SelectedItem%2A> プロパティは読み取り専用プロパティであるため、明示的に設定することはできません。 ユーザーが <xref:System.Windows.Controls.TreeViewItem> コントロールをクリックした場合、または、<xref:System.Windows.Controls.TreeViewItem> コントロールで <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> プロパティが `true` に設定された場合、<xref:System.Windows.Controls.TreeView.SelectedItem%2A> プロパティが設定されます。  
  
 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> の<xref:System.Windows.Controls.TreeView.SelectedValue%2A> を指定するには、<xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> プロパティを使用しします。 詳細については、「[SelectedValue、SelectedValuePath、および SelectedItem を使用する](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)」を参照してください。  
  
 <xref:System.Windows.Controls.TreeView.SelectedItemChanged> イベントにイベント ハンドラーを登録することにより、選択されている <xref:System.Windows.Controls.TreeViewItem> が変更されたことを検出できます。 イベント ハンドラーに提供される <xref:System.Windows.RoutedPropertyChangedEventArgs%601> では、前の選択項目である <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A> と、現在の選択項目である <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A> が指定されています。 アプリケーションまたはユーザーが以前または現在の選択を行っていない場合、どちらの値も `null` にできます。  
  
<a name="TreeView_Style"></a>
## <a name="treeview-style"></a>TreeView のスタイル  
 既定のスタイルの <xref:System.Windows.Controls.TreeView> コントロールは、<xref:System.Windows.Controls.ScrollViewer> コントロールが格納されている <xref:System.Windows.Controls.StackPanel> オブジェクト内に配置されます。 <xref:System.Windows.Controls.TreeView> に対して <xref:System.Windows.FrameworkElement.Width%2A> プロパティと <xref:System.Windows.FrameworkElement.Height%2A> プロパティを設定すると、これらの値を使用して、<xref:System.Windows.Controls.TreeView> が表示される <xref:System.Windows.Controls.StackPanel> オブジェクトのサイズが設定されます。 表示される内容が表示領域より大きい場合、<xref:System.Windows.Controls.ScrollViewer> は、ユーザーが <xref:System.Windows.Controls.TreeView> の内容をスクロールできるように自動的に表示されます。  
  
 <xref:System.Windows.Controls.TreeViewItem> コントロールの外観をカスタマイズするには、<xref:System.Windows.FrameworkElement.Style%2A> プロパティにカスタムの <xref:System.Windows.Style> を設定します。  
  
 次の例では、<xref:System.Windows.FrameworkElement.Style%2A> を使用して <xref:System.Windows.Controls.TreeViewItem> コントロールの<xref:System.Windows.Controls.Control.Foreground%2A> プロパティと <xref:System.Windows.Controls.Control.FontSize%2A> プロパティの値を設定する方法を示します。  
  
 [!code-xaml[TreeViewSimple#8](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#8)]  
  
<a name="Adding_Images_and_oOther_Content_to_TreeView_Items"></a>
## <a name="adding-images-and-other-content-to-treeview-items"></a>TreeView 項目へのイメージとその他のコンテンツの追加  
 <xref:System.Windows.Controls.TreeViewItem> の <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> の内容には、複数のオブジェクトを含めることができます。 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> の内容に複数のオブジェクトを含めるには、<xref:System.Windows.Controls.Panel> や <xref:System.Windows.Controls.StackPanel> などのレイアウト コントロールでオブジェクトを囲みます。  
  
 次の例では、<xref:System.Windows.Controls.TreeViewItem> の <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> を <xref:System.Windows.Controls.CheckBox> および <xref:System.Windows.Controls.TextBlock> (両方とも <xref:System.Windows.Controls.DockPanel> コントロールで囲まれています) として定義する方法を示します。  
  
 [!code-xaml[TreeViewSnips#TVIHeader](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#tviheader)]  
  
 次の例では、<xref:System.Windows.Controls.DockPanel> コントロールで囲まれた <xref:System.Windows.Controls.Image> および <xref:System.Windows.Controls.TextBlock> が含まれる <xref:System.Windows.DataTemplate> を定義する方法を示します。 <xref:System.Windows.DataTemplate> を使用して、<xref:System.Windows.Controls.TreeViewItem> の <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> または <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> を設定できます。  
  
 [!code-xaml[TreeViewDataBinding#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewDataBinding/CSharp/Window1.xaml#6)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [方法トピック](treeview-how-to-topics.md)
- [WPF のコンテンツ モデル](wpf-content-model.md)
