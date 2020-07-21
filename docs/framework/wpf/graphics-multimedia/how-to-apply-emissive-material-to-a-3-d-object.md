---
title: '方法: 3D モデルに放射性素材を適用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- EmissiveMaterial [WPF], applying to 3D objects
- 3D objects [WPF], applying EmissiveMaterial
ms.assetid: fd442cc2-5adc-487a-ba70-e45ed54bb3b4
ms.openlocfilehash: bf32b41ec2410c01ad137ec0ca9311f7c2b70061
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112155"
---
# <a name="how-to-apply-emissive-material-to-a-3d-object"></a>方法: 3D モデルに放射性素材を適用する
次の例は、<xref:System.Windows.Media.Media3D.EmissiveMaterial> を使用して、EmissiveMaterial のブラシの色に等しい既存の素材に色を追加する方法を示しています。 次のコードでは、<xref:System.Windows.Media.Media3D.DiffuseMaterial> と <xref:System.Windows.Media.Media3D.EmissiveMaterial> を組み合わせて適用して、DiffuseMaterial の外観に青を追加しています。  
  
 [!code-xaml[3DGallery_snip#EmmisiveMaterialAnimationExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/EmissiveMaterialExample.xaml#emmisivematerialanimationexampleinline1)]  
  
 手続き型コード:  
  
 [!code-csharp[3DGallery_procedural_snip#EmissiveMaterialCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/EmissiveMaterialExample.cs#emissivematerialcodeexampleinline1)]
 [!code-vb[3DGallery_procedural_snip#EmissiveMaterialCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/emissivematerialexample.vb#emissivematerialcodeexampleinline1)]  
  
## <a name="example"></a>例  
 次のコードは、XAML のサンプル全体を示しています。  
  
 [!code-xaml[3DGallery_snip#EmissiveMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/EmissiveMaterialExample.xaml#emissivematerialexamplewholepage)]  
  
## <a name="example"></a>例  
 以下は、手続き型コードのサンプル全体です。  
  
 [!code-csharp[3DGallery_procedural_snip#EmissiveMaterialCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/EmissiveMaterialExample.cs#emissivematerialcodeexamplewholepage)]
 [!code-vb[3DGallery_procedural_snip#EmissiveMaterialCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/emissivematerialexample.vb#emissivematerialcodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D シーンを作成する](how-to-create-a-3-d-scene.md)
- [3D グラフィックスの概要](3-d-graphics-overview.md)
- [3D シーンで素材プロパティをアニメーション化する](how-to-animate-material-properties-in-a-3-d-scene.md)
- [3D オブジェクトの前面および背面に素材を適用する](how-to-apply-material-to-the-front-and-back-of-a-3-d-object.md)
