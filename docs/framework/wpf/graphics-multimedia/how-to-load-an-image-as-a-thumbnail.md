---
title: '方法: サムネイルとしてイメージを読み込む'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- loading images as thumbnails [WPF]
- images [WPF], loading as thumbnails
- thumbnails [WPF], loading images as
ms.assetid: 02e055a0-54df-499a-b8b6-ab6ff7535cff
ms.openlocfilehash: f984293a395e925368b20cef6aa0cd902bd6fc15
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62003185"
---
# <a name="how-to-load-an-image-as-a-thumbnail"></a>方法: サムネイルとしてイメージを読み込む
次の例は、<xref:System.Windows.Controls.Image> をサムネイルとして読み込み、アプリケーション メモリを節約する方法を示しています。  
  
## <a name="example"></a>例  
 次の例では、イメージの読み込みに必要なメモリを減らすために、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で <xref:System.Windows.Media.Imaging.BitmapImage> の <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> プロパティを設定します。  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
## <a name="example"></a>例  
 次の例では、イメージの読み込みに必要なメモリを減らすために、コードで <xref:System.Windows.Media.Imaging.BitmapImage> の <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> プロパティを設定します。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
## <a name="see-also"></a>関連項目

- [イメージングの概要](imaging-overview.md)
