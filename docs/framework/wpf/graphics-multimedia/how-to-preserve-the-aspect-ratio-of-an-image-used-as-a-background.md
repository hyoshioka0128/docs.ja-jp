---
title: '方法: 背景として使用するイメージの縦横比を保持する'
ms.date: 03/30/2017
helpviewer_keywords:
- aspect ratios of background images [WPF], preserving
- brushes [WPF], preserving aspect ratios of background images
- background images [WPF], preserving aspect ratios
ms.assetid: 28c39478-13d7-4011-80a3-8b9cc3e54478
ms.openlocfilehash: b467fcd353994faef19b5a997e03d6582789eac1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186030"
---
# <a name="how-to-preserve-the-aspect-ratio-of-an-image-used-as-a-background"></a>方法: 背景として使用するイメージの縦横比を保持する
この例では、イメージの縦横比を保持するために <xref:System.Windows.Media.ImageBrush> の <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを使用する方法を示します。  
  
 既定では、<xref:System.Windows.Media.ImageBrush> を使用して領域を塗りつぶすと、出力領域が完全に塗りつぶされるようにコンテンツが引き伸ばされます。 出力領域とイメージの縦横比が異なる場合は、この引き伸ばしによってイメージがゆがめられます。  
  
 <xref:System.Windows.Media.ImageBrush> がそのイメージの縦横比を保持するようにするには、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを <xref:System.Windows.Media.Stretch.Uniform> または <xref:System.Windows.Media.Stretch.UniformToFill> に設定します。  
  
## <a name="example"></a>例  
 次の例では、2 つの <xref:System.Windows.Media.ImageBrush> オブジェクトを使用して、2 つの四角形を塗りつぶしています。 これらの四角形は 300 × 150 ピクセルで、どちらも 300 × 300 ピクセルのイメージを保持しています。 最初のブラシの <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティは <xref:System.Windows.Media.Stretch.Uniform> に設定され、2 番目のブラシの <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティは <xref:System.Windows.Media.Stretch.UniformToFill> に設定されています。  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushStretchModesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/StretchModes.cs#imagebrushstretchmodesexamplewholepage)]  
  
 <xref:System.Windows.Media.TileBrush.Stretch%2A> を <xref:System.Windows.Media.Stretch.Uniform> に設定した最初のブラシの出力を次の図に示します。  
  
 ![Uniform 拡大を使用した ImageBrush](./media/graphicsmm-imagebrushuniformstretch.jpg "graphicsmm_ImageBrushUniformStretch")  
  
 <xref:System.Windows.Media.TileBrush.Stretch%2A> を <xref:System.Windows.Media.Stretch.UniformToFill> に設定した 2 番目のブラシの出力を次の図に示します。  
  
 ![UniformToFill 拡大を使用した ImageBrush](./media/graphicsmm-imagebrushuniformtofillstretch.jpg "graphicsmm_ImageBrushUniformToFillStretch")  
  
 <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティは、他の <xref:System.Windows.Media.TileBrush> オブジェクト、つまり <xref:System.Windows.Media.DrawingBrush> と <xref:System.Windows.Media.VisualBrush> に対してもまったく同じように動作することに注意してください。 <xref:System.Windows.Media.ImageBrush> と他の <xref:System.Windows.Media.TileBrush> オブジェクトの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。  
  
 また、<xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティは、<xref:System.Windows.Media.TileBrush> コンテンツを出力領域に合わせて引き伸ばす方法を指定するように見えますが、実際には基本タイルを塗りつぶすように <xref:System.Windows.Media.TileBrush> コンテンツを引き伸ばす方法を指定することにも注意してください。 詳細については、「<xref:System.Windows.Media.TileBrush>」を参照してください。  
  
 このコード例は、<xref:System.Windows.Media.ImageBrush> クラスで提供されている、より大きな例の一部です。 完全なサンプルについては、「[ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.TileBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
