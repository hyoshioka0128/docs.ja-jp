---
title: '方法: 複合描画を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- drawings [WPF], composite
- composite drawings [WPF]
- graphics [WPF], composite drawings
ms.assetid: 066eb0ab-5f0e-439d-85c6-dca60af269fc
ms.openlocfilehash: 0af7fbca593627ebe8cd102a02617a27eac50aa5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61909991"
---
# <a name="how-to-create-a-composite-drawing"></a>方法: 複合描画を作成する
この例では、<xref:System.Windows.Media.DrawingGroup> を使用し、複数の <xref:System.Windows.Media.Drawing> オブジェクトを組み合わせて 1 つの描画を合成することで複雑な描画を作成する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.DrawingGroup> を使用し、<xref:System.Windows.Media.GeometryDrawing> オブジェクトと <xref:System.Windows.Media.ImageDrawing> オブジェクトから複合描画を作成します。 次の図は、この例で生成される出力を示しています。  
  
 ![複数の描画を含む DrawingGroup](./media/graphicsmm-simple.jpg "graphicsmm_simple")  
DrawingGroup を利用して作成された複合描画  
  
 描画の境界を示す灰色の枠線に注目してください。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 <xref:System.Windows.Media.DrawingGroup> を使用し、<xref:System.Windows.Media.DrawingGroup.Transform%2A>、<xref:System.Windows.Media.DrawingGroup.Opacity%2A> 設定、<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>、<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>、<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>、または <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> をそれが含まれる描画に適用できます。 <xref:System.Windows.Media.DrawingGroup> は <xref:System.Windows.Media.Drawing> でもあるため、他の <xref:System.Windows.Media.DrawingGroup> オブジェクトを含めることができます。  
  
 次の例は前の例に似ていますが、追加の <xref:System.Windows.Media.DrawingGroup> オブジェクトを使用し、その描画の一部にビットマップ効果と不透明度マスクを適用する点が異なっています。 次の図は、この例で生成される出力を示しています。  
  
 ![複数の描画を含む DrawingGroup](./media/graphicsmm-multiple.jpg "graphicsmm_multiple")  
DrawingGroup オブジェクトが複数ある複合描画  
  
 描画の境界を示す灰色の枠線に注目してください。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmmultipledrawinggroupsexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmmultipledrawinggroupsexample)]  
  
 <xref:System.Windows.Media.Drawing> オブジェクトの詳細については、「[Drawing オブジェクトの概要](drawing-objects-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>
- <xref:System.Windows.Media.DrawingGroup.Transform%2A>
- <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>
- <xref:System.Windows.Media.DrawingGroup.Opacity%2A>
- <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>
- <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
