---
title: '方法: クロックの状態が変化したときに通知を受け取る'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clocks [WPF], notification of state changes
- notifications [WPF], clocks' state changes
ms.assetid: ecb10fc9-d0c2-45c3-b0a1-7b11baa733da
ms.openlocfilehash: dc3fffb88ce59ceb908d6febd2f078820513b641
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942138"
---
# <a name="how-to-receive-notification-when-a-clocks-state-changes"></a>方法: クロックの状態が変化したときに通知を受け取る
クロックの <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> イベントは、クロックが開始または停止されるなど、その <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> が無効になったときに発生します。 このイベントには、<xref:System.Windows.Media.Animation.Clock> を使用して直接登録することも、<xref:System.Windows.Media.Animation.Timeline> を使用して登録することもできます。  
  
 次の例では、2 つの四角形の幅をアニメーション化するために、<xref:System.Windows.Media.Animation.Storyboard> を 1 つと <xref:System.Windows.Media.Animation.DoubleAnimation> オブジェクトを 2 つ使用しています。 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> イベントは、クロックの状態の変化をリッスンするために使用しています。  
  
## <a name="example"></a>例  
 [!code-xaml[timingbehaviors_snip#_graphicsmm_StateExampleMarkupWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml#_graphicsmm_stateexamplemarkupwholepage)]  
  
 [!code-csharp[timingbehaviors_snip#_graphicsmm_StateEventHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml.cs#_graphicsmm_stateeventhandlers)]
 [!code-vb[timingbehaviors_snip#_graphicsmm_StateEventHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/stateexample.xaml.vb#_graphicsmm_stateeventhandlers)]  
  
 次の図では、親タイムライン ("*ストーリーボード*") の進捗に伴い、アニメーションが入るさまざまな状態を示しています。  
  
 ![2 つアニメーションがあるストーリーボードのクロックの状態](./media/graphicsmm-3timelines.png "graphicsmm_3timelines")  
  
 次の表は、*Animation1* の <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> イベントが発生する時刻を示しています。  
  
||||||||  
|-|-|-|-|-|-|-|  
|時間 (秒)|1|10|19|21|30|39|  
|状態|アクティブ|アクティブ|Stopped|アクティブ|アクティブ|Stopped|  
  
 次の表は、*Animation2* の <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> イベントが発生する時刻を示しています。  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
|時間 (秒)|1|9|11|19|21|29|31|39|  
|状態|アクティブ|フィル|アクティブ|Stopped|アクティブ|フィル|アクティブ|Stopped|  
  
 *Animation1*の状態が <xref:System.Windows.Media.Animation.ClockState.Active> のままであっても、<xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> イベントは 10 秒のときに発生することに着目してください。 これは、それの状態が 10 秒のときに変更されたけれども、同じティック内で <xref:System.Windows.Media.Animation.ClockState.Active> から <xref:System.Windows.Media.Animation.ClockState.Filling> に変更され、その後 <xref:System.Windows.Media.Animation.ClockState.Active> に戻っているためです。
