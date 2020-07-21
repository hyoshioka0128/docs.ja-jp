---
title: '方法: TreeView での TreeViewItem の検索'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TreeView control [WPF], finding a TreeViewItem
- TreeViewItem [WPF], finding
ms.assetid: 72ecd40c-3939-4e01-b617-5e9daa6074d9
ms.openlocfilehash: ad72c7a7fb11dfe605db4119dde831b47dd7c5a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962090"
---
# <a name="how-to-find-a-treeviewitem-in-a-treeview"></a>方法: TreeView での TreeViewItem の検索
<xref:System.Windows.Controls.TreeView> コントロールは、階層データを表示するための便利な方法です。 <xref:System.Windows.Controls.TreeView> がデータ ソースにバインドされている場合、<xref:System.Windows.Controls.TreeView.SelectedItem%2A> プロパティを使用すると、選択したデータ オブジェクトをすばやく簡単に取得できます。 通常は、基になるデータ オブジェクトを操作することをお勧めしますが、<xref:System.Windows.Controls.TreeViewItem> を含むデータをプログラムで操作することが必要になる場合もあります。 たとえば、プログラムを使用して <xref:System.Windows.Controls.TreeViewItem> を展開したり、<xref:System.Windows.Controls.TreeView> で別の項目を選択したりすることが必要になる場合があります。  
  
 特定のデータ オブジェクトを含む <xref:System.Windows.Controls.TreeViewItem> を検索するには、<xref:System.Windows.Controls.TreeView> の各レベルを走査する必要があります。 <xref:System.Windows.Controls.TreeView> 内の項目は、パフォーマンスを向上させるために仮想化することもできます。 項目が仮想化される可能性がある場合は、データ オブジェクトが含まれているかどうかを確認するために <xref:System.Windows.Controls.TreeViewItem> も認識する必要があります。  
  
## <a name="example"></a>例  
  
## <a name="description"></a>説明  
 次の例では、特定のオブジェクトの <xref:System.Windows.Controls.TreeView> が検索され、<xref:System.Windows.Controls.TreeViewItem> が含まれるオブジェクトが返されます。 この例では、各 <xref:System.Windows.Controls.TreeViewItem> がインスタンス化され、その子項目を検索できるようになっています。 この例は、<xref:System.Windows.Controls.TreeView> で仮想化された項目が使用されていない場合にも機能します。  
  
> [!NOTE]
> 次の例は、基になるデータ モデルに関係なく、すべての <xref:System.Windows.Controls.TreeView> に対して機能し、オブジェクトが見つかるまですべての <xref:System.Windows.Controls.TreeViewItem> が検索されます。 パフォーマンスがより優れたもう 1 つの方法は、指定されたオブジェクトのデータ モデルを検索し、データ階層内での位置を追跡して、<xref:System.Windows.Controls.TreeView> 内の対応する <xref:System.Windows.Controls.TreeViewItem> を見つけることです。 ただし、このパフォーマンスがより優れた方法では、データ モデルに関する知識が必要であり、あらゆる <xref:System.Windows.Controls.TreeView> に対して一般化することはできません。  
  
## <a name="code"></a>コード  
 [!code-csharp[TreeViewFindTVI#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[TreeViewFindTVI#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#1)]  
  
 上記のコードは、`BringIntoView` という名前のメソッドを公開するカスタム <xref:System.Windows.Controls.VirtualizingStackPanel> に依存しています。 次のコードでは、カスタム <xref:System.Windows.Controls.VirtualizingStackPanel> が定義されます。  
  
 [!code-csharp[TreeViewFindTVI#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#2)]
 [!code-vb[TreeViewFindTVI#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#2)]  
  
 次の XAML は、カスタム <xref:System.Windows.Controls.VirtualizingStackPanel> を使用する <xref:System.Windows.Controls.TreeView> の作成方法を示しています。  
  
 [!code-xaml[TreeViewFindTVI#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml#3)]  
  
## <a name="see-also"></a>関連項目

- [TreeView のパフォーマンスを改善する](how-to-improve-the-performance-of-a-treeview.md)
