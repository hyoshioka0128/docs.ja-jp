---
title: '方法: TileBrush を使用してさまざまなタイル パターンを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF], creating tile patterns
- tile patterns [WPF], creating
- creating [WPF], tile patterns with TileBrush
ms.assetid: 5aa46632-3527-4668-9d8d-0375c8af28aa
ms.openlocfilehash: c1051b234961eee9ae740af2abac3d64c523656c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61905134"
---
# <a name="how-to-create-different-tile-patterns-with-a-tilebrush"></a>方法: TileBrush を使用してさまざまなタイル パターンを作成する
この例からは、<xref:System.Windows.Media.TileBrush> の <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティを利用してパターンを作成する方法がわかります。  
  
 <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティでは、<xref:System.Windows.Media.TileBrush> のコンテンツを繰り返す方法を、つまり、出力領域を塗りつぶす目的で並べる方法を指定できます。 パターンを作成するために、<xref:System.Windows.Media.TileBrush.TileMode%2A> を <xref:System.Windows.Media.TileMode.Tile>、<xref:System.Windows.Media.TileMode.FlipX>、<xref:System.Windows.Media.TileMode.FlipY>、<xref:System.Windows.Media.TileMode.FlipXY> に設定します。 また、色を塗りつぶす領域より小さくなるよう、<xref:System.Windows.Media.TileBrush> の <xref:System.Windows.Media.TileBrush.Viewport%2A> を設定する必要があります。このように設定しないと、使用する <xref:System.Windows.Media.TileBrush.TileMode%2A> 設定に関係なく、タイルが 1 つだけ生成されます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.DrawingBrush> オブジェクトが 5 つ作成され、それぞれに異なる <xref:System.Windows.Media.TileBrush.TileMode%2A> 設定が与えられ、このオブジェクトを利用して 5 つの四角形が塗りつぶされます。 この例では <xref:System.Windows.Media.DrawingBrush> クラスを使用することで <xref:System.Windows.Media.TileBrush.TileMode%2A> 動作が示されていますが、<xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティは、すべての <xref:System.Windows.Media.TileBrush> オブジェクトに対して、つまり、<xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.VisualBrush>、<xref:System.Windows.Media.DrawingBrush> に対して同じように機能します。  
  
 次の図は、この例で生成される出力を示しています。  
  
 ![TileBrush タイルの出力例](./media/graphicsmm-drawingbrushtilemodeexample.png "graphicsmm_DrawingBrushTileModeExample")  
TileMode プロパティで作成されたタイル パターン  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/TileModeExample.cs#graphicsmmdrawingbrushtilemodeexample)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/tilemodeexample.vb#graphicsmmdrawingbrushtilemodeexample)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/TileModeExample.xaml#graphicsmmdrawingbrushtilemodeexample)]  
  
## <a name="see-also"></a>関連項目

- [TileBrush のタイル サイズを設定する](how-to-set-the-tile-size-for-a-tilebrush.md)
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
