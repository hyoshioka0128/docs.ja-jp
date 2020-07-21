---
title: メタデータ
ms.date: 12/13/2019
description: データベースに関するメタデータを取得する方法について説明します。
ms.openlocfilehash: b2f2704a748627d9943943fa2fa7b1b7e9f3007f
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450430"
---
# <a name="metadata"></a>メタデータ

ADO.NET でメタデータを取得するための API は 2 つあります。 1 つは、クエリ結果に関するメタデータを取得します。 もう 1 つは、データベース スキーマに関するメタデータを取得します。

## <a name="query-result-metadata"></a>クエリ結果のメタデータ

`SqliteDataReader` の <xref:Microsoft.Data.Sqlite.SqliteDataReader.GetSchemaTable%2A> メソッドを使用して、クエリの結果に関するメタデータを取得できます。 返される <xref:System.Data.DataTable> には次の列が含まれます。

| Column             | 種類    | 説明                                                               |
| ------------------ | ------- | ------------------------------------------------------------------------- |
| `AllowDBNull`      | ブール型 | 元の列で NULL が許容される場合は true。                                    |
| `BaseCatalogName`  | String  | 元の列のデータベースの名前。 式では常に NULL です。    |
| `BaseColumnName`   | String  | 元の列の (別名ではない) 名前。 式では常に NULL です。    |
| `BaseSchemaName`   | String  | 常に NULL です。 SQLite ではスキーマはサポートされません。                              |
| `BaseServerName`   | String  | 接続文字列の中で指定されたデータベース ファイルへのパス。         |
| `BaseTableName`    | String  | 元の列のテーブルの名前。 式では常に NULL です。       |
| `ColumnName`       | String  | 結果セット内の列の名前または別名。                        |
| `ColumnOrdinal`    | Int32   | 結果セット内の列の序数。                              |
| `ColumnSize`       | Int32   | 常に -1 です。 これは、将来のバージョンの `Microsoft.Data.Sqlite` では変更される可能性があります。   |
| `DataType`         | 種類    | 列の既定の .NET データ型。                                 |
| `DataTypeName`     | String  | 列の SQLite データ型。                                       |
| `IsAliased`        | ブール型 | 結果セット内で列名に別名を使用する場合は true。                     |
| `IsAutoIncrement`  | ブール型 | 元の列が AUTOINCREMENT キーワードを使用して作成された場合は true。     |
| `IsExpression`     | ブール型 | 列がクエリ内の式から生成される場合は true。            |
| `IsKey`            | ブール型 | 元の列が PRIMARY KEY の一部である場合は true。                     |
| `IsUnique`         | ブール型 | 元の列が UNIQUE の場合は true。                                      |
| `NumericPrecision` | Int16   | 常に NULL です。 これは、将来のバージョンの `Microsoft.Data.Sqlite` では変更される可能性があります。 |
| `NumericScale`     | Int16   | 常に NULL です。 これは、将来のバージョンの `Microsoft.Data.Sqlite` では変更される可能性があります。 |

次の例は、`GetSchemaTable` を使用して、結果に関するメタデータを表示するデバッグ文字列を作成する方法を示しています。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ResultMetadataSample/Program.cs?name=snippet_ResultMetadata)]

たとえば、次のクエリでは、以下のデバッグ文字列が生成されます。

```sql
SELECT id AS post_id,
       title,
       body,
       random() AS random
FROM post
```

```output
post.id AS post_id INTEGER PRIMARY KEY AUTOINCREMENT
post.title TEXT NOT NULL UNIQUE
post.body TEXT
(expression) AS random BLOB
```

## <a name="schema-metadata"></a>スキーマ メタデータ

Microsoft.Data.Sqlite では、DbConnection の GetSchema メソッドは実装していません。 代わりに、[sqlite_master](https://www.sqlite.org/fileformat.html#storage_of_the_sql_database_schema) テーブルと、[table_info](https://www.sqlite.org/pragma.html#pragma_table_info) や [foreign_key_list](https://www.sqlite.org/pragma.html#pragma_foreign_key_list) などの PRAGMA ステートメントを使用して、スキーマ情報のクエリを直接実行できます。

たとえば、次のクエリでは、データベース内のすべての列に関するメタデータが取得されます。

```sql
SELECT t.name AS tbl_name, c.name, c.type, c.notnull, c.dflt_value, c.pk
FROM sqlite_master AS t,
     pragma_table_info(t.name) AS c
WHERE t.type = 'table';
```

## <a name="see-also"></a>関連項目

* [SQL Database スキーマの格納](https://www.sqlite.org/fileformat.html#storage_of_the_sql_database_schema)
* [PRAGMA ステートメント](https://www.sqlite.org/pragma.html)
* [データ型](types.md)
