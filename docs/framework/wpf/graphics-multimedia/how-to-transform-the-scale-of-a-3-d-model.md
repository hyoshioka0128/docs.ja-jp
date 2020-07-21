---
title: '方法: 3D モデルのスケールを変換する'
ms.date: 03/30/2017
helpviewer_keywords:
- scaling [WPF], 3D objects
- 3D objects [WPF], scaling
ms.assetid: f3fdfe33-f7dc-44b0-84a5-e43b89947f35
ms.openlocfilehash: be41a0e10929912c1b54bf7140d743d9453199bf
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111986"
---
# <a name="how-to-transform-the-scale-of-a-3d-model"></a>方法: 3D モデルのスケールを変換する
次の例では、3D オブジェクトを拡大縮小する方法を示します。 3D オブジェクトを拡大縮小するには、<xref:System.Windows.Media.Media3D.ScaleTransform3D> を使用します。 <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A>、<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A>、<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A> の各プロパティは、指定した係数で要素のサイズを変更します。 たとえば、<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A> 値が 1.5 の場合、オブジェクトは元の幅の 150% に拡大します。 <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A> 値が 0.5 の場合は、オブジェクトの高さが 50% 縮小します。 次のコードは、<xref:System.Windows.Media.Media3D.GeometryModel3D> の変換として <xref:System.Windows.Media.Media3D.ScaleTransform3D> を使用する方法を示しています。  
  
 [!code-xaml[3DGallery_snip#ScaleTransform3DExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexampleinline1)]  
  
## <a name="example"></a>例  
 次のコードは、サンプル全体を示しています。  
  
 [!code-xaml[3DGallery_snip#ScaleTransform3DExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D 変換をアニメーション化する](how-to-animate-3-d-translations.md)
- [3D シーンを作成する](how-to-create-a-3-d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
