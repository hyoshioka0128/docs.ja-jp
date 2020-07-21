---
title: '方法: 四元数を使用して 3D 回転をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- quaternions [WPF]
- animation [WPF], 3D translations [WPF], with quaternions
- 3D translations [WPF], animating [WPF], with quaternions
ms.assetid: adca9cb1-066b-4de8-abbb-6b4007579ee7
ms.openlocfilehash: 0d229b0a714cc53459943fae751ab4d4f787d7d8
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112246"
---
# <a name="how-to-animate-a-3d-rotation-using-quaternions"></a>方法: 四元数を使用して 3D 回転をアニメーション化する
この例では、四元数を使用して 3D オブジェクトの回転をアニメーション化する方法を示します。  
  
 次のコードは、<xref:System.Windows.Media.Media3D.RotateTransform3D> の <xref:System.Windows.Media.Media3D.RotateTransform3D.Rotation%2A> プロパティの値として使用される <xref:System.Windows.Media.Media3D.QuaternionRotation3D> を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline1)]  
  
 この <xref:System.Windows.Media.Media3D.QuaternionRotation3D> は、次のコードを使用して <xref:System.Windows.Media.Animation.Storyboard> 内の <xref:System.Windows.Media.Animation.QuaternionAnimation> でアニメーション化されます。  
  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline2)]  
  
## <a name="example"></a>例  
 次のコードは、サンプル全体を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [3D シーンを作成する](how-to-create-a-3-d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [変換の概要](transforms-overview.md)
- [ストーリーボードを使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-storyboards.md)
- [Rotation3DAnimation を使用して 3D 回転をアニメーション化する](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
