---
title: '方法: 3D 翻訳をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], 3D translations
- 3D translations [WPF], animating
ms.assetid: d4eece1f-0cd2-4a2c-8370-293354c380e4
ms.openlocfilehash: 7d4fff9c74663bd220ad5d15a983bcb639621afd
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112259"
---
# <a name="how-to-animate-3d-translations"></a>方法: 3D 翻訳をアニメーション化する
このトピックでは、3D モデルで平行移動セットをアニメーション化する方法について説明します。  
  
 次のコードは、<xref:System.Windows.Media.Media3D.GeometryModel3D> の <xref:System.Windows.Media.Media3D.Model3D.Transform%2A> プロパティへの <xref:System.Windows.Media.Media3D.TranslateTransform3D> オブジェクトの適用を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#Translation3DAnimationInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationinline1)]  
  
 この <xref:System.Windows.Media.Media3D.TranslateTransform3D> オブジェクトの <xref:System.Windows.Media.Media3D.TranslateTransform3D.OffsetX%2A> プロパティは、次のコードを使用してアニメーション化されます。  
  
 [!code-xaml[Animation3DGallery_snip#Translation3DAnimationInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationinline2)]  
  
## <a name="example"></a>例  
 次のコードは、サンプル全体を示しています。  
  
 [!code-xaml[Animation3DGallery_snip#Translation3DAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [3D シーンを作成する](how-to-create-a-3-d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [変換の概要](transforms-overview.md)
