---
title: CommittableTransaction を使用した明示的なトランザクションの実装
description: .NET で CommittableTransaction を使用した明示的なトランザクションを実装します。 このクラスによって、アプリケーションでトランザクションを使用する明示的な方法が提供されました。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 29efe5e5-897b-46c2-a35f-e599a273acc8
ms.openlocfilehash: 40001422e665a7dda3fb938c8d57860909525404
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141992"
---
# <a name="implementing-an-explicit-transaction-using-committabletransaction"></a>CommittableTransaction を使用した明示的なトランザクションの実装
<xref:System.Transactions.CommittableTransaction> クラスは、<xref:System.Transactions.TransactionScope> クラスが暗黙的に使用されるのと対照的に、アプリケーションがトランザクションを明示的に使用する方法を提供します。 これは、複数の関数呼び出しまたは複数のスレッド呼び出しで同じトランザクションを使用するアプリケーションで役立ちます。 <xref:System.Transactions.TransactionScope> クラスとは異なり、アプリケーション作成者はトランザクションをコミットまたは中止するために、具体的に <xref:System.Transactions.CommittableTransaction.Commit%2A> メソッドまたは <xref:System.Transactions.Transaction.Rollback%2A> メソッドを呼び出す必要があります。  
  
## <a name="overview-of-the-committabletransaction-class"></a>CommittableTransaction クラスの概要  
 <xref:System.Transactions.CommittableTransaction> クラスは、<xref:System.Transactions.Transaction> クラスから派生するため、後者のすべての機能を提供します。 特に有用なのは、<xref:System.Transactions.Transaction.Rollback%2A> クラスの <xref:System.Transactions.Transaction> メソッドで、これは <xref:System.Transactions.CommittableTransaction> オブジェクトのロールバックにも使用できます。  
  
 <xref:System.Transactions.Transaction> クラスは <xref:System.Transactions.CommittableTransaction> クラスに類似していますが、`Commit` メソッドは提供しません。 これにより、トランザクションのコミット時に制御を継続しながら、トランザクション オブジェクト (またはその複製) を他のメソッド (他のスレッド上に存在する可能性もあり) に渡すことができます。 呼び出されたコードでは、トランザクションの参加や処理の選択を行えますが、トランザクションをコミットできるのは <xref:System.Transactions.CommittableTransaction> オブジェクトの作成者のみです。  
  
 <xref:System.Transactions.CommittableTransaction> クラスを使用する場合には、次のことに注意する必要があります。  
  
- <xref:System.Transactions.CommittableTransaction> トランザクションを作成しても、アンビエント トランザクションは設定されません。 リソース マネージャーが必要に応じて正しいトランザクション コンテキストで動作することを保証するには、アンビエント トランザクションを具体的に設定およびリセットする必要があります。 現在のアンビエント トランザクションを設定するには、グローバルな <xref:System.Transactions.Transaction.Current%2A> オブジェクトの静的な <xref:System.Transactions.Transaction> プロパティを設定します。  
  
- <xref:System.Transactions.CommittableTransaction> オブジェクトは再利用できません。 <xref:System.Transactions.CommittableTransaction> オブジェクトがコミットまたはロールバックされると、トランザクションで再び使用することはできません。 つまり、現在のアンビエント トランザクション コンテキストとして設定することはできません。  
  
