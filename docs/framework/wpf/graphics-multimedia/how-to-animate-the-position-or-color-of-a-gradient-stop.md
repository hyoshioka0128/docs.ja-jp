---
title: '方法: グラデーション ストップの位置または色をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- position [WPF], animating
- animation [WPF], position of GradientStop objects
- GradientStop objects [WPF], animating color of
- colors [WPF], animating
- animation [WPF], color of GradientStop objects
- GradientStop objects [WPF], animating position of
ms.assetid: 6f5b8b47-6c32-4b8e-98ee-fdf6515ec843
ms.openlocfilehash: aeae33f5f3c8016808988f58d61969e9b6f05039
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452845"
---
# <a name="how-to-animate-the-position-or-color-of-a-gradient-stop"></a>方法: グラデーション ストップの位置または色をアニメーション化する
この例では、<xref:System.Windows.Media.GradientStop> オブジェクトの <xref:System.Windows.Media.GradientStop.Color%2A> と <xref:System.Windows.Media.GradientStop.Offset%2A> をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.LinearGradientBrush> 内の 3 つのグラデーション境界をアニメーション化します。 この例では、3 つのアニメーションを使用して、それぞれ異なるグラデーション境界をアニメーション化します。  
  
- 1 番目のアニメーション (<xref:System.Windows.Media.Animation.DoubleAnimation>) では、アニメーション化で 1 番目のグラデーション境界の <xref:System.Windows.Media.GradientStop.Offset%2A> を 0.0 から 1.0 まで移動し、次に 0.0 に戻します。 その結果、グラデーションの最初の色が四角形の左側から右側に移動し、次に左側に戻ります。  
  
- 2 番目のアニメーション (<xref:System.Windows.Media.Animation.ColorAnimation>) では、アニメーション化で 2 番目のグラデーション境界の <xref:System.Windows.Media.GradientStop.Color%2A> を <xref:System.Windows.Media.Colors.Purple%2A> から <xref:System.Windows.Media.Colors.Yellow%2A> まで変え、次に <xref:System.Windows.Media.Colors.Purple%2A> に戻します。 その結果、グラデーションの中間色が紫色から黄色に変わり、紫色に戻ります。  
  
- 3 番目のアニメーション (これも <xref:System.Windows.Media.Animation.ColorAnimation>) では、アニメーション化で 3 番目のグラデーション境界の <xref:System.Windows.Media.GradientStop.Color%2A> の不透明度を 1 減らし、次に元に戻します。 その結果、グラデーションの 3 番目の色が薄くなり、その後、不透明に戻ります。  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/GradientStopAnimationExample.cs#graphicsmmgradientanimationexampleswholepage)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/gradientstopanimationexample.vb#graphicsmmgradientanimationexampleswholepage)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/GradientStopAnimationExample.xaml#graphicsmmgradientanimationexampleswholepage)]  
  
 この例では <xref:System.Windows.Media.LinearGradientBrush> を使用していますが、プロセスは <xref:System.Windows.Media.RadialGradientBrush> 内の <xref:System.Windows.Media.GradientStop> オブジェクトをアニメーション化する場合と同じです。  
  
 その他の例については、「[ブラシのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.GradientStop>
- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
