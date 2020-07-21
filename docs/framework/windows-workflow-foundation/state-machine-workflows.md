---
title: ステート マシン ワークフロー
description: この記事では、StateMachine アクティビティを使用してステートマシンワークフローを作成する方法の概要について説明します。
ms.date: 03/30/2017
ms.assetid: 344caacd-bf3b-4716-bd5a-eca74fc5a61d
ms.openlocfilehash: 2b259f315e0186c13ca44c5eed50d861bce3668a
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421333"
---
# <a name="state-machine-workflows"></a>ステート マシン ワークフロー
ステート マシンは、プログラムの開発に関する、よく知られたパラダイムの 1 つです。 <xref:System.Activities.Statements.StateMachine> アクティビティを、<xref:System.Activities.Statements.State>、<xref:System.Activities.Statements.Transition> および他のアクティビティと共に使用することで、ステート マシン ワークフロー プログラムをビルドできます。 このトピックでは、ステート マシン ワークフローの概要について説明します。  
  
## <a name="state-machine-workflow-overview"></a>ステート マシン ワークフローの概要  
 ステート マシン ワークフローで使用するモデル化スタイルでは、ワークフローをイベント ドリブン型にモデル化します。 <xref:System.Activities.Statements.StateMachine> アクティビティは、ステート マシンのロジックを構成する状態および遷移を含んでおり、何かのアクティビティを使用する任意の場所で使用できます。 ステート マシン ランタイムには、次に示すいくつかのクラスがあります。  
  
- <xref:System.Activities.Statements.StateMachine>  
  
- <xref:System.Activities.Statements.State>  
  
- <xref:System.Activities.Statements.Transition>  
  
 ステートマシンワークフローを作成するために、状態はアクティビティに追加され、 <xref:System.Activities.Statements.StateMachine> 遷移は状態間のフローを制御するために使用されます。 次のスクリーンショットでは、[はじめにチュートリアル](getting-started-tutorial.md)の手順[「方法: ステートマシンワークフローを作成](how-to-create-a-state-machine-workflow.md)する」では、3つの状態と3つの遷移を持つステートマシンワークフローを示します。 **Initialize ターゲット**は初期状態であり、ワークフローの最初の状態を表します。 これは、**開始**ノードからこの行に到達する行によって指定されます。 ワークフローの最終状態は**Finalstate**という名前で、ワークフローが完了した時点を表します。  
  
 ![完成したステートマシンのワークフローを示す図。](./media/state-machine-workflows/complete-state-machine-workflow.jpg)  
  
 ステート マシン ワークフローには、初期状態が 1 つのみ、および最終状態が少なくとも 1 つ必要です。 最終状態以外の各状態には、遷移が少なくとも 1 つ必要です。 以降のセクションでは、状態および遷移の作成と構成について説明します。  
  
## <a name="creating-and-configuring-states"></a>状態の作成および構成  
 <xref:System.Activities.Statements.State> はステート マシンの状態を表します。 をワークフローに追加するには、[ <xref:System.Activities.Statements.State> **ツールボックス**] の [**ステートマシン**] セクションから**state**アクティビティデザイナーをドラッグして、 <xref:System.Activities.Statements.StateMachine> Windows ワークフローデザイナー画面のアクティビティにドロップします。  
  
 ![ツールボックスの [ステートマシン] セクションのスクリーンショット。](./media/state-machine-workflows/state-machine-section-toolbox.jpg)  
  
 **初期状態**として状態を構成するには、状態を右クリックし、[**初期状態として設定**] を選択します。 また、現在の初期状態がない場合は、ワークフローの最上部にある [**開始**] ノードから目的の状態に行をドラッグして初期状態を指定できます。 <xref:System.Activities.Statements.StateMachine>アクティビティがワークフローデザイナーにドロップされると、 **State1**という名前の初期状態で事前構成されます。 ステート マシン ワークフローには初期状態が 1 つのみ必要です。  
  
 ステート マシンを終了させる状態を表す状態は、最終状態と呼ばれます。 最終状態とは、<xref:System.Activities.Statements.State.IsFinal%2A> プロパティが `true` に設定され、<xref:System.Activities.Statements.State.Exit%2A> のアクティビティを持たず、そこから発生する遷移がない状態です。 ワークフローに最終状態を追加するには、[**ツールボックス**] の [**ステートマシン**] セクションから**finalstate**アクティビティデザイナーをドラッグし、 <xref:System.Activities.Statements.StateMachine> Windows ワークフローデザイナー画面のアクティビティにドロップします。 ステート マシン ワークフローには最終ステートが少なくとも 1 つ必要です。  
  
