---
title: ADO.NET の制限事項
ms.date: 12/13/2019
description: 経験する可能性がある ADO.NET の制限事項について説明します。
ms.openlocfilehash: 8664b73071fc859ed30080f549b05e7d6ed020f4
ms.sourcegitcommit: 7088f87e9a7da144266135f4b2397e611cf0a228
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75901261"
---
# <a name="adonet-limitations"></a>ADO.NET の制限事項

Microsoft.Data.Sqlite には、ADO.NET 抽象化の多くが実装されていますが、いくつかの制限事項があります。

## <a name="database-schema-information"></a>データベース スキーマの情報

クエリ結果に関するメタデータは、<xref:Microsoft.Data.Sqlite.SqliteDataReader.GetSchemaTable%2A> メソッドを使用して取得できます。

`DbConnection.GetSchema()` は実装されていません。 この API は適切に定義されていないため、[sqlite_master](https://www.sqlite.org/fileformat.html#storage_of_the_sql_database_schema) テーブルや [table_info](https://www.sqlite.org/pragma.html#pragma_table_info) PRAGMA などの標準 SQLite API を使用して、データベースのメタデータを直接取得することをお勧めします。

詳細については、「[メタデータ](metadata.md)」を参照してください。

## <a name="systemtransactions"></a>System.Transactions

Microsoft.Data.Sqlite では、System.Transactions はまだサポートされていません。 代わりに ADO.NET トランザクションを使用してください。 詳細については、「[トランザクション](transactions.md)」を参照してください。

問題 [#13825](https://github.com/dotnet/efcore/issues/13825) で、System.Transactions がサポートされていないことに関するフィードバックをお送りください。

## <a name="data-adapters"></a>データ アダプター

`DbDataAdapter` は、Microsoft.Data.Sqlite ではまだ実装されていません。 つまり、ADO.NET の `DataSet` と `DataTable` はデータの読み込むのみに使用でき、更新には使用できません。

`DbDataAdapter` の実装に関するフィードバックを送信するには、問題 [#13838](https://github.com/dotnet/efcore/issues/13838) を使用してください。

## <a name="output-parameters"></a>出力パラメーター

SQLite では、出力パラメーターはサポートされません。

## <a name="positional-parameters"></a>位置指定パラメーター

Microsoft.Data.Sqlite では、名前付きの[パラメーター](parameters.md)だけがサポートされます。 位置指定パラメーターはサポートされません。

## <a name="stored-procedures"></a>ストアド プロシージャ

SQLite ではストアド プロシージャはサポートされません。

## <a name="isolation-levels"></a>分離レベル

SQLite トランザクションでは、分離レベル `Chaos` と `Snapshot` はサポートされません。

## <a name="see-also"></a>関連項目

* [非同期の制限事項](async.md)
* [データ型](types.md)
* [トランザクション](transactions.md)
