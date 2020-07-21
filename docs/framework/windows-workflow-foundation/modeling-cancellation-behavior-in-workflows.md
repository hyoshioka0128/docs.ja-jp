---
title: ワークフローでの取り消し動作のモデル化
ms.date: 03/30/2017
ms.assetid: d48f6cf3-cdde-4dd3-8265-a665acf32a03
ms.openlocfilehash: 8738afa838f1d0ca36b7fd6def00f0794bcf47ac
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79143045"
---
# <a name="modeling-cancellation-behavior-in-workflows"></a>ワークフローでの取り消し動作のモデル化
アクティビティは、たとえば <xref:System.Activities.Statements.Parallel> アクティビティを使用して、ワークフロー内部で取り消すことができます。このアクティビティでは、<xref:System.Activities.Statements.Parallel.CompletionCondition%2A> の評価結果が `true` になると、完了していない分岐が取り消されます。また、ホストで <xref:System.Activities.WorkflowApplication.Cancel%2A> を呼び出すと、アクティビティをワークフロー外から取り消すこともできます。 取り消し処理を指定するには、ワークフローの作成者は、<xref:System.Activities.Statements.CancellationScope> アクティビティまたは <xref:System.Activities.Statements.CompensableActivity> アクティビティを使用するか、取り消しロジックを指定するカスタム アクティビティを作成します。 このトピックでは、ワークフローにおける取り消しの概要について説明します。  
  
## <a name="cancellation-compensation-and-transactions"></a>取り消し、補正、およびトランザクション  
 アプリケーションでトランザクションを使用すると、トランザクションのプロセスでエラーが発生した場合、トランザクション内で実行されたすべての変更を中止 (ロールバック) できます。 ただし、長期間にわたって実行される処理やトランザクション リソースを含まない処理など、取り消す (元に戻す) 必要がある処理によってはトランザクションに適さないものもあります。 補正は、ワークフローでエラーが発生した場合に、前に完了した非トランザクションの処理を元に戻すためのモデルを提供します。 取り消しは、完了していない非トランザクションの処理をワークフローやアクティビティの作成者が処理できるようにするためのモデルを提供します。 実行を完了していないアクティビティが取り消された場合、取り消しロジックが指定されていればそのロジックが呼び出されます。  
  
> [!NOTE]
> トランザクションと報酬の詳細については、「[トランザクション](workflow-transactions.md)と[報酬](compensation.md)」を参照してください。  
  
## <a name="using-cancellationscope"></a>CancellationScope の使用  
 <xref:System.Activities.Statements.CancellationScope> アクティビティには、子アクティビティを含めることができる <xref:System.Activities.Statements.CancellationScope.Body%2A> および <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> という 2 つのセクションがあります。 <xref:System.Activities.Statements.CancellationScope.Body%2A> には、アクティビティのロジックを構成するアクティビティを配置し、<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> には、アクティビティの取り消しロジックを指定するアクティビティを配置します。 アクティビティは、完了していない場合にのみ取り消すことができます。 <xref:System.Activities.Statements.CancellationScope> アクティビティの場合は、<xref:System.Activities.Statements.CancellationScope.Body%2A> のアクティビティが完了すると完了したことになります。 取り消し要求がスケジュールされている場合、<xref:System.Activities.Statements.CancellationScope.Body%2A> のアクティビティが完了していなければ、<xref:System.Activities.Statements.CancellationScope> が <xref:System.Activities.ActivityInstanceState.Canceled> とマークされ、<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> アクティビティが実行されます。  
  
### <a name="canceling-a-workflow-from-the-host"></a>ホストからのワークフローの取り消し  
 ホストでワークフローを取り消すには、ワークフローをホストしている <xref:System.Activities.WorkflowApplication.Cancel%2A> インスタンスの <xref:System.Activities.WorkflowApplication> メソッドを呼び出します。 次の例では、<xref:System.Activities.Statements.CancellationScope> を含むワークフローが作成されます。 このワークフローが呼び出され、ホストで <xref:System.Activities.WorkflowApplication.Cancel%2A> が呼び出されます。 ワークフローのメインの実行が停止し、<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> の <xref:System.Activities.Statements.CancellationScope> メソッドが呼び出され、ワークフローがステータス <xref:System.Activities.ActivityInstanceState.Canceled> で完了します。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#35](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#35)]  
  
 このワークフローが呼び出されると、次の出力がコンソールに表示されます。  
  
 **ワークフローを開始します。**  
**キャンセルハンドラーが呼び出されました。**
**ワークフロー b30ebb30-df46-4d90-a211-e31c38d8db3c はキャンセルされました。**
> [!NOTE]
> <xref:System.Activities.Statements.CancellationScope> アクティビティを取り消して <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> を呼び出す場合、適切な取り消しロジックを指定するには、ワークフローの作成者が、アクティビティが取り消されるまでの進行状況を確認する必要があります。 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> からは、取り消されるアクティビティの進行状況に関する情報は提供されません。  
  
 ワークフローのルートの後に未処理の例外がバブルアップされ、<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> ハンドラーから <xref:System.Activities.UnhandledExceptionAction.Cancel> が返された場合も、ホストからワークフローを取り消すことができます。 次の例では、ワークフローの開始後に、ワークフローから <xref:System.ApplicationException> がスローされます。 この例外はワークフローで処理されないため、<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> ハンドラーが呼び出されます。 ハンドラーがランタイムにワークフローを取り消すように指示し、現在実行中の <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> アクティビティの <xref:System.Activities.Statements.CancellationScope> が呼び出されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#36](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#36)]  
  
 このワークフローが呼び出されると、次の出力がコンソールに表示されます。  
  
 **ワークフローを開始します。**  
