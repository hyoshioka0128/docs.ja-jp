---
title: '方法: 純色で領域を塗りつぶす'
ms.date: 03/30/2017
helpviewer_keywords:
- solid colors [WPF], painting with
- brushes [WPF], painting with solid colors
- painting [WPF], with solid colors
ms.assetid: 5d27d8a7-4bd7-4063-bdf3-2c5c0f19f9d3
ms.openlocfilehash: be28a0af04c4e43cdf745a5429468aee99e34c40
ms.sourcegitcommit: 515469828d0f040e01bde01df6b8e4eb43630b06
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78849523"
---
# <a name="how-to-paint-an-area-with-a-solid-color"></a>方法: 純色で領域を塗りつぶす
純色で領域を塗りつぶす場合、<xref:System.Windows.Media.Brushes.Red%2A> や <xref:System.Windows.Media.Brushes.Blue%2A> などの定義済みのシステム ブラシを使用することも、新しい <xref:System.Windows.Media.SolidColorBrush> を作成し、アルファ、赤、緑、青の値を使用してその <xref:System.Windows.Media.SolidColorBrush.Color%2A> を記述することもできます。 XAML では、16 進数表記を使用して、純色で領域を塗りつぶすこともできます。  
  
 これらの各手法を使用して <xref:System.Windows.Shapes.Rectangle> を青で塗りつぶす例を次に示します。  
  
## <a name="example"></a>例  
 **定義済みのブラシの使用**  
  
 次の例では、定義済みのブラシ <xref:System.Windows.Media.Brushes.Blue%2A> を使用して、四角形を青で塗りつぶします。  
  
 [!code-xaml[brushsamples_snip#_graphicsmm_PredefinedBrush1](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_predefinedbrush1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_PredefinedBrush1](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_predefinedbrush1)]  
  
 **16 進数表記の使用**  
  
 次の例では、8 桁の 16 進数表記を使用して、四角形を青で塗りつぶします。  
  
 [!code-xaml[brushsamples_snip#_graphicsmm_HexNotation8Digit1](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_hexnotation8digit1)]  
  
 **ARGB 値の使用**  
  
 次の例では、<xref:System.Windows.Media.SolidColorBrush> を作成し、青色の ARGB 値を使用してその <xref:System.Windows.Media.SolidColorBrush.Color%2A> を記述します。  
  
 [!code-xaml[brushsamples_snip#_graphicsmm_RgbNotation1](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_rgbnotation1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_RgbNotation1](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_rgbnotation1)]  
  
 色を記述するその他の方法については、<xref:System.Windows.Media.Color> 構造体を参照してください。  
  
 **関連トピック**  
  
 <xref:System.Windows.Media.SolidColorBrush> の詳細とその他の例については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」を参照してください。  
  
 このコード例は、<xref:System.Windows.Media.SolidColorBrush> クラスのために提供されている大規模な例の一部です。 完全なサンプルについては、「[ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Brushes>
