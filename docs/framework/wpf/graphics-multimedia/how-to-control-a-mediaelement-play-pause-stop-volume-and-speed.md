---
title: '方法: MediaElement (再生、一時停止、停止、ボリューム、および速度) を制御する'
description: Windows Presentation Foundation (WPF) でメディアの再生を制御します。 開始、停止、一時停止、前後へのスキップ、ボリュームと速度の調整を行います。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- playback of media [WPF], controlling
- controlling playback of media [WPF]
- multimedia [WPF], controlling playback of media
- media [WPF], controlling playback of
ms.assetid: 6885a730-e054-4c16-8c1e-ffe17b1f7c32
ms.openlocfilehash: da846299eaa1e36b6e5caab08bc1f861e9f9c46d
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853601"
---
# <a name="how-to-control-a-mediaelement-play-pause-stop-volume-and-speed"></a>方法: MediaElement (再生、一時停止、停止、ボリューム、および速度) を制御する
次の例では、<xref:System.Windows.Controls.MediaElement> を使用してメディアの再生を制御する方法を示します。 この例では、メディアの再生、一時停止、停止、前後へのスキップに加え、ボリュームと速度の調整も可能な簡単なメディア プレーヤーを作成します。  
  
## <a name="example"></a>例  
 次のコードでは、UI を作成します。  
  
> [!NOTE]
> メディアを対話的に停止、一時停止、再生できるようにするには、<xref:System.Windows.Controls.MediaElement> の <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> プロパティを `Manual` に設定する必要があります。  
  
 [!code-xaml[MediaGallery_snip#MediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml#mediaelementexamplewholepage)]  
  
## <a name="example"></a>例  
 次のコードは、サンプル UI コントロールの機能を実装しています。 <xref:System.Windows.Controls.MediaElement.Play%2A> メソッド、<xref:System.Windows.Controls.MediaElement.Pause%2A> メソッド、<xref:System.Windows.Controls.MediaElement.Stop%2A> メソッドを使用して、メディアをそれぞれ再生、一時停止、停止します。 <xref:System.Windows.Controls.MediaElement> の <xref:System.Windows.Controls.MediaElement.Position%2A> プロパティを変更すると、メディア内でスキップできます。 最後に、<xref:System.Windows.Controls.MediaElement.Volume%2A> プロパティと <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> プロパティを使用して、メディアのボリュームと再生速度を調整します。  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaElementExample.xaml.cs#codebehindmediaelementexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml.vb#codebehindmediaelementexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [ストーリーボードを使用して MediaElement を制御する](how-to-control-a-mediaelement-by-using-a-storyboard.md)
