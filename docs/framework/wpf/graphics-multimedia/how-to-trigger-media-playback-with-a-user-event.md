---
title: '方法: ユーザー イベントによってメディアの再生をトリガーする'
ms.date: 03/30/2017
helpviewer_keywords:
- synchronizing media playback with events [WPF]
- playback of media [WPF], synchronizing with events
- media [WPF], synchronizing playback with events
- multimedia [WPF], synchronizing media playback with events
ms.assetid: c4dbe632-6e7f-4d7f-9df5-98737a758bc3
ms.openlocfilehash: ae8ba54cc852bb85350492c95e3e890aebf6534f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769279"
---
# <a name="how-to-trigger-media-playback-with-a-user-event"></a>方法: ユーザー イベントによってメディアの再生をトリガーする
この例では、メディアの再生とイベントを同期する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.MediaElement> コントロールと <xref:System.Windows.Media.MediaTimeline> クラスを使用し、ユーザーが <xref:System.Windows.Controls.Button> をクリックしたときに発生する音を再生します。  
  
 [!code-xaml[MediaGallery_snippet#SoundFromUserEventExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/SoundFromUserEventExample.xaml#soundfromusereventexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.MediaElement>
- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.EventTrigger.RoutedEvent%2A>
- <xref:System.Windows.Media.Animation.Storyboard>
- [方法トピック](audio-and-video-how-to-topics.md)
- [グラフィックスとマルチメディア](index.md)
