---
title: '方法: イメージで領域を塗りつぶす'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [WPF], painting with
- painting [WPF], with images
- brushes [WPF], painting with images
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
ms.openlocfilehash: 92969778c04c6ac634a2964c402d6c3439b96b49
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186050"
---
# <a name="how-to-paint-an-area-with-an-image"></a>方法: イメージで領域を塗りつぶす
この例では、<xref:System.Windows.Media.ImageBrush> クラスを使用してイメージで領域を塗りつぶす方法を示します。 <xref:System.Windows.Media.ImageBrush> は、<xref:System.Windows.Media.ImageBrush.ImageSource%2A> プロパティによって指定された 1 つのイメージを表示します。  
  
## <a name="example"></a>例  
 次の例は、<xref:System.Windows.Media.ImageBrush> を使用して、ボタンの <xref:System.Windows.Controls.Control.Background%2A> を塗りつぶします。  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 既定では、<xref:System.Windows.Media.ImageBrush> はイメージを引き伸ばして、描画する領域を完全に塗りつぶします。 前の例のようにイメージを引き伸ばしてボタンを塗りつぶすと、イメージにゆがみが生じることがあります。 この動作を制御するには、<xref:System.Windows.Media.TileBrush> の <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティを <xref:System.Windows.Media.Stretch.Uniform> または <xref:System.Windows.Media.Stretch.UniformToFill> に設定します。これにより、ブラシは画像の縦横比を保持します。  
  
 <xref:System.Windows.Media.ImageBrush> の <xref:System.Windows.Media.TileBrush.Viewport%2A> および <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティを設定すると、繰り返しパターンを作成できます。 次の例は、イメージから作成したパターンを使用してボタンを塗りつぶします。  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 <xref:System.Windows.Media.ImageBrush> クラスの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。  
  
 このコード例は、<xref:System.Windows.Media.ImageBrush> クラスで提供されている、より大きな例の一部です。 完全なサンプルについては、[ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
