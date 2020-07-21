---
title: アニメーションとタイミング システムの概要
ms.date: 03/30/2017
helpviewer_keywords:
- timing system [WPF]
- animation [WPF]
ms.assetid: 172cd5a8-a333-4c81-9456-fafccc19f382
ms.openlocfilehash: d0ac2a8160a1e6f9bcdb333593ec207954b391aa
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187716"
---
# <a name="animation-and-timing-system-overview"></a>アニメーションとタイミング システムの概要
このトピックでは、タイミング システムがアニメーション、<xref:System.Windows.Media.Animation.Timeline>、および <xref:System.Windows.Media.Animation.Clock> クラスを使用してプロパティをアニメーション化する方法について説明します。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、「[アニメーションの概要](animation-overview.md)」で説明されているように、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーションを使ってプロパティをアニメーション化できる必要があります。 依存関係プロパティの理解も役に立ちます。詳しくは、「[依存関係プロパティの概要](../advanced/dependency-properties-overview.md)」をご覧ください。  
  
<a name="timelinesandclocks"></a>
## <a name="timelines-and-clocks"></a>タイムラインとクロック  
 「[アニメーションの概要](animation-overview.md)」では、<xref:System.Windows.Media.Animation.Timeline> が時間のセグメントを表す方法、およびアニメーションが出力値を生成する <xref:System.Windows.Media.Animation.Timeline> の種類であることを説明しました。 <xref:System.Windows.Media.Animation.Timeline> だけでは、時間のセグメントを記述すること以外何も行われません。 実際の処理を行うのは、タイムラインの <xref:System.Windows.Media.Animation.Clock> オブジェクトです。 同様に、アニメーションは実際にはプロパティをアニメーション化しません。アニメーション クラスでは出力値の計算方法が記述されますが、アニメーションの出力を生成してそれをプロパティに適用するのは、アニメーションに対して作成された <xref:System.Windows.Media.Animation.Clock> です。  
  
 <xref:System.Windows.Media.Animation.Clock> は、<xref:System.Windows.Media.Animation.Timeline> に対するタイミング関連の実行時状態を保持する特殊な種類のオブジェクトです。 これは、アニメーションとタイミング システムに不可欠な 3 つの情報である <xref:System.Windows.Media.Animation.Clock.CurrentTime%2A>、<xref:System.Windows.Media.Animation.Clock.CurrentProgress%2A>、<xref:System.Windows.Media.Animation.Clock.CurrentState%2A> を提供します。 <xref:System.Windows.Media.Animation.Clock> は、<xref:System.Windows.Media.Animation.Timeline> によって記述されるタイミング動作を使用して、現在時間、進行状況、状態を決定します (<xref:System.Windows.Media.Animation.Timeline.Duration%2A>、<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>、<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> など)。  
  
 ほとんどの場合、<xref:System.Windows.Media.Animation.Clock> はタイムラインに対して自動的に作成されます。 <xref:System.Windows.Media.Animation.Storyboard> または <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用してアニメーションを作成すると、タイムラインとアニメーションに対してクロックが自動的に作成されて、対象のプロパティに適用されます。 また、<xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> メソッドを使用して <xref:System.Windows.Media.Animation.Clock> を明示的に作成することもできます。 <xref:System.Windows.Media.MediaTimeline.CreateClock%2A?displayProperty=nameWithType> メソッドは、呼び出された <xref:System.Windows.Media.Animation.Timeline> に対して適切な型のクロックを作成します。 <xref:System.Windows.Media.Animation.Timeline> に子タイムラインが含まれる場合は、それらに対しても <xref:System.Windows.Media.Animation.Clock> オブジェクトを作成します。 結果の <xref:System.Windows.Media.Animation.Clock> オブジェクトは、作成元の <xref:System.Windows.Media.Animation.Timeline> オブジェクト ツリーの構造と一致するツリーに編成されます。  
  
 異なる型のタイムラインに対して異なる型のクロックがあります。 次の表では、<xref:System.Windows.Media.Animation.Timeline> の異なる型に対応する <xref:System.Windows.Media.Animation.Clock> の型を示します。  
  
