---
title: '方法: BMP イメージのエンコードおよびデコード'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- encoding BMP images [WPF]
- BMP encoding [WPF]
- decoding BMP images [WPF]
- encoding image formats [WPF]
- BMP decoding [WPF]
- decoding image formats [WPF]
ms.assetid: feb5ef27-28ac-40ab-bfc2-e0456990d32c
ms.openlocfilehash: 7d3520a1b1913fe68fedb0ea9d76cc138ed661c4
ms.sourcegitcommit: 09d699aca28ae9723399bbd9d3d44aa0cbd3848d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68331733"
---
# <a name="how-to-encode-and-decode-a-bmp-image"></a>方法: BMP イメージのエンコードおよびデコード
次の例は、特定の <xref:System.Windows.Media.Imaging.BmpBitmapDecoder> オブジェクトと <xref:System.Windows.Media.Imaging.BmpBitmapEncoder> オブジェクトを使用して、ビットマップ (BMP) イメージをデコードおよびエンコードする方法を示しています。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Uri> の <xref:System.Windows.Media.Imaging.BmpBitmapDecoder> を使用して BMP イメージをデコードする方法を示します。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Media.Imaging.BmpBitmapEncoder> を使用して <xref:System.Windows.Media.Imaging.BitmapSource> を BMP イメージにエンコードする方法を示します。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#4](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#4)]
 [!code-csharp[BmpBitmapDecoderEncoder#4](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#4)]
 [!code-vb[BmpBitmapDecoderEncoder#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
