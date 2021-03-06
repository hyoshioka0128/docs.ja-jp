---
title: '方法 : ToolTip を配置する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], positioning
- positioning ToolTip controls [WPF]
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
ms.openlocfilehash: e51be52301197a66ef49339245e60404d823b36c
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43512294"
---
# <a name="how-to-position-a-tooltip"></a>方法 : ToolTip を配置する
この例では、画面上のツールヒントの位置を指定する方法を示します。  
  
## <a name="example"></a>例  
 両方で定義されている 5 つのプロパティのセットを使用して、tooltip を配置することができます、<xref:System.Windows.Controls.ToolTip>と<xref:System.Windows.Controls.ToolTipService>クラス。 次の表は、これら 2 つの 5 つのプロパティのセットを説明し、クラスに基づいて、リファレンス ドキュメントへのリンクを示します。  
  
### <a name="corresponding-tooltip-properties-according-to-class"></a>対応するツールヒント プロパティ クラス  
  
|<xref:System.Windows.Controls.ToolTip?displayProperty=nameWithType> クラスのプロパティ|<xref:System.Windows.Controls.ToolTipService?displayProperty=nameWithType> クラスのプロパティ|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=nameWithType>|  
  
 使用して、ツールヒントの内容を定義するかどうか、<xref:System.Windows.Controls.ToolTip>オブジェクトのいずれかのクラス プロパティを使用することができます。 ただし、、<xref:System.Windows.Controls.ToolTipService>プロパティも優先されます。 使用して、<xref:System.Windows.Controls.ToolTipService>プロパティとして定義されていないヒントを<xref:System.Windows.Controls.ToolTip>オブジェクト。  
  
 次の図は、これらのプロパティを使用して、tooltip を配置する方法を示します。 ですが、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]のこれらの図の例で定義されているプロパティを設定する方法を示して、<xref:System.Windows.Controls.ToolTip>クラスの対応するプロパティ、<xref:System.Windows.Controls.ToolTipService>クラスと同じレイアウト規則に従います。 配置プロパティの値の詳細については、次を参照してください。[ポップアップの配置動作](../../../../docs/framework/wpf/controls/popup-placement-behavior.md)します。  
  
 ![ツールヒント配置](../../../../docs/framework/wpf/controls/media/tooltipplacement.png "ToolTipPlacement")  
配置プロパティを使用してツールヒントの配置  
  
 ![配置四角形を使用して、ツールヒントの配置](../../../../docs/framework/wpf/controls/media/tooltipplacementrectangle.png "ToolTipPlacementRectangle")  
配置、および PlacementRectangle の各プロパティを使用してツールヒントの配置  
  
 ![ツールヒント配置のダイアグラム](../../../../docs/framework/wpf/controls/media/tooltipplacementprhv.png "ToolTipPlacementPRHV")  
配置、PlacementRectangle、およびオフセット プロパティを使用してツールヒントの配置  
  
 次の例は、使用する方法を示します、<xref:System.Windows.Controls.ToolTip>プロパティが表示されるツールヒントの位置を指定する、<xref:System.Windows.Controls.ToolTip>オブジェクト。  
  
 [!code-xaml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 次の例は、使用する方法を示します、<xref:System.Windows.Controls.ToolTipService>内容がツールヒントの位置を指定するプロパティを<xref:System.Windows.Controls.ToolTip>オブジェクト。  
  
 [!code-xaml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Windows.Controls.ToolTip>  
 <xref:System.Windows.Controls.ToolTipService>  
 [方法トピック](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)  
 [ToolTip の概要](../../../../docs/framework/wpf/controls/tooltip-overview.md)  
 [ContextMenuService および ToolTipService を使用します。](https://msdn.microsoft.com/library/809b0e9c-d612-4cda-b8af-1a698c68f4d1)
