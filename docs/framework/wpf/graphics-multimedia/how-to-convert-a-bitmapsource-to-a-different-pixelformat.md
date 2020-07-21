---
title: '方法: BitmapSource を別の PixelFormat に変換する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BitmapSource objects [WPF], converting to indexed pixel format
- converting images [WPF]
- converting [WPF], BitmapSource objects to indexed pixel formats
- converting [WPF], BitmapSource objects to palettized pixel format
- BitmapSource objects [WPF], converting to palettized pixel format
ms.assetid: cd9df1e4-d5dc-4f57-b67b-4ec67e086b33
ms.openlocfilehash: ea042599369da8435198e4206f89f3fa356a80c2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910170"
---
# <a name="how-to-convert-a-bitmapsource-to-a-different-pixelformat"></a>方法: BitmapSource を別の PixelFormat に変換する
この例では、<xref:System.Windows.Media.Imaging.FormatConvertedBitmap> を利用し、<xref:System.Windows.Media.Imaging.BitmapSource> オブジェクト (<xref:System.Windows.Media.Imaging.BitmapImage>) を別の <xref:System.Windows.Media.PixelFormat> に変換する方法を示します。  
  
## <a name="example"></a>例  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#PixelFormatConversion](~/samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/PixelFormatsExample.cs#pixelformatconversion)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#PixelFormatConversion](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/PixelFormatsExample.vb#pixelformatconversion)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
