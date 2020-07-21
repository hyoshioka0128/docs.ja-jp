---
title: '方法: PNG イメージのエンコードおよびデコード'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- PNG encoding [WPF]
- decoding PNG images [WPF]
- PNG decoding [WPF]
- encoding image formats [WPF]
- decoding image formats [WPF]
- encoding PNG images [WPF]
ms.assetid: 3d31d186-af73-47f0-b5a7-c26ae46409a6
ms.openlocfilehash: 0a0a2f2625901f7ee32ba9fe70e71681a1b9ccd3
ms.sourcegitcommit: 43761fcee10aeefcf851ea81cea3f3c691420856
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69545278"
---
# <a name="how-to-encode-and-decode-a-png-image"></a>方法: PNG イメージのエンコードおよびデコード
次の例では、特定の <xref:System.Windows.Media.Imaging.PngBitmapDecoder> オブジェクトと <xref:System.Windows.Media.Imaging.PngBitmapEncoder> オブジェクトを使用して、ポータブル ネットワーク グラフィックス (PNG) イメージをデコードおよびエンコードする方法を示します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.IO.FileStream> の <xref:System.Windows.Media.Imaging.PngBitmapDecoder> を使用して PNG イメージをデコードする方法を示します。  
  
 [!code-cpp[PngBitmapDecoderEncoder#1](~/samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#1)]
 [!code-csharp[PngBitmapDecoderEncoder#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#1)]
 [!code-vb[PngBitmapDecoderEncoder#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#1)]  
  
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Media.Imaging.PngBitmapEncoder> を使用して <xref:System.Windows.Media.Imaging.BitmapSource> を PNG イメージにエンコードする方法を示します。  
  
 [!code-cpp[PngBitmapDecoderEncoder#4](~/samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#4)]
 [!code-csharp[PngBitmapDecoderEncoder#4](~/samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#4)]
 [!code-vb[PngBitmapDecoderEncoder#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
