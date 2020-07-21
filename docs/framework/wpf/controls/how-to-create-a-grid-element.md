---
title: '方法: グリッド要素を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], creating [WPF], grid instance
ms.assetid: b2f07626-9df8-43b8-8d36-492f3cb42837
ms.openlocfilehash: ebb9369da73bd595338e5b6ef42bda639bde6ed4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001365"
---
# <a name="how-to-create-a-grid-element"></a>方法: グリッド要素を作成する
## <a name="example"></a>例  
 次の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] またはコードを使用して <xref:System.Windows.Controls.Grid> のインスタンスを作成して使用する方法を示します。 この例では、3 つの <xref:System.Windows.Controls.ColumnDefinition> オブジェクトと 3 つの <xref:System.Windows.Controls.RowDefinition> オブジェクトを使用して、ワークシートなどで 9 つのセルが含まれるグリッドを作成します。 各セルには、データを表す <xref:System.Windows.Controls.TextBlock> 要素が含まれています。一番上の行には、<xref:System.Windows.Controls.Grid.ColumnSpan%2A> プロパティが適用された <xref:System.Windows.Controls.TextBlock> が含まれています。 各セルの境界を表示するには、<xref:System.Windows.Controls.Grid.ShowGridLines%2A> プロパティを有効にします。  
  
 [!code-csharp[Grid#3](~/samples/snippets/csharp/VS_Snippets_Wpf/Grid/CSharp/Grid_Code.cs#3)]
 [!code-vb[Grid#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Grid/VisualBasic/grid_vb.vb#3)]
 [!code-xaml[Grid#3](~/samples/snippets/xaml/VS_Snippets_Wpf/Grid/XAML/default.xaml#3)]  
  
  どちらの方法でも、次のようにまったく同じ外観のユーザー インターフェイスが生成されます。

  ![スクリーンショットは、3 つの列に分割されたグリッドを含む WPF ユーザー インターフェイスを示しています。  先頭の行のすべての列にまたがって "2018 年の出荷製品" という見出しがあり、3 つの列のそれぞれに四半期ごとの売上数が示されています。  一番下の行には、2 列にまたがってテキストが示されています。そのメッセージには、"合計単位: 300,000" とあります。](././media/how-to-create-a-grid-element/how-to-create-a-grid-element.png)
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Grid>
- [パネルの概要](panels-overview.md)
