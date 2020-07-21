---
title: '方法: キー フレームを使用して点をアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], animating Points with
- Points [WPF], animating with key frames
- animation [WPF], Points with key frames
ms.assetid: d2e2ef10-0773-4133-856e-d41c09f60ded
ms.openlocfilehash: edcba36644cf78d6e98f934d9bd8b593af38b328
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344877"
---
# <a name="how-to-animate-a-point-by-using-key-frames"></a>方法: キー フレームを使用して点をアニメーション化する
この例では、<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> クラスを使用して <xref:System.Windows.Point> をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、三角形のパスに沿って楕円を移動します。 この例では、<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Media.EllipseGeometry> の <xref:System.Windows.Media.EllipseGeometry.Center%2A> プロパティをアニメーション化します。 このアニメーションは、次の方法で 3 つのキー フレームを使用します。  
  
1. 最初の 0.5 秒間は、<xref:System.Windows.Media.Animation.LinearPointKeyFrame> クラスのインスタンスを使用して、楕円を開始位置からパスに沿って一定の速度で移動します。 <xref:System.Windows.Media.Animation.LinearPointKeyFrame> のような線形キー フレームは、ある値から次の値への滑らかな線状補間を作成します。  
  
2. 次の 0.5 秒の終わりに、<xref:System.Windows.Media.Animation.DiscretePointKeyFrame> クラスのインスタンスを使用して、楕円をパスに沿って次の位置に突然移動させます。 <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> のような不連続キー フレームは、ある値から次の値への突然の変化を作成します。  
  
3. 最後の 2 秒間は、<xref:System.Windows.Media.Animation.SplinePointKeyFrame> クラスのインスタンスを使用して、楕円を開始位置まで戻します。 <xref:System.Windows.Media.Animation.SplinePointKeyFrame> のようなスプライン キー フレームは、<xref:System.Windows.Media.Animation.SplinePointKeyFrame.KeySpline%2A> プロパティの値に従って、ある値から次の値への可変遷移を作成します。 この例では、アニメーションは最初はゆっくりしていますが、時間セグメントの終点に向かって急激に速くなります。  
  
 [!code-csharp[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/PointAnimationUsingKeyFramesExample.cs#pointanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/pointanimationusingkeyframesexample.vb#pointanimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#PointAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/PointAnimationUsingKeyFramesExample.xaml#pointanimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
 他のアニメーション例との一貫性を保つために、この例のコードでは、<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用して <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> を適用しています。 ただし、コード内で 1 つのアニメーションを適用する場合は、<xref:System.Windows.Media.Animation.Storyboard> よりも <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用する方が簡単です。 例については、「[ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>
- <xref:System.Windows.Media.EllipseGeometry.Center%2A?displayProperty=nameWithType>
- <xref:System.Windows.Media.EllipseGeometry>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
