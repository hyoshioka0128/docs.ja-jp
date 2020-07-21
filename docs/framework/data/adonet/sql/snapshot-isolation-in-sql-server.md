---
title: SQL Server でのスナップショット分離
description: SQL Server でのスナップショット分離と行バージョン管理の概要を説明します。また、分離レベルでコンカレンシーを管理する方法についても説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.openlocfilehash: 7fa769448dd922925a5eccf4c85bd1840155df68
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286249"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server でのスナップショット分離
スナップショット分離により、OLTP アプリケーションのコンカレンシーが向上しています。  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>スナップショット分離と行バージョン管理について  
 スナップショット分離を有効にしたら、各トランザクションの更新された行のバージョンを保持する必要があります。  SQL Server 2019 より前は、これらのバージョンは **tempdb** に格納されていました。 SQL Server 2019 で導入された新機能の高速データベース復旧 (ADR) では、独自の行バージョンのセットが必要です。  そのため、SQL Server 2019 では、ADR が有効になっていない場合、行バージョンは常に **tempdb** に保持されます。  ADR が有効になっている場合は、スナップショット分離と ADR の両方に関連するすべての行バージョンが、ユーザーが指定したファイル グループ内のユーザー データベースにある ADR の永続的なバージョン ストア (PVS) に保持されます。 一意のトランザクション シーケンス番号が各トランザクションを識別し、これらの一意の番号がそれぞれの行バージョン用に記録されます。 トランザクションは、トランザクションのシーケンス番号の前にシーケンス番号が付いた最新の行バージョンで動作します。 トランザクションの開始後に作成された新しい行バージョンは、トランザクションによって無視されます。  
  
 "スナップショット" という用語は、トランザクション内のすべてのクエリが、トランザクションの開始時点のデータベースの状態に基づいて、データベースの同じバージョン、つまりスナップショットを参照するという事実を表しています。 ロックは、スナップショット トランザクション内の基になるデータ行やデータ ページでは取得されません。スナップショット トランザクションでは、先に開始されてまだ完了していないトランザクションによりブロックされることなく、他のトランザクションを実行できます。 データを変更するトランザクションは、データを読み取るトランザクションをブロックしません。また、データを読み取るトランザクションは、データを書き込むトランザクションをブロックしません。この理由は、通常、これらのトランザクションは SQL Server の既定の READ COMMITTED 分離レベルにあるためです。 また、ブロック不可の動作は、複雑なトランザクションのデッドロックの可能性を大幅に軽減します。  
  
 スナップショット分離では、オプティミスティック同時実行制御モデルが使用されます。 スナップショット トランザクションで、トランザクションの開始後に変更されたデータに対して変更をコミットしようとすると、トランザクションがロールバックされ、エラーが発生します。 これを回避するには、変更するデータにアクセスする SELECT ステートメントに UPDLOCK ヒントを使用します。 詳細については、SQL Server オンラインブックの「ロック ヒント」を参照してください。  
  
 スナップショット分離を有効にするには、トランザクションで使用する前に、ALLOW_SNAPSHOT_ISOLATION ON データベース オプションを設定する必要があります。 これにより、行バージョンを一時データベース (**tempdb**) 内に保存するためのメカニズムがアクティブになります。 Transact-SQL の ALTER DATABASE ステートメントで使用するスナップショット分離を、各データベースで有効にする必要があります。 この点で、スナップショット分離は、構成を必要としない、READ COMMITTED、REPEATABLE READ、SERIALIZABLE、および READ UNCOMMITTED という従来の分離レベルとは異なります。 次のステートメントでは、スナップショット分離をアクティブ化し、既定の READ COMMITTED 動作を SNAPSHOT に置き換えます。  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
 READ_COMMITTED_SNAPSHOT ON オプションを設定すると、既定の READ COMMITTED 分離レベルでバージョン管理された行にアクセスできます。 READ_COMMITTED_SNAPSHOT オプションが OFF に設定されている場合、バージョン管理された行にアクセスするためには、各セッションのスナップショット分離レベルを明示的に設定する必要があります。  
  
