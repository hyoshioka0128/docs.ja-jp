---
title: データのトレース
ms.date: 03/30/2017
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.openlocfilehash: 2b2a33739619ba09e56d4cc9ce99c51423678918
ms.sourcegitcommit: 19014f9c081ca2ff19652ca12503828db8239d48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980224"
---
# <a name="data-tracing-in-adonet"></a>ADO.NET のデータ追跡

ADO.NET に組み込まれているデータ トレース機能は、SQL Server、Oracle、OLE DB、ODBC 用の .NET データ プロバイダーと、ADO.NET <xref:System.Data.DataSet> および SQL Server ネットワーク プロトコルによりサポートされています。

データ アクセス API 呼び出しのトレースは、次の問題を診断する際に役立ちます。

- クライアント プログラムとデータベース間のスキーマの不一致

- データベースの使用不可またはネットワーク ライブラリの問題

- 誤った SQL がアプリケーションによりハードコーディングまたは生成された

- プログラミング ロジックが不適切

- 複数の ADO.NET コンポーネント間または ADO.NET と独自コンポーネント間の対話に起因する問題

トレースを拡張することにより異なるトレース技術をサポートできます。このため、開発者はアプリケーション スタックのあらゆるレベルで問題をトレースできます。 トレースは ADO.NET のみで使用できる機能ではありませんが、Microsoft プロバイダーでは、汎用トレース機能および instrumentation API を活用しています。

ADO.NET におけるマネージド トレースの設定と構成について詳しくは、[データ アクセスのトレース](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))に関する記事をご覧ください。

## <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>拡張イベント ログの診断情報へのアクセス

.NET Framework Data Provider for SQL Server では、拡張イベント ログのサーバーの接続のリング バッファーやアプリケーションのパフォーマンス情報から、接続の障害などのクライアントのイベントを診断情報と関連付けることを容易にするため、データ アクセスのトレース ([データ アクセスのトレース](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))に関する記事を参照) が更新されました。 拡張イベント ログを表示する方法については、「[イベント セッション データの表示](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh710068(v=sql.110))」を参照してください。

接続操作では、ADO.NET はクライアント接続 ID を送信します。 接続に失敗した場合は、接続リング バッファー ([接続リング バッファーによる SQL Server 2008 での接続トラブルシューティング](https://docs.microsoft.com/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)に関する記事を参照) にアクセスし、`ClientConnectionID` フィールドを見つけて、接続エラーに関する診断情報を取得することができます。 クライアント接続 ID は、エラーが発生した場合にのみリング バッファーに記録されます。 (ログイン前のパケットを送信する前に接続に失敗した場合、クライアント接続 ID は生成されません。)クライアント接続 ID は 16 バイトの GUID です。 拡張イベント セッション内のイベントに `client_connection_id` アクションが追加された場合にも、拡張イベントのターゲット出力のクライアント接続 ID を見つけることができます。 それ以上にクライアントのドライバーの診断について支援が必要な場合は、データ アクセスのトレースを有効にし、接続コマンドを再実行して、データ アクセスのトレースの `ClientConnectionID` フィールドを確認することができます。

`SqlConnection.ClientConnectionID` プロパティを使用して、クライアント接続 ID をプログラムによって取得できます。

`ClientConnectionID` は、正常に接続を確立する <xref:System.Data.SqlClient.SqlConnection> オブジェクトで使用できます。 接続試行が失敗すると、`ClientConnectionID` は `SqlException.ToString` を通じて利用可能になることがあります。

ADO.NET は、スレッド固有のアクティビティ ID も送信します。 TRACK_CAUSALITY オプションが有効な状態でセッションが開始された場合、アクティビティ ID は拡張イベントのセッションでキャプチャされます。 アクティブな接続のパフォーマンスの問題については、クライアントのデータ アクセスのトレース (`ActivityID` フィールド) からアクティビティ ID を取得した後、その拡張イベントの出力のアクティビティ ID を検索できます。 拡張イベントのアクティビティ ID は 16 バイトの GUID (クライアント接続 ID の GUID と同じではありません) であり、4 バイトのシーケンス番号が追加されています。 シーケンス番号は、スレッド内で要求の順序を表し、スレッドのバッチと RPC ステートメントの相対的順序を示します。 `ActivityID` は、現在、データ アクセスのトレースが有効な場合、データ アクセスのトレースの構成のワードの 18 番目のビットが有効にされると、オプションとして SQL のバッチ ステートメントと RPC の要求に送信されるようになっています。

次に示すのは、リング バッファーに格納され、RPC とバッチ操作でクライアントから送信されるアクティビティ ID を記録する拡張イベントのセッションを開始するために Transact-SQL を使用するサンプルです。

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>関連項目

- [.NET Framework のネットワークのトレース](../../network-programming/network-tracing.md)
- [アプリケーションのトレースとインストルメント](../../debug-trace-profile/tracing-and-instrumenting-applications.md)
- [ADO.NET の概要](ado-net-overview.md)
