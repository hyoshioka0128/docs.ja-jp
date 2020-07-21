---
title: '方法: キー フレームを使用して Double 値をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Doubles [WPF], animating with key frames
- animation [WPF], Doubles with key frames
- key frames [WPF], animating Doubles with
ms.assetid: 3a1a7dba-7694-4907-8a2f-3408baebfa82
ms.openlocfilehash: 9eab794cc8411230226cddc97beaa13c1bdd9405
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344929"
---
# <a name="how-to-animate-a-double-by-using-key-frames"></a>方法: キー フレームを使用して Double 値をアニメーション化する
この例では、<xref:System.Double> を受け取るプロパティの値をキー フレームを使用してアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、画面を横切るように四角形を移動します。 この例では、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Shapes.Rectangle> に適用された <xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティをアニメーション化します。 無期限に繰り返すこのアニメーションでは、次の方法で 3 つのキー フレームを使用します。  
  
1. 最初の 3 秒間は、<xref:System.Windows.Media.Animation.LinearDoubleKeyFrame> クラスのインスタンスを使用して、四角形を開始位置からパスに沿って 500 の位置まで一定の速度で移動します。 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame> のような線形キー フレームは、ある値から次の値への滑らかで直線的な遷移を作成します。  
  
2. 4 秒目の後わりに、<xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame> クラスのインスタンスを使用して、四角形を次の位置まで突然移動します。 <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame> のような不連続キー フレームは、ある値から次の値への突然の変化を作成します。 この例では、開始位置にあった四角形が突然 500 の位置に出現します。  
  
3. 最後の 2 秒間は、<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> クラスのインスタンスを使用して、四角形を開始位置まで戻します。 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> のようなスプライン キー フレームは、<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A> プロパティの値に従って、ある値から次の値への可変遷移を作成します。 この例では、四角形の動きは最初はゆっくりしていますが、時間セグメントの終点に向かった急激に速くなります。  
  
 [!code-csharp[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/AltDoubleAnimationUsingKeyFramesExample.cs#altdoubleanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/altdoubleanimationusingkeyframesexample.vb#altdoubleanimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/AltDoubleAnimationUsingKeyFramesExample.xaml#altdoubleanimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
 他のアニメーション例との一貫性を保つために、この例のコード バージョンでは、<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用して <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> を適用しています。 ただし、コード内で 1 つのアニメーションを適用する場合は、<xref:System.Windows.Media.Animation.Storyboard> よりも <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用する方が簡単です。 例については、「[ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>
- <xref:System.Windows.Shapes.Rectangle>
- <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>
- <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>
- <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
