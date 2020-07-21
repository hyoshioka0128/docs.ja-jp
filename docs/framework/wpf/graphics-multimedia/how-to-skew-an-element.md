---
title: '方法: 要素を傾斜させる'
ms.date: 03/30/2017
helpviewer_keywords:
- skewing elements [WPF]
- graphics [WPF], skewing elements
- classes [WPF], SkewTransform
ms.assetid: 56b65f2f-dc6e-4238-923f-ca44ec53c52f
ms.openlocfilehash: 10b00044c1c518641281e2e72cdb5a68474b5170
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112025"
---
# <a name="how-to-skew-an-element"></a>方法: 要素を傾斜させる
この例では、<xref:System.Windows.Media.SkewTransform> を使用して要素を傾斜させる方法を示します。 傾斜 (スキューと呼ばれることもあります) は、一様でない方法で座標空間を拡大する変換です。 <xref:System.Windows.Media.SkewTransform> の一般的な用途の 1 つは、2D オブジェクトで 3D の奥行をシミュレートすることです。  
  
 <xref:System.Windows.Media.SkewTransform> の中心点を指定するには、<xref:System.Windows.Media.SkewTransform.CenterX%2A> および <xref:System.Windows.Media.SkewTransform.CenterY%2A> プロパティを使用します。  
  
 x 軸と y 軸の傾斜角度を指定し、これらの軸に沿って現在の座標系を傾斜させるには、<xref:System.Windows.Media.SkewTransform.AngleX%2A> および <xref:System.Windows.Media.SkewTransform.AngleY%2A> プロパティを使用します。  
  
 傾斜変換の効果を予測する際は、<xref:System.Windows.Media.SkewTransform.AngleX%2A> によって元の座標系に対して x 軸の値が傾斜することを考慮します。 したがって、<xref:System.Windows.Media.SkewTransform.AngleX%2A> が 30 の場合、y 軸が原点を中心に 30 度回転し、x の値がその原点から 30 度傾斜します。 同様に、<xref:System.Windows.Media.SkewTransform.AngleY%2A> が 30 の場合、図形の y 値が原点から 30 度傾斜します。 これは、座標系の x または y での 30 度の平行移動 (移動) と同じ効果はないことに注意してください。  
  
 次の例では、中心点 (0, 0) から水平方向に 45 度の傾斜を <xref:System.Windows.Shapes.Rectangle> に適用します。  
  
## <a name="example"></a>例  
 [!code-xaml[transformsSample#41](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#41)]  
  
 次の例では、中心点 (25,25) から水平方向に 45 度の傾斜を <xref:System.Windows.Shapes.Rectangle> に適用します。  
  
 [!code-xaml[transformsSample#42](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#42)]  
  
 次の例では、中心点 (25,25) から垂直方向に 45 度の傾斜を <xref:System.Windows.Shapes.Rectangle> に適用します。  
  
 [!code-xaml[transformsSample#43](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#43)]  
  
 次の図は、この例で使用されている各種の傾斜を示しています。  
  
 ![SkewTransform の例](./media/img-wcpsdk-graphicsmm-skewtransformexample.gif "img_wcpsdk_graphicsmm_skewtransformexample")  
説明した 3 つの SkewTransform の例  
  
 サンプル全体については、「[2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.SkewTransform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
