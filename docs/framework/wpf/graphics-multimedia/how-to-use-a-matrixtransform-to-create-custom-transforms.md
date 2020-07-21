---
title: '方法: MatrixTransform を使用してカスタム変換を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], custom Transforms
ms.assetid: 919381ca-989f-47cf-86b4-1094060236e4
ms.openlocfilehash: 1971d5fe9422c5138f140517e6fd4c9f9b2cf48b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913917"
---
# <a name="how-to-use-a-matrixtransform-to-create-custom-transforms"></a>方法: MatrixTransform を使用してカスタム変換を作成する
この例では、<xref:System.Windows.Media.MatrixTransform> を使用して、<xref:System.Windows.Controls.Button> の位置、伸縮、および傾斜を変換 (移動) する方法を示します。  
  
> [!NOTE]
> <xref:System.Windows.Media.MatrixTransform> クラスを使用して、<xref:System.Windows.Media.RotateTransform> クラス、<xref:System.Windows.Media.SkewTransform> クラス、<xref:System.Windows.Media.ScaleTransform> クラス、または <xref:System.Windows.Media.TranslateTransform> クラスによって指定されないカスタム変換を作成します。  
  
## <a name="example"></a>例  
 [!code-xaml[Transforms_snip#MatrixTransform](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/MatrixTransformExample.xaml#matrixtransform)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.MatrixTransform>
- <xref:System.Windows.Media.Transform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
