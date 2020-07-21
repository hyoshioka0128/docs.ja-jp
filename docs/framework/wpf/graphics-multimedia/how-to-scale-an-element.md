---
title: '方法: 要素をスケーリングする'
ms.date: 03/30/2017
helpviewer_keywords:
- scaling [WPF], elements
- graphics [WPF], scaling elements
ms.assetid: 18158d94-bbe7-4f6a-814e-84d27fa748bf
ms.openlocfilehash: 34d954f68747be9eedc0ef71634e0c18b411d260
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112051"
---
# <a name="how-to-scale-an-element"></a>方法: 要素をスケーリングする
この例では、<xref:System.Windows.Media.ScaleTransform> を使用して要素を拡大縮小する方法を示します。  
  
 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> プロパティと <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> プロパティは、指定した係数で要素のサイズを変更します。 たとえば、<xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 値が 1.5 の場合、要素は元の幅の 150% に拡大します。 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 値が 0.5 の場合は、要素の高さが 50% 縮小します。  
  
 <xref:System.Windows.Media.ScaleTransform.CenterX%2A> プロパティと <xref:System.Windows.Media.ScaleTransform.CenterY%2A> プロパティを使用して、拡大縮小操作の中心となる点を指定します。 既定では、<xref:System.Windows.Media.ScaleTransform> の中心点は (0, 0) であり、四角形の左上隅に該当します。 <xref:System.Windows.Media.Transform> を適用すると、オブジェクトが存在する座標空間が変更されるため、要素が移動するという効果に加え、大きくなるように見えるという効果が起こります。  
  
 次の例は、<xref:System.Windows.Media.ScaleTransform> を使用して、50 × 50 の <xref:System.Windows.Shapes.Rectangle> のサイズを 2 倍にします。 <xref:System.Windows.Media.ScaleTransform> の値は、<xref:System.Windows.Media.ScaleTransform.CenterX%2A> と <xref:System.Windows.Media.ScaleTransform.CenterY%2A> の両方に対して 0 (既定) に設定されています。  
  
## <a name="example"></a>例  
 [!code-xaml[transformsSample#21](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#21)]  
  
 通常は、<xref:System.Windows.Media.ScaleTransform.CenterX%2A> と <xref:System.Windows.Media.ScaleTransform.CenterY%2A> を、拡大縮小するオブジェクトの中心、つまり (<xref:System.Windows.FrameworkElement.Width%2A>/2, <xref:System.Windows.FrameworkElement.Height%2A>/2) に設定します。  
  
 次の例に、サイズを 2 倍にしたもう 1 つの <xref:System.Windows.Shapes.Rectangle> を示します。ただし、この <xref:System.Windows.Media.ScaleTransform> では、<xref:System.Windows.Media.ScaleTransform.CenterX%2A> と <xref:System.Windows.Media.ScaleTransform.CenterY%2A>の両方の値が 25 に設定されており、これは長方形の中心に相当します。  
  
 [!code-xaml[transformsSample#22](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#22)]  
  
 次の図は、2 つの <xref:System.Windows.Media.ScaleTransform> 操作間の相違を示しています。 点線は、拡大/縮小する前の四角形のサイズと位置を示しています。  
  
 ![中心点が異なる 2 倍の拡大](./media/wcpsdk-graphicsmm-scalecenter.gif "wcpsdk_graphicsmm_scalecenter")  
2 つの ScaleTransform 操作では、ScaleX と ScaleY の値は同じですが、中心点が異なっています。  
  
 サンプル全体については、「[2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.ScaleTransform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