## <a name="managing-concurrency-with-isolation-levels"></a>分離レベルによるコンカレンシーの管理  
 Transact-SQL ステートメントを実行する分離レベルは、ロック動作と行バージョン管理動作を決定します。 分離レベルには接続全体のスコープがあり、SET TRANSACTION ISOLATION LEVEL ステートメントを使用して接続に設定すると、接続が閉じられるか別の分離レベルが設定されるまで、有効なままになります。 接続が閉じられ、プールに返されると、最後の SET TRANSACTION ISOLATION LEVEL ステートメントの分離レベルが保持されます。 プールされた接続を再利用する後続の接続では、接続がプールされたときに有効であった分離レベルが使用されます。  
  
 接続内で発行される個々のクエリには、1 つのステートメントまたはトランザクションの分離を変更しても、接続の分離レベルには影響しないロック ヒントを含めることができます。 ストアド プロシージャまたは関数で設定された分離レベルまたはロック ヒントでは、それらを呼び出す接続の分離レベルは変更されず、ストアド プロシージャまたは関数呼び出しの実行中にのみ有効にされます。  
  
 以前のバージョンの SQL Server では、SQL-92 標準に定義されている 4 つの分離レベルがサポートされていました。  
  
- READ UNCOMMITTED は、他のトランザクションによって設定されたロックを無視するため、最も制限の緩い分離レベルです。 READ UNCOMMITTED で実行されているトランザクションは、他のトランザクションによってまだコミットされていない変更されたデータ値を読み取ることができます。これらは "ダーティ" リードと呼ばれます。  
  
- READ COMMITTED は、SQL Server の既定の分離レベルです。 これにより、ステートメントで他のトランザクションによって変更されていてもまだコミットされていないデータ値を読み取ることができないように指定することで、ダーティ リードを防止できます。 その他のトランザクションでは、現在のトランザクション内の個々のステートメントの実行で、引き続きデータの変更、挿入、削除が可能であるため、反復不可能な読み取りや "ファントム" データが発生します。  
  
- REPEATABLE READ は、READ COMMITTED よりも制限の厳しい分離レベルです。 これは READ COMMITTED を含み、加えて現在のトランザクションがコミットされるまで、現在のトランザクションによって読み取られたデータを他のトランザクションが変更または削除できないことを指定します。 読み取りデータに対する共有ロックは、各ステートメントの最後に解放されるのではなく、トランザクションの実行中に保持されるため、コンカレンシーは READ COMMITTED よりも低くなります。  
  
- SERIALIZABLE は、最も限定度の高い分離レベルで、トランザクションが完了するまで全範囲のキーをロックし、そのロックを保持します。 これは REPEATABLE READ を含み、トランザクションが完了するまで、トランザクションによって読み取られた範囲に新しい行を挿入できないという制限を追加します。  
  
 詳細については、「[トランザクションのロックおよび行のバージョン管理ガイド](/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide)」を参照してください。  
  
### <a name="snapshot-isolation-level-extensions"></a>スナップショット分離レベルの拡張機能  
 SQL Server では、SNAPSHOT 分離レベルの導入および READ COMMITTED の追加実装と共に、SQL-92 分離レベルの拡張機能が導入されました。 READ_COMMITTED_SNAPSHOT 分離レベルは、すべてのトランザクションの READ COMMITTED を自動的に置き換えることができます。  
  
- SNAPSHOT 分離は、トランザクション内で読み取られるデータには、他の同時実行トランザクションによる変更が反映されないことを指定します。 このトランザクションでは、トランザクションの開始時に存在していたデータ行のバージョンが使用されます。 データが読み取られるときにロックが設定されないため、SNAPSHOT トランザクションは、他のトランザクションによるデータの書き込みをブロックしません。 データを書き込むトランザクションは、スナップショット トランザクションによるデータの読み取りをブロックしません。 スナップショット分離を使用するには ALLOW_SNAPSHOT_ISOLATION データベース オプションを設定して、それを有効にする必要があります。  
  
