---
title: '方法: グリッドを使用して標準 UI ダイアログ ボックスをビルドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dialog boxes [WPF], creating
- Grid control [WPF], creating [WPF], dialog box
ms.assetid: d6ac3d51-844b-4d29-96d8-81a696a7b960
ms.openlocfilehash: 68c9653e616388374aad2ad33ac7dab68446241d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923416"
---
# <a name="how-to-build-a-standard-ui-dialog-box-by-using-grid"></a>方法: グリッドを使用して標準 UI ダイアログ ボックスをビルドする
この例では、<xref:System.Windows.Controls.Grid> 要素を使用して、標準 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] ダイアログ ボックスを作成する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、Windows オペレーティング システムの **[実行]** ダイアログ ボックスのようなダイアログ ボックスを作成します。  
  
 この例では、<xref:System.Windows.Controls.Grid> を作成し、<xref:System.Windows.Controls.ColumnDefinition> クラスと <xref:System.Windows.Controls.RowDefinition> クラスを使用して、5 つの列と 4 つの行を定義します。  
  
 次に、この例では、ダイアログ ボックスにあるイメージを表すために、<xref:System.Windows.Controls.Image>、`RunIcon.png` を追加して配置します。 イメージは、<xref:System.Windows.Controls.Grid> の最初の列と行 (左上隅) に配置されます。  
  
 次に、この例では、最初の行の残りの列にまたがる <xref:System.Windows.Controls.TextBlock> 要素を最初の列に追加します。 最初の列の 2 番目の行に別の <xref:System.Windows.Controls.TextBlock> 要素が追加されて、 **[開く]** テキスト ボックスが表されます。 <xref:System.Windows.Controls.TextBlock> が続き、データ入力領域が表されます。  
  
 最後に、この例では、最後の行に 3 つの <xref:System.Windows.Controls.Button> 要素を追加します。これにより、**OK** イベント、**キャンセル** イベント、**参照**イベントが表されます。  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.GridUnitType>
- [パネルの概要](panels-overview.md)
- [方法トピック](grid-how-to-topics.md)
