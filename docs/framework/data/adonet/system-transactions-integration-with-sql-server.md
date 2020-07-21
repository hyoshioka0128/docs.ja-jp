---
title: SQL Server と System.Transactions の統合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b555544e-7abb-4814-859b-ab9cdd7d8716
ms.openlocfilehash: 42007dafbdc9f61b9fc0776e0aaa2987551b704a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174239"
---
# <a name="systemtransactions-integration-with-sql-server"></a>SQL Server と System.Transactions の統合
.NET Framework バージョン 2.0 では、<xref:System.Transactions> 名前空間を介してアクセスできるトランザクション フレームワークが導入されました。 このフレームワークでは、ADO.NET を含む .NET Framework に完全に統合された形でトランザクションが公開されます。  
  
 プログラミング上の強化に加えて、<xref:System.Transactions> と ADO.NET の連係により、トランザクション処理が最適化されます。 昇格可能なトランザクションとは、必要に応じて完全な分散トランザクションに自動的に昇格する、軽量の (ローカル) トランザクションです。  
  
 ADO.NET 2.0 以降の <xref:System.Data.SqlClient> では、SQL Server を組み合わせて使用した場合、昇格可能なトランザクションがサポートされます。 昇格可能なトランザクションは、必要な場合以外、分散トランザクションのオーバーヘッドの増加を引き起こすことはありません。 昇格可能なトランザクションは自動的に処理され、開発者による介入は必要ありません。  
  
 昇格可能なトランザクションは、.NET Framework Data Provider for SQL Server (`SqlClient`) を SQL Serverで使用する場合のみ使用可能です。  
  
## <a name="creating-promotable-transactions"></a>昇格可能なトランザクションの作成  
 .NET Framework Provider for SQL Server では昇格可能なトランザクションがサポートされており、.NET Framework の <xref:System.Transactions> 名前空間内のクラスを介して処理されます。 昇格可能なトランザクションでは、必要が生じるまで分散トランザクションの作成を延期することで、分散トランザクションが最適化されます。 必要なリソース マネージャーが 1 つだけである場合は、分散トランザクションは発生しません。  
  
> [!NOTE]
> 部分信頼のシナリオで分散トランザクションに昇格するには、 <xref:System.Transactions.DistributedTransactionPermission> が必要です。  
  
## <a name="promotable-transaction-scenarios"></a>昇格可能なトランザクションのシナリオ  
 分散トランザクションは一般的にシステム リソースを大量に消費するため、トランザクションでアクセスされるすべてのリソース マネージャーを統合する、Microsoft Distributed Transaction Coordinator (MS DTC) で管理されます。 昇格可能なトランザクションは特殊な形式の <xref:System.Transactions> トランザクションで、単純な SQL Server トランザクションに処理を効果的に委任できます。 <xref:System.Transactions>、 <xref:System.Data.SqlClient>、および SQL Server では、トランザクションの処理に関連する作業が調整され、必要に応じて、トランザクションは完全な分散トランザクションに昇格されます。  
  
 昇格可能なトランザクションを使用する利点は、アクティブな <xref:System.Transactions.TransactionScope> トランザクションによって接続が開かれ、その他の接続が開いていない場合に、完全な分散トランザクションによるオーバーヘッドが生じることなく、トランザクションが軽量なトランザクションとしてコミットされることです。  
  
### <a name="connection-string-keywords"></a>接続文字列キーワード  
 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> プロパティではキーワード `Enlist`がサポートされており、 <xref:System.Data.SqlClient> によってトランザクションのコンテキストが検出され、分散トランザクションに接続が自動的に参加するかどうかが示されます。 `Enlist=true`である場合は、開いているスレッドの現在のトランザクション コンテキストに接続が自動的に参加します。 `Enlist=false`である場合、 `SqlClient` 接続は分散トランザクションとは対話しません。 `Enlist` の既定値は true です。 `Enlist` が接続文字列で指定されていない場合、接続が開いたときに分散トランザクションがあればそれに自動的に参加します。  
  
 参加する `Transaction Binding` トランザクションと接続の関連付けは、 <xref:System.Data.SqlClient.SqlConnection> 接続文字列の `System.Transactions` キーワードによって制御されます。 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.TransactionBinding%2A> の <xref:System.Data.SqlClient.SqlConnectionStringBuilder>プロパティを介して利用することもできます。  
  
 次の表で使用可能な値について説明します。  
  
|キーワード|説明|  
|-------------|-----------------|  
|Implicit Unbind|これが既定値です。 完了時に接続がトランザクションからデタッチされ、自動コミット モードに切り替わります。|  
|Explicit Unbind|トランザクションが閉じられるまで、接続がトランザクションにアタッチされたままになります。 関連付けられているトランザクションがアクティブでない場合や、 <xref:System.Transactions.Transaction.Current%2A>と一致しない場合、接続は失敗します。|  
  
