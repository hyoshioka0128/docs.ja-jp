---
title: '方法: タイムラインを自動的に反転するかどうかを指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- AutoReverse property of timelines [WPF]
- Timelines [WPF], AutoReverse property
ms.assetid: 1648dd90-1bee-409a-ac69-ac729867f557
ms.openlocfilehash: 0fe2d337d8afa5197475e5b9ee40950226596e8b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024665"
---
# <a name="how-to-specify-whether-a-timeline-automatically-reverses"></a>方法: タイムラインを自動的に反転するかどうかを指定する
タイムラインの <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティによって、前方の反復が完了した後、逆方向に再生するかどうかが決定されます。 次の例ではいくつかのアニメーションを確認できますが、継続時間とターゲット値が同じでも、<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 設定が異なっています。 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 設定を変えたときの <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティの動作を見せる目的で、一部のアプリケーションが繰り返されるように設定されています。 最後のアニメーションでは、入れ子になっているタイムラインでの <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> プロパティの動作を示します。  
  
## <a name="example"></a>例  
 [!code-xaml[timingbehaviors_snip#AutoReverseAndRepeatBehaviorExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AutoReverseExample.xaml#autoreverseandrepeatbehaviorexamplewholepage)]
