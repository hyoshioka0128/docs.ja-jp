---
title: '方法: オブジェクトに複数の変換を適用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- grouping Transform objects [WPF]
- Transform objects [WPF], grouping
- graphics [WPF], grouping Transform objects
- TransformGroup [WPF]
ms.assetid: 98cd1921-12bc-4bf5-8193-529228fb7402
ms.openlocfilehash: 3ef11104b2a4fc775d29d2a388c9a70a69a3f10f
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112116"
---
# <a name="how-to-apply-multiple-transforms-to-an-object"></a>方法: オブジェクトに複数の変換を適用する
この例では、<xref:System.Windows.Media.TransformGroup> を使用して、2 つ以上の <xref:System.Windows.Media.Transform> オブジェクトを 1 つの複合 <xref:System.Windows.Media.Transform> にグループ化する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.TransformGroup> を使用して、<xref:System.Windows.Media.ScaleTransform> と <xref:System.Windows.Media.RotateTransform> を <xref:System.Windows.Controls.Button> に適用します。  
  
 [!code-xaml[Transforms_snip#MultipleTransformExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/MultipleTransformExample.xaml#multipletransformexamplewholepage)]  
  
 [!code-csharp[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/MultipleTransformsExample.cs#multipletransformscodeexamplewholepage)]
 [!code-vb[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/MultipleTransformsExample.vb#multipletransformscodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.UIElement.RenderTransform%2A>
- <xref:System.Windows.Media.TransformGroup>
- [変換の概要](transforms-overview.md)
- [2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)
