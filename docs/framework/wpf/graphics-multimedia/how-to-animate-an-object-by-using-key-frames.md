---
title: '方法: キー フレームを使用してオブジェクトをアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], objects with key frames
- key frames [WPF], animating objects with
ms.assetid: b1f15ba9-cac7-4cea-8699-5c6b55c05c5e
ms.openlocfilehash: 0bc33b189fd856dbe8106c1db35bc18e27ea131e
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344702"
---
# <a name="how-to-animate-an-object-by-using-key-frames"></a>方法: キー フレームを使用してオブジェクトをアニメーション化する
この例では、キー フレームを使用して、オブジェクト (この例では、<xref:System.Windows.Controls.Page> コントロールの <xref:System.Windows.Controls.Page.Background%2A> プロパティ) をアニメーション化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> クラスを使用して、<xref:System.Windows.Controls.Page> コントロールの <xref:System.Windows.Controls.Page.Background%2A> プロパティの色の変化をアニメーション化します。 このアニメーション例は、一定の間隔で別の背景ブラシに変わります。 このアニメーションでは、<xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> クラスを使用して、3 つの異なるキー フレームを作成します。 このアニメーションは、次の方法でキー フレームを使用します。  
  
1. 最初の 1 秒の終わりに、<xref:System.Windows.Media.LinearGradientBrush> クラスのインスタンスをアニメーション化します。 この例のこの部分では、色が黄色からオレンジ色、そして赤に変化するように、背景色に線状グラデーションを適用します。  
  
2. 2 秒目の終わりに、<xref:System.Windows.Media.RadialGradientBrush> クラスのインスタンスをアニメーション化します。 この例のこの部分では、色が白から青、そして黒に変化するように背景色に放射状グラデーションを適用します。  
  
3. 3 秒目の終わりに、<xref:System.Windows.Media.DrawingBrush> クラスのインスタンスをアニメーション化します。 この例のこの部分では、背景にチェッカーボード パターンを適用します。  
  
4. アニメーションが再開され、無限に繰り返されます。  
  
> [!NOTE]
> <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> は、<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> クラスで使用できる唯一の種類のキー フレームです。 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> のようなキー フレームを使用すると、値が突然変化します。つまり、この例では色の変化が突然発生します。  
  
 [!code-xaml[keyframes_snip#ObjectAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ObjectAnimationUsingKeyFramesExample.xaml#objectanimationusingkeyframeswholepage)]  
  
 サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>
- <xref:System.Windows.Controls.Page.Background%2A>
- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- <xref:System.Windows.Media.DrawingBrush>
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [キー フレームに関する「方法」トピック](key-frame-animation-how-to-topics.md)
