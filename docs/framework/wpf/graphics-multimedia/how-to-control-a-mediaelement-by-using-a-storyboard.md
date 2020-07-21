---
title: '方法: ストーリーボードを使用して MediaElement を制御する'
description: Windows Presentation Foundation (WPF) でストーリーボードを使用してメディアの再生を制御します。 単純なメディア プレーヤーを作成する場合は、この例を検討してください。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- multimedia [WPF], controlling playback of media with Storyboards
- controlling playback of media [WPF], with Storyboards
- Storyboards [WPF], controlling playback of media with
- media [WPF], controlling playback with Storyboards
- playback of media [WPF], controlling with Storyboards
ms.assetid: 6128ca77-b826-4e36-b968-6f237157c543
ms.openlocfilehash: 5a5e41b9a28211495fd3374c1a51a655dd867bca
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853739"
---
# <a name="how-to-control-a-mediaelement-by-using-a-storyboard"></a>方法: ストーリーボードを使用して MediaElement を制御する
この例では、<xref:System.Windows.Media.Animation.Storyboard> で <xref:System.Windows.Media.MediaTimeline> を使用し、<xref:System.Windows.Controls.MediaElement> を制御する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.Storyboard> で <xref:System.Windows.Media.MediaTimeline> を使用して <xref:System.Windows.Controls.MediaElement> のタイミングを制御するとき、機能は、アニメーションなど、他の <xref:System.Windows.Media.Animation.Timeline> オブジェクトの機能と同じになります。 たとえば、<xref:System.Windows.Media.MediaTimeline> では、<xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> プロパティなどの <xref:System.Windows.Media.Animation.Timeline> プロパティを使用し、<xref:System.Windows.Controls.MediaElement> を起動するタイミングを指定します (メディア再生開始)。 また、<xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティを使用し、<xref:System.Windows.Controls.MediaElement> がアクティブになる時間を指定します (メディア再生時間)。 <xref:System.Windows.Media.Animation.Storyboard> で <xref:System.Windows.Media.Animation.Timeline> オブジェクトを使用する方法の詳細については、「[ストーリーボードの概要](storyboards-overview.md)」を参照してください。  
  
 この例では、<xref:System.Windows.Media.MediaTimeline> を使用して再生を制御する単純なメディア プレーヤーを作成する方法を示します。 メディア プレーヤーには、再生、一時停止、再開、停止のボタンがあります。 プレーヤーにはまた、進行状況バーとして機能する <xref:System.Windows.Controls.Slider> コントロールがあります。  
  
 次の例では、メディア プレーヤーの [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] が作成されます。  
  
 [!code-xaml[MediaGallery_snip#MediaTimelineExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml#mediatimelineexamplewholepage)]  
  
 次の例では、進行状況バーの機能が作成されます。  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaTimelineExample.xaml.cs#codebehindmediatimelineexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml.vb#codebehindmediatimelineexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.MediaElement>
- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.Media.Animation.Storyboard>
- [MediaElement (再生、一時停止、停止、ボリューム、および速度) を制御する](how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)
- [ストーリーボードの概要](storyboards-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [アニメーションの概要](animation-overview.md)
- [方法トピック](audio-and-video-how-to-topics.md)
- [グラフィックスとマルチメディア](index.md)
