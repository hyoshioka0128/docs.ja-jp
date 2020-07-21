---
title: '方法: ジオメトリック パスを使用してオブジェクトを回転させる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- geometric paths [WPF], rotating objects by
- rotating objects by geometric paths [WPF]
ms.assetid: cb31ca4d-f05a-4c6b-9a18-4b6faaf38d45
ms.openlocfilehash: a351fdc936f634b7c57ba5a49e51501f7572a3c9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186876"
---
# <a name="how-to-rotate-an-object-by-using-a-geometric-path"></a>方法: ジオメトリック パスを使用してオブジェクトを回転させる
この例では、<xref:System.Windows.Media.PathGeometry> オブジェクトで定義されたジオメトリック パスに沿ってオブジェクトを回転 (ピボット) する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、3 つの <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> オブジェクトを使用して、ジオメトリック パスに沿って四角形を移動します。  
  
- 最初の <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> は、四角形に適用されている <xref:System.Windows.Media.RotateTransform> をアニメーション化します。 アニメーションは、角度の値を生成します。 これにより、四角形がパスの輪郭に沿って回転 (ピボット) します。  
  
- 他の 2 つのオブジェクトは、四角形に適用されている <xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> と <xref:System.Windows.Media.TranslateTransform.Y%2A> の値をアニメーション化します。 これにより、四角形が、パスに沿って水平方向と垂直方向に移動します。  
  
 [!code-xaml[PathAnimationGallery_snippet#RotateAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/rotateanimationusingpathexample.xaml#rotateanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#RotateAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/RotateAnimationUsingPathExample.cs#rotateanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#RotateAnimationUsingPathWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/RotateAnimationUsingPathExample.vb#rotateanimationusingpathwholepage)]  
  
 ジオメトリック パスを使用してオブジェクトを回転させるもう 1 つの方法は、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> オブジェクトを使用して、その <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> プロパティを `true` に設定することです。 詳細と例については、「[方法: ジオメトリック パスを使用してオブジェクトを回転させる (行列アニメーション)](how-to-rotate-an-object-by-using-a-geometric-path-matrix-animation.md)」をご覧ください。  
  
 サンプル全体については、「[パス アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/PathAnimations)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [パス アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/PathAnimations)
- [パス アニメーションに関する「方法」トピック](path-animation-how-to-topics.md)
