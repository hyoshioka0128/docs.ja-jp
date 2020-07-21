---
title: '方法: 直線または線分の終点のキャップを変更する'
ms.date: 03/30/2017
helpviewer_keywords:
- Shape elements [WPF], ends
- Shape elements [WPF], caps
- graphics [WPF], Shape caps
ms.assetid: f4bf3416-b3d8-4568-b98e-3eda8f6dbf7a
ms.openlocfilehash: 5f755d7b4d1682755ea461121f91c0666d450ad1
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452780"
---
# <a name="how-to-modify-the-cap-at-the-end-of-a-line-or-segment"></a>方法: 直線または線分の終点のキャップを変更する
この例では、開いた <xref:System.Windows.Shapes.Shape> 要素の始点または終点で図形を変更する方法を示します。 開いた <xref:System.Windows.Shapes.Shape> の始点の線端を変更するには、<xref:System.Windows.Shapes.Shape.StrokeStartLineCap%2A> プロパティを使用します。 開いた <xref:System.Windows.Shapes.Shape> の終点の線端を変更するには、<xref:System.Windows.Shapes.Shape.StrokeEndLineCap%2A> プロパティを使用します。 使用可能な線端を確認するには、<xref:System.Windows.Media.PenLineCap> 列挙体をご覧ください。  
  
> [!NOTE]
> このプロパティは、開いた図形 (<xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Polyline>、開いた <xref:System.Windows.Shapes.Path> 要素など) にのみ影響します。  
  
 次の例では、4 つの <xref:System.Windows.Shapes.Polyline> 要素を描画し、それぞれの端で異なる図形セットを使用します。  
  
## <a name="example"></a>例  
 [!code-xaml[drawingwithshapeelements#ShapeLineCaps1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/linecapsandjoinsexample.xaml#shapelinecaps1)]  
  
 この例は、より大きなサンプルの一部です。サンプル全体については、「[Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Shapes.Polyline>
- <xref:System.Windows.Media.PenLineCap>
