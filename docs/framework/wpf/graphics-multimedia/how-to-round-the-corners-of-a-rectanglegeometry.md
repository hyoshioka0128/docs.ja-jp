---
title: '方法: RectangleGeometry の角に丸みを付ける'
ms.date: 03/30/2017
helpviewer_keywords:
- corners [WPF], rounding
- RectangleGeometry class [WPF], rounding corners
- graphics [WPF], rounding corners of RectangleGeometry objects [WPF]
- rounding corners of RectangleGeometry objects [WPF]
ms.assetid: 926644bc-1357-4c0b-ac81-694bd090ae87
ms.openlocfilehash: eb2f173bedb903e12b2795264c684524cfa09825
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651396"
---
# <a name="how-to-round-the-corners-of-a-rectanglegeometry"></a>方法: RectangleGeometry の角に丸みを付ける
<xref:System.Windows.Media.RectangleGeometry> の角を丸めるには、その <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> と <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> のプロパティを 0 より大きい値に設定します。 値が大きいほど、四角形の角が丸くなります。  
  
## <a name="example"></a>例  
 次の例は <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> と <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> の設定が異なるいくつかの <xref:System.Windows.Media.RectangleGeometry> オブジェクトを示しています。 <xref:System.Windows.Media.RectangleGeometry> オブジェクトは <xref:System.Windows.Shapes.Path> 要素を使用して表示されます。  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRoundedRectangleGeometryExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/RectangleGeometryRoundedCornerExample.xaml#graphicsmmroundedrectanglegeometryexamplewholepage)]  
  
 ![RadiusX&#47;RadiusY の設定が異なる四角形](./media/graphicsmm-rounded.png "graphicsmm_rounded")  
角が丸い四角形  
  
## <a name="see-also"></a>関連項目

- [ジオメトリの概要](geometry-overview.md)
- [複合図形を作成する](how-to-create-a-composite-shape.md)
- [PathGeometry を使用して図形を作成する](how-to-create-a-shape-by-using-a-pathgeometry.md)
