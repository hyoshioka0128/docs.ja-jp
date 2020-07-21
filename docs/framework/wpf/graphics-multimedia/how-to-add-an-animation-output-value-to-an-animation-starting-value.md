---
title: '方法: アニメーションの出力値をアニメーションの開始値に追加する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF]
ms.assetid: b89a82be-b03d-481e-a8d3-cc513d09ca00
ms.openlocfilehash: 945675d03a280e2394fdb0eab27c0978dc7cc320
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010242"
---
# <a name="how-to-add-an-animation-output-value-to-an-animation-starting-value"></a>方法: アニメーションの出力値をアニメーションの開始値に追加する
この例では、アニメーションの出力値をアニメーションの開始値に追加する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> プロパティでは、アニメーションの出力値をアニメーション化されたプロパティの開始値 (基本値) に追加するかどうかを指定します。 ほとんどの基本的なアニメーションと、ほとんどのキー フレーム アニメーションでは、<xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> プロパティを使用できます。 詳細については、「[アニメーションの概要](animation-overview.md)」と「[キーフレーム アニメーションの概要](key-frame-animations-overview.md)」を参照してください。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> で <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A?displayProperty=nameWithType> プロパティを使用し、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>で <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsAdditive%2A?displayProperty=nameWithType> プロパティを使用した場合の効果を示しています。  
  
 [!code-xaml[timingbehaviors_snip#IsAdditiveWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsAdditiveExample.xaml#isadditivewholepage)]  
  
## <a name="see-also"></a>関連項目

- [反復サイクル中にアニメーション値を累積する](how-to-accumulate-animation-values-during-repeat-cycles.md)
- [アニメーションの概要](animation-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
