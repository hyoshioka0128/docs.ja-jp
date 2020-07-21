---
title: '方法: 四角形をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], rectangles
- rectangles [WPF], animating
ms.assetid: 572ffb95-790d-4ace-adbf-b2ea8a90e75b
ms.openlocfilehash: 7f7cf24f7883553329de3761ff0670e8e3a09463
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760910"
---
# <a name="how-to-animate-a-rectangle"></a>方法: 四角形をアニメーション化する
この例では、四角形のサイズと位置の変化をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.RectAnimation> クラスのインスタンスを使用して <xref:System.Windows.Media.RectangleGeometry> の <xref:System.Windows.Media.RectangleGeometry.Rect%2A> プロパティをアニメーション化します。この場合、長方形のサイズと位置の変化がアニメーション化されます。  
  
 [!code-csharp[BasicAnimations_snip#RectAnimationWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/RectAnimationExample.cs#rectanimationwholepage)]
 [!code-vb[BasicAnimations_snip#RectAnimationWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/RectAnimationExample.vb#rectanimationwholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.RectAnimation>
- <xref:System.Windows.Media.RectangleGeometry.Rect%2A>
- <xref:System.Windows.Media.RectangleGeometry>
- [アニメーションの概要](animation-overview.md)
- [グラフィックスとマルチメディア](index.md)
- [グラフィックスに関する「方法」トピック](graphics-how-to-topics.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
