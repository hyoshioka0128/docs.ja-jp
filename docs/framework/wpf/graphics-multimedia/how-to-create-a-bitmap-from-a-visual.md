---
title: '方法: ビジュアルからビットマップを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bitmaps [WPF], rendering from visuals
- visuals [WPF], rendering to bitmaps
ms.assetid: 103fc7f5-7306-4026-9d61-2005e79959f3
ms.openlocfilehash: a622d99f7c477f8654526ed399f1eb37288682fe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910261"
---
# <a name="how-to-create-a-bitmap-from-a-visual"></a>方法: ビジュアルからビットマップを作成する
この例では、<xref:System.Windows.Media.Visual> からビットマップを作成する方法を示します。 <xref:System.Windows.Media.DrawingVisual> は <xref:System.Windows.Media.FormattedText> でレンダリングされます。 次に <xref:System.Windows.Media.Visual> は <xref:System.Windows.Media.Imaging.RenderTargetBitmap> にレンダリングされ、所与のテキストのビットマップが作成されます。  
  
## <a name="example"></a>例  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#CreateRTBImage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample.cs#creatertbimage)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#CreateRTBImage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample.vb#creatertbimage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingContext>
- [イメージングの概要](imaging-overview.md)
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [DrawingVisual オブジェクトの使用](using-drawingvisual-objects.md)
