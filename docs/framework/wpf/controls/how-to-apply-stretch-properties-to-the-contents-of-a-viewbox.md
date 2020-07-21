---
title: '方法: Viewbox のコンテンツに Stretch プロパティを適用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StretchDirection properties [WPF]
- Stretch properties [WPF]
- controls [WPF], Viewbox
- Viewbox control [WPF]
ms.assetid: b9c22ef4-bce4-4300-9e0c-8260b7db83cc
ms.openlocfilehash: 08358ea07e0c41e3b7cdf52251a3ed4296035e2d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62019036"
---
# <a name="how-to-apply-stretch-properties-to-the-contents-of-a-viewbox"></a>方法: Viewbox のコンテンツに Stretch プロパティを適用する
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Controls.Viewbox> の <xref:System.Windows.Controls.Viewbox.StretchDirection%2A> プロパティと <xref:System.Windows.Controls.Viewbox.Stretch%2A> プロパティの値を変更する方法を示します。  
  
 最初の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して、<xref:System.Windows.Controls.Viewbox> 要素を定義します。 400 の <xref:System.Windows.FrameworkElement.MaxWidth%2A> と <xref:System.Windows.FrameworkElement.MaxHeight%2A> が割り当てられます。 この例では、<xref:System.Windows.Controls.Viewbox> 内に <xref:System.Windows.Controls.Image> 要素を入れ子にしています。 <xref:System.Windows.Controls.Viewbox.Stretch%2A> および <xref:System.Windows.Controls.StretchDirection> の列挙体のプロパティ値に対応する <xref:System.Windows.Controls.Button> 要素により、入れ子になった <xref:System.Windows.Controls.Image> の伸縮動作の操作が行われます。  
  
 [!code-xaml[viewboxStretchLayoutSamp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml#1)]  
  
 次の分離コードファイルでは、前の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の例で定義されている <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントが処理されます。  
  
 [!code-csharp[viewboxStretchLayoutSamp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[viewboxStretchLayoutSamp#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/viewboxStretchLayoutSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Viewbox>
- <xref:System.Windows.Media.Stretch>
- <xref:System.Windows.Controls.StretchDirection>
