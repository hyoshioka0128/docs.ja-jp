---
title: '方法: GeometryDrawing を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], renderable
- renderable shapes [WPF]
- graphics [WPF], GeometryDrawing class
- classes [WPF], GeometryDrawing
ms.assetid: 11d3c096-91ba-4d41-9bba-aeac0db70f97
ms.openlocfilehash: f5cdcfdb68ad8030bcbd6c689f45a8baddd000e1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904957"
---
# <a name="how-to-create-a-geometrydrawing"></a>方法: GeometryDrawing を作成する
この例では、<xref:System.Windows.Media.GeometryDrawing> を作成し、表示する方法を示します。 <xref:System.Windows.Media.GeometryDrawing> を利用すると、<xref:System.Windows.Media.Pen> と <xref:System.Windows.Media.Brush> を <xref:System.Windows.Media.Geometry> に関連付け、塗りつぶしと枠線で図形を作成できます。 <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> によって図形の構造が説明され、<xref:System.Windows.Media.GeometryDrawing.Brush%2A> によって図形の塗りつぶしが説明され、<xref:System.Windows.Media.GeometryDrawing.Pen%2A> によって図形の枠線が説明されます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.GeometryDrawing> を使用して図形を表現します。 この図形は 1 つの <xref:System.Windows.Media.GeometryGroup> オブジェクトと 2 つの <xref:System.Windows.Media.EllipseGeometry> オブジェクトによって説明されます。 図形の内側は <xref:System.Windows.Media.LinearGradientBrush> で塗りつぶされ、その枠線は <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen> で描かれます。 <xref:System.Windows.Media.GeometryDrawing> は、<xref:System.Windows.Media.ImageDrawing> と <xref:System.Windows.Controls.Image> 要素を使用して表示されます。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexamplewholepage)]  
  
 結果的に生成される <xref:System.Windows.Media.GeometryDrawing> を次の図に示します。  
  
 ![2 つの楕円からなる GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
  
 もっと複雑な描画を作成するには、<xref:System.Windows.Media.DrawingGroup> を利用し、複数の描画オブジェクトを組み合わせて 1 つの描画に複合できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingGroup>
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [ジオメトリの概要](geometry-overview.md)
- [複合描画を作成する](how-to-create-a-composite-drawing.md)
