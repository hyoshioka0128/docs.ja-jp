---
title: '方法: 3D シーンを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- scenes [WPF], 3D
- 3D scenes
ms.assetid: adb4a598-71a2-4dd5-b677-ea3fc11b78b2
ms.openlocfilehash: 36453894e06e7b59f339c21713449140c17f6851
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112103"
---
# <a name="how-to-create-a-3d-scene"></a>方法: 3D シーンを作成する
この例では、回転した平らな 1 枚の紙のように見える 3D オブジェクトを作成する方法を示します。 この単純な 3D シーンの作成には、次のコンポーネントと共に <xref:System.Windows.Controls.Viewport3D> が使用されます。  
  
- <xref:System.Windows.Media.Media3D.PerspectiveCamera> を使用してカメラが作成されます。 カメラは、3D シーンのどの部分を表示できるかを指定します。  
  
- <xref:System.Windows.Media.Media3D.GeometryModel3D> の <xref:System.Windows.Media.Media3D.GeometryModel3D.Geometry%2A> プロパティを使用して、3D オブジェクト (1 枚の紙) の形状を指定するために、メッシュが作成されます。  
  
- <xref:System.Windows.Media.Media3D.GeometryModel3D> の <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> プロパティを使用して、オブジェクト (この例では線状グラデーション) の表面に表示される素材が指定されます。  
  
- <xref:System.Windows.Media.Media3D.DirectionalLight> を使用して、オブジェクトに光をかけるためのライトが作成されます。  
  
## <a name="example"></a>例  
 次のコードは、XAML で 3D シーンを作成する方法を示しています。  
  
 [!code-xaml[3DGallery_snip#Basic3DShapeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/Basic3DShapeExample.xaml#basic3dshapeexamplewholepage)]  
  
## <a name="example"></a>例  
 次のコードは、手続き型コードで同じ 3D シーンを作成する方法を示しています。  
  
 [!code-csharp[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Basic3DShapeExample.cs#basic3dshapecodeexamplewholepage)]
 [!code-vb[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/basic3dshapeexample.vb#basic3dshapecodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [3D グラフィックスの概要](3-d-graphics-overview.md)
