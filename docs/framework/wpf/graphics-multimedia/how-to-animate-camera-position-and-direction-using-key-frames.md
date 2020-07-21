---
title: '方法: キー フレームを使用してカメラの位置および方向をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera direction with key frames
- key frames [WPF], animating camera direction
- animation [WPF], camera position with key frames
- camera position [WPF], animating with key frames
- key frames [WPF], animating camera position
- camera direction [WPF], animating with key frames
ms.assetid: 5753024e-0057-454d-947f-43ea686879c7
ms.openlocfilehash: 28471f9b42140a6c75b043d33939503528b63194
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112168"
---
# <a name="how-to-animate-camera-position-and-direction-using-key-frames"></a>方法: キー フレームを使用してカメラの位置および方向をアニメーション化する
次の例では、<xref:System.Windows.Media.Animation.Point3DAnimationUsingKeyFrames> を使用して、3D シーンにおける <xref:System.Windows.Media.Media3D.PerspectiveCamera> の位置をアニメーション化します。 また、<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames> を使用して、3D シーンでカメラが指す方向をアニメーション化します。 どちらのアニメーションでも、次のようなキー フレームを使用して、一連のアニメーション効果を生み出します。  
  
1. <xref:System.Windows.Media.Animation.LinearPoint3DKeyFrame> と <xref:System.Windows.Media.Animation.LinearVector3DKeyFrame> を使用して、値間に滑らかな線形補間を作成します。  
  
2. <xref:System.Windows.Media.Animation.DiscretePoint3DKeyFrame> と <xref:System.Windows.Media.Animation.DiscreteVector3DKeyFrame> を使用して、ある値から別の値への突然の "変化" を作成します。  
  
3. <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame> と <xref:System.Windows.Media.Animation.SplineVector3DKeyFrame> を使用して、<xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame.KeySpline%2A> プロパティに応じて値間に可変遷移を作成します。 次の例では、アニメーションはゆっくりと始まりますが、時間セグメントの終点に向かって急激に速くなります。  
  
## <a name="example"></a>例  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationUsingKeyFramesExample.xaml#pointvector3danimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D シーンでカメラの位置および方向をアニメーション化する](how-to-animate-camera-position-and-direction-in-a-3d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
