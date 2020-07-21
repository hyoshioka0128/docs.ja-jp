---
title: WorkflowInvoker と WorkflowApplication の使用
description: この記事では、Windows Workflow Foundation で WorkflowInvoker 元と WorkflowApplication を使用したワークフローホスティングについて説明します。
ms.date: 03/30/2017
ms.assetid: cd0e583c-a3f9-4fa2-b247-c7b3368c48a7
ms.openlocfilehash: 50ad291bc73818092e7a08d489d6860636f9c379
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421320"
---
# <a name="using-workflowinvoker-and-workflowapplication"></a>WorkflowInvoker と WorkflowApplication の使用
Windows Workflow Foundation (WF) では、ワークフローをホストする方法がいくつかあります。 <xref:System.Activities.WorkflowInvoker> は、メソッド呼び出しのようにワークフローを呼び出す簡単な方法を提供し、永続化を使用しないワークフローのみに使用できます。 <xref:System.Activities.WorkflowApplication> は、ライフサイクル イベントの通知、実行制御、ブックマークの再開、および永続化を含むワークフローを実行するための豊富なモデルを提供します。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> は、メッセージング アクティビティをサポートし、主にワーク フロー サービスと一緒に使用されます。 このトピックでは、<xref:System.Activities.WorkflowInvoker> と <xref:System.Activities.WorkflowApplication> を使用したワークフロー ホスティングついて説明します。 を使用したワークフローのホストの詳細につい <xref:System.ServiceModel.Activities.WorkflowServiceHost> ては、「[ワークフローサービス](../wcf/feature-details/workflow-services.md)と[ホストワークフローサービスの概要](../wcf/feature-details/hosting-workflow-services-overview.md)」を参照してください。  
  
