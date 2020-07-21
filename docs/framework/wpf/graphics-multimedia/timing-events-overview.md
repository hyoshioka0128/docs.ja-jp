---
title: タイミング イベントの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- timelines [WPF]
- timing events [WPF]
ms.assetid: 597e3280-0867-4359-a97b-5b2f4149e350
ms.openlocfilehash: ee45441e9ad09c60d8b61ecce4ef08b0027ce29e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79145411"
---
# <a name="timing-events-overview"></a>タイミング イベントの概要
このトピックでは、<xref:System.Windows.Media.Animation.Timeline> および <xref:System.Windows.Media.Animation.Clock> オブジェクトで使用できる 5 つのタイミング イベントの使用方法について説明します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、アニメーションの作成方法と使用方法について理解している必要があります。 アニメーションの概要については、「[アニメーションの概要](animation-overview.md)」をご覧ください。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でプロパティをアニメーション化するには、複数の方法があります。  
  
- **ストーリーボード オブジェクトを使用する** (マークアップとコード): <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用して、1 つ以上のオブジェクトにアニメーションを配置および均等配置することができます。 例については、「[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)」をご覧ください。  
  
- **ローカル アニメーションを使用する** (コードのみ): アニメーション化するプロパティに <xref:System.Windows.Media.Animation.AnimationTimeline> オブジェクトを直接適用できます。 例については、「[ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)」を参照してください。  
  
- **クロックを使用する** (コードのみ): クロックを明示的に作成し、アニメーション クロックを自分で均等配置できます。  例については、「[AnimationClock を使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-an-animationclock.md)」をご覧ください。  
  
 マークアップとコードで使用できるという理由から、この概要の例では <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用しています。 ただし、説明されている概念は、プロパティをアニメーション化するためのその他の方法にも適用できます。  
  
### <a name="what-is-a-clock"></a>クロックとは  
 タイムラインは、時間のセグメントについて説明する以外は、それ自身が実際に何かを行うものではありません。 実際の処理を行うのは、タイムラインの <xref:System.Windows.Media.Animation.Clock> オブジェクトです。このオブジェクトは、タイムラインのタイミングに関連する実行時状態を維持します。 多くの場合(ストーリー ボードを使用する場合など)には、タイムラインに対してクロックが自動的に作成されます。 また、<xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> メソッドを使用して <xref:System.Windows.Media.Animation.Clock> を明示的に作成することもできます。 <xref:System.Windows.Media.Animation.Clock> オブジェクトについて詳しくは、「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください。  
  
