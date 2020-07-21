---
title: '方法: WDP イメージのエンコードおよびデコード'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- WDP encoding [WPF]
- WDP decoding [WPF]
- encoding image formats [WPF]
- decoding WDP images [WPF]
- decoding image formats [WPF]
- encoding WDP images [WPF]
ms.assetid: 911777d1-516b-49db-a87b-b54e31b18532
ms.openlocfilehash: 8c5c312c7e58d48a865e493c38c3defd3f5f3d1d
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040778"
---
# <a name="how-to-encode-and-decode-a-wdp-image"></a>方法: WDP イメージのエンコードおよびデコード
次の例では、特定の <xref:System.Windows.Media.Imaging.WmpBitmapDecoder> オブジェクトと <xref:System.Windows.Media.Imaging.WmpBitmapEncoder> オブジェクトを使用して、Microsoft Windows Media Photo イメージをデコードおよびエンコードする方法を示します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Uri> の <xref:System.Windows.Media.Imaging.WmpBitmapDecoder> を使用して Microsoft Windows Media Photo イメージをデコードする方法を示します。  
  
 [!code-cpp[WdpBitmapDecoderEncoder#1](~/samples/snippets/cpp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CPP/WDPEncoderDecoder.cpp#1)]
 [!code-csharp[WdpBitmapDecoderEncoder#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CSharp/WDPEncoderDecoder.cs#1)]
 [!code-vb[WdpBitmapDecoderEncoder#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/VB/WDPEncoderDecoder.vb#1)]  
  
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Media.Imaging.WmpBitmapEncoder> を使用して <xref:System.Windows.Media.Imaging.BitmapSource> を Microsoft Windows Media Photo イメージにエンコードする方法を示します。  
  
 [!code-cpp[WdpBitmapDecoderEncoder#4](~/samples/snippets/cpp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CPP/WDPEncoderDecoder.cpp#4)]
 [!code-csharp[WdpBitmapDecoderEncoder#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CSharp/WDPEncoderDecoder.cs#4)]
 [!code-vb[WdpBitmapDecoderEncoder#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/VB/WDPEncoderDecoder.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