## <a name="using-transactionscope"></a>TransactionScope の使用  
 <xref:System.Transactions.TransactionScope> クラスでは、接続を分散トランザクションに暗黙的に参加させることで、コード ブロックがトランザクションのコード ブロックになります。 <xref:System.Transactions.TransactionScope.Complete%2A> ブロックの末尾では、終了する前に <xref:System.Transactions.TransactionScope> メソッドを呼び出す必要があります。 ブロックを終了すると、 <xref:System.Transactions.TransactionScope.Dispose%2A> メソッドが呼び出されます。 例外がスローされてコードがスコープから外れている場合は、トランザクションがアボートされたと見なされます。  
  
 使用中のブロックを終了したときに `using` オブジェクトで <xref:System.Transactions.TransactionScope.Dispose%2A> が呼び出されるように、 <xref:System.Transactions.TransactionScope> ブロックを使用することをお勧めします。 保留中のトランザクションのコミットまたはロールバックに失敗すると、 <xref:System.Transactions.TransactionScope> の既定のタイムアウトが 1 分であるため、パフォーマンスが大幅に低下する場合があります。 `using` ステートメントを使用しない場合は、すべての処理を `Try` ブロックで実行し、 <xref:System.Transactions.TransactionScope.Dispose%2A> メソッドを `Finally` ブロック内で明示的に呼び出す必要があります。  
  
 <xref:System.Transactions.TransactionScope>内で例外が発生した場合、そのトランザクションは矛盾しているとしてマークされ、破棄されます。 トランザクションは、 <xref:System.Transactions.TransactionScope> が破棄されるとロールバックされます。 例外が発生しない場合は、参加しているトランザクションがコミットされます。  
  
> [!NOTE]
> 既定では、 `TransactionScope` クラスは、 <xref:System.Transactions.Transaction.IsolationLevel%2A> が `Serializable` であるトランザクションを作成します。 使用しているアプリケーションによっては、アプリケーション内での競合を回避するために、分離レベルを低下させる必要がある場合があります。  
  
> [!NOTE]
> データベース リソースを大量に消費するため、分散トランザクション内で実行するのは更新、挿入、削除だけにすることをお勧めします。 Select ステートメントを使用すると、データベース リソースが不必要にロックされることがあり、シナリオによっては選択にトランザクションを使用する必要がある場合があります。 処理済みのその他のリソース マネージャーに関係する場合以外、データベース以外の処理はトランザクションのスコープ外で実行する必要があります。 トランザクションのスコープ内で例外が発生するとトランザクションのコミットが防止されますが、 <xref:System.Transactions.TransactionScope> クラスでは、作成したコードによってトランザクションのスコープ外で行われた変更はロールバックされません。 トランザクションがロールバックされたときに何らかの動作を行うようにする場合は、 <xref:System.Transactions.IEnlistmentNotification> インターフェイスを独自に実装し、トランザクションに明示的に参加する必要があります。  
  
## <a name="example"></a>例  
 <xref:System.Transactions> を使用する場合は、System.Transactions.dll への参照が必要になります。  
  
 次の関数は、 <xref:System.Data.SqlClient.SqlConnection> ブロックでラップされている、異なる 2 つの <xref:System.Transactions.TransactionScope> オブジェクトで表された異なる 2 つの SQL Server インスタンスに対する、昇格可能なトランザクションを作成する方法を示しています。 このコードにより、 <xref:System.Transactions.TransactionScope> ステートメントを持つ `using` ブロックが作成され、最初の接続が開き、 <xref:System.Transactions.TransactionScope>に自動的に参加します。 このトランザクションは、完全な分散トランザクションとしてではなく、最初に軽量のトランザクションとして参加します。 2 つ目の接続は、1 つ目の接続のコマンドで例外がスローされなかった場合にのみ、 <xref:System.Transactions.TransactionScope> に参加します。 2 つ目の接続が開かれると、トランザクションが完全な分散トランザクションに自動的に昇格されます。 <xref:System.Transactions.TransactionScope.Complete%2A> メソッドが呼び出され、例外がスローされなかった場合にのみ、トランザクションがコミットされます。 <xref:System.Transactions.TransactionScope> ブロックの任意の場所で例外がスローされると、 `Complete` が呼び出されず、 <xref:System.Transactions.TransactionScope> ブロックの最後で `using` が破棄されたときに分散トランザクションがロールバックされます。  
  
