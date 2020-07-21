---
title: '方法: Dock の値を取得または設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dock values [WPF], setting
- Dock values [WPF], getting
ms.assetid: fcf4ab8a-c7cd-4835-8d04-de1c999ab4a8
ms.openlocfilehash: fb6c8a7d62aa09a6e1d82cb4079d1425a7f39f8c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910287"
---
# <a name="how-to-get-or-set-a-dock-value"></a>方法: Dock の値を取得または設定する
次の例では、オブジェクトの <xref:System.Windows.Controls.Dock> 値を割り当てる方法を示します。 例では、<xref:System.Windows.Controls.DockPanel> の <xref:System.Windows.Controls.DockPanel.GetDock%2A> メソッドと <xref:System.Windows.Controls.DockPanel.SetDock%2A> メソッドが使用されます。  
  
## <a name="example"></a>例  
 例では、<xref:System.Windows.Controls.TextBlock> 要素のインスタンス `txt1` が作成され、<xref:System.Windows.Controls.DockPanel> の <xref:System.Windows.Controls.DockPanel.SetDock%2A> メソッドを利用して `Top` の <xref:System.Windows.Controls.Dock> 値が割り当てられます。 次に、<xref:System.Windows.Controls.DockPanel.GetDock%2A> メソッドを利用し、<xref:System.Windows.Controls.Dock> プロパティの値が <xref:System.Windows.Controls.TextBlock> 要素の <xref:System.Windows.Controls.TextBlock.Text%2A> に追加されます。 この例では最後に、<xref:System.Windows.Controls.TextBlock> 要素が親 <xref:System.Windows.Controls.DockPanel> の `dp1` に追加されます。  
  
 [!code-csharp[DockPanelSetDock#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelSetDock/CSharp/DockPanel_SetDock.cs#1)]
 [!code-vb[DockPanelSetDock#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelSetDock/VisualBasic/DockPanel_SetDock.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DockPanel>
- <xref:System.Windows.Controls.DockPanel.GetDock%2A>
- <xref:System.Windows.Controls.DockPanel.SetDock%2A>
- [パネルの概要](panels-overview.md)
