---
title: 複数のアクティブな結果セットの有効化
description: 接続文字列で MARS を有効または無効にする方法について説明します。MARS は、SQL Server で動作し、複数のバッチを ADO.NET の単一の接続で実行できます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.openlocfilehash: 43bdfebce291c3c1d6c90104c5fef440b295934b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286482"
---
# <a name="enabling-multiple-active-result-sets"></a>複数のアクティブな結果セットの有効化
複数のアクティブな結果セット (MARS : Multiple Active Result Set) は、SQL Server で動作する機能であり、複数のバッチを単一の接続で実行することができます。 SQL Server で使用できるように MARS が有効になっているときは、使用中の各コマンド オブジェクトは接続にセッションを追加します。  
  
> [!NOTE]
> 単一の MARS セッションは、MARS 用に 1 つの論理接続を開いた後、アクティブな各コマンドにつき 1 つの論理接続を開きます。  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>接続文字列で MARS を有効または無効にする  
  
> [!NOTE]
> 次の接続文字列では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 指定されている接続文字列は、データベースが MSSQL1 という名前のサーバーにインストールされているものとします。 実際の環境では必要に応じて接続文字列を変更してください。  
  
 既定では、MARS 機能は無効になっています。 これは、接続文字列に "MultipleActiveResultSets=True" キーワード ペアを追加することによって有効にできます。 "True" は、MARS を有効にするための唯一の有効な値です。 次の例は、SQL Server のインスタンスに接続する方法、および MARS を有効にすることを指定する方法を示しています。  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 MARS は、接続文字列に "MultipleActiveResultSets=False" キーワード ペアを追加することによって無効にできます。 "False" は、MARS を無効にするための唯一の有効な値です。 次の接続文字列では、MARS を無効にしています。  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>MARS の使用に関する特記事項  
 一般に、MARS の有効な接続を使用するために、既存のアプリケーションを修正する必要はありません。 ただし、MARS 機能をご自分のアプリケーションで使用する場合、次の特記事項について理解しておく必要があります。  
  
### <a name="statement-interleaving"></a>ステートメント インタリーブ  
 MARS 操作は、サーバー上で同期して実行されます。 SELECT および BULK INSERT ステートメントのステートメントのインターリーブが許可されます。 ただし、データ操作言語 (DML) およびデータ定義言語 (DDL) ステートメントはアトミックに実行されます。 アトミック バッチの実行中にステートメントを実行しようとすると、すべてブロックされます。 サーバーでの並列実行は MARS 機能ではありません。  
  
 MARS 接続のもとで 2 つのバッチが送信され、そのうちの 1 つに SELECT ステートメントが含まれ、もう一方に DML ステートメントが含まれている場合は、SELECT ステートメントの実行内で DML の実行を開始できます。 ただし、SELECT ステートメントが先に進むには、DML ステートメントが実行を完了する必要があります。 両方のステートメントが同じトランザクションのもとで実行されている場合、SELECT ステートメントが実行を開始した後で DML ステートメントが行ったすべての変更は読み取り操作に表示されません。  
  
 SELECT ステートメント内の WAITFOR ステートメントは、待機中、つまり最初の行が生成されるまではトランザクションを生成しません。 これは、WAITFOR ステートメントが待機している間は、同一の接続内では他のいかなるバッチも実行されないことを意味します。  
  
### <a name="mars-session-cache"></a>MARS セッションのキャッシュ  
 MARS を有効にして接続が開かれている場合、論理セッションが作成されます。このセッションによってオーバーヘッドが増加します。 オーバーヘッドを最小化してパフォーマンスを向上させるため、**SqlClient** は接続内の MARS セッションをキャッシュします。 このキャッシュには、最大で 10 個の MARS セッションが含まれます。 この値をユーザーが調整することはできません。 セッションの制限に達した場合は、新しいセッションが作成され、エラーは生成されません。 キャッシュとそこに含まれているセッションは接続ごとに保持され、接続間では共有されません。 セッションが解放されると、プールの上限に達していない限り、そのセッションはプールに返されます。 キャッシュ プールがいっぱいになると、セッションは閉じられます。 MARS セッションに有効期限はありません。 これらは、接続オブジェクトが破棄された場合にのみクリーンアップされます。 MARS セッションのキャッシュは事前には読み込まれません。 アプリケーションがさらに多くのセッションを要求したときに読み込まれます。  
  
