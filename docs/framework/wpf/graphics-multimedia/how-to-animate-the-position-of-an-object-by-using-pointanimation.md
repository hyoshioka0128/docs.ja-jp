---
title: '方法: PointAnimation を使用してオブジェクトの位置をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], animation
- animation [WPF], PointAnimation
ms.assetid: 42310977-cc90-438a-8a47-0345898e01be
ms.openlocfilehash: 1ef3f77e551affaa7e61d2aabf95f10c29275417
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651351"
---
# <a name="how-to-animate-the-position-of-an-object-by-using-pointanimation"></a>方法: PointAnimation を使用してオブジェクトの位置をアニメーション化する
この例は、<xref:System.Windows.Media.Animation.PointAnimation> クラスを使用して、<xref:System.Windows.Shapes.Path> に沿ってオブジェクトをアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例は、画面上のある点から別の点まで、<xref:System.Windows.Shapes.Path> に沿って楕円が移動しています。 この例では、<xref:System.Windows.Media.Animation.PointAnimation> を使用して <xref:System.Windows.Media.EllipseGeometry.Center%2A> プロパティをアニメーション化することによって、<xref:System.Windows.Media.EllipseGeometry> の位置をアニメーション化しています。  
  
 [!code-csharp[BasicAnimations_snip#PointAnimationWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/PointAnimationExample.cs#pointanimationwholepage)]
 [!code-vb[BasicAnimations_snip#PointAnimationWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/PointAnimationExample.vb#pointanimationwholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.PointAnimation>
- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.EllipseGeometry>
- <xref:System.Windows.Media.EllipseGeometry.Center%2A>
- [アニメーションの概要](animation-overview.md)
- [グラフィックスとマルチメディア](index.md)
- [グラフィックスに関する「方法」トピック](graphics-how-to-topics.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
