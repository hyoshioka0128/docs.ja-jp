---
title: '方法: キー フレームを使用して 3D 回転をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], 3D translations [WPF], with key frames (Rotation3DAnimation)
- key frames [WPF], Rotation3DAnimation
- 3D translations [WPF], animating [WPF], with key frames (Rotation3DAnimation)
ms.assetid: 6f671b95-7f30-4836-9a4f-aeb7dc30121f
ms.openlocfilehash: 2b9059df079125c34c70237c0f600751020044c6
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112311"
---
# <a name="how-to-animate-a-3d-rotation-using-key-frames"></a>方法: キー フレームを使用して 3D 回転をアニメーション化する
次の例では、<xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames> を使用して3D オブジェクトを回転させますが、その回転軸が動き、結果として "揺れ" が発生します。 このアニメーションでは、次のキー フレームが使用されます。  
  
1. <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> は、値間に滑らかな線形補間を作成するために使用されます。  
  
2. <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> は、ある値から別の値への突然の "変化" を作成するために使用されます (補間なし)。  
  
3. <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> は、<xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A> プロパティに応じて、値間に可変遷移を作成するために使用されます。 次の例では、アニメーションのこの部分は、ゆっくりと始まりますが、時間セグメントの終点に向かって急激に速くなります。  
  
## <a name="example"></a>例  
 [!code-xaml[Animation3DGallery_snip#Rotation3DAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotation3DAnimationUsingKeyFramesExample.xaml#rotation3danimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [ストーリーボードを使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-storyboards.md)
- [Rotation3DAnimation を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [四元数を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-quaternions.md)
- [キー フレーム (QuaternionAnimationUsingKeyFrames) を使用して 3D 回転をアニメーション化する](animate-a-3-d-rotation-quaternionanimationusingkeyframes.md)
