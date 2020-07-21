---
title: '方法: TileBrush のタイル サイズを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- TileBrush [WPF], size of tile properties
- Viewport property of TileBrush [WPF]
ms.assetid: 04f41090-1b46-4e36-832f-d27d28708b8c
ms.openlocfilehash: af7bab59a292549b29dad9b6a7417f22b1b84e48
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186836"
---
# <a name="how-to-set-the-tile-size-for-a-tilebrush"></a>方法: TileBrush のタイル サイズを設定する

次の例は、<xref:System.Windows.Media.TileBrush> のタイル サイズを設定する方法を示しています。 既定では、<xref:System.Windows.Media.TileBrush> は、描画する領域全体を塗りつぶす 1 つのタイルを生成します。 <xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティと <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティを設定することで、この動作をオーバーライドできます。

<xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティは、<xref:System.Windows.Media.TileBrush> のタイル サイズを指定します。 既定では、<xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティの値は、描画される領域のサイズに対する相対的な値です。 <xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティで絶対タイル サイズを指定するには、<xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティを <xref:System.Windows.Media.BrushMappingMode.Absolute> に設定します。

## <a name="example"></a>例

次の例では、<xref:System.Windows.Media.TileBrush> の一種である <xref:System.Windows.Media.ImageBrush> を使用して、タイルで四角形を塗りつぶします。 例では、各タイルを出力領域 (四角形) の 50% x 50% に設定します。 その結果、四角形は、イメージの 4 つの投影で塗りつぶされます。

次の図は、この例で生成される出力を示しています。

![イメージ ブラシを使用したタイルの例を示す 4 つのサクランボを含む四角形。](./media/how-to-set-the-tile-size-for-a-tilebrush/rectangle-tile-image-brush.png)

[!code-csharp[UsingImageBrush_snip#RelativeTileSizeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#relativetilesizeexample)]

次の例では、<xref:System.Windows.Media.ImageBrush> を作成し、その <xref:System.Windows.Media.TileBrush.Viewport%2A> を `0,0,25,25`、<xref:System.Windows.Media.TileBrush.ViewportUnits%2A> を <xref:System.Windows.Media.BrushMappingMode.Absolute> に設定して、それを使用して別の四角形を塗りつぶします。 その結果、ブラシは、幅が 25 ピクセル、高さが 25 ピクセルのタイルを生成します。

次の図は、この例で生成される出力を示しています。

![ビューポートを使用してタイル化された TileBrush を示す 48 個のサクランボを含む四角形。](./media/how-to-set-the-tile-size-for-a-tilebrush/25-x-25-viewport-tilebrush.png)

[!code-csharp[UsingImageBrush_snip#AbsoluteTileSizeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#absolutetilesizeexample)]

上記の例は、大規模なサンプルの一部です。 サンプル全体については、「[ImageBrush のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)」をご覧ください。

この例では <xref:System.Windows.Media.ImageBrush> クラスを使用していますが、<xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティと <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> プロパティは、他の <xref:System.Windows.Media.TileBrush> オブジェクト (つまり、<xref:System.Windows.Media.DrawingBrush> と <xref:System.Windows.Media.VisualBrush>) でも同じように動作します。 <xref:System.Windows.Media.ImageBrush> および他の <xref:System.Windows.Media.TileBrush> オブジェクトの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.TileBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [TileBrush を使用してさまざまなタイル パターンを作成する](how-to-create-different-tile-patterns-with-a-tilebrush.md)
