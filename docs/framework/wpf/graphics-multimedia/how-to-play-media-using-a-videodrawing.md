---
title: '方法: VideoDrawing を使用してメディアを再生する'
ms.date: 03/30/2017
helpviewer_keywords:
- playback of media [WPF]
- classes [WPF], MediaPlayer
ms.assetid: 165d47ed-22ce-4ded-aa6a-aa9b7467de87
ms.openlocfilehash: 2e2007525be770186a17cf9d2d42a7c52ba93fba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956951"
---
# <a name="how-to-play-media-using-a-videodrawing"></a>方法: VideoDrawing を使用してメディアを再生する
オーディオ ファイルまたはビデオ ファイルを再生するには、<xref:System.Windows.Media.VideoDrawing> と <xref:System.Windows.Media.MediaPlayer> を使用します。 メディアを読み込んで再生するには、2 つの方法があります。 1 つ目の方法は、<xref:System.Windows.Media.MediaPlayer> と <xref:System.Windows.Media.VideoDrawing> を単独で使用することです。2 つ目の方法は、<xref:System.Windows.Media.MediaPlayer> と <xref:System.Windows.Media.VideoDrawing> で使用する独自の <xref:System.Windows.Media.MediaTimeline> を作成することです。  
  
> [!NOTE]
> アプリケーションでメディアを配布するときは、イメージのようにプロジェクト リソースとしてメディア ファイルを使うことはできません。 プロジェクト ファイルで、メディアの種類を `Content` に設定し、`CopyToOutputDirectory` を `PreserveNewest` または `Always` に設定する必要があります。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.VideoDrawing> と <xref:System.Windows.Media.MediaPlayer> を使用して、ビデオ ファイルを 1 回再生します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 メディアに対する追加のタイミング制御を取得するには、<xref:System.Windows.Media.MediaPlayer> オブジェクトと <xref:System.Windows.Media.VideoDrawing> オブジェクトで <xref:System.Windows.Media.MediaTimeline> を使用します。 <xref:System.Windows.Media.MediaTimeline> を使用すると、ビデオを繰り返す必要があるかどうかを指定できます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.MediaPlayer> オブジェクトと <xref:System.Windows.Media.VideoDrawing> オブジェクトで <xref:System.Windows.Media.MediaTimeline> を使用して、ビデオを繰り返し再生します。  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 <xref:System.Windows.Media.MediaTimeline> を使用する場合は、<xref:System.Windows.Media.MediaPlayer> の対話型メソッドではなく、<xref:System.Windows.Media.MediaClock> の <xref:System.Windows.Media.Animation.Clock.Controller%2A> プロパティから返された対話型の <xref:System.Windows.Media.Animation.ClockController> を使用して、メディアの再生を制御します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.VideoDrawing>
- [Drawing オブジェクトの概要](drawing-objects-overview.md)
