---
title: '方法 : 直線または線分の終点のキャップを変更する'
ms.date: 03/30/2017
helpviewer_keywords:
- Shape elements [WPF], ends
- Shape elements [WPF], caps
- graphics [WPF], Shape caps
ms.assetid: f4bf3416-b3d8-4568-b98e-3eda8f6dbf7a
ms.openlocfilehash: aef85383a10629eb42f51ea86305636fd90600cb
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43504077"
---
# <a name="how-to-modify-the-cap-at-the-end-of-a-line-or-segment"></a>方法 : 直線または線分の終点のキャップを変更する
この例では、先頭または末尾の開いている図形を変更する方法を示しています<xref:System.Windows.Shapes.Shape>要素。 オープンの先頭に上限を変更する<xref:System.Windows.Shapes.Shape>を使用して、その<xref:System.Windows.Shapes.Shape.StrokeStartLineCap%2A>プロパティ。 オープンの終点のキャップを変更する<xref:System.Windows.Shapes.Shape>を使用して、その<xref:System.Windows.Shapes.Shape.StrokeEndLineCap%2A>プロパティ。 使用可能なライン キャップを表示するを参照してください。、<xref:System.Windows.Media.PenLineCap>列挙体。  
  
> [!NOTE]
>  このプロパティは、開いている図形をなど、 <xref:System.Windows.Shapes.Line>、 <xref:System.Windows.Shapes.Polyline>、または開いている<xref:System.Windows.Shapes.Path>要素。  
  
 次の例では、4 つを描画<xref:System.Windows.Shapes.Polyline>要素の各端にさまざまな図形を使用しています。  
  
## <a name="example"></a>例  
 [!code-xaml[drawingwithshapeelements#ShapeLineCaps1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/linecapsandjoinsexample.xaml#shapelinecaps1)]  
  
 この例より大きなサンプルの一部です。サンプル全体については、次を参照してください。 [Shape 要素のサンプル](https://go.microsoft.com/fwlink/?LinkID=160037)します。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Windows.Shapes.Polyline>  
 <xref:System.Windows.Media.PenLineCap>
