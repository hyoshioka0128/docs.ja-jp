---
title: '方法: ストーリーボードを使用して 3D 回転をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- Storyboards [WPF]
- 3D translations [WPF], animating [WPF], with Storyboards
- animation [WPF], 3D translations [WPF], with Storyboards
ms.assetid: 1020e44e-e21e-49a8-be53-53cbc1910e83
ms.openlocfilehash: 088f1a33cfc73a706ffed55ffff6494adaf8fca4
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112216"
---
# <a name="how-to-animate-a-3d-rotation-using-storyboards"></a>方法: ストーリーボードを使用して 3D 回転をアニメーション化する
次の例では、<xref:System.Windows.Media.Media3D.AxisAngleRotation3D> オブジェクトの <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> プロパティおよび <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> プロパティをアニメーション化することによって、3D オブジェクトを "揺らし" ながら回転させる方法を示します。 この <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> オブジェクトは、3D オブジェクトの回転による変換を指定し、そのプロパティをアニメーション化することによって、目的の回転効果が得られるようにします。 ストーリーボードでは、<xref:System.Windows.Media.Animation.DoubleAnimation> は <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> プロパティのアニメーション化に使用され、<xref:System.Windows.Media.Animation.Vector3DAnimation> は <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> プロパティのアニメーション化に使用されます。  
  
## <a name="example"></a>例  
 [!code-xaml[Animation3DGallery_snip#Rotate3DUsingAxisAngleRotation3DExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotat3DUsingAxisAngleRotation3DExample.xaml#rotate3dusingaxisanglerotation3dexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [Rotation3DAnimation を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [キー フレーム (Rotation3DAnimationUsingKeyFrames) を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-key-frames.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
