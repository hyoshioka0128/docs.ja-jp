---
title: '方法: 反復サイクル中にアニメーション値を累積する'
ms.date: 03/30/2017
helpviewer_keywords:
- accumulating animation values across repeating cycles [WPF]
- animation [WPF], accumulating values across repeating cycles
ms.assetid: 548df369-c7cc-4dab-b569-08b95ced2e7e
ms.openlocfilehash: bccdc9b7bf2d5a0ea476e39e8d54107854db7ae3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591468"
---
# <a name="how-to-accumulate-animation-values-during-repeat-cycles"></a>方法: 反復サイクル中にアニメーション値を累積する
この例では、<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> プロパティを使用して、反復サイクルでアニメーション値を累積する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> プロパティを使用して、反復サイクル中のアニメーションの基本値を累積します。 たとえば、アニメーションを 9 回繰り返す (<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> = "9x") ように設定し、10 から 15 (From = 10 To = 15) の間でアニメーション化するようにプロパティを設定した場合、プロパティは、最初のサイクルで 10 から 15 まで、2 番目のサイクルで 15 から 20 まで、3 番目のサイクルで 20 から 25 まで (以下同様) アニメーション化されます。 したがって、各アニメーション サイクルでは、前のアニメーション サイクルの終了アニメーション値が基本値として使用されます。  
  
 ほとんどの基本的なアニメーションと、ほとんどのキー フレーム アニメーションでは、`IsCumulative` プロパティを使用できます。 詳細については、「[アニメーションの概要](animation-overview.md)」と「[キーフレーム アニメーションの概要](key-frame-animations-overview.md)」を参照してください。  
  
 次の例では、4 つの四角形の幅をアニメーション化することで、この動作を示しています。 この例では、次の処理を実行します。  
  
- 最初の四角形を <xref:System.Windows.Media.Animation.DoubleAnimation> でアニメーション化し、<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> プロパティを `true` に設定します。  
  
- <xref:System.Windows.Media.Animation.DoubleAnimation> で 2 番目の四角形をアニメーション化し、<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> プロパティを `false` の既定値に設定します。  
  
- 3 番目の四角形を <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> でアニメーション化し、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> プロパティを `true` に設定します。  
  
- 最後の四角形を <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> でアニメーション化し、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> プロパティを `false` に設定します。  
  
 [!code-xaml[timingbehaviors_snip#IsCumulativeWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsCumulativeExample.xaml#iscumulativewholepage)]  
  
## <a name="see-also"></a>関連項目

- [アニメーションの出力値をアニメーションの開始値に追加する](how-to-add-an-animation-output-value-to-an-animation-starting-value.md)
- [アニメーションを反復する](how-to-repeat-an-animation.md)
- [アニメーションの概要](animation-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [方法トピック](animation-and-timing-how-to-topics.md)