```csharp  
// This function takes arguments for the 2 connection strings and commands in order  
// to create a transaction involving two SQL Servers. It returns a value > 0 if the  
// transaction committed, 0 if the transaction rolled back. To test this code, you can
// connect to two different databases on the same server by altering the connection string,  
// or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
static public int CreateTransactionScope(  
    string connectString1, string connectString2,  
    string commandText1, string commandText2)  
{  
    // Initialize the return value to zero and create a StringWriter to display results.  
    int returnValue = 0;  
    System.IO.StringWriter writer = new System.IO.StringWriter();  
  
    // Create the TransactionScope in which to execute the commands, guaranteeing  
    // that both commands will commit or roll back as a single unit of work.  
    using (TransactionScope scope = new TransactionScope())  
    {  
        using (SqlConnection connection1 = new SqlConnection(connectString1))  
        {  
            try  
            {  
                // Opening the connection automatically enlists it in the
                // TransactionScope as a lightweight transaction.  
                connection1.Open();  
  
                // Create the SqlCommand object and execute the first command.  
                SqlCommand command1 = new SqlCommand(commandText1, connection1);  
                returnValue = command1.ExecuteNonQuery();  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue);  
  
                // if you get here, this means that command1 succeeded. By nesting  
                // the using block for connection2 inside that of connection1, you  
                // conserve server and network resources by opening connection2
                // only when there is a chance that the transaction can commit.
                using (SqlConnection connection2 = new SqlConnection(connectString2))  
                    try  
                    {  
                        // The transaction is promoted to a full distributed  
                        // transaction when connection2 is opened.  
                        connection2.Open();  
  
                        // Execute the second command in the second database.  
                        returnValue = 0;  
                        SqlCommand command2 = new SqlCommand(commandText2, connection2);  
                        returnValue = command2.ExecuteNonQuery();  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue);  
                    }  
                    catch (Exception ex)  
                    {  
                        // Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue);  
                        writer.WriteLine("Exception Message2: {0}", ex.Message);  
                    }  
            }  
            catch (Exception ex)  
            {  
                // Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue);  
                writer.WriteLine("Exception Message1: {0}", ex.Message);  
            }  
        }  
  
        // If an exception has been thrown, Complete will not
        // be called and the transaction is rolled back.  
        scope.Complete();  
    }  
  
    // The returnValue is greater than 0 if the transaction committed.  
    if (returnValue > 0)  
    {  
        writer.WriteLine("Transaction was committed.");  
    }  
    else  
    {  
        // You could write additional business logic here, notify the caller by  
        // throwing a TransactionAbortedException, or log the failure.  
        writer.WriteLine("Transaction rolled back.");  
    }  
  
    // Display messages.  
    Console.WriteLine(writer.ToString());  
  
    return returnValue;  
}  
```  
  
```vb  
' This function takes arguments for the 2 connection strings and commands in order  
' to create a transaction involving two SQL Servers. It returns a value > 0 if the  
' transaction committed, 0 if the transaction rolled back. To test this code, you can
' connect to two different databases on the same server by altering the connection string,  
' or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
Public Function CreateTransactionScope( _  
  ByVal connectString1 As String, ByVal connectString2 As String, _  
  ByVal commandText1 As String, ByVal commandText2 As String) As Integer  
  
    ' Initialize the return value to zero and create a StringWriter to display results.  
    Dim returnValue As Integer = 0  
    Dim writer As System.IO.StringWriter = New System.IO.StringWriter  
  
    ' Create the TransactionScope in which to execute the commands, guaranteeing  
    ' that both commands will commit or roll back as a single unit of work.  
    Using scope As New TransactionScope()  
        Using connection1 As New SqlConnection(connectString1)  
            Try  
                ' Opening the connection automatically enlists it in the
                ' TransactionScope as a lightweight transaction.  
                connection1.Open()  
  
                ' Create the SqlCommand object and execute the first command.  
                Dim command1 As SqlCommand = New SqlCommand(commandText1, connection1)  
                returnValue = command1.ExecuteNonQuery()  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue)  
  
                ' If you get here, this means that command1 succeeded. By nesting  
                ' the Using block for connection2 inside that of connection1, you  
                ' conserve server and network resources by opening connection2
                ' only when there is a chance that the transaction can commit.
                Using connection2 As New SqlConnection(connectString2)  
                    Try  
                        ' The transaction is promoted to a full distributed  
                        ' transaction when connection2 is opened.  
                        connection2.Open()  
  
                        ' Execute the second command in the second database.  
                        returnValue = 0  
                        Dim command2 As SqlCommand = New SqlCommand(commandText2, connection2)  
                        returnValue = command2.ExecuteNonQuery()  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue)  
  
                    Catch ex As Exception  
                        ' Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue)  
                        writer.WriteLine("Exception Message2: {0}", ex.Message)  
                    End Try  
                End Using  
  
            Catch ex As Exception  
                ' Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue)  
                writer.WriteLine("Exception Message1: {0}", ex.Message)  
            End Try  
        End Using  
  
        ' If an exception has been thrown, Complete will
        ' not be called and the transaction is rolled back.  
        scope.Complete()  
    End Using  
  
    ' The returnValue is greater than 0 if the transaction committed.  
    If returnValue > 0 Then  
        writer.WriteLine("Transaction was committed.")  
    Else  
        ' You could write additional business logic here, notify the caller by  
        ' throwing a TransactionAbortedException, or log the failure.  
       writer.WriteLine("Transaction rolled back.")  
     End If  
  
    ' Display messages.  
    Console.WriteLine(writer.ToString())  
  
    Return returnValue  
End Function  
```  
  
## <a name="see-also"></a>関連項目

- [トランザクションとコンカレンシー](transactions-and-concurrency.md)
- [ADO.NET の概要](ado-net-overview.md)