## <a name="why-use-events"></a>イベントを使用する理由  
 1 つの例外 (最後のティックに配置されたシーク) を除いて、すべての対話型タイミング操作は非同期です。 これらがいつ実行されるかを正確に知る方法はありません。 これは、タイミング操作に依存する他のコードが存在する場合に、問題となることがあります。 たとえば、四角形をアニメーション化するタイムラインを停止する必要があるとします。 そしてタイムラインを停止した後に、四角形の色を変更するとします。  
  
 [!code-csharp[events_procedural#NeedForEventsFragment](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#needforeventsfragment)]
 [!code-vb[events_procedural#NeedForEventsFragment](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#needforeventsfragment)]  
  
 上記の例では、ストーリー ボードが停止する前に、2 行目のコードが実行される可能性があります。 これは、停止が非同期の操作であるためです。 タイムラインやクロックに停止を指示すると、タイミング エンジンの次のティックまで処理されない「停止要求」が作成されます。  
  
 タイムラインの完了後にコマンドを実行するには、タイミング イベントを使用します。 次の例では、ストーリー ボードが停止した後に四角形の色が変更されるよう、イベント ハンドラーが使用されています。  
  
 [!code-csharp[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#registerforstoryboardcurrentstateinvalidatedevent)]
 [!code-vb[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#registerforstoryboardcurrentstateinvalidatedevent)]  
[!code-csharp[events_procedural#StoryboardCurrentStateInvalidatedEvent2](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#storyboardcurrentstateinvalidatedevent2)]
[!code-vb[events_procedural#StoryboardCurrentStateInvalidatedEvent2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#storyboardcurrentstateinvalidatedevent2)]  
  
 より詳しい例については、「[クロックの状態が変化したときに通知を受け取る](how-to-receive-notification-when-clock-state-changes.md)」をご覧ください。  
  
## <a name="public-events"></a>パブリック イベント  
 <xref:System.Windows.Media.Animation.Timeline> および <xref:System.Windows.Media.Animation.Clock> クラスでは、5 つのタイミング イベントが提供されます。 次の表は、これらのイベントと、それらをトリガーする条件を示したものです。  
  
|event|対話型操作のトリガー|その他のトリガー|  
|-----------|--------------------------------------|--------------------|  
|**Completed**|塗りつぶしまでスキップ|時計が完了する。|  
|**CurrentGlobalSpeedInvalidated**|一時停止、再開、シーク、速度比を設定、塗りつぶしまでスキップ、停止|クロックが反転、加速、開始、または停止する。|  
|**CurrentStateInvalidated**|開始、塗りつぶしまでスキップ、停止|クロックが開始、停止、または塗りつぶされる。|  
|**CurrentTimeInvalidated**|開始、シーク、塗りつぶしまでスキップ、停止|クロックが進行する。|  
|**RemoveRequested**|削除||  
  
## <a name="ticking-and-event-consolidation"></a>ティッキングとイベントの統合  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でオブジェクトをアニメーション化する際、アニメーションを管理するのはタイミング エンジンです。 タイミング エンジンは、時間の進行状況を追跡し、それぞれのアニメーションの状態を計算します。 これにより、多数の評価パスが瞬時に作成されます。 これらの評価パスは「ティック」と呼ばれます。  
  
 ティックは頻繁に発生しますが、各ティックの間には多くのことが起こる可能性があります。 たとえば、タイムラインが停止され、開始され、再度停止された場合、その現行状態は 3 回変更されることになります。 理論上、イベントは 1 つのティックで複数回発生することができますが、タイミング エンジンではイベントが統合されるため、各イベントの発生回数はティックあたり最大で 1回となります。  
  
## <a name="registering-for-events"></a>イベントの登録  
 タイミング イベントを登録する方法は 2 つあります。 タイムラインに登録する方法と、タイムラインから作成されたクロックに登録する方法です。 クロックに直接登録する方法は非常に分かりやすいですが、これはコードからのみ実行できます。 タイムラインに登録する場合は、マークアップまたはコードからイベントを登録できます。 次のセクションでは、クロック イベントをタイムラインに登録する方法について説明します。  
  
<a name="registeringforclockeventswithatimeline"></a>
## <a name="registering-for-clock-events-with-a-timeline"></a>クロック イベントをタイムラインに登録する  
 タイムラインの <xref:System.Windows.Media.Animation.Timeline.Completed>、<xref:System.Windows.Media.Animation.Timeline.CurrentGlobalSpeedInvalidated>、<xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated>、<xref:System.Windows.Media.Animation.Timeline.CurrentTimeInvalidated>、および <xref:System.Windows.Media.Animation.Timeline.RemoveRequested> イベントは、タイムラインに関連付けられているように見えますが、これらのイベントを登録した場合、実際には、タイムラインに対して作成された <xref:System.Windows.Media.Animation.Clock> に、イベント ハンドラーが関連付けられます。  
  
 たとえば、<xref:System.Windows.Media.Animation.Timeline.Completed> イベントをタイムラインに登録した場合、実際には、タイムラインに対して作成された各クロックの <xref:System.Windows.Media.Animation.Clock.Completed> イベントを登録するようシステムに指示したことになります。 コードでは、そのタイムラインに対して <xref:System.Windows.Media.Animation.Clock> が作成される前に、このイベントを登録する必要があります。そうしないと、通知を受信できません。 これは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では自動的に処理されます。<xref:System.Windows.Media.Animation.Clock> が作成される前に、パーサーが自動的にイベントを登録します。  
  
## <a name="see-also"></a>関連項目

- [アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)
- [アニメーションの概要](animation-overview.md)
- [タイミング動作の概要](timing-behaviors-overview.md)
