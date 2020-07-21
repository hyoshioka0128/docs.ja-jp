---
title: '方法: アニメーションを反復する'
ms.date: 03/30/2017
helpviewer_keywords:
- RepeatBehavior property of timelines [WPF]
- repeating animating [WPF]
- Timelines RepeatBehavior property [WPF]
- animation [WPF], repeating
ms.assetid: e6f3b068-eeeb-47fd-8d40-8848c31f1e1e
ms.openlocfilehash: 1512c49a658c80f3ab6af652839c3562af3dd205
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141550"
---
# <a name="how-to-repeat-an-animation"></a>方法: アニメーションを反復する
この例では、<xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを使用して、アニメーションの反復動作を制御する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティは、アニメーションがその単純継続時間を反復する回数を制御します。 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> を使用すると、特定の回数 (反復回数) または指定した期間、<xref:System.Windows.Media.Animation.Timeline> を繰り返すように指定できます。 いずれの場合も、アニメーションは、要求されたカウントまたは期間を満たすのに必要な回数だけ最初から最後までの実行を反復します。  
  
 既定では、タイムラインの反復回数は 1.0 です。これは、1 回だけ再生して繰り返さないことを意味します。 ただし、<xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A> に設定すると、タイムラインは無期限に反復されます。  
  
 この例では、<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> プロパティを使用して、アニメーションの反復動作を制御する方法を示します。 この例では、5 つの四角形の <xref:System.Windows.FrameworkElement.Width%2A> プロパティをアニメーション化し、それぞれの四角形では異なる種類の反復動作が使用されます。  
  
 [!code-xaml[timingbehaviors_snip#RepeatBehaviorWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/RepeatBehaviorExample.xaml#repeatbehaviorwholepage)]  
  
 サンプル全体については、「[アニメーションのタイミング動作のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationTiming)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [反復サイクル中にアニメーション値を累積する](how-to-accumulate-animation-values-during-repeat-cycles.md)
- [タイムラインを自動的に反転するかどうかを指定する](how-to-specify-whether-a-timeline-automatically-reverses.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
- [アニメーションの概要](animation-overview.md)
- [アニメーションのタイミング動作のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationTiming)
