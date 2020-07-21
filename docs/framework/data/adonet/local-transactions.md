---
title: ローカル トランザクション
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
ms.openlocfilehash: 979d51a97245bc9616349679ec8cf05cae8c595a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783711"
---
# <a name="local-transactions"></a>ローカル トランザクション
ADO.NET でのトランザクションは、複数のタスクをバインドして単一の作業単位として実行する場合に使用します。 たとえば、あるアプリケーションが 2 つのタスクを実行するものとします。 まず、注文情報に従ってテーブルが更新されます。 次に、在庫情報を含むテーブルが更新され、注文品の金額が借方記入されます。 いずれかのタスクが失敗すると、両方の更新がロールバックされます。  
  
## <a name="determining-the-transaction-type"></a>トランザクションの種類の判別  
 トランザクションは、単一フェーズであり、データベースによって直接処理される場合、ローカル トランザクションと見なされます。 トランザクション モニターによって調整され、トランザクションの解決にフェール セーフ機構 (2 フェーズのコミットなど) が使用されているトランザクションは、分散トランザクションと見なされます。  
  
 各 .NET Framework データ プロバイダーには、ローカル トランザクションを実行するための独自の `Transaction` オブジェクトがあります。 トランザクションを SQL Server データベースで実行できるようにする場合は、<xref:System.Data.SqlClient> トランザクションを選択します。 Oracle トランザクションの場合は、<xref:System.Data.OracleClient> プロバイダーを使用します。 さらに、トランザクションを必要とする、プロバイダーに依存しないコードを記述するための <xref:System.Data.Common.DbTransaction> クラスもあります。  
  
> [!NOTE]
> トランザクションは、サーバー上で実行するのが最も効率的です。 明示的なトランザクションを広範に使用する SQL Server データベースを操作する場合は、Transact-SQL の BEGIN TRANSACTION ステートメントを使用して、ストアド プロシージャとしてトランザクション処理を記述するとよいでしょう。
  
## <a name="performing-a-transaction-using-a-single-connection"></a>単一の接続を使用したトランザクションの実行  
 ADO.NET では、`Connection` オブジェクトを使用してトランザクションを制御します。 ローカル トランザクションは、`BeginTransaction` メソッドを使用して開始できます。 トランザクションを開始すると、`Transaction` オブジェクトの `Command` プロパティを使用して、そのトランザクションにコマンドを参加させることができます。 次に、トランザクションの内容が成功したか失敗したかに基づいて、データ ソースに対する変更をコミットまたはロールバックします。  
  
> [!NOTE]
> `EnlistDistributedTransaction` メソッドをローカル トランザクションで使用することはできません。  
  
 トランザクションのスコープは、接続に限定されています。 次の例では、`try` ブロック内の 2 つの個別のコマンドで構成される明示的なトランザクションを実行しています。 これらのコマンドでは、SQL Server の AdventureWorks サンプル データベース内の Production.ScrapReason テーブルに対して INSERT ステートメントが実行され、例外がスローされない場合はコミットされます。 `catch` ブロック内のコードは、例外がスローされた場合にトランザクションをロールバックします。 トランザクションが完了する前に中止されるか接続が終了すると、トランザクションは自動的にロールバックされます。  
  
## <a name="example"></a>例  
 トランザクションを実行するには、次の手順に従います。  
  
1. <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> オブジェクトの <xref:System.Data.SqlClient.SqlConnection> メソッドを呼び出して、トランザクションの開始位置をマークします。 <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> メソッドは、トランザクションへの参照を返します。 この参照は、トランザクションに参加する <xref:System.Data.SqlClient.SqlCommand> オブジェクトに割り当てられます。  
  
2. 実行する `Transaction` の <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> プロパティに、<xref:System.Data.SqlClient.SqlCommand> オブジェクトを割り当てます。 アクティブなトランザクションを持つ接続上でコマンドが実行され、`Transaction` オブジェクトの `Transaction` プロパティに `Command` オブジェクトが割り当てられていない場合は、例外がスローされます。  
  
3. 必要なコマンドを実行します。  
  
4. <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> オブジェクトの <xref:System.Data.SqlClient.SqlTransaction> メソッドを呼び出してトランザクションを完了するか、<xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> メソッドを呼び出してトランザクションを終了します。 <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> または <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> メソッドが実行される前に接続が終了または破棄されると、トランザクションはロールバックされます。  
  
 次のコード サンプルでは、Microsoft SQL Server で ADO.NET を使用するトランザクション ロジックを示します。  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [トランザクションとコンカレンシー](transactions-and-concurrency.md)
- [分散トランザクション](distributed-transactions.md)
- [SQL Server と System.Transactions の統合](system-transactions-integration-with-sql-server.md)
- [ADO.NET の概要](ado-net-overview.md)