### <a name="configuring-entry-and-exit-actions"></a>エントリおよび終了アクションの構成  
 状態には、<xref:System.Activities.Statements.State.Entry%2A> アクションおよび <xref:System.Activities.Statements.State.Exit%2A> アクションを設定できます (最終状態として構成された状態にはエントリ アクションを 1 つのみ設定できます)。 ワークフロー インスタンスが、ある状態に入ると、エントリ アクションのあらゆるアクティビティが実行されます。 エントリアクションが完了すると、状態の遷移のトリガーがスケジュールされます。 別のステートへの遷移が確認されると、状態遷移が同じ状態に戻ったとしても、終了アクションのアクティビティが実行されます。 終了操作が完了すると、遷移のアクションのアクティビティが実行され、新しい状態がに遷移し、そのエントリアクションがスケジュールされます。  
  
> [!NOTE]
> ステート マシン ワークフローをデバッグするときは、ステート マシン ワークフロー内のルート ステート マシンのアクティビティおよび状態にブレークポイントを設定できます。 ブレークポイントを設定できる対象は、状態内または遷移内の任意のアクティビティです。遷移に対して直接設定することはできません。  
  
## <a name="creating-and-configuring-transitions"></a>遷移の作成および構成  
 すべての状態には少なくとも1つの遷移が必要です。ただし、最終的な状態は遷移を含むことはできません。 遷移は、状態マシン ワークフローに状態を追加した後に追加されます。または、状態をドロップしたときに作成されます。  
  
 を追加 <xref:System.Activities.Statements.State> して1つのステップで遷移を作成するには、[**ツールボックス**] の [ステート**マシン**] セクションから**state**アクティビティをドラッグし、ワークフローデザイナーの別の状態にポイントします。 ドラッグされている <xref:System.Activities.Statements.State> が別の <xref:System.Activities.Statements.State> の上にある場合、もう一方の <xref:System.Activities.Statements.State> の周囲に 4 つの三角形が表示されます。 <xref:System.Activities.Statements.State> を 4 つの三角形のいずれかにドロップすると、ステート マシンに追加され、遷移元の <xref:System.Activities.Statements.State> からドロップされた遷移先の <xref:System.Activities.Statements.State> に遷移が作成されます。 詳細については、「 [Transition アクティビティデザイナー](/visualstudio/workflow-designer/transition-activity-designer)」を参照してください。  
  
 状態の追加後に遷移を作成する方法は 2 つあります。 1 つ目は、ワークフロー デザイナー サーフェスから状態をドラッグして既存の状態の上に置き、ドロップ ポイントのいずれかにドロップする方法です。 これは、前のセクションで説明した方法に似ています。 もう 1 つは、マウス ポインターを目的のソースの状態の上に置き、線を適切な目的の状態にドラッグする方法です。  
  
