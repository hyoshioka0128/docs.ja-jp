---
title: '方法: ImageDrawing を使用してイメージを描画する'
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], images
- graphics [WPF], drawing images
- images [WPF], drawing
ms.assetid: df28ab41-25fb-4ab3-b51d-7f695b24f55e
ms.openlocfilehash: f9459185bf81160b45222e7d6821e0f945ada381
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947599"
---
# <a name="how-to-draw-an-image-using-imagedrawing"></a>方法: ImageDrawing を使用してイメージを描画する
この例では、<xref:System.Windows.Media.ImageDrawing> を使用してイメージを描画する方法を示します。 <xref:System.Windows.Media.ImageDrawing> を使用すると、<xref:System.Windows.Media.ImageSource> に、<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.DrawingImage>、または <xref:System.Windows.Media.Visual> を表示できます。 イメージを描画するには、<xref:System.Windows.Media.ImageDrawing> を作成し、それの <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=nameWithType> プロパティと <xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=nameWithType> プロパティを設定します。 <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=nameWithType> プロパティでは描画するイメージを指定し、<xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=nameWithType> プロパティでは各イメージの位置とサイズを指定します。  
  
## <a name="example"></a>例  
 次の例では、4 つの <xref:System.Windows.Media.ImageDrawing> オブジェクトが使用された合成画が作成されます。 この例では、次の画像が生成されます。  
  
 ![いくつかの DrawingImage オブジェクト](./media/graphicsmm-imagedrawingexample.jpg "graphicsmm_ImageDrawingExample")  
4 つの ImageDrawing オブジェクト  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawingExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawingexample)]
 [!code-xaml[DrawingMiscSnippets_snip#ImageDrawingExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawingexample)]  
  
 <xref:System.Windows.Media.ImageDrawing> を使用せずにイメージを表示する簡単な方法の例については、「[イメージ要素使用する](../controls/how-to-use-the-image-element.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Freezable.Freeze%2A>
- <xref:System.Windows.Controls.Image>
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
- [PresentationOptions:Freeze 属性](../advanced/presentationoptions-freeze-attribute.md)
