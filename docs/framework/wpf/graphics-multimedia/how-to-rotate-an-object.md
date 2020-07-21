---
title: '方法: オブジェクトを回転させる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rotating objects [WPF]
- rotating objects [WPF]
ms.assetid: ee3466cd-e66f-4e8f-8a5a-71d77bc1e390
ms.openlocfilehash: e17d3b7b9986b477df198480129edaf4c139c6bc
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112064"
---
# <a name="how-to-rotate-an-object"></a>方法: オブジェクトを回転させる
次の例では、オブジェクトを回転させる方法を示します。 この例では、最初に <xref:System.Windows.Media.RotateTransform> を作成し、その <xref:System.Windows.Media.RotateTransform.Angle%2A> を度単位で指定します。  
  
 次の例では、<xref:System.Windows.Shapes.Polyline> オブジェクトを、左上隅を中心に 45 度回転します。  
  
## <a name="example"></a>例  
 [!code-xaml[Transforms_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineabouttopleft)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineabouttopleft)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineabouttopleft)]  
  
 <xref:System.Windows.Media.RotateTransform> の <xref:System.Windows.Media.RotateTransform.CenterX%2A> と <xref:System.Windows.Media.RotateTransform.CenterY%2A> プロパティは、オブジェクトを回転させる中心点を指定します。 この中心点は、変換する要素の座標空間で表します。 既定では、回転は (0,0) に適用されます。これは変換対象のオブジェクトの左上隅です。  
  
 次の例では、<xref:System.Windows.Shapes.Polyline> オブジェクトを、点 (25,50) を中心にして時計回りに 45 度回転します。  
  
 [!code-xaml[Transforms_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineaboutcenter)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineaboutcenter)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineaboutcenter)]  
  
 次の図は、2 つのオブジェクトに <xref:System.Windows.Media.Transform> を適用した結果を示しています。  
  
 ![中心点が異なる 45 度の回転](./media/wcpsdk-graphicsmm-rotatetransform45degrees.gif "wcpsdk_graphicsmm_rotatetransform45degrees")  
異なる中心点を軸に 45 度回転させた 2 つのオブジェクト  
  
 前の例での <xref:System.Windows.Shapes.Polyline> は <xref:System.Windows.UIElement> です。 <xref:System.Windows.UIElement> の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.Transform> を適用するときは、<xref:System.Windows.UIElement.RenderTransformOrigin%2A> プロパティを使用して、その要素に適用するすべての <xref:System.Windows.Media.Transform> の原点を指定できます。 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> プロパティは相対座標を使用するため、要素のサイズがわからなくても、要素の中心に変換を適用できます。 詳細および例については、「[変換の原点を相対値で指定する](how-to-specify-the-origin-of-a-transform-by-using-relative-values.md)」を参照してください。  
  
 完全なサンプルについては、「[2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Transform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
