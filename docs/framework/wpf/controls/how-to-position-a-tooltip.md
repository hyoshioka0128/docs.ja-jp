---
title: '方法: ToolTip を配置する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], positioning
- positioning ToolTip controls [WPF]
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
ms.openlocfilehash: 0f52703e4fe127daa40f220280f084b2026580cc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186950"
---
# <a name="how-to-position-a-tooltip"></a>方法: ToolTip を配置する
この例では、画面上のツールヒントの位置を指定する方法を示します。  
  
## <a name="example"></a>例  
 ツールヒントを配置するには、<xref:System.Windows.Controls.ToolTip> クラスと <xref:System.Windows.Controls.ToolTipService> クラスの両方で定義されている 5 つのプロパティのセットを使用します。 次の表では、これら 5 つのプロパティの 2 つのセットを示し、クラスに対応したリファレンス ドキュメントへのリンクを提供します。  
  
### <a name="corresponding-tooltip-properties-according-to-class"></a>クラスに応じた対応するツールヒント プロパティ  
  
|<xref:System.Windows.Controls.ToolTip?displayProperty=nameWithType> クラスのプロパティ|<xref:System.Windows.Controls.ToolTipService?displayProperty=nameWithType> クラスのプロパティ|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=nameWithType>|  
  
 <xref:System.Windows.Controls.ToolTip> オブジェクトを使用してツールヒントの内容を定義する場合は、どちらのクラスのプロパティでも使用できます。ただし、<xref:System.Windows.Controls.ToolTipService> のプロパティが優先されます。 <xref:System.Windows.Controls.ToolTip> オブジェクトとして定義されないツールヒントには、<xref:System.Windows.Controls.ToolTipService> のプロパティを使用します。  
  
 次の図では、これらのプロパティを使用してツールヒントを配置する方法を示します。 これらの図の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の例では、<xref:System.Windows.Controls.ToolTip> クラスによって定義されているプロパティを設定する方法が示されていますが、<xref:System.Windows.Controls.ToolTipService> クラスの対応するプロパティも同じレイアウト規則に従います。 Placement プロパティに使用できる値の詳細については、「[ポップアップの配置動作](popup-placement-behavior.md)」を参照してください。  

 次の図では、Placement プロパティを使用したツールヒントの配置を示します。  
  
 ![Placement プロパティを使用したツールヒントの配置を示す図。](./media/how-to-position-a-tooltip/tooltip-placement-property.png)

 次の図では、Placement プロパティと PlacementRectangle プロパティを使用したツールヒントの配置を示します。

 ![PlacementRectangle プロパティを使用したツールヒントの配置を示す図。](./media/how-to-position-a-tooltip/tooltip-placement-rectangle-property.png)  

 次の図では、Placement、PlacementRectangle、Offset の各プロパティを使用したツールヒントの配置を示します。
  
 ![Offset プロパティを使用したツールヒントの配置を示す図。](./media/how-to-position-a-tooltip/tooltip-placement-offset-property.png)

 次の例では、<xref:System.Windows.Controls.ToolTip> プロパティを使用して、内容が <xref:System.Windows.Controls.ToolTip> オブジェクトであるツールヒントの位置を指定する方法を示します。  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 次の例では、<xref:System.Windows.Controls.ToolTipService> プロパティを使用して、内容が <xref:System.Windows.Controls.ToolTip> オブジェクトではないツールヒントの位置を指定する方法を示します。  
  
 [!code-xaml[ToolTipService#NoToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [方法トピック](tooltip-how-to-topics.md)
- [ToolTip の概要](tooltip-overview.md)