## <a name="creating-a-committabletransaction"></a>CommittableTransaction の作成  
 新しい <xref:System.Transactions.CommittableTransaction> を作成してコミットする例を次に示します。  
  
 [!code-csharp[Tx_CommittableTx#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_committabletx/cs/committabletxwithsql.cs#1)]
 [!code-vb[Tx_CommittableTx#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_committabletx/vb/committabletxwithsql.vb#1)]  
  
 <xref:System.Transactions.CommittableTransaction> のインスタンスを作成しても、アンビエント トランザクション コンテキストは自動的に設定されません。 したがって、リソース マネージャーに対する操作は、そのトランザクションの一部に含まれません。 アンビエント トランザクションを設定または取得するには、グローバル <xref:System.Transactions.Transaction.Current%2A> オブジェクトの静的な <xref:System.Transactions.Transaction> プロパティを使用します。アプリケーションでは、リソース マネージャーがトランザクションに参加できるようにするために、手動でこのプロパティを設定する必要があります。 古いアンビエント トランザクションを保存し、<xref:System.Transactions.CommittableTransaction> オブジェクトの使用が終了したら復元することをお勧めします。  
  
 トランザクションをコミットするには、<xref:System.Transactions.CommittableTransaction.Commit%2A> メソッドを明示的に呼び出す必要があります。 トランザクションをロールバックするには、<xref:System.Transactions.Transaction.Rollback%2A> メソッドを呼び出す必要があります。 <xref:System.Transactions.CommittableTransaction> がコミットまたはロールバックされるまで、そのトランザクションに関連するすべてのリソースはロックされたままであることに注意してください。  
  
 <xref:System.Transactions.CommittableTransaction> オブジェクトは、複数の関数呼び出しおよびスレッドにわたって使用できます。 ただし、例外を処理し、特に障害発生時に <xref:System.Transactions.Transaction.Rollback%28System.Exception%29> メソッドを呼び出すことはアプリケーション開発者の責任です。  
  
## <a name="asynchronous-commit"></a>非同期コミット  
 <xref:System.Transactions.CommittableTransaction> クラスは、トランザクションを非同期にコミットするための機構も提供します。 トランザクションのコミットは、複数回のデータベース アクセスや潜在的なネットワーク待機時間が含まれる場合、かなりの時間を要することがあります。 高いスループットのアプリケーションでデッドロックを回避するため、非同期コミットを使用してできるだけ早期にトランザクションの処理を完了し、バックグラウンド タスクとしてコミット処理を実行できます。 このために、<xref:System.Transactions.CommittableTransaction.BeginCommit%2A> クラスの <xref:System.Transactions.CommittableTransaction.EndCommit%2A> メソッドおよび <xref:System.Transactions.CommittableTransaction> メソッドを使用できます。  
  
 <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> を呼び出すことで、スレッド プールからのスレッドにコミット ホールドアップをディスパッチできます。 また、<xref:System.Transactions.CommittableTransaction.EndCommit%2A> を呼び出して、トランザクションが実際にコミットされたかどうかを判断することもできます。 なんらかの理由でトランザクションがコミットされなかった場合、<xref:System.Transactions.CommittableTransaction.EndCommit%2A> はトランザクションの例外を発生させます。 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> が呼び出された時点でトランザクションがまだコミットされていない場合、トランザクションがコミットまたは中止されるまで、呼び出し元がブロックされます。  
  
 非同期のコミットを行う最も簡単な方法は、コミットの完了時に呼び出されるコールバック メソッドを提供することです。 ただし、呼び出しを実行するために使用する元の <xref:System.Transactions.CommittableTransaction.EndCommit%2A> オブジェクトに対して <xref:System.Transactions.CommittableTransaction> メソッドを呼び出す必要があります。 そのオブジェクトを取得するには、コールバック メソッドの *IAsyncResult* パラメーターをダウンキャストできます。これは、<xref:System.Transactions.CommittableTransaction> クラスで <xref:System.IAsyncResult> クラスが実装されているためです。  
  
 次の例は、非同期コミットの実行方法を示しています。  
  
```csharp  
public void DoTransactionalWork()  
{  
     Transaction oldAmbient = Transaction.Current;  
     CommittableTransaction committableTransaction = new CommittableTransaction();  
     Transaction.Current = committableTransaction;  
  
     try  
     {  
          /* Perform transactional work here */  
          // No errors - commit transaction asynchronously  
          committableTransaction.BeginCommit(OnCommitted,null);  
     }  
     finally  
     {  
          //Restore the ambient transaction
          Transaction.Current = oldAmbient;  
     }  
}  
void OnCommitted(IAsyncResult asyncResult)  
{  
     CommittableTransaction committableTransaction;  
     committableTransaction = asyncResult as CommittableTransaction;
     Debug.Assert(committableTransaction != null);  
     try  
     {  
          using(committableTransaction)  
          {  
               committableTransaction.EndCommit(asyncResult);  
          }  
     }  
     catch(TransactionException e)  
     {  
          //Handle the failure to commit  
     }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [トランザクション スコープを使用した暗黙的なトランザクションの実装](implementing-an-implicit-transaction-using-transaction-scope.md)
- [トランザクション処理](index.md)
