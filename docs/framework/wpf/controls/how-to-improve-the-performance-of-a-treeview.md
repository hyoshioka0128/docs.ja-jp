---
title: '方法: TreeView のパフォーマンスを改善する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TreeView control [WPF], improving the performance
ms.assetid: b792c740-cf2b-4da8-8ba8-3d2e5a821874
ms.openlocfilehash: de1b46da2a7c6c3db0c0c19cdbb654fcf2fbbd6c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771008"
---
# <a name="how-to-improve-the-performance-of-a-treeview"></a>方法: TreeView のパフォーマンスを改善する
<xref:System.Windows.Controls.TreeView> に含まれる項目が多い場合、ユーザー インターフェイスで読み込みにかかる時間が大幅に遅くなる可能性があります。 `VirtualizingStackPanel.IsVirtualizing` 添付プロパティを `true` に設定して、読み込み時間を改善することができます。  また、ユーザーがマウス ホイールを使用したり、スクロール バーのつまみをドラッグしたりして、ユーザーが <xref:System.Windows.Controls.TreeView> をスクロールするときの UI の反応も遅くなることがあります。 `VirtualizingStackPanel.VirtualizationMode` 添付プロパティを <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> に設定することで、ユーザーがスクロールしたときの <xref:System.Windows.Controls.TreeView> のパフォーマンスを向上させることができます。  
  
## <a name="example"></a>例  
  
## <a name="description"></a>説明  
次の例では、`VirtualizingStackPanel.IsVirtualizing` 添付プロパティを true に設定し、`VirtualizingStackPanel.VirtualizationMode` 添付プロパティを <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> に設定して <xref:System.Windows.Controls.TreeView> を作成し、そのパフォーマンスを最適化します。  
  
## <a name="code"></a>コード  
 [!code-xaml[RecycleItemContainerShippets#VirtualizingTreeView](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizingtreeview)]  
  
 次の例は、前の例で使用するデータを示しています。  
  
 [!code-csharp[RecycleItemContainerShippets#TreeViewData](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#treeviewdata)]
 [!code-vb[RecycleItemContainerShippets#TreeViewData](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#treeviewdata)]  
  
## <a name="see-also"></a>関連項目

- [コントロール](../advanced/optimizing-performance-controls.md)
