---
title: '方法: キー フレームを使用してブール値をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Booleans [WPF], animating with key frames
- animation [WPF], Booleans with key frames
- key frames [WPF], animating Booleans with
ms.assetid: 4b0fac96-6231-4fcf-9775-4dd673ddc785
ms.openlocfilehash: 35704996dcf21fe463169dc13572941bcd8fbad1
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344935"
---
# <a name="how-to-animate-a-boolean-by-using-key-frames"></a>方法: キー フレームを使用してブール値をアニメーション化する
この例では、キー フレームを使用して、<xref:System.Windows.Controls.Button> コントロールの Boolean プロパティ値をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Controls.Button> コントロールの <xref:System.Windows.UIElement.IsEnabled%2A> プロパティをアニメーション化します。 この例のすべてのキー フレームでは、<xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame> クラスのインスタンスが使用されます。 <xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame> のような不連続キー フレームによって、ある値から次の値への突然の変化が作成されます。つまり、アニメーションの動きがぎくしゃくします。  
  
 [!code-csharp[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/BooleanAnimationUsingKeyFramesExample.cs#booleananimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/booleananimationusingkeyframesexample.vb#booleananimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/BooleanAnimationUsingKeyFramesExample.xaml#booleananimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>
- <xref:System.Windows.UIElement.IsEnabled%2A>
- <xref:System.Windows.Controls.Button>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
