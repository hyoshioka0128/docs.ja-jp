---
title: '方法: キー フレーム (QuaternionAnimationUsingKeyFrames) を使用して 3D 回転をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- 3D translations [WPF], animating [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
- key frames [WPF], QuaternionAnimationUsingKeyFrames
- animation [WPF], 3D translations [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
ms.assetid: 09e5707b-7523-4a08-9aa7-bb13cbedccdf
ms.openlocfilehash: 5273183aaa49a743cc401dec0b4b16bae09e3129
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112298"
---
# <a name="how-to-animate-a-3d-rotation-using-key-frames-quaternionanimationusingkeyframes"></a>方法: キー フレーム (QuaternionAnimationUsingKeyFrames) を使用して 3D 回転をアニメーション化する
次の例では、3D オブジェクトを回転させるために <xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames> が使用されています。 このアニメーションでは、次のキー フレームが使用されます。  
  
1. <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> は、値間に滑らかな線形補間を作成するために使用されます。  
  
2. <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> は、ある値から別の値への突然の "変化" を作成するために使用されます (補間なし)。  
  
3. <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> は、<xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A> プロパティに応じて、値間に可変遷移を作成するために使用されます。 以下の例では、アニメーションのこの部分は、ゆっくりと始まりますが、時間セグメントの終点に向かって急激に速くなります。  
  
## <a name="example"></a>例  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationUsingKeyFramesExample.xaml#quaternionanimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [ストーリーボードを使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-storyboards.md)
- [Rotation3DAnimation を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [四元数を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-quaternions.md)
- [キー フレーム (Rotation3DAnimationUsingKeyFrames) を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-key-frames.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
