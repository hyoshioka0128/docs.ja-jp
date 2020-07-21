---
title: '方法: ビジュアルの描画コンテンツを列挙する'
ms.date: 03/30/2017
helpviewer_keywords:
- retrieving the DrawingGroup value of a Visual [WPF]
- enumerating the contents of a Visual [WPF]
ms.assetid: 2974ddb3-2997-4713-8fd2-e93d549c58a8
ms.openlocfilehash: 25aa0c3706005c1e16cedd7e06914db764545ebb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930072"
---
# <a name="how-to-enumerate-drawing-content-of-a-visual"></a>方法: ビジュアルの描画コンテンツを列挙する
<xref:System.Windows.Media.Drawing> オブジェクトは、<xref:System.Windows.Media.Visual> のコンテンツを列挙するためのオブジェクト モデルを提供します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> メソッドを使用して <xref:System.Windows.Media.Visual> の <xref:System.Windows.Media.DrawingGroup> 値を取得し、それを列挙します。  
  
> [!NOTE]
> ビジュアルのコンテンツを列挙する場合は、レンダリング データの基になる表現をベクター グラフィックス命令リストとして取得するのではなく、<xref:System.Windows.Media.Drawing> オブジェクトを取得することになります。 詳しくは、「[WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)」をご覧ください。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Drawing>
- <xref:System.Windows.Media.DrawingGroup>
- <xref:System.Windows.Media.VisualTreeHelper>
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
