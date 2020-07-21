---
title: '方法: GIF イメージのエンコードおよびデコード'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- encoding GIF images [WPF]
- encoding image formats [WPF]
- decoding GIF images [WPF]
- decoding image formats [WPF]
- GIF decoding [WPF]
- GIF encoding [WPF]
ms.assetid: 9cdd9ec7-71eb-444b-b9e3-991958461163
ms.openlocfilehash: ec509a03d95e5f72af0b1f362e253799b07edc1f
ms.sourcegitcommit: 3eeea78f52ca771087a6736c23f74600cc662658
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68671689"
---
# <a name="how-to-encode-and-decode-a-gif-image"></a>方法: GIF イメージのエンコードおよびデコード
次の例では、特定の <xref:System.Windows.Media.Imaging.GifBitmapDecoder> オブジェクトと <xref:System.Windows.Media.Imaging.GifBitmapEncoder> オブジェクトを使用して、グラフィックス交換形式 (GIF) イメージをデコードおよびエンコードする方法を示します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.IO.FileStream> の <xref:System.Windows.Media.Imaging.GifBitmapDecoder> を使用して GIF イメージをデコードする方法を示します。  
  
 [!code-cpp[GifBitmapDecoderEncoder#1](~/samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#1)]
 [!code-csharp[GifBitmapDecoderEncoder#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#1)]
 [!code-vb[GifBitmapDecoderEncoder#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#1)]  
  
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Media.Imaging.GifBitmapEncoder> を使用して <xref:System.Windows.Media.Imaging.BitmapSource> を GIF イメージにエンコードする方法を示します。  
  
 [!code-cpp[GifBitmapDecoderEncoder#4](~/samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#4)]
 [!code-csharp[GifBitmapDecoderEncoder#4](~/samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#4)]
 [!code-vb[GifBitmapDecoderEncoder#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
