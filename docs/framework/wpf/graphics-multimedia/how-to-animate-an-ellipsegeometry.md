---
title: '方法: EllipseGeometry をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], EllipseGeometry objects [WPF]
- EllipseGeometry objects [WPF], animating
- graphics [WPF], animation
ms.assetid: 767b9b6e-9cb7-482e-b6c2-fee7750c3995
ms.openlocfilehash: 0f8174a2144435c9ad65904ee587355e8b38e935
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760923"
---
# <a name="how-to-animate-an-ellipsegeometry"></a>方法: EllipseGeometry をアニメーション化する
この例では、<xref:System.Windows.Shapes.Path> 要素内で <xref:System.Windows.Media.Geometry> をアニメーション化する方法を示します。 次の例では、<xref:System.Windows.Media.Animation.PointAnimation> は <xref:System.Windows.Media.EllipseGeometry> の <xref:System.Windows.Media.EllipseGeometry.Center%2A> をアニメーション化するために使用されます。  
  
## <a name="example"></a>例  
 [!code-xaml[animatepath_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/animatepath_snip_XAML/CS/EllipseGeometryExample.xaml#1)]  
  
 [!code-csharp[animatepath_snip#101](~/samples/snippets/csharp/VS_Snippets_Wpf/animatepath_snip/CSharp/EllipseGeometryExample.cs#101)]  
  
 [!code-vb[animatepath_snip#201](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animatepath_snip/VisualBasic/EllipseGeometryExample.vb#201)]  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [ジオメトリの概要](geometry-overview.md)
