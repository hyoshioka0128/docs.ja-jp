---
title: '方法: 開始後のストーリーボードをイベント トリガーを使用して制御する'
ms.date: 03/30/2017
helpviewer_keywords:
- triggers [WPF], controlling Storyboards
- event triggers [WPF], controlling Storyboards
- Storyboards [WPF], controlling after start
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
ms.openlocfilehash: 518f5d7ea0b5dc00677489f1383814563c565145
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186703"
---
# <a name="how-to-use-event-triggers-to-control-a-storyboard-after-it-starts"></a>方法: 開始後のストーリーボードをイベント トリガーを使用して制御する

この例では、<xref:System.Windows.Media.Animation.Storyboard>を開始後に制御する方法を示します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して <xref:System.Windows.Media.Animation.Storyboard> を開始するには <xref:System.Windows.Media.Animation.BeginStoryboard> を使用します。これは、アニメーション化するオブジェクトとプロパティにアニメーションを配布し、ストーリーボードを開始します。 <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> プロパティを指定して <xref:System.Windows.Media.Animation.BeginStoryboard> に名前を付けると、制御可能なストーリーボードになります。 これで、開始後のストーリーボードを対話的に制御できます。

次のストーリーボード アクションを <xref:System.Windows.EventTrigger> オブジェクトと共に使用して、ストーリーボードを制御します。

- <xref:System.Windows.Media.Animation.PauseStoryboard>:ストーリーボードを一時停止します。

- <xref:System.Windows.Media.Animation.ResumeStoryboard>:一時停止したストーリーボードを再開します。

- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>:ストーリーボードの速度を変更します。

- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>:ストーリーボードをその保留期間 (ある場合) の最後に進めます。

- <xref:System.Windows.Media.Animation.StopStoryboard>:ストーリーボードを停止します。

- <xref:System.Windows.Media.Animation.RemoveStoryboard>:ストーリーボードを削除し、リソースを解放します。

## <a name="example"></a>例

次の例では、制御可能なストーリーボード アクションを使用して、ストーリーボードを対話的に制御しています。

> [!NOTE]
> コードを使用してストーリーボードを制御する例については、[対話型メソッドを使用してストーリーボードを開始後に制御する](how-to-control-a-storyboard-after-it-starts.md)方法に関するページを参照してください。

[!code-xaml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]

その他の例については、「[アニメーション サンプル ギャラリー](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationExamples)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.ResumeStoryboard>
- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>
- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>
- <xref:System.Windows.Media.Animation.PauseStoryboard>
- <xref:System.Windows.Media.Animation.StopStoryboard>
- <xref:System.Windows.Media.Animation.SeekStoryboard>
- [対話型メソッドを使用してストーリーボードを開始後に制御する](how-to-control-a-storyboard-after-it-starts.md)
- [アニメーションの概要](animation-overview.md)
- [ストーリーボードの概要](storyboards-overview.md)