## <a name="using-workflowinvoker"></a>WorkflowInvoker の使用  
 <xref:System.Activities.WorkflowInvoker> は、メソッドを呼び出すようにワークフローを実行するモデルを提供します。 <xref:System.Activities.WorkflowInvoker> を使用してワークフローを呼び出すには、<xref:System.Activities.WorkflowInvoker.Invoke%2A> メソッドを呼び出し、呼び出すワークフローのワークフロー定義を渡します。 次の例では、<xref:System.Activities.Statements.WriteLine> を使用して <xref:System.Activities.WorkflowInvoker> アクティビティを呼び出します。  
  
 [!code-csharp[CFX_WorkflowInvokerExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#1)]  
  
 <xref:System.Activities.WorkflowInvoker> を使用してワークフローを呼び出すと、呼び出し元のスレッドでワークフローが実行され、ワークフローが完了するまで (アイドル時間を含む) <xref:System.Activities.WorkflowInvoker.Invoke%2A> メソッドがブロックされます。 ワークフローを完了しなければならないタイムアウト期間を構成するには、<xref:System.Activities.WorkflowInvoker.Invoke%2A> パラメーターを受け取る <xref:System.TimeSpan> オーバーロードのいずれかを使用します。 この例では、2 つの異なるタイムアウト期間を使用してワークフローを 2 回呼び出します。 最初のワークフローは完了しますが、2 回目は完了しません。  
  
 [!code-csharp[CFX_WorkflowInvokerExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#50)]  
  
> [!NOTE]
> <xref:System.TimeoutException> がスローされるのは、タイムアウト期間が経過してワークフローが実行中にアイドル状態になった場合だけです。 指定されたタイムアウト時間内には完了しないワークフローが正常に完了するのは、アイドル状態にならない場合です。  
  
 <xref:System.Activities.WorkflowInvoker> も非同期バージョンのメソッド呼び出しを提供します。 詳細については、次のトピックを参照してください。 <xref:System.Activities.WorkflowInvoker.InvokeAsync%2A> および <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A>  
  
### <a name="setting-input-arguments-of-a-workflow"></a>ワークフローの入力引数の設定  
 ワークフローの入力引数にマップされ、引数名によってキー指定されている入力パラメーターの辞書を使用して、データをワークフローに渡すことができます。 次の例では、<xref:System.Activities.Statements.WriteLine> が呼び出され、その <xref:System.Activities.Statements.WriteLine.Text%2A> 引数の値は入力パラメーターの辞書を使用して指定されています。  
  
 [!code-csharp[CFX_WorkflowInvokerExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#3)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>ワークフローの出力引数の取得  
 ワークフローの出力パラメーターは、<xref:System.Activities.WorkflowInvoker.Invoke%2A> の呼び出しから返される出力辞書を使用して取得できます。 次の例は、2 つの入力引数と 2 つの出力引数を持つ 1 つの `Divide` アクティビティで構成されるワークフローを呼び出します。 ワークフローを呼び出すと、`arguments` 辞書が渡されます。ここには引数名でキー指定された各入力引数の値が含まれています。 `Invoke` の呼び出しから制御が戻るときに、同様に引数名でキー指定された各出力引数が、`outputs` 辞書で返されます。  
  
 [!code-csharp[CFX_WorkflowInvokerExample#120](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#120)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#20](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#20)]  
  
 ワークフローが `CodeActivity<TResult>` や `Activity<TResult>` などの <xref:System.Activities.ActivityWithResult> から派生し、適切に定義された <xref:System.Activities.Activity%601.Result%2A> 出力引数以外にも出力引数がある場合は、`Invoke` の非ジェネリック オーバーロードを使用して、追加の引数を取得する必要があります。 これを行うには、`Invoke` に渡されるワークフロー定義は <xref:System.Activities.Activity> 型である必要があります。 この例では、`Divide` アクティビティは `CodeActivity<int>` から派生していますが、<xref:System.Activities.Activity> として宣言されているため、1 つの戻り値ではなく引数の辞書を返す、`Invoke` の非ジェネリック オーバーロードが使用されます。  
  
 [!code-csharp[CFX_WorkflowInvokerExample#121](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#121)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#21)]  
  
## <a name="using-workflowapplication"></a>WorkflowApplication の使用  
 <xref:System.Activities.WorkflowApplication> は、ワークフロー インスタンス管理を実現する豊富な機能を備えています。 <xref:System.Activities.WorkflowApplication> は実際の <xref:System.Activities.Hosting.WorkflowInstance> に対してスレッド セーフなプロキシとして動作し、ランタイムをカプセル化します。また、ワークフロー インスタンスの作成と読み込み、ライフサイクル イベントの一時停止と再開、終了、および通知を行うメソッドを提供します。 <xref:System.Activities.WorkflowApplication> を使用してワークフローを実行するには、<xref:System.Activities.WorkflowApplication> を作成して必要なライフサイクル イベントに定期受信し、ワークフローを開始して、それが終了するまで待機します。 この例では、<xref:System.Activities.Statements.WriteLine> アクティビティから成るワークフロー定義が作成され、そのワークフロー定義を使用して <xref:System.Activities.WorkflowApplication> が作成されます。 ワーク フローが完了したときにホストに通知されるように <xref:System.Activities.WorkflowApplication.Completed%2A> が処理され、<xref:System.Activities.WorkflowApplication.Run%2A> の呼び出しによってワーク フローが開始され、ホストはワークフローが完了するのを待ちます。 次の例に示すように、ワークフローが完了すると <xref:System.Threading.AutoResetEvent> が設定され、ホスト アプリケーションは実行を再開できます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#31](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#31)]  
  
### <a name="workflowapplication-lifecycle-events"></a>WorkflowApplication のライフサイクル イベント  
 <xref:System.Activities.WorkflowApplication.Completed%2A> の他にも、ワークフローがアンロードされたとき (<xref:System.Activities.WorkflowApplication.Unloaded%2A>)、中止されたとき (<xref:System.Activities.WorkflowApplication.Aborted%2A>)、アイドル状態になったとき (<xref:System.Activities.WorkflowApplication.Idle%2A> および <xref:System.Activities.WorkflowApplication.PersistableIdle%2A>)、または未処理の例外が発生したとき (<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>) にホストの作成者に通知されます。 次の例に示すように、ワークフロー アプリケーションの開発者はこれらの通知を処理して適切なアクションを行うことができます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#32](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#32)]  
  
### <a name="setting-input-arguments-of-a-workflow"></a>ワークフローの入力引数の設定  
 <xref:System.Activities.WorkflowInvoker> を使用しているときにデータを渡す方法と同様に、起動時にパラメーターの辞書を使用してデータをワークフローに渡すことができます。 辞書の各項目は、指定されたワークフローの入力引数にマップされます。 次の例では、<xref:System.Activities.Statements.WriteLine> アクティビティから成るワークフローが呼び出され、その <xref:System.Activities.Statements.WriteLine.Text%2A> 引数が入力パラメーターの辞書を使用して指定されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#30](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#30)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>ワークフローの出力引数の取得  
 ワークフローが完了したら、<xref:System.Activities.WorkflowApplicationCompletedEventArgs.Outputs%2A?displayProperty=nameWithType> 辞書にアクセスして、<xref:System.Activities.WorkflowApplication.Completed%2A> ハンドラーの出力引数を取得できます。 次の例では、<xref:System.Activities.WorkflowApplication> を使用してワークフローをホストしています。 <xref:System.Activities.WorkflowApplication>1 つのアクティビティで構成されるワークフロー定義を使用して、インスタンスが構築され `DiceRoll` ます。 `DiceRoll` アクティビティには、サイコロ振り操作の結果を表す 2 つの出力引数があります。 ワークフローが完了すると、この出力が <xref:System.Activities.WorkflowApplication.Completed%2A> ハンドラーで取得されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#130](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#130)]  
  
 [!code-csharp[CFX_WorkflowApplicationExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#21)]  
  
> [!NOTE]
> <xref:System.Activities.WorkflowApplication> と <xref:System.Activities.WorkflowInvoker> は入力引数の辞書を取得し、`out` 引数の辞書を返します。 これらの辞書のパラメーター、プロパティ、および戻り値は `IDictionary<string, object>` 型です。 渡される辞書クラスの実際のインスタンスには、`IDictionary<string, object>` を実装した任意のクラスを使用できます。 これらの例では、`Dictionary<string, object>` が使用されています。 ディクショナリの詳細については、「」および「」を参照してください <xref:System.Collections.Generic.IDictionary%602> <xref:System.Collections.Generic.Dictionary%602> 。  
  
### <a name="passing-data-into-a-running-workflow-using-bookmarks"></a>ブックマークを使用した実行中のワークフローへのデータの受け渡し  
 ブックマークは、アクティビティが再開されるのを受動的に待機するメカニズムです。また、実行中のワークフロー インスタンスにデータを渡すメカニズムでもあります。 次の例に示すように、アクティビティがデータを待機している場合、<xref:System.Activities.Bookmark> を作成し、<xref:System.Activities.Bookmark> が再開されたときに呼び出されるコールバック メソッドを登録します。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
 実行されると、`ReadLine` アクティビティは <xref:System.Activities.Bookmark> を作成し、コールバックを登録してから、<xref:System.Activities.Bookmark> が再開されるのを待機します。 再開されると、`ReadLine` アクティビティは <xref:System.Activities.Bookmark> と一緒に渡されたデータを <xref:System.Activities.Activity%601.Result%2A> 引数に代入します。 次の例では、`ReadLine` アクティビティを使用してユーザー名を収集し、それをコンソール ウィンドウに表示するワークフローを作成します。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#22](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#22)]  
  
 `ReadLine` アクティビティが実行されると、<xref:System.Activities.Bookmark> という名前の `UserName` が作成され、ブックマークが再開されるのを待機します。 ホストは必要なデータを収集し、<xref:System.Activities.Bookmark> を再開します。 ワークフローが再開されると名前が表示されて、完了します。  
  
 ホスト アプリケーションでは、ワークフローを調べて、アクティブなブックマークがあるかどうかを確認できます。 この操作を実行するには、<xref:System.Activities.WorkflowApplication.GetBookmarks%2A> インスタンスの <xref:System.Activities.WorkflowApplication> メソッドを呼び出すか、<xref:System.Activities.WorkflowApplicationIdleEventArgs> ハンドラーの <xref:System.Activities.WorkflowApplication.Idle%2A> を調べます。  
  
 次のコード例は前の例と似ていますが、ブックマークを再開する前にアクティブなブックマークを列挙する点が異なります。 ワークフローが開始され、<xref:System.Activities.Bookmark> が作成されてワークフローがアイドル状態になると、<xref:System.Activities.WorkflowApplication.GetBookmarks%2A> が呼び出されます。 このワークフローが完了すると、次の出力がコンソールに表示されます。  
  
 **お名前は何ですか。**  
**BookmarkName: UserName-OwnerDisplayName: ReadLine** 
**上田** 
**こんにちは、上田さん**

[!code-csharp[CFX_WorkflowApplicationExample#14](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#14)]  
  
 <xref:System.Activities.WorkflowApplicationIdleEventArgs> インスタンスの <xref:System.Activities.WorkflowApplication.Idle%2A> ハンドラーに渡される <xref:System.Activities.WorkflowApplication> を調べるコード サンプルを次に示します。 この例では、アイドル状態になるワークフローに、<xref:System.Activities.Bookmark> という名前で `EnterGuess` というアクティビティによって所有されている 1 つの `ReadInt` があります。 このコード例は、[はじめにチュートリアル](getting-started-tutorial.md)の一部である[ワークフローを実行する方法](how-to-run-a-workflow.md)に基づいています。 この例のコードを含めるようにこの手順の <xref:System.Activities.WorkflowApplication.Idle%2A> ハンドラーを変更すると、次の出力が表示されます。  
  
 **BookmarkName: EnterGuess - OwnerDisplayName: ReadInt**

 [!code-csharp[CFX_WorkflowApplicationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#2)]  
  
## <a name="summary"></a>要約  
 <xref:System.Activities.WorkflowInvoker> はワークフローを呼び出す簡単な方法を提供します。また、ワークフローの開始時にデータを渡し、完了したワークフローからデータを抽出する方法を提供しますが、<xref:System.Activities.WorkflowApplication> を使用できるような複雑なシナリオには使用できません。
