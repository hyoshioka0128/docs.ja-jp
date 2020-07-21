---
title: '方法: GridView を実装する ListView の項目をグループ化する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], grouping items with GridViews
- grouping items in ListViews implementing GridViews [WPF]
- GridView controls [WPF], grouping items
ms.assetid: eebef25b-ddc6-424e-a66d-ea228d1bf33d
ms.openlocfilehash: b3dd6891976a942b299c87fca25e430e9ee59a51
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910274"
---
# <a name="how-to-group-items-in-a-listview-that-implements-a-gridview"></a>方法: GridView を実装する ListView の項目をグループ化する
この例からは、<xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.GridView> 表示モードで項目グループを表示する方法がわかります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.ListView> で項目グループを表示するには、<xref:System.Windows.Data.CollectionViewSource> を定義します。 次の例では、`Catalog` データ フィールドの値に基づいてデータ項目をグループ化する <xref:System.Windows.Data.CollectionViewSource> を示します。  
  
 [!code-xaml[GridViewWithGroups#GroupingCollectionViewSource](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#groupingcollectionviewsource)]  
  
 次の例では、前の例で定義された <xref:System.Windows.Data.CollectionViewSource> に <xref:System.Windows.Controls.ListView> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> が設定されます。 例ではまた、<xref:System.Windows.Controls.Expander> コントロールを実装する <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> が定義されます。  
  
 [!code-xaml[GridViewWithGroups#ListViewGroups](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewgroups)]  
[!code-xaml[GridViewWithGroups#ListViewEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewend)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