> [!NOTE]
> ステート マシンの 1 つの状態では、ワークフロー デザイナーを使用して作成された遷移を最大 76 個まで含めることができます。 デザイナー以外で作成されたワークフローの状態の遷移に関する制限は、システム リソースによってのみ制限されます。  
  
 遷移は <xref:System.Activities.Statements.Transition.Trigger%2A>、<xref:System.Activities.Statements.Transition.Condition%2A>、および <xref:System.Activities.Statements.Transition.Action%2A> を持つことができます。 切り替え効果 <xref:System.Activities.Statements.Transition.Trigger%2A> は、遷移のソース状態の <xref:System.Activities.Statements.State.Entry%2A> アクションが完了したときにスケジュールされます。 通常 <xref:System.Activities.Statements.Transition.Trigger%2A> は、ある種のイベント発生を待つアクティビティですが、その他のアクティビティであっても、または何もアクティビティがなくてもかまいません。 <xref:System.Activities.Statements.Transition.Trigger%2A> のアクティビティが完了したら、<xref:System.Activities.Statements.Transition.Condition%2A> がある場合は評価されます。 アクティビティがない場合は <xref:System.Activities.Statements.Transition.Trigger%2A> 、 <xref:System.Activities.Statements.Transition.Condition%2A> が直ちに評価されます。 条件がと評価された場合 `false` 、遷移はキャンセルされ、 <xref:System.Activities.Statements.Transition.Trigger%2A> 状態からのすべての遷移のアクティビティが再スケジュールされます。 現在の遷移と同じソース状態を共有する遷移が他にもある場合、それらの <xref:System.Activities.Statements.Transition.Trigger%2A> アクションはキャンセルされ、再スケジュールされます。 <xref:System.Activities.Statements.Transition.Condition%2A> が `true` である場合、または条件がない場合、ソース状態の <xref:System.Activities.Statements.State.Exit%2A> のアクションが実行され、遷移の <xref:System.Activities.Statements.Transition.Action%2A> が実行されます。 が完了すると、 <xref:System.Activities.Statements.Transition.Action%2A> 制御は**ターゲット**の状態に移ります。  
  
 共通トリガーを共有する遷移は、共有トリガー遷移と呼ばれます。 共有トリガー遷移グループに含まれる遷移は、いずれも同じトリガーを使用しますが、それぞれの <xref:System.Activities.Statements.Transition.Condition%2A> およびアクションは一意です。 遷移に追加のアクションを追加して共有遷移を作成するには、目的の遷移の始点を表す円をクリックし、目的の状態にドラッグします。 新しい遷移では最初の遷移と同じトリガーが共有されますが、その条件とアクションは一意になります。 切り替え効果は、切り替え効果デザイナーの下部にある [**共有トリガー遷移の追加**] をクリックして、[**接続可能な状態**] ボックスから目的のターゲット状態を選択することによっても作成できます。  
  
> [!NOTE]
> 遷移の <xref:System.Activities.Statements.Transition.Condition%2A> が `False` と評価された場合 (またはトリガーを共有する遷移すべての状態が `False` と評価された場合)、遷移は行われず、その状態からのすべての遷移のすべてのトリガーが再スケジュールされます。  
  
 ステートマシンワークフローの作成の詳細については、「[方法: ステートマシンワークフローを作成](how-to-create-a-state-machine-workflow.md)する」、「 [StateMachine アクティビティデザイナー](/visualstudio/workflow-designer/statemachine-activity-designer)」、「[状態アクティビティデザイナー](/visualstudio/workflow-designer/state-activity-designer)」、「 [Finalstate アクティビティデザイナー](/visualstudio/workflow-designer/finalstate-activity-designer)」、および「 [Transition アクティビティデザイナー](/visualstudio/workflow-designer/transition-activity-designer)」を参照してください。  
  
## <a name="state-machine-terminology"></a>ステート マシン用語  
 このセクションでは、このトピック全体で使用しているステート マシン用語の定義を示します。  
  
 州  
 ステート マシンを構成する基本単位。 1 つのステート マシンは、任意の特定の時点において 1 つの状態をとることができます。  
  
 エントリ アクション  
 状態に入るときに実行されるアクティビティです。  
  
 終了アクション  
 状態を終了するときに実行されるアクティビティです。  
  
 移行  
 特定の種類のイベント発生時のステートマシンの完全な応答を表す2つの状態の間の有向リレーションシップ。  
  
 共有遷移  
 1 つ以上の別の遷移と同じソースの状態およびトリガーを共有する遷移。一意の条件とアクションを持ちます。  
  
 トリガー  
 遷移を発生させるトリガー アクティビティです。  
  
 条件  
 `true`遷移を完了するために、トリガーが発生した後にに評価される必要がある制約。  
  
 遷移アクション  
 特定の遷移を実行するときに実行されるアクティビティ。  
  
 条件付き遷移  
 明示的な条件付きの遷移です。  
  
 自己遷移  
 状態からそれ自体に遷移する遷移。  
  
 初期状態  
 ステートマシンの開始点を表す状態。  
  
 最終状態  
 ステートマシンの完了を表す状態。  
  
## <a name="see-also"></a>関連項目

- [方法: ステート マシン ワークフローを作成する](how-to-create-a-state-machine-workflow.md)
- [StateMachine アクティビティ デザイナー](/visualstudio/workflow-designer/statemachine-activity-designer)
- [State アクティビティ デザイナー](/visualstudio/workflow-designer/state-activity-designer)
- [FinalState アクティビティ デザイナー](/visualstudio/workflow-designer/finalstate-activity-designer)
- [Transition アクティビティ デザイナー](/visualstudio/workflow-designer/transition-activity-designer)
