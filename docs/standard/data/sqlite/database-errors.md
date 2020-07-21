---
title: データベース エラー
ms.date: 12/13/2019
description: データベースのエラーと再試行がライブラリでどのように処理されるかについて説明します。
ms.openlocfilehash: 9a613b6f94a89dc40e627c14f46836be77080035
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450490"
---
# <a name="database-errors"></a>データベース エラー

SQLite エラーが発生すると、<xref:Microsoft.Data.Sqlite.SqliteException> がスローされます。 メッセージは SQLite によって発行されます。 `SqliteErrorCode` と `SqliteExtendedErrorCode` プロパティには、エラーの SQLite [結果コード](https://www.sqlite.org/rescode.html)が含まれています。

エラーが発生する可能性があるのは、Microsoft.Data.Sqlite でネイティブ SQLite ライブラリとの対話が行われているときです。 次の一覧に、エラーが発生する可能性がある一般的なシナリオを示します。

* 接続のオープン。
* トランザクションの開始。
* コマンドの実行。
* <xref:Microsoft.Data.Sqlite.SqliteDataReader.NextResult%2A> の呼び出し

これらのエラーがアプリによってどのように処理されるかを慎重に検討してください。

## <a name="locking-retries-and-timeouts"></a>ロック、再試行、タイムアウト

SQLite では、テーブルとデータベース ファイルのロックは積極的に行われます。 アプリでデータベースへの同時アクセスが有効になっている場合、ビジー状態とロック状態のエラーが発生する可能性があります。 [共有キャッシュ](connection-strings.md#cache) と[先行書き込みログ](async.md)を使用することで、エラーの多くを低減できます。

Microsoft.Data.Sqlite では、ビジー状態またはロック状態のエラーが発生すると、成功するかコマンドがタイムアウトになるまで自動的に再試行されます。

<xref:Microsoft.Data.Sqlite.SqliteCommand.CommandTimeout%2A> を設定すると、コマンドのタイムアウトを延長できます。 既定のタイムアウトは 30 秒です。 値 `0` は、タイムアウトがないことを意味します。

```csharp
// Retry for 60 seconds while locked
command.CommandTimeout = 60;
```

Microsoft.Data.Sqlite では、暗黙的なコマンド オブジェクトの作成が必要になる場合があります。 たとえば、BeginTransaction 中です。 これらのコマンドのタイムアウトを設定するには、<xref:Microsoft.Data.Sqlite.SqliteConnection.DefaultTimeout%2A> を使用します。

```csharp
// Set the default timeout of all commands on this connection
connection.DefaultTimeout = 60;
```

## <a name="see-also"></a>関連項目

* [SQLite エラー コード](https://www.sqlite.org/rescode.html)
* [SQLite でのファイルのロック](https://www.sqlite.org/lockingv3.html)
* [共有キャッシュ モード](https://www.sqlite.org/sharedcache.html)
* [先行書き込みログ](https://www.sqlite.org/wal.html)