|タイムラインの型|クロックの型|クロックの目的|  
|-------------------|----------------|-------------------|  
|Animation (<xref:System.Windows.Media.Animation.AnimationTimeline>から継承)|<xref:System.Windows.Media.Animation.AnimationClock>|依存関係プロパティの出力値を生成します。|  
|<xref:System.Windows.Media.MediaTimeline>|<xref:System.Windows.Media.MediaClock>|メディア ファイルを処理します。|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|<xref:System.Windows.Media.Animation.ClockGroup>|子の <xref:System.Windows.Media.Animation.Clock> オブジェクトをグループ化して制御します。|  
|<xref:System.Windows.Media.Animation.Storyboard>|<xref:System.Windows.Media.Animation.ClockGroup>|子の <xref:System.Windows.Media.Animation.Clock> オブジェクトをグループ化して制御します。|  
  
 <xref:System.Windows.Media.Animation.IAnimatable.ApplyAnimationClock%2A> メソッドを使用することで、作成した <xref:System.Windows.Media.Animation.AnimationClock> オブジェクトを互換性のある依存関係プロパティに適用できます。  
  
 多数の似たオブジェクトのアニメーション化など、負荷の高いシナリオでは、独自の <xref:System.Windows.Media.Animation.Clock> の使用を管理するとパフォーマンスの利点があります。  
  
<a name="timemanager"></a>
## <a name="clocks-and-the-time-manager"></a>クロックとタイム マネージャー  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でオブジェクトをアニメーション化するとき、タイムラインに対して作成された <xref:System.Windows.Media.MediaPlayer.Clock%2A> オブジェクトを管理するのはタイム マネージャーです。 タイム マネージャーは <xref:System.Windows.Media.MediaPlayer.Clock%2A> オブジェクトのツリーのルートで、そのツリー内の時間の流れを制御します。  タイム マネージャーは各 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションに自動的に作成され、アプリケーション開発者には表示されません。 タイム マネージャーは 1 秒間に何度も "タイマーを刻み" ます。1 秒ごとに刻まれるタイマーの実際の数は、使用可能なシステム リソースによって異なります。 これらのティックごとに、タイム マネージャーはタイミング ツリー内のすべての <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> オブジェクトの状態を計算します。  
  
 次の図では、タイム マネージャー、<xref:System.Windows.Media.Animation.AnimationClock>、およびアニメーション化される依存関係プロパティの間の関係を示します。  
  
 ![タイミング システムのコンポーネント](./media/graphicsmm-clocks-1clock1prop.png "graphicsmm_clocks_1clock1prop")  
プロパティのアニメーション化  
  
 タイム マネージャーは、タイマーを刻むとき、アプリケーション内のすべての <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> の時刻を更新します。 <xref:System.Windows.Media.Animation.Clock> が <xref:System.Windows.Media.Animation.AnimationClock> の場合は、作成元の <xref:System.Windows.Media.Animation.AnimationTimeline> の <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> メソッドを使用して、現在の出力値を計算します。 <xref:System.Windows.Media.Animation.AnimationClock> は、<xref:System.Windows.Media.Animation.AnimationTimeline> に、現在のローカル時刻、入力値 (通常はプロパティの基本値)、既定の目標値を提供します。 <xref:System.Windows.DependencyObject.GetValue%2A> メソッドまたはその CLR アクセサーを使用してプロパティによってアニメーション化された値を取得するときは、その <xref:System.Windows.Media.Animation.AnimationClock> の出力を取得します。  
  
#### <a name="clock-groups"></a>クロック グループ  
 前のセクションでは、タイムラインの異なる型に対して <xref:System.Windows.Media.Animation.Clock> オブジェクトの異なる型があることを説明しました。 次の図では、タイム マネージャー、<xref:System.Windows.Media.Animation.ClockGroup>、<xref:System.Windows.Media.Animation.AnimationClock>、およびアニメーション化される依存関係プロパティの間の関係を示します。 <xref:System.Windows.Media.Animation.ClockGroup> は、アニメーションと他のタイムラインをグループ化する <xref:System.Windows.Media.Animation.Storyboard> クラスなど、他のタイムラインをグループ化するタイムラインに対して作成されます。  
  
 ![タイミング システムのコンポーネント](./media/graphicsmm-clocks-2clock1clockgroup2prop.png "graphicsmm_clocks_2clock1clockgroup2prop")  
ClockGroup  
  
