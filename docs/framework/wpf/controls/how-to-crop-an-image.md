---
title: '方法: イメージをトリミングする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [WPF], cropping
- cropping images [WPF]
ms.assetid: c6bba109-c6e7-4cf8-bfe6-9cf8d01bb4fc
ms.openlocfilehash: e672c7e24ec4db2d6424fa0b611cb1c135cf8eec
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053393"
---
# <a name="how-to-crop-an-image"></a>方法: イメージをトリミングする
この例では、<xref:System.Windows.Media.Imaging.CroppedBitmap> を使用してイメージをトリミングする方法を示します。  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap> は主に、トリミングしたイメージをエンコードしてファイルに保存するときに使用されます。 表示目的でイメージをトリミングする方法については、「[方法: クリップ領域を作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms746710(v=vs.90))」を参照してください。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、以下のサンプル内で使用されるリソースを定義します。  
  
 [!code-xaml[imageelementexample#CroppedXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml1)]  
  
 次の例では、そのソースとして <xref:System.Windows.Media.Imaging.CroppedBitmap> を使用し、イメージが作成されます。  
  
 [!code-xaml[imageelementexample#CroppedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml2)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp1)]
 [!code-vb[imageelementexample#CroppedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp1)]  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap> は別の <xref:System.Windows.Media.Imaging.CroppedBitmap> のソースとして利用し、トリミングを連結することもできます。 <xref:System.Windows.Media.Imaging.CroppedBitmap.SourceRect%2A> では、最初のイメージではなく、ソースのトリミングされたビットマップの相対値が使用されることにご注意ください。  
  
 [!code-xaml[imageelementexample#CroppedXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml3)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp2)]
 [!code-vb[imageelementexample#CroppedCSharp2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp2)]  
  
## <a name="see-also"></a>関連項目

- [方法: クリップ領域を作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms746710(v=vs.90))
