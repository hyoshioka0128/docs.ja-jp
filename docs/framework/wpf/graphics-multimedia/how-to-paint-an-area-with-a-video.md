---
title: '方法: ビデオを使用して領域を塗りつぶす'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- painting with a video [WPF]
- video [WPF], painting with
- brushes [WPF], painting with a video
ms.assetid: 04dd6600-4a6e-4b43-a93e-21cce7dfbcb8
ms.openlocfilehash: be09d1310847cd7214ea795a704c25d994f07b7a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921733"
---
# <a name="how-to-paint-an-area-with-a-video"></a>方法: ビデオを使用して領域を塗りつぶす
この例では、メディアを使用して領域を塗りつぶす方法を示します。 メディアを使用して領域を塗りつぶす 1 つの方法は、<xref:System.Windows.Media.VisualBrush> と共に <xref:System.Windows.Controls.MediaElement> を使用する方法です。 <xref:System.Windows.Controls.MediaElement> を使用してメディアを読み込み、再生し、それを使用して <xref:System.Windows.Media.VisualBrush> の <xref:System.Windows.Media.VisualBrush.Visual%2A> プロパティを設定します。 それから、<xref:System.Windows.Media.VisualBrush> を使用して、読み込まれたメディアで領域を塗りつぶします。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.MediaElement> と <xref:System.Windows.Media.VisualBrush> を使用して、<xref:System.Windows.Controls.TextBlock> コントロールの <xref:System.Windows.Controls.TextBlock.Foreground%2A> をビデオで塗りつぶします。 この例では、<xref:System.Windows.Controls.MediaElement> の <xref:System.Windows.Controls.MediaElement.IsMuted%2A> プロパティを `true` に設定して、音声が生成されないようにします。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundinline)]  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.VisualBrush> は <xref:System.Windows.Media.TileBrush> クラスから継承されるため、いくつかのタイル モードが用意されています。 <xref:System.Windows.Media.VisualBrush> の <xref:System.Windows.Media.TileBrush.TileMode%2A> プロパティを <xref:System.Windows.Media.TileMode.Tile> に設定し、その <xref:System.Windows.Media.TileBrush.Viewport%2A> プロパティを塗りつぶす領域よりも小さい値に設定すると、タイル化されたパターンを作成できます。  
  
 次の例は、前の例と <xref:System.Windows.Media.VisualBrush> がビデオからパターンを生成することを除き同じです。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundtiledinline)]  
  
 メディア ファイルなどのコンテンツ ファイルをお使いのアプリケーションに追加する方法については、「[WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](../app-development/wpf-application-resource-content-and-data-files.md)」を参照してください。 メディア ファイルを追加する場合は、それをリソース ファイルとしてではなく、コンテンツ ファイルとして追加する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.VisualBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [TileBrush の概要](tilebrush-overview.md)
- [マルチメディアの概要](multimedia-overview.md)