**ワークフロー 6bb2d5d6-f49a-4c6d-a988-478afb86dbe9**
**アプリケーション例外がスローされました。**
**キャンセルハンドラーが呼び出されました。**
**ワークフロー 6bb2d5d6-f49a-4c6d-a988-478afb86dbe9 キャンセルされました。**
### <a name="canceling-an-activity-from-inside-a-workflow"></a>ワークフロー内部からのアクティビティの取り消し  
 アクティビティは、親から取り消すこともできます。 たとえば、<xref:System.Activities.Statements.Parallel> アクティビティに実行中の分岐が複数ある場合、その <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> の評価結果が `true` になると、完了していない分岐は取り消されます。 次の例では、2 つの分岐がある <xref:System.Activities.Statements.Parallel> アクティビティが作成されます。 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> が `true` に設定されているため、どちらかの分岐が完了した時点で <xref:System.Activities.Statements.Parallel> が完了します。 この例では、分岐 2 が完了するため、分岐 1 が取り消されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#37](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#37)]  
  
 このワークフローが呼び出されると、次の出力がコンソールに表示されます。  
  
 **分岐 1 開始。**  
**ブランチ 2 が完了しました。**
**ブランチ 1 がキャンセルされました。**
**ワークフロー e0685e24-18ef-4a47-acf3-5c638732f3be 完了しました。**  アクティビティは、アクティビティのルートの後に例外がバブルアップされ、その例外がワークフローの上位で処理されていない場合にも取り消されます。 次の例では、ワークフローのメイン ロジックが <xref:System.Activities.Statements.Sequence> アクティビティで構成されています。 <xref:System.Activities.Statements.Sequence> は、<xref:System.Activities.Statements.CancellationScope.Body%2A> アクティビティに含まれる <xref:System.Activities.Statements.CancellationScope> アクティビティの <xref:System.Activities.Statements.TryCatch> として指定されています。 <xref:System.Activities.Statements.Sequence> の本体から例外がスローされて親の <xref:System.Activities.Statements.TryCatch> アクティビティによって処理され、<xref:System.Activities.Statements.Sequence> が取り消されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#39](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#39)]  
  
 このワークフローが呼び出されると、次の出力がコンソールに表示されます。  
  
 **シーケンスを開始します。**  
**シーケンスがキャンセルされました。**
**例外がキャッチされました。**
**ワークフロー e3c18939-121e-4c43-af1c-ba1ce97ce55 完了しました。**
### <a name="throwing-exceptions-from-a-cancellationhandler"></a>CancellationHandler からの例外のスロー  
 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> の <xref:System.Activities.Statements.CancellationScope> からスローされるすべての例外は、ワークフローにとって致命的なものです。 例外が <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> からエスケープされる可能性がある場合は、<xref:System.Activities.Statements.TryCatch> の <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> を使用して、それらの例外をキャッチして処理するようにしてください。  
  
### <a name="cancellation-using-compensableactivity"></a>CompensableActivity を使用した取り消し  
 <xref:System.Activities.Statements.CancellationScope> アクティビティと同様に、<xref:System.Activities.Statements.CompensableActivity> には <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> があります。 <xref:System.Activities.Statements.CompensableActivity> が取り消されると、その <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> に含まれるアクティビティが呼び出されます。 これは、部分的に完了した補正可能な処理を元に戻す場合に役立ちます。 補償とキャンセルの使用方法<xref:System.Activities.Statements.CompensableActivity>については、[補償](compensation.md)を参照してください。  
  
## <a name="cancellation-using-custom-activities"></a>カスタム アクティビティを使用した取り消し  
 カスタム アクティビティの作成者は、いくつかの方法でカスタム アクティビティに取り消しロジックを実装することができます。 <xref:System.Activities.Activity> から派生するカスタム アクティビティは、<xref:System.Activities.Statements.CancellationScope> またはキャンセル ロジックを含む他のカスタム アクティビティをアクティビティの本体に配置することによって、取り消しロジックを実装できます。 <xref:System.Activities.AsyncCodeActivity> および <xref:System.Activities.NativeActivity> から派生したアクティビティは、それぞれの <xref:System.Activities.NativeActivity.Cancel%2A> メソッドをオーバーライドして、取り消しロジックを提供できます。 <xref:System.Activities.CodeActivity> 派生アクティビティでは取り消しの処置を行うことはできません。ランタイムが <xref:System.Activities.CodeActivity.Execute%2A> メソッドを呼び出すと、すべての作業が一度に実行されるためです。 実行メソッドが呼び出される前に <xref:System.Activities.CodeActivity> ベースのアクティビティを取り消した場合、アクティビティはステータス <xref:System.Activities.ActivityInstanceState.Canceled> で終了し、<xref:System.Activities.CodeActivity.Execute%2A> メソッドは呼び出されません。  
  
