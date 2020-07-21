---
title: '方法: キー フレームを使用して四角形のジオメトリをアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], animating RectangleGeometry objects with
- RectangleGeometry objects [WPF], animating with key frames
- animation [WPF], RectangleGeometry objects with key frames
ms.assetid: a8b45ceb-0e32-4ba1-928f-df6d30db17c6
ms.openlocfilehash: bcc9e7f198b8a20ffe13daf6508fb8a735937652
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344679"
---
# <a name="how-to-animate-a-rectangle-geometry-by-using-key-frames"></a>方法: キー フレームを使用して四角形のジオメトリをアニメーション化する
この例では、キー フレームを使用して <xref:System.Windows.Media.RectangleGeometry> の <xref:System.Windows.Media.RectangleGeometry.Rect%2A> プロパティをアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Media.RectangleGeometry> の <xref:System.Windows.Media.RectangleGeometry.Rect%2A> プロパティをアニメーション化します。 このアニメーションは、次の方法で 3 つのキー フレームを使用します。  
  
1. 最初の 2 秒間は、<xref:System.Windows.Media.Animation.LinearRectKeyFrame> クラスのインスタンスを使用して、四角形の位置、幅、および高さが徐々に変化する様子をアニメーション化します。 <xref:System.Windows.Media.Animation.LinearRectKeyFrame> のような線形キー フレームは、ある値から次の値への滑らかで直線的な遷移を作成します。  
  
2. 次の 0.5 秒間の後わりに、<xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> クラスのインスタンスを使用して、四角形の高さを突然低くします。 <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> のような不連続キー フレームは、ある値から次の値への突然の変化を作成します。つまり、高さの減少は急速に行われ、滑らかではありません。  
  
3. 最後の 2 秒間は、<xref:System.Windows.Media.Animation.SplineRectKeyFrame> クラスのインスタンスを使用して、四角形を元のサイズと位置に戻します。 <xref:System.Windows.Media.Animation.SplineRectKeyFrame> のようなスプライン キー フレームは、<xref:System.Windows.Media.Animation.SplineRectKeyFrame.KeySpline%2A> プロパティの値に従って、ある値から次の値への可変遷移を作成します。 この例では、変化は最初はゆっくりしていますが、時間セグメントの終点に向かって急激に速くなります。  
  
 [!code-csharp[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/RectAnimationUsingKeyFramesExample.cs#rectanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/rectanimationusingkeyframesexample.vb#rectanimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#RectAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/RectAnimationUsingKeyFramesExample.xaml#rectanimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.RectangleGeometry>
- <xref:System.Windows.Media.RectangleGeometry.Rect%2A>
- <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
