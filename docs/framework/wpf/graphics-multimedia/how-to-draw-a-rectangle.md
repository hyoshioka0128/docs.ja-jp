---
title: '方法: 四角形を描画する'
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], rectangles
- graphics [WPF], rectangles
- rectangles [WPF], drawing
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
ms.openlocfilehash: 95191e9d90bc2ac32902399125d9a51192e897bf
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452936"
---
# <a name="how-to-draw-a-rectangle"></a>方法: 四角形を描画する
この例では、<xref:System.Windows.Shapes.Rectangle> 要素を使用して四角形を描画する方法を示します。  
  
 四角形を描画するには、<xref:System.Windows.Shapes.Rectangle> 要素を作成し、その <xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> を指定します。 四角形の内部を塗りつぶすには、その <xref:System.Windows.Shapes.Shape.Fill%2A> を設定します。 四角形に輪郭線を付けるには、その <xref:System.Windows.Shapes.Shape.Stroke%2A> と <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> プロパティを使用します。  
  
 四角形の角を丸くするには、オプションの <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> と <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> プロパティを指定します。 <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> と <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> プロパティは、四角形の角を丸めるために使用される楕円の X 軸と Y 軸の半径を設定します。  
  
 次の例では、2つの <xref:System.Windows.Shapes.Rectangle> 要素が <xref:System.Windows.Controls.Canvas> に描画されます。 最初の四角形には <xref:System.Windows.Media.Brushes.Blue%2A> の内部があります。 2 番目の四角形には、<xref:System.Windows.Media.Brushes.Blue%2A> の内部、<xref:System.Windows.Media.Brushes.Black%2A> の輪郭線、および角の丸みがあります。  
  
## <a name="example"></a>例  
 [!code-xaml[drawingwithshapeelements#Rectangle1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 この例では、<xref:System.Windows.Controls.Canvas> を使用して四角形を格納していますが、テキスト以外のコンテンツをサポートする <xref:System.Windows.Controls.Panel> または <xref:System.Windows.Controls.Control> がある四角形要素 (およびその他のすべての図形要素) を使用できます。 実際に、四角形は、<xref:System.Windows.Controls.Grid> パネルの一部の背景を提供する場合に特に便利です。 例については、「[テーブルの概要](../advanced/table-overview.md)」を参照してください。  
  
 この例は、より大きなサンプルの一部です。サンプル全体については、「[Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Shapes.Rectangle>
- [Shape 要素のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
- [テーブルの概要](../advanced/table-overview.md)
