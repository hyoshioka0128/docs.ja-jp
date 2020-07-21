---
title: '方法: 3D オブジェクトの前面および背面に素材を適用する'
ms.date: 03/30/2017
helpviewer_keywords:
- 3D objects [WPF], applying Material class
- Material class [WPF], applying to both sides of 3D object
- classes [WPF], Material
ms.assetid: d93c8ad6-4939-4d29-9544-4d16d98093c1
ms.openlocfilehash: 5c24879d97e7857fb07fcef4a9ba8efa901e4a39
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112142"
---
# <a name="how-to-apply-material-to-the-front-and-back-of-a-3d-object"></a>方法: 3D オブジェクトの前面および背面に素材を適用する
次の例では、3D オブジェクトの前面および背面に <xref:System.Windows.Media.Media3D.Material> を適用し、オブジェクトをアニメーション化してオブジェクトの両面を表示する方法を示します。 <xref:System.Windows.Media.Media3D.GeometryModel3D> の <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> プロパティを使用して、オブジェクトの前面に赤色の <xref:System.Windows.Media.Brush> を適用し、<xref:System.Windows.Media.Media3D.GeometryModel3D> の <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> プロパティを使用して、オブジェクトの背面に青色の <xref:System.Windows.Media.Brush> を適用します。 次のコードは、オブジェクトへの素材の適用を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#BackMaterialAnimationExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexampleinline1)]  
  
## <a name="example"></a>例  
 次のコードは、サンプル全体を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#BackMaterialAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D シーンを作成する](how-to-create-a-3-d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [3D シーンで素材プロパティをアニメーション化する](how-to-animate-material-properties-in-a-3-d-scene.md)
- [3D オブジェクトに発色マテリアルを適用する](how-to-apply-emissive-material-to-a-3-d-object.md)
