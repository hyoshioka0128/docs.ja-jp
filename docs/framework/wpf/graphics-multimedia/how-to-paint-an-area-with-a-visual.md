---
title: '方法: ビジュアルで領域を塗りつぶす'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- painting [WPF]
- visuals [WPF], painting with
- brushes [WPF], painting with visuals
ms.assetid: 35f92996-1d03-4542-acc4-3469dcf09492
ms.openlocfilehash: 793a14f0d395a60bf73ca7dc173b82237a139f35
ms.sourcegitcommit: 515469828d0f040e01bde01df6b8e4eb43630b06
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78849368"
---
# <a name="how-to-paint-an-area-with-a-visual"></a>方法: ビジュアルで領域を塗りつぶす
この例では、<xref:System.Windows.Media.VisualBrush> クラスを使用して <xref:System.Windows.Media.Visual> で領域を塗りつぶす方法を示します。  
  
 次の例では、いくつかのコントロールとパネルが四角形の背景として使用されています。  
  
## <a name="example"></a>例  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/VisualBrushExample.xaml#graphicsmmvisualbrushasrectanglebackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/VisualBrushExample.cs#graphicsmmvisualbrushasrectanglebackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/visualbrushexample.vb#graphicsmmvisualbrushasrectanglebackgroundexample1)]  
  
 <xref:System.Windows.Media.VisualBrush> の詳細とその他の例については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」の概要を参照してください。  
  
 このコード例は、<xref:System.Windows.Media.VisualBrush> クラスのために提供されている大規模な例の一部です。 完全なサンプルについては、[VisualBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
