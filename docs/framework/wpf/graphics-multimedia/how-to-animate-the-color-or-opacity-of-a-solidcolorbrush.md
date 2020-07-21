---
title: '方法: SolidColorBrush の色または不透明度をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- SolidColorBrush [WPF], animating color of
- colors [WPF], animating
- opacity [WPF], animating
- animation [WPF], color of SolidColorBrush
- animation [WPF], opacity of SolidColorBrush
- SolidColorBrush [WPF], animating opacity of
ms.assetid: d9154354-843f-4713-bad1-35bb0ba6eaeb
ms.openlocfilehash: 08b85935e0cb1ababd1fb63b9d02518ea3fcfa17
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452884"
---
# <a name="how-to-animate-the-color-or-opacity-of-a-solidcolorbrush"></a>方法: SolidColorBrush の色または不透明度をアニメーション化する
この例では、<xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> および <xref:System.Windows.Media.Brush.Opacity%2A> をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、3 つのアニメーションを使用して、<xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> および <xref:System.Windows.Media.Brush.Opacity%2A> をアニメーション化します。  
  
- 最初のアニメーションの <xref:System.Windows.Media.Animation.ColorAnimation> では、マウスが四角形の中に入ると、ブラシの色が <xref:System.Windows.Media.Colors.Gray%2A> に変わります。  
  
- 次のアニメーション (別の <xref:System.Windows.Media.Animation.ColorAnimation>) では、マウスが四角形の外に出ると、ブラシの色が <xref:System.Windows.Media.Colors.Orange%2A> に変わります。  
  
- 最後のアニメーションの <xref:System.Windows.Media.Animation.DoubleAnimation> では、マウスの左ボタンを押すと、ブラシの不透明度が 0.0 に変わります。  
  
 [!code-csharp[brushanimations_snip#SolidColorBrushAnimationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/brushanimations_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushanimationexample)]  
  
 さまざまな種類のブラシをアニメーション化する方法を示した、より完全なサンプルについては、[ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)を参照してください。 アニメーション化の詳細については、「[アニメーションの概要](animation-overview.md)」を参照してください。  
  
 他のアニメーション例との一貫性を保つために、この例のコード バージョンでは、<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用してアニメーションを適用しています。 ただし、コード内で 1 つのアニメーションを適用する場合は、<xref:System.Windows.Media.Animation.Storyboard> よりも <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用する方が簡単です。 例については、「[ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
- [ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)