- データベースでスナップショット分離が有効になっている場合、READ_COMMITTED_SNAPSHOT データベース オプションによって、既定の READ COMMITTED 分離レベルの動作が決定されます。 READ_COMMITTED_SNAPSHOT ON を明示的に指定しない場合、すべての暗黙のトランザクションに READ COMMITTED が適用されます。 これにより、READ_COMMITTED_SNAPSHOT OFF (既定) を設定する場合と同じ動作が生成されます。 READ_COMMITTED_SNAPSHOT OFF が有効な場合、データベース エンジンでは、共有ロックを使用して既定の分離レベルが適用されます。 READ_COMMITTED_SNAPSHOT データベース オプションが ON に設定されている場合、データベース エンジンは、ロックを使用してデータを保護せずに、既定として行バージョン管理とスナップショット分離を使用します。  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>スナップショット分離と行バージョン管理の機能について  
 SNAPSHOT 分離レベルが有効になっている場合、行が更新されるたびに、SQL Server データベース エンジンは **tempdb** 内の元の行のコピーを保存し、行にトランザクション シーケンス番号を追加します。 次に一連のイベントの発生を示します。  
  
- 新しいトランザクションが開始され、トランザクション シーケンス番号が割り当てられます。  
  
- データベース エンジンは、トランザクション内の行を読み取り、トランザクション シーケンス番号より小さくて、トランザクション シーケンス番号に最も近いシーケンス番号の行バージョンを、**tempdb** から取得します。  
  
- データベース エンジンでは、スナップショット トランザクションが開始されたときにアクティブになっており、コミットされていないトランザクションのトランザクション シーケンス番号の一覧に、トランザクション シーケンス番号が含まれているかどうかがチェックされます。  
  
- トランザクションは、トランザクションの開始時点で最新だった **tempdb** から、行のバージョンを読み取ります。 トランザクションの開始後に挿入された新しい行は、それらのシーケンス番号値がトランザクション シーケンス番号値よりも大きくなるため、確認されません。  
  
- 現在のトランザクションは、トランザクションの開始後に削除された行を確認します。この理由は、トランザクション シーケンス番号より小さいシーケンス番号の値を持つ行バージョンが **tempdb** 内に存在する可能性があるためです。  
  
 スナップショット分離の実質的な効果として、トランザクションでは、基になるテーブルへのロックの適用や配置を行うことなく、すべてのデータがトランザクションの開始時に存在していたものと見なされます。 これにより、競合が発生している状況でパフォーマンスが向上することができます。  
  
 スナップショット トランザクションでは常にオプティミスティック同時実行制御が使用され、他のトランザクションによる行の更新を妨げるようなロックが行われません。 スナップショット トランザクションは、トランザクションの開始後に変更された行への更新をコミットしようとすると、このトランザクションがロールバックし、エラーになります。  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>ADO.NET でのスナップショット分離の使用  
 スナップショット分離は、<xref:System.Data.SqlClient.SqlTransaction> クラスによって ADO.NET 内でサポートされます。 データベースでスナップショット分離が有効になっているが、READ_COMMITTED_SNAPSHOT ON に構成されていない場合、<xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> メソッドの呼び出し時に **IsolationLevel.Snapshot** 列挙値を使って、<xref:System.Data.SqlClient.SqlTransaction> を開始する必要があります。 このコード フラグメントでは、接続が開いている <xref:System.Data.SqlClient.SqlConnection> オブジェクトであることを前提としています。  
  
```vb  
Dim sqlTran As SqlTransaction = _  
  connection.BeginTransaction(IsolationLevel.Snapshot)  
```  
  