### <a name="thread-safety"></a>スレッド セーフ  
 MARS 操作は、スレッド セーフではありません。  
  
### <a name="connection-pooling"></a>接続プール  
 MARS の有効な接続は、その他の接続と同じようにプールされます。 アプリケーションが 2 つの接続を開き、その一方は MARS が有効で他方は MARS が無効になっている場合、それら 2 つの接続は別々のプールに入れられます。 詳しくは、「[SQL Server の接続プール (ADO.NET)](../sql-server-connection-pooling.md)」をご覧ください。  
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server のバッチ実行環境  
 接続を開くとき、既定の環境が定義されます。 その後、この環境が論理 MARS セッションにコピーされます。  
  
 バッチ実行環境には、次のコンポーネントが含まれています。  
  
- Set オプション (ANSI_NULLS、DATE_FORMAT、LANGUAGE、TEXTSIZE など)  
  
- セキュリティ コンテキスト (ユーザー/アプリケーション ロール)  
  
- データベース コンテキスト (現在のデータベース)  
  
- 実行状態変数 (@@ERROR、@@ROWCOUNT、@@FETCH_STATUS @@IDENTITY など)  
  
- 最上位の一時テーブル  
  
 MARS では、既定の実行環境が接続に関連付けられています。 所定の接続で実行を開始する新しいバッチは、いずれも既定の環境のコピーを受け取ります。 特定のバッチのもとでコードが実行された場合は、常に環境に加えられたすべての変更がその特定のバッチにスコープ指定されます。 実行が完了すると、実行の設定は既定の環境にコピーされます。 単一のバッチが複数のコマンドを発行し、それらが同じトランザクションで連続して実行される場合、そのセマンティクスは、以前のクライアントやサーバーを含む接続で公開されているときのセマンティクスと同じです。  
  
### <a name="parallel-execution"></a>並列実行  
 MARS は、アプリケーション内で複数の接続に対するすべての要件を削除するようには設計されていません。 あるアプリケーションで、サーバーに対するコマンドの真の並列実行が必要な場合は、複数の接続を使用する必要があります。  
  
 たとえば、次のようなシナリオがあるとします。 結果セットを処理するためのコマンド オブジェクトと、データを更新するための別のコマンド オブジェクトの 2 つが作成されます。これらは、MARS 経由で共通の接続を共有します。 最初のコマンド オブジェクトの結果をすべて読み取るまで、`Transaction`.`Commit` による 更新に失敗し、次の例外が発生します。  
  
 メッセージ:トランザクション コンテキストを他のセッションが使用中です。  
  
 ソース: .NET SqlClient Data Provider  
  
 期待される出力: (null)  
  
 受信: System.Data.SqlClient.SqlException  
  
 このシナリオに対応するには、次の 3 つの方法があります。  
  
1. リーダーが作成された後にトランザクションを開始し、それがトランザクションの一部にならないようにします。 それにより、すべての更新が独自のトランザクションになります。  
  
2. リーダーが終了した後ですべての作業をコミットします。 この場合は、大量の更新バッチが生成される可能性があります。  
  
3. MARS を使用せず、代わりに MARS が導入される以前に行っていたように、コマンド オブジェクトごとに別々の接続を使用します。  
  
### <a name="detecting-mars-support"></a>MARS サポートの検出  
 アプリケーションは、`SqlConnection.ServerVersion` の値を読み取って MARS サポートを確認することができます。 SQL Server 2005 のメジャー番号は 9、SQL Server 2008 のメジャー番号は 10 です。  
  
## <a name="see-also"></a>関連項目

- [複数のアクティブな結果セット (MARS)](multiple-active-result-sets-mars.md)
- [ADO.NET の概要](../ado-net-overview.md)
