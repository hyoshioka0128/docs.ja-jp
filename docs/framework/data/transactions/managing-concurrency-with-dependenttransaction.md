---
title: DependentTransaction によるコンカレンシーの管理
description: .NET の DependentTransaction クラスを使用することで、非同期タスクなど、トランザクション コンカレンシーを管理します。
ms.date: 03/30/2017
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
ms.openlocfilehash: 9c825c977419718c8b9870b40699c4d3516e8533
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141889"
---
# <a name="managing-concurrency-with-dependenttransaction"></a>DependentTransaction によるコンカレンシーの管理
<xref:System.Transactions.Transaction> オブジェクトは、<xref:System.Transactions.Transaction.DependentClone%2A> メソッドを使用して作成されます。 このオブジェクトの唯一の目的は、他のコード (ワーカー スレッドなど) でトランザクションの処理を実行している間、トランザクションをコミットできないように保証することです。 複製されたトランザクション内の処理が完了してコミットの準備が整うと、<xref:System.Transactions.DependentTransaction.Complete%2A> メソッドを使用して、そのトランザクションの作成者に通知できます。 これにより、データの一貫性と正確性を保持できます。  
  
 <xref:System.Transactions.DependentTransaction> クラスは、非同期タスク間のコンカレンシーの管理にも使用できます。 この場合は、トランザクションに依存している複製が独自のタスクの処理を行う間、親が任意のコードの実行を継続できます。 つまり、依存している複製が完了するまで親の実行がブロックされることはありません。  
  
## <a name="creating-a-dependent-clone"></a>トランザクションに依存している複製の作成  
 依存トランザクションを作成するには、<xref:System.Transactions.Transaction.DependentClone%2A> メソッドを呼び出し、パラメーターとして <xref:System.Transactions.DependentCloneOption> 列挙体を渡します。 このパラメーターは、トランザクションに依存している複製が `Commit` メソッドを呼び出してトランザクションのコミットの準備が整ったことを示す前に、親トランザクションで <xref:System.Transactions.DependentTransaction.Complete%2A> が呼び出された場合のトランザクションの動作を定義します。 このパラメーターで有効な値は次のとおりです。  
  
- <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete> では、親トランザクションがタイムアウトするまで、またはすべての依存トランザクションで完了を示す <xref:System.Transactions.DependentTransaction.Complete%2A> が呼び出されるまで、親トランザクションのコミットプロセスをブロックする、依存トランザクションが作成されます。 これは、依存トランザクションが完了するまで、クライアントが親トランザクションのコミットを望まない場合に役立ちます。 親トランザクションが依存トランザクションより前に処理を完了して <xref:System.Transactions.CommittableTransaction.Commit%2A> を呼び出した場合、すべての依存トランザクションが <xref:System.Transactions.DependentTransaction.Complete%2A> を呼び出すまで、コミット プロセスはブロックされ、そのトランザクションで追加処理を実行し、新しい参加リストを作成できる状態になります。 すべての依存トランザクションの処理が完了し、<xref:System.Transactions.DependentTransaction.Complete%2A> を呼び出すとすぐに、トランザクションのコミット プロセスが開始します。  
  
- 一方、<xref:System.Transactions.DependentCloneOption.RollbackIfNotComplete> では、<xref:System.Transactions.CommittableTransaction.Commit%2A> が呼び出される前に親トランザクションで <xref:System.Transactions.DependentTransaction.Complete%2A> が呼び出された場合、自動的に中止する依存トランザクションが作成されます。 この場合、依存トランザクションで行われたすべての処理は、1 つのトランザクションの有効期間内はそのまま変更されず、その一部でもコミットすることはできません。  
  
 アプリケーションが依存トランザクションでその処理を完了した場合、<xref:System.Transactions.DependentTransaction.Complete%2A> メソッドを 1 回だけ呼び出す必要があります。それ以外の場合は、<xref:System.InvalidOperationException> がスローされます。 この呼び出しを行った後は、トランザクションで追加作業を行わないでください。例外が発生します。  
  
 次のコード例では、依存トランザクションの複製を作成してワーカー スレッドに渡すことにより、2 つの同時実行タスクを管理する依存トランザクションを作成する方法を示しています。  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);
    }  
  
    public void ThreadMethod(object transaction)
    {
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();
             dependentTransaction.Dispose();
        }  
    }  
  
//Client code
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
```  
  
 このクライアント コードは、アンビエント トランザクションの設定も行うトランザクション スコープを作成します。 アンビエント トランザクションをワーカー スレッドに渡さないでください。 その代わりに、現在のトランザクションで <xref:System.Transactions.Transaction.DependentClone%2A> メソッドを呼び出すことにより、現在の (アンビエント) トランザクションを複製し、依存トランザクションをワーカー スレッドに渡す必要があります。  
  
 `ThreadMethod` メソッドは、新しいスレッドで実行されます。 クライアントは新しいスレッドを開始し、`ThreadMethod` パラメーターとして依存トランザクションを渡します。  
  
 依存トランザクションは <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete> により作成されるため、2 番目のスレッド上ですべてのトランザクションの処理が完了し、依存トランザクションで <xref:System.Transactions.DependentTransaction.Complete%2A> が呼び出されるまで、トランザクションがコミットされないことが保証されます。 つまり、新しいスレッドが依存トランザクションで <xref:System.Transactions.DependentTransaction.Complete%2A> を呼び出す前にクライアントのスコープが終了した場合 (`using` ステートメントの最後でトランザクション オブジェクトの破棄を試みた場合)、依存トランザクションで <xref:System.Transactions.DependentTransaction.Complete%2A> が呼び出されるまで、クライアント コードはブロックします。 その後、トランザクションはコミットまたは中止の処理を完了できます。  
  
## <a name="concurrency-issues"></a>コンカレンシーに関する問題  
 コンカレンシーに関して、<xref:System.Transactions.DependentTransaction> クラスを使用する場合に注意が必要な問題がいくつかあります。  
  
- ワーカー スレッドがトランザクションをロールバックし、親がトランザクションのコミットを試みた場合、<xref:System.Transactions.TransactionAbortedException> がスローされます。  
  
- トランザクション内の各ワーカー スレッドについて、トランザクションに依存している複製を新しく作成する必要があります。 同一の依存している複製を複数のスレッドに渡さないでください。その複製に対して <xref:System.Transactions.DependentTransaction.Complete%2A> を呼び出すことができるのは、1 つのスレッドのみであるためです。  
  
- ワーカー スレッドが新しいワーカー スレッドを生成する場合、依存している複製から依存している複製を作成し、それを新しいスレッドに渡してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Transactions.DependentTransaction>