```csharp  
SqlTransaction sqlTran =
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>例  
 次の例では、ロックされたデータにアクセスを試みて、さまざまな分離レベルがどのように動作するかを示すものですが、運用環境コードでの使用を意図するものではありません。  
  
 このコードは、SQL Server の **AdventureWorks** サンプル データベースに接続し、**TestSnapshot** というテーブルを作成し、1 行のデータを挿入します。 このコードでは、ALTER DATABASE Transact-SQL ステートメントを使用して、データベースのスナップショット分離を有効にしていますが、READ_COMMITTED_SNAPSHOT オプションは設定せず、既定の READ COMMITTED 分離レベルの動作を有効なままにしています。 次に、このコードでは次のアクションを実行します。  
  
- これは sqlTransaction1 を開始しますが、完了するのではなく、SERIALIZABLE 分離レベルを使用して更新トランザクションを開始します。 これには、テーブルをロックする効果があります。  
  
- 2 つ目の接続を開き、SNAPSHOT 分離レベルを使って 2 つ目のトランザクションを開始し、**TestSnapshot** テーブル内のデータを読み取ります。 スナップショット分離が有効になっているため、このトランザクションでは、sqlTransaction1 が開始される前に存在していたデータを読み取ることができます。  
  
- これは 3 番目の接続を開き、READ COMMITTED 分離レベルを使用してトランザクションを開始し、テーブル内のデータの読み取りを試みます。 この場合、コードはデータを読み取れません。コードは最初のトランザクション内のテーブルに置かれたロックを超えて読み取りを行うことができず、タイムアウトになるためです。REPEATABLE READ 分離レベルと SERIALIZABLE 分離レベルが使用されている場合は、これらの分離レベルも、最初のトランザクション内に置かれたロックを超えて読み取りを行うことができないため、同じ結果になります。  
  
- これは 4 番目の接続を開き、READ UNCOMMITTED 分離レベルを使用してトランザクションを開始し、sqlTransaction1 でコミットされていない値のダーティ リードを実行します。 最初のトランザクションがコミットされていない場合、この値は実際にはデータベースに存在しない可能性があります。  
  
- **TestSnapshot** テーブルを削除し、**AdventureWorks** データベースのスナップショット分離をオフにすることにより、最初のトランザクションをロールバックおよびクリーンアップします。  
  
> [!NOTE]
> 次の例では、接続プールを無効にして、同じ接続文字列を使用します。 接続がプールされている場合、その分離レベルをリセットしても、サーバーの分離レベルはリセットされません。 その結果、プールされている同じ内部接続を使用する後続の接続は、その分離レベルをプールされている接続の分離レベルに設定して開始されます。 接続プールを無効にする代わりに、各接続の分離レベルを明示的に設定することもできます。  
  
 [!code-csharp[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/VB/source.vb#1)]  
  
### <a name="example"></a>例  
 次の例では、データの変更中のスナップショット分離の動作を示しています。 コードは、次のアクションを実行します。  
  
- **AdventureWorks** サンプル データベースに接続し、SNAPSHOT 分離を有効にします。  
  
- **TestSnapshotUpdate** という名前のテーブルを作成し、3 行のサンプル データを挿入します。  
  
- SNAPSHOT 分離を使用して sqlTransaction1 を開始しますが、完了はしません。 トランザクションでは、3 行のデータが選択されます。  
  
- 2 つ目の **SqlConnection** を **AdventureWorks** に対して作成し、sqlTransaction1 内で選択された行のうち 1 行の値を更新する READ COMMITTED 分離レベルを使用して、2 つ目のトランザクションを作成します。  
  
- sqlTransaction2 をコミットします。  
  
- sqlTransaction1 に戻り、sqlTransaction1 がすでにコミットした同じ行を更新しようとします。 エラー 3960 が発生し、sqlTransaction1 が自動的にロールバックされます。 **SqlException.Number** と **SqlException.Message** がコンソール ウィンドウに表示されます。  
  
- クリーンアップ コードを実行して **AdventureWorks** 内のスナップショット分離をオフにし、**TestSnapshotUpdate** テーブルを削除します。  
  
 [!code-csharp[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/VB/source.vb#1)]  
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>スナップショット分離でのロック ヒントの使用  
 前の例では、最初のトランザクションがデータを選択し、このトランザクションが完了する前に 2 つ目のトランザクションがデータを更新しています。その結果、最初のトランザクションが同じ行を更新しようとすると、競合が発生します。 トランザクションの開始時にロック ヒントを指定することで、実行時間の長いスナップショット トランザクションで更新の競合が発生する機会を削減できます。 次の SELECT ステートメントでは、UPDLOCK ヒントを使用して、選択した行をロックします。  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
 UPDLOCK ロック ヒントを使用すると、最初のトランザクションが完了する前に行を更新しようとするすべての行がブロックされます。 これにより、トランザクションの後半で、選択した行が更新されるときに、確実に競合が発生しなくなります。 SQL Server オンラインブックの「ロック ヒント」を参照してください。  
  
 アプリケーションで多くの競合が発生する場合は、スナップショット分離が最適な選択肢にならないことがあります。 ヒントは、本当に必要な場合にのみ使用してください。 アプリケーションは、ロック ヒントに常に依存する操作にならないように設計されている必要があります。  
  
## <a name="see-also"></a>関連項目

- [SQL Server と ADO.NET](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
- [トランザクションのロックおよび行のバージョン管理ガイド](/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide)
