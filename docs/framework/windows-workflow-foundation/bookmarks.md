---
title: ブックマーク - WF
ms.date: 03/30/2017
ms.assetid: 9b51a346-09ae-455c-a70a-e2264ddeb9e2
ms.openlocfilehash: c5bd8130ee623599e80014777baf92986c3b6969
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183011"
---
# <a name="bookmarks"></a>ブックマーク
ブックマークは、ワークフローのスレッド上に保持することなく、アクティビティが受動的に入力を待機できるようにする機構です。 アクティビティが働きかけを待機していることを示すときは、ブックマークを作成できます。 これは、現在実行中の (<xref:System.Activities.Bookmark> を作成した) メソッドから返された場合でも、アクティビティの実行が完了していると見なさないことをランタイムに対して示します。  
  
## <a name="bookmark-basics"></a>ブックマークの基本  
 <xref:System.Activities.Bookmark> は、ワークフロー インスタンス内で実行を再開できるポイント (および入力を渡すことができるポイント) を表します。 通常、<xref:System.Activities.Bookmark> には名前が付けられ、外部 (ホストまたは拡張) コードで、関連データを含むブックマークを再開する処理を実行します。 <xref:System.Activities.Bookmark> を再開すると、ワークフロー ランタイムは、作成時に、その <xref:System.Activities.BookmarkCallback> と関連付けられた <xref:System.Activities.Bookmark> のデリゲートをスケジュールします。  
  
## <a name="bookmark-options"></a>ブックマークのオプション  
 <xref:System.Activities.BookmarkOptions> クラスは、作成する <xref:System.Activities.Bookmark> の種類を指定します。 互いに矛盾しない値として、<xref:System.Activities.BookmarkOptions.None>、<xref:System.Activities.BookmarkOptions.MultipleResume>、および <xref:System.Activities.BookmarkOptions.NonBlocking> があります。 1 度のみ再開される想定の <xref:System.Activities.BookmarkOptions.None> を作成する場合、既定では <xref:System.Activities.Bookmark> を使用します。 複数回再開できる <xref:System.Activities.BookmarkOptions.MultipleResume> を作成する場合は、<xref:System.Activities.Bookmark> を使用します。 再開しない <xref:System.Activities.BookmarkOptions.NonBlocking> を作成する場合は、<xref:System.Activities.Bookmark> を使用します。 既定の <xref:System.Activities.BookmarkOptions> を使用して作成されるブックマークとは異なり、<xref:System.Activities.BookmarkOptions.NonBlocking> ブックマークはアクティビティの完了を妨げません。  
  
## <a name="bookmark-resumption"></a>ブックマークの再開  
 ブックマークは、ワークフロー以外のコードから、<xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> オーバーロードのいずれかを使用して再開できます。 この例では、`ReadLine` アクティビティが作成されます。 実行されると、`ReadLine` アクティビティは <xref:System.Activities.Bookmark> を作成し、コールバックを登録してから、<xref:System.Activities.Bookmark> が再開されるのを待機します。 再開されると、`ReadLine` アクティビティは <xref:System.Activities.Bookmark> と一緒に渡されたデータを <xref:System.Activities.Activity%601.Result%2A> 引数に代入します。  
  
```csharp  
public sealed class ReadLine : NativeActivity<string>  
{  
    [RequiredArgument]  
    public  InArgument<string> BookmarkName { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        // Create a Bookmark and wait for it to be resumed.  
        context.CreateBookmark(BookmarkName.Get(context),
            new BookmarkCallback(OnResumeBookmark));  
    }  
  
    // NativeActivity derived activities that do asynchronous operations by calling
    // one of the CreateBookmark overloads defined on System.Activities.NativeActivityContext
    // must override the CanInduceIdle property and return true.  
    protected override bool CanInduceIdle  
    {  
        get { return true; }  
    }  
  
    public void OnResumeBookmark(NativeActivityContext context, Bookmark bookmark, object obj)  
    {  
        // When the Bookmark is resumed, assign its value to  
        // the Result argument.  
        Result.Set(context, (string)obj);  
    }  
}  
```  
  
 次の例では、`ReadLine` アクティビティを使用してユーザー名を収集し、それをコンソール ウィンドウに表示するワークフローを作成します。 ホスト アプリケーションは入力を収集する実際の作業を実行し、<xref:System.Activities.Bookmark> を再開することでワークフローに渡します。  
  
```csharp  
Variable<string> name = new Variable<string>  
{  
    Name = "name"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        name  
    },  
    Activities =  
    {  
        new WriteLine()  
        {  
            Text = "What is your name?"  
        },  
        new ReadLine()  
        {  
            BookmarkName = "UserName",  
            Result = name  
        },  
        new WriteLine()  
        {  
            Text = new InArgument<string>((env) => "Hello, " + name.Get(env))  
        }  
    }  
};  
  
AutoResetEvent syncEvent = new AutoResetEvent(false);  
  
// Create the WorkflowApplication using the desired  
// workflow definition.  
WorkflowApplication wfApp = new WorkflowApplication(wf);  
  
// Handle the desired lifecycle events.  
wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)  
{  
    // Signal the host that the workflow is complete.  
    syncEvent.Set();  
};  
  
// Start the workflow.  
wfApp.Run();  
  
// Collect the user's name and resume the bookmark.  
// Bookmark resumption only occurs when the workflow  
// is idle. If a call to ResumeBookmark is made and the workflow  
// is not idle, ResumeBookmark blocks until the workflow becomes  
// idle before resuming the bookmark.  
wfApp.ResumeBookmark("UserName", Console.ReadLine());  
  
// Wait for Completed to arrive and signal that  
// the workflow is complete.  
syncEvent.WaitOne();  
```  
  
 `ReadLine` アクティビティが実行されると、<xref:System.Activities.Bookmark> という名前の `UserName` が作成され、ブックマークが再開されるのを待機します。 ホストは必要なデータを収集し、<xref:System.Activities.Bookmark> を再開します。 ワークフローが再開されると名前が表示されて、完了します。 ブックマークの再開に関して、同期コードは必要ありません。 <xref:System.Activities.Bookmark> を再開できるのは、ワークフローがアイドルの場合のみです。ワークフローがアイドルではない場合、<xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> を呼び出すと、ワークフローがアイドルになるまでブロックされます。  
  
## <a name="bookmark-resumption-result"></a>ブックマークの再開結果  
 <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> は、ブックマークの再開要求の結果を示す <xref:System.Activities.BookmarkResumptionResult> 列挙値を返します。 戻り値には <xref:System.Activities.BookmarkResumptionResult.Success>、<xref:System.Activities.BookmarkResumptionResult.NotReady>、および <xref:System.Activities.BookmarkResumptionResult.NotFound> があります。 ホストと拡張ではこの値を使用して処理の進め方を決定します。
