---
title: '方法: ポリライン要素を使用してポリラインを描画する'
ms.date: 03/30/2017
helpviewer_keywords:
- connected lines [WPF]
- polylines [WPF], drawing
- graphics [WPF], polylines
- lines [WPF], connected (see polylines)
- drawing [WPF], polylines
ms.assetid: 65db8935-d047-4295-87c4-b427ff3ad293
ms.openlocfilehash: 6698141bcaa3b0fd5f5b9cf66bcab1be1f4ea2f0
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452962"
---
# <a name="how-to-draw-a-polyline-by-using-the-polyline-element"></a>方法: ポリライン要素を使用してポリラインを描画する
この例では、<xref:System.Windows.Shapes.Polyline> 要素を使用してポリラインを描画する方法を示します。ポリラインは、接続された一連の線です。  
  
 ポリラインを描画するには、<xref:System.Windows.Shapes.Polyline> 要素を作成し、その <xref:System.Windows.Shapes.Polyline.Points%2A> プロパティを使用して図形の頂点を指定します。 最後に、<xref:System.Windows.Shapes.Shape.Stroke%2A> および <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> プロパティを使用してポリラインの輪郭を記述します。ストロークのない線は表示されないためです。  
  
> [!NOTE]
> <xref:System.Windows.Shapes.Polyline> 要素は閉じた図形ではないため、図形の輪郭を意図的に閉じた場合でも、<xref:System.Windows.Shapes.Shape.Fill%2A> プロパティに効力はありません。 <xref:System.Windows.Shapes.Shape.Fill%2A> で閉じた図形を作成するには、<xref:System.Windows.Shapes.Polygon> 要素を使用します。  
  
 次の例では、<xref:System.Windows.Controls.Canvas> 内に 2 つの <xref:System.Windows.Shapes.Polyline> 要素を描画しています。  
  
## <a name="example"></a>例  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、ポイントを表す有効な構文は、コンマで区切られた x と y の座標ペアのスペース区切りリストです。  
  
 [!code-xaml[drawingwithshapeelements#PolylineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polylineexample.xaml#polylineexample1)]  
  
 この例では、<xref:System.Windows.Controls.Canvas> を使用してポリラインを格納していますが、テキスト以外のコンテンツをサポートする <xref:System.Windows.Controls.Panel> または <xref:System.Windows.Controls.Control> があるポリライン要素 (およびその他のすべての図形要素) を使用できます。  
  
 この例は、大規模なサンプルの一部です。完全なサンプルについては、「[Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Shapes.Polyline>
- <xref:System.Windows.Shapes.Polygon>
- <xref:System.Windows.Shapes.Shape>
- [Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
