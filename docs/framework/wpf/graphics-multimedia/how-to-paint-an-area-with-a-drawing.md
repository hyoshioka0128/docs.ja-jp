---
title: '方法: 描画を使用して領域を塗りつぶす'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with drawings
- painting [WPF], with drawings
- drawings [WPF], painting with
ms.assetid: c10dc4b1-09b1-41e8-ad14-456b5fb377df
ms.openlocfilehash: 6b204ae631912181333e2559ebadcdc37e7693b7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010075"
---
# <a name="how-to-paint-an-area-with-a-drawing"></a>方法: 描画を使用して領域を塗りつぶす
この例では、描画を使用して領域を塗りつぶす方法を示します。 描画を使用して領域を塗りつぶすには、<xref:System.Windows.Media.DrawingBrush> と、1 つ以上の <xref:System.Windows.Media.Drawing> オブジェクトを使用します。   次の例では、<xref:System.Windows.Media.DrawingBrush> を使用して 2 つの楕円の描画でオブジェクトを塗りつぶす方法を示しています。  
  
## <a name="example"></a>例  
 [!code-xaml[drawingbrush_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/DrawingBrushExample.vb#drawingbrushexamplewholepage)]  
  
 この例の出力を次の図に示します。  
  
 ![DrawingBrush からの出力](./media/graphicsmm-drawingbrush-simple.png "graphicsmm_drawingbrush_simple")  
  
 (図形の中心が白い理由は、「[複合図形の塗りつぶしを制御する](how-to-control-the-fill-of-a-composite-shape.md)」に説明されています。)  
  
 <xref:System.Windows.Media.DrawingBrush> オブジェクトの <xref:System.Windows.Media.TileBrush.Viewport%2A> と <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティを設定すると、繰り返しパターンを作成できます。 2 つの楕円の描画から作成されるパターンで、オブジェクトを塗りつぶす例を次に示します。  
  
 [!code-xaml[drawingbrush_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/TiledDrawingBrushExample.xaml#tileddrawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/TiledDrawingBrushExample.cs#tileddrawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/TiledDrawingBrushExample.vb#tileddrawingbrushexamplewholepage)]  
  
 並べて表示された <xref:System.Windows.Media.DrawingBrush> の出力を次の図に示します。  
  
 ![並べて表示された DrawingBrush の出力](./media/graphicsmm-drawingbrush-tiled.png "graphicsmm_drawingbrush_tiled")  
  
 描画ブラシの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。 <xref:System.Windows.Media.Drawing> オブジェクトの詳細については、「[Drawing オブジェクトの概要](drawing-objects-overview.md)」を参照してください。