### <a name="cancellation-using-nativeactivity"></a>NativeActivity を使用した取り消し  
 <xref:System.Activities.NativeActivity> 派生アクティビティでは、<xref:System.Activities.NativeActivity.Cancel%2A> メソッドをオーバーライドしてカスタムの取り消しロジックを指定できます。 このメソッドがオーバーライドされていない場合は、既定のワークフロー取り消しロジックが適用されます。 既定の取り消しは、メソッドを<xref:System.Activities.NativeActivity>オーバーライドしない場合、または<xref:System.Activities.NativeActivity.Cancel%2A>メソッドが基本<xref:System.Activities.NativeActivity.Cancel%2A><xref:System.Activities.NativeActivity><xref:System.Activities.NativeActivity.Cancel%2A>メソッドを呼び出すプロセスです。 アクティビティが取り消されると、ランタイムは、取り消し対象のフラグをアクティビティに設定し、特定のクリーンアップ処理を自動的に実行します。 アクティビティに未処理のブックマークしかない場合、それらのブックマークが削除され、アクティビティが <xref:System.Activities.ActivityInstanceState.Canceled> とマークされます。 取り消されるアクティビティに未処理の子アクティビティがある場合は、それらも取り消されます。 子アクティビティを追加でスケジュールしようとすると無視され、アクティビティは <xref:System.Activities.ActivityInstanceState.Canceled> とマークされます。 未処理の子アクティビティが <xref:System.Activities.ActivityInstanceState.Canceled> または <xref:System.Activities.ActivityInstanceState.Faulted> の状態で完了した場合、アクティビティは <xref:System.Activities.ActivityInstanceState.Canceled> とマークされます。 取り消し要求は無視される場合があることに注意してください。 アクティビティに未処理のブックマークも実行中の子アクティビティもなく、取り消し対象のフラグが設定された後に追加の作業項目のスケジュールも行っていない場合は、アクティビティが正常に完了します。 ほとんどの場合はこの既定の取り消しで十分ですが、別の取り消しロジックが必要な場合は、組み込みの取り消しアクティビティやカスタム アクティビティを使用できます。  
  
 次の例では、<xref:System.Activities.NativeActivity.Cancel%2A> ベースのカスタム <xref:System.Activities.NativeActivity> アクティビティの `ParallelForEach` オーバーライドが定義されます。 アクティビティが取り消されると、このオーバーライドによってアクティビティの取り消しロジックが処理されます。 この例は、[非ジェネリック ParallelForEach](./samples/non-generic-parallelforeach.md)サンプルの一部です。  
  
```csharp  
protected override void Cancel(NativeActivityContext context)  
{  
    // If we do not have a completion condition then we can just  
    // use default logic.  
    if (this.CompletionCondition == null)  
    {  
        base.Cancel(context);  
    }  
    else  
    {  
        context.CancelChildren();  
    }  
}  
```  
  
 <xref:System.Activities.NativeActivity> 派生アクティビティでは、<xref:System.Activities.NativeActivityContext.IsCancellationRequested%2A> プロパティを調べることによって取り消しが要求されたかどうかを確認し、<xref:System.Activities.NativeActivityContext.MarkCanceled%2A> メソッドを呼び出して取り消し対象としてマークできます。 <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> を呼び出した後、すぐにアクティビティが完了するわけではありません。 ランタイムは通常どおり、未処理の処理がなくなってからアクティビティを完了します。ただし、<xref:System.Activities.NativeActivityContext.MarkCanceled%2A> が呼び出された場合は、最終的な状態が <xref:System.Activities.ActivityInstanceState.Canceled> ではなく <xref:System.Activities.ActivityInstanceState.Closed> になります。  
  
### <a name="cancellation-using-asynccodeactivity"></a>AsyncCodeActivity を使用した取り消し  
 <xref:System.Activities.AsyncCodeActivity> ベースのアクティビティでも、<xref:System.Activities.AsyncCodeActivity.Cancel%2A> メソッドをオーバーライドしてカスタムの取り消しロジックを指定できます。 このメソッドがオーバーライドされていない場合は、アクティビティが取り消されても取り消し処理は実行されません。 次の例では、<xref:System.Activities.AsyncCodeActivity.Cancel%2A> ベースのカスタム <xref:System.Activities.AsyncCodeActivity> アクティビティの `ExecutePowerShell` オーバーライドが定義されます。 アクティビティが取り消されると、必要な取り消し動作が実行されます。
  
 [!code-csharp[CFX_WorkflowApplicationExample#1020](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1020)]  
  
 <xref:System.Activities.AsyncCodeActivity> 派生アクティビティでは、<xref:System.Activities.AsyncCodeActivityContext.IsCancellationRequested%2A> プロパティを調べることによって取り消しが要求されたかどうかを確認し、<xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A> メソッドを呼び出して取り消し対象としてマークできます。
