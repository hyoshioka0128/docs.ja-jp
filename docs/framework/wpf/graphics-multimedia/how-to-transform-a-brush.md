---
title: '方法: ブラシを変換する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], rotating contents
- brushes [WPF], Transform property
- rotating contents of brushes [WPF]
ms.assetid: ebada2f9-f01f-4863-9ea2-c2e4e51610f1
ms.openlocfilehash: b4484e2fc1ae3e969b02b1d8f3ae4ab2a035558e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187337"
---
# <a name="how-to-transform-a-brush"></a>方法: ブラシを変換する
この例では、2 つの変換プロパティの <xref:System.Windows.Media.Brush.RelativeTransform%2A> と <xref:System.Windows.Media.Brush.Transform%2A> を使用して、<xref:System.Windows.Media.Brush> オブジェクトを変換する方法を示します。  
  
 次の例では、<xref:System.Windows.Media.RotateTransform> を使用して、<xref:System.Windows.Media.ImageBrush> のコンテンツを 45 度回転させます。  
  
 次の図は、<xref:System.Windows.Media.ImageBrush> について、<xref:System.Windows.Media.RotateTransform> が適用されていないもの、<xref:System.Windows.Media.RotateTransform> が <xref:System.Windows.Media.Brush.RelativeTransform%2A> プロパティに適用されているもの、<xref:System.Windows.Media.RotateTransform> が <xref:System.Windows.Media.Brush.Transform%2A> プロパティに適用されているものをそれぞれ示しています。  
  
 ![ブラシの RelativeTransform と Transform の設定](./media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk_graphicsmm_transformandrelativetransform")  
  
## <a name="example"></a>例  
 最初の例では、<xref:System.Windows.Media.ImageBrush> の <xref:System.Windows.Media.Brush.RelativeTransform%2A> プロパティに <xref:System.Windows.Media.RotateTransform> を適用します。 <xref:System.Windows.Media.RotateTransform> オブジェクトの <xref:System.Windows.Media.RotateTransform.CenterX%2A> プロパティおよび <xref:System.Windows.Media.RotateTransform.CenterY%2A> プロパティは両方とも 0.5 に設定されています。これは、このコンテンツの中心点の相対座標です。 結果として、<xref:System.Windows.Media.ImageBrush> コンテンツはその中心を基点に回転します。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 2 番目の例でも <xref:System.Windows.Media.RotateTransform> を <xref:System.Windows.Media.ImageBrush> に適用していますが、この例では、<xref:System.Windows.Media.Brush.RelativeTransform%2A> プロパティの代わりに <xref:System.Windows.Media.Brush.Transform%2A> プロパティを使用しています。  
  
 この例では、中心を基点にブラシを回転させるために、<xref:System.Windows.Media.RotateTransform> オブジェクトの <xref:System.Windows.Media.RotateTransform.CenterX%2A> プロパティおよび <xref:System.Windows.Media.RotateTransform.CenterY%2A> プロパティを絶対座標に設定しています。 このブラシは、175 x 90 ピクセルの四角形を描画するため、四角形の中心点は (87.5, 45) になります。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 <xref:System.Windows.Media.Brush.RelativeTransform%2A> プロパティおよび <xref:System.Windows.Media.Brush.Transform%2A> プロパティの動作については、「[ブラシの変換の概要](brush-transformation-overview.md)」をご覧ください。  
  
 完全なサンプルについては、「[ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)」を参照してください。 ブラシの詳細については、「[純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ブラシの変換の概要](brush-transformation-overview.md)
- [純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)
- [変換の概要](transforms-overview.md)