#### <a name="composition"></a>コンポジション  
 複数のクロックを 1 つのプロパティと関連付けることができます。その場合、各クロックは前のクロックの出力値を基本値として使います。 次の図は、同じプロパティに適用された 3 つの <xref:System.Windows.Media.Animation.AnimationClock> オブジェクトを示したものです。 Clock1 は、アニメーション化されたプロパティの基本値を入力として使って、出力を生成します。 Clock2 は、Clock1 の出力を入力として受け取り、それを使って出力を生成します。 Clock3 は、Clock2 の出力を入力として受け取り、それを使って出力を生成します。 複数のクロックが同じプロパティに同時に影響を与える場合、それらはコンポジション チェーン内にあると言います。  
  
 ![タイミング システムのコンポーネント](./media/graphicsmm-clocks-2clock1prop.png "graphicsmm_clocks_2clock1prop")  
コンポジション チェーン  
  
 コンポジション チェーン内の <xref:System.Windows.Media.Animation.AnimationClock> オブジェクトの入力と出力の間には関係が作成されますが、それらのタイミング動作は影響を受けません。<xref:System.Windows.Media.Animation.Clock> オブジェクト (<xref:System.Windows.Media.Animation.AnimationClock> オブジェクトを含みます) には、親の <xref:System.Windows.Media.Animation.Clock> オブジェクトに対する階層的依存関係があります。  
  
 複数のクロックを同じプロパティに適用するには、<xref:System.Windows.Media.Animation.Storyboard>、アニメーション、または <xref:System.Windows.Media.Animation.AnimationClock> を適用するときに、<xref:System.Windows.Media.Animation.HandoffBehavior.Compose> <xref:System.Windows.Media.Animation.HandoffBehavior> を使用します。  
  
#### <a name="ticks-and-event-consolidation"></a>ティックとイベントの統合  
 出力値を計算するだけでなく、タイム マネージャーはティックのたびに他の処理を行います。つまり、クロックの状態を判断し、必要に応じてイベントを発生させます。  
  
 ティックは頻繁に発生しますが、各ティックの間には多くのことが起こる可能性があります。 たとえば、<xref:System.Windows.Media.Animation.Clock> が停止し、開始し、再び停止することがあります。このような場合、<xref:System.Windows.Media.Animation.Clock.CurrentState%2A> の値は 3 回変化します。 理論的には、1 回のティックで <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> イベントを複数回発生させることができます。ただし、タイミング エンジンは、<xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> イベントがティックごとに多くても 1 回だけ発生するように、イベントを統合します。 これは、すべてのタイミング イベントにあてはまります。特定の <xref:System.Windows.Media.Animation.Clock> オブジェクトに対して生成される各種類のイベントは、多くても 1 回です。  
  
 ティックの間に <xref:System.Windows.Media.Animation.Clock> が状態を切り替えて元の状態に戻る場合でも (<xref:System.Windows.Media.Animation.ClockState.Active> から <xref:System.Windows.Media.Animation.ClockState.Stopped> になり、<xref:System.Windows.Media.Animation.ClockState.Active> に戻る場合など)、関連するイベントが発生します。  
  
 タイミング イベントについて詳しくは、「[タイミング イベントの概要](timing-events-overview.md)」をご覧ください。  
  
<a name="currentvaluesbasevaluesofproperties"></a>
## <a name="current-values-and-base-values-of-properties"></a>プロパティの現在値と基本値  
 アニメーション化可能なプロパティは、基本値と現在値の 2 つの値を持つことができます。 CLR アクセサーまたは <xref:System.Windows.DependencyObject.SetValue%2A> メソッドを使用してプロパティを設定すると、基本値が設定されます。 プロパティがアニメーション化されない場合は、基本値と現在値は同じです。  
  
 プロパティをアニメーション化すると、<xref:System.Windows.Media.Animation.AnimationClock> はプロパティの "*現在*" の値を設定します。 CLR アクセサーまたは <xref:System.Windows.DependencyObject.GetValue%2A> メソッドを使用してプロパティの値を取得すると、<xref:System.Windows.Media.Animation.AnimationClock> が <xref:System.Windows.Media.Animation.ClockState.Active> または <xref:System.Windows.Media.Animation.ClockState.Filling> であるときの <xref:System.Windows.Media.Animation.AnimationClock> の出力が返されます。 プロパティの基本値は、<xref:System.Windows.Media.Animation.IAnimatable.GetAnimationBaseValue%2A> メソッドを使用して取得できます。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [タイミング イベントの概要](timing-events-overview.md)
- [タイミング動作の概要](timing-behaviors-overview.md)
