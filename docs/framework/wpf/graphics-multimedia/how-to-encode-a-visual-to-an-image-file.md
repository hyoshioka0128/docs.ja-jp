---
title: '方法: ビジュアルをイメージ ファイルにエンコードする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- image files [WPF], encoding from visuals
- encoding image formats [WPF]
- visuals [WPF], encoding to an image file
ms.assetid: 2036385b-ea47-4d54-8027-5797f52c8149
ms.openlocfilehash: 193b6a14e404d32bb49d6e0ef3cbd513166bcce2
ms.sourcegitcommit: 43761fcee10aeefcf851ea81cea3f3c691420856
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69545295"
---
# <a name="how-to-encode-a-visual-to-an-image-file"></a>方法: ビジュアルをイメージ ファイルにエンコードする
この例では、<xref:System.Windows.Media.Imaging.RenderTargetBitmap> と <xref:System.Windows.Media.Imaging.PngBitmapEncoder> を使用して <xref:System.Windows.Media.Visual> オブジェクトをイメージ ファイルにエンコードする方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.DrawingVisual> は、<xref:System.Windows.Media.Imaging.RenderTargetBitmap> にレンダリングされる <xref:System.Windows.Media.Imaging.BitmapImage> と <xref:System.Windows.Media.FormattedText> を使用して作成されます。 次に、レンダリングされたビットマップを使用して、<xref:System.Windows.Media.Imaging.PngBitmapEncoder> に追加される <xref:System.Windows.Media.Imaging.BitmapFrame> を作成して、新しいポータブル ネットワーク グラフィックス (PNG) ファイルを作成します。  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample_Encode.cs#rtbencodeinline1)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample_Encode.vb#rtbencodeinline1)]  
  
 この例では、<xref:System.Windows.Media.Imaging.PngBitmapEncoder> を使用しましたが、派生した <xref:System.Windows.Media.Imaging.BitmapEncoder> オブジェクトのいずれかを使用してイメージ ファイルを作成することもできます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingContext>
- [イメージングの概要](imaging-overview.md)
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [DrawingVisual オブジェクトの使用](using-drawingvisual-objects.md)
