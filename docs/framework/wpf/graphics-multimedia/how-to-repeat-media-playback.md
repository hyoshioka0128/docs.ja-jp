---
title: '方法: メディアの再生を反復する'
ms.date: 03/30/2017
helpviewer_keywords:
- media [WPF], repeating playback
- repeating media playback [WPF]
- multimedia [WPF], repeating media playback
- playback of media [WPF], repeating
ms.assetid: 02ab486d-c6b6-4918-9edd-45a12aca4683
ms.openlocfilehash: 788bc6f31d61626f15548791135adb8c60258b49
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942052"
---
# <a name="how-to-repeat-media-playback"></a>方法: メディアの再生を反復する
この例では、メディアを無制限に再生する (無限ループで再生されるようにメディアを設定する) 方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.Storyboard> で <xref:System.Windows.Controls.MediaElement> と <xref:System.Windows.Media.MediaTimeline> を使用して、無限ループでメディア クリップを再生します。  
  
 [!code-xaml[MediaGallery_snippet#SoundRepeatExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/SoundRepeatExample.xaml#soundrepeatexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.MediaElement>
- <xref:System.Windows.Media.MediaTimeline>
- <xref:System.Windows.Media.Animation.Storyboard>
- [方法トピック](audio-and-video-how-to-topics.md)
- [グラフィックスとマルチメディア](index.md)
