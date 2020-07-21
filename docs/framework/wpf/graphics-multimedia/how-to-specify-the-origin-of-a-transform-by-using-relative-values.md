---
title: '方法: 変換の原点を相対値で指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- origins of Transforms [WPF]
- Transforms [WPF], origins of
- graphics [WPF], origins of Transforms
ms.assetid: f4dbc29d-93c7-41cd-96d8-5cfd8624b470
ms.openlocfilehash: 48b3b0df8dab8516873495a996074eae57ffe00f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651143"
---
# <a name="how-to-specify-the-origin-of-a-transform-by-using-relative-values"></a>方法: 変換の原点を相対値で指定する
この例は、相対値を使用して、<xref:System.Windows.FrameworkElement> に適用される <xref:System.Windows.UIElement.RenderTransform%2A> の原点を指定する方法を示します。  
  
 <xref:System.Windows.UIElement.RenderTransform%2A> プロパティを使用して <xref:System.Windows.FrameworkElement> の回転、拡大縮小、または傾斜を行うと、既定の設定により変換が要素の左上隅に適用されます。 要素の中心から回転、拡大縮小、または傾斜させる場合は、要素の中心に変換の中心を設定して補正することができます。 ただし、そのソリューションでは、要素のサイズがわかっている必要があります。 要素の中心に変換を適用する簡単な方法は、変換自体に中心値を設定する代わりに、<xref:System.Windows.UIElement.RenderTransformOrigin%2A> プロパティを (0.5, 0.5) に設定することです。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.RotateTransform> を使用して、<xref:System.Windows.Controls.Button> を 45 度時計回りに回転しています。 この例では中心を指定していないので、ボタンは、左上隅の点 (0, 0) の周りを回転します。 <xref:System.Windows.Media.RotateTransform> は <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに適用されます。  
  
 次の図は、それに続く例の変換結果を示しています。  
  
 ![RenderTransform を使用して変換されたボタン](./media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm_RenderTransformWithDefaultCenter")  
RenderTransform プロパティを使用して時計回りに 45 度回転  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 次の例では、<xref:System.Windows.Controls.Button> を 45 度時計回りに回転するために <xref:System.Windows.Media.RotateTransform> も使用しています。ただし、この例ではボタンの <xref:System.Windows.UIElement.RenderTransformOrigin%2A> が (0.5, 0.5) に設定されています。 その結果、回転は、左上隅ではなくボタンの中心に適用されています。  
  
 次の図は、それに続く例の変換結果を示しています。  
  
 ![中心を軸に変換されたボタン](./media/graphicsmm-rendertransformrelativecenter.png "graphicsmm_RenderTransformRelativeCenter")  
RenderTransformOrigin が (0.5, 0.5) の RenderTransform を使用した 45 度の回転  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 <xref:System.Windows.FrameworkElement> オブジェクトの変換について詳しくは、「[変換の概要](transforms-overview.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Transform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
