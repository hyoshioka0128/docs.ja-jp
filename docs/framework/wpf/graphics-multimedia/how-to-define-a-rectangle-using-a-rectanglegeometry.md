---
title: '方法: RectangleGeometry を使用して四角形を定義する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rectangles
- rectangles [WPF], creating with RectangleGeometry class
ms.assetid: e40b8a8e-54b8-416b-a9f2-be6dca9fdf0b
ms.openlocfilehash: 146ca7017ee38ad5c1065e59662ac441e7bfbfe2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61965413"
---
# <a name="how-to-define-a-rectangle-using-a-rectanglegeometry"></a>方法: RectangleGeometry を使用して四角形を定義する
この例では、<xref:System.Windows.Media.RectangleGeometry> クラスを使用して四角形を記述する方法について説明します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.RectangleGeometry> を作成してレンダリングする方法を示します。  四角形の相対位置と大きさは、<xref:System.Windows.Rect> 構造体によって定義されます。 相対位置は `50,50`、高さと幅は両方とも `25` で、正方形が作成されます。 四角形の内部は、<xref:System.Windows.Media.Brushes.LemonChiffon%2A> ブラシで塗りつぶされ、輪郭は `1` の太さの <xref:System.Windows.Media.Brushes.Black%2A> ストロークで描かれます。  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 ![RectangleGeometry](./media/graphicsmm-rectangle.gif "graphicsmm_rectangle")  
RectangleGeometry  
  
 この例では、<xref:System.Windows.Shapes.Path> 要素を使用して、<xref:System.Windows.Media.RectangleGeometry> をレンダリングしていますが、<xref:System.Windows.Media.RectangleGeometry> オブジェクトを使用する方法は他にも多数あります。 たとえば、<xref:System.Windows.Media.RectangleGeometry> を使用して、<xref:System.Windows.UIElement> の <xref:System.Windows.UIElement.Clip%2A>、または <xref:System.Windows.Media.GeometryDrawing> の <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> を指定することができます。  
  
 その他の単純なジオメトリ クラスには <xref:System.Windows.Media.LineGeometry> と <xref:System.Windows.Media.EllipseGeometry> が含まれています。 これらのジオメトリも、もっと複雑なジオメトリも、<xref:System.Windows.Media.PathGeometry> または <xref:System.Windows.Media.StreamGeometry> を利用して作成できます。  
  
## <a name="see-also"></a>関連項目

- [ジオメトリの概要](geometry-overview.md)
- [複合図形を作成する](how-to-create-a-composite-shape.md)
- [PathGeometry を使用して図形を作成する](how-to-create-a-shape-by-using-a-pathgeometry.md)
