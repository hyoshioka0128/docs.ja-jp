---
title: '方法: BetweenShowDelay プロパティを使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolTip control [WPF], BetweenShowDelay time property
- BetweenShowDelay time property [WPF]
ms.assetid: 984ea76d-f2a2-4326-a02e-f97ec3d036d6
ms.openlocfilehash: 9b63675ec21294496117860aa5b58af132c4284a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614529"
---
# <a name="how-to-use-the-betweenshowdelay-property"></a>方法: BetweenShowDelay プロパティを使用する
この例では、<xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> の時間プロパティを使用して、ユーザーがマウス ポインターをあるツールヒントから別のツールヒントに直接移動したときにそのツールヒントをすばやく (遅延なし、またはほとんどなく) 表示させる方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> プロパティが 1 秒 (1,000 ミリ秒) に設定され、<xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> は両方の <xref:System.Windows.Shapes.Ellipse> コントロールのツールヒントで 2 秒 (2,000 ミリ秒) に設定されています。 いずれかの省略記号のツールヒントを表示し、2 秒以内にマウス ポインターを別の省略記号に移動して一時停止すると、2 番目の省略記号のツールヒントがすぐに表示されます。  
  
 次のいずれのシナリオでも、<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> が適用され、2 番目の省略記号のツールヒントが 1 秒間待機してから表示されます。  
  
- 2 番目のボタンへの移動にかかる時間が 2 秒を超えている場合。  
  
- 最初の省略記号の時間間隔の開始時にツールヒントが表示されない場合。  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
[!code-xaml[ToolTipService#NoToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [方法トピック](tooltip-how-to-topics.md)
- [ToolTip の概要](tooltip-overview.md)
