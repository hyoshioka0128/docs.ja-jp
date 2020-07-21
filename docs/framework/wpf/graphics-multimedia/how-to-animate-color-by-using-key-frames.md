---
title: '方法: キー フレームを使用して色をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [WPF], animating with key frames
- animation [WPF], colors with key frames
- key frames [WPF], animating colors with
ms.assetid: ab04ffa6-4de9-4d5b-a3b4-4e35d5b2ef35
ms.openlocfilehash: 8a444706f7541b52722ab8257a88e76c3e1b0938
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344749"
---
# <a name="how-to-animate-color-by-using-key-frames"></a>方法: キー フレームを使用して色をアニメーション化する
この例では、キー フレームを使用して <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> プロパティをアニメーション化します。 このアニメーションは、次の方法で 3 つのキー フレームを使用します。  
  
1. 最初の 2 秒間は、<xref:System.Windows.Media.Animation.LinearColorKeyFrame> クラスのインスタンスを使用して、緑から赤へ徐々に色を変化させます。 <xref:System.Windows.Media.Animation.LinearColorKeyFrame> のような線形キー フレームは、ある値から次の値への滑らかで直線的な遷移を作成します。  
  
2. 次の 0.5 秒間の後わりに、<xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> クラスのインスタンスを使用して、赤から黄色へすばやく色を変化させます。 <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> のような不連続キー フレームは、ある値から次の値への突然の変化を作成します。つまり、この部分のアニメーションの色の変化は急速に行われ、滑らかではありません。  
  
3. 最後の 2 秒間は、<xref:System.Windows.Media.Animation.SplineColorKeyFrame> クラスのインスタンスを使用して、色を再度変更します (この例では黄色から緑へ戻ります)。 <xref:System.Windows.Media.Animation.SplineColorKeyFrame> のようなスプライン キー フレームは、<xref:System.Windows.Media.Animation.SplineColorKeyFrame.KeySpline%2A> プロパティの値に従って、ある値から次の値への可変遷移を作成します。 この例では、色の変化は最初はゆっくりしていますが、時間セグメントの終点に向かって急激に速くなります。  
  
 [!code-csharp[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/ColorAnimationUsingKeyFramesExample.cs#coloranimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/coloranimationusingkeyframesexample.vb#coloranimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ColorAnimationUsingKeyFramesExample.xaml#coloranimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.SolidColorBrush.Color%2A>
- <xref:System.Windows.Media.SolidColorBrush>
- <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
