---
title: FILESTREAM データ
ms.date: 03/30/2017
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.openlocfilehash: 87bed5dd345c240cc00b2c36aa976ec53fe63b93
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794099"
---
# <a name="filestream-data"></a>FILESTREAM データ

FILESTREAM ストレージ属性は、varbinary(max) 列に格納されるバイナリ (BLOB) データに対応しています。 FILESTREAM 以前は、バイナリデータの格納に特別な処理が必要でした。 テキスト ドキュメント、イメージ、ビデオなどの非構造化データはデータベース外に保存されることが多く、そのために管理が困難でした。

> [!NOTE]
> SqlClient を使用して FILESTREAM データを操作するには、.NET Framework 3.5 SP1 以降をインストールする必要があります。

varbinary(max) 列に FILESTREAM 属性を指定すると、SQL Server ではデータはデータベース ファイルではなくローカルの NTFS ファイル システムに保存されます。 データは個別に保存されますが、データベースに保存されている varbinary(max) データの操作をサポートする同じ Transact-SQL ステートメントを使用できます。

## <a name="sqlclient-support-for-filestream"></a>FILESTREAM の SqlClient サポート

.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient>) では、<xref:System.Data.SqlTypes> 名前空間で定義されている <xref:System.Data.SqlTypes.SqlFileStream> クラスを使用して、FILESTREAM のデータの読み取りと書き込みがサポートされています。 `SqlFileStream` は <xref:System.IO.Stream> クラスを継承します。このクラスは、データのストリームへの読み込みと書き込みを行うためのメソッドを提供します。 ストリームからの読み取りでは、データをストリームからバイト配列などのデータ構造に転送します。 書き込みを行うと、データはデータ構造からストリームに転送されます。

### <a name="creating-the-sql-server-table"></a>SQL Server テーブルの作成

次の Transact-SQL ステートメントによって、従業員の名前の付いたテーブルが作成され、データ行が挿入されます。 FILESTREAM ストレージを有効にしたら、このテーブルを以下のコード例と組み合わせて使用できます。 SQL Server オンライン ブックの関連トピックへのリンクは、このトピックの終わりにあります。

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>例:FILESTREAM データの読み取り、上書き、挿入

次のサンプルでは、FILESTREAM からデータを読み取る方法を示します。 このコードでは、ファイルへの論理パスを取得し、`FileAccess` を `Read` に、`FileOptions` を `SequentialScan` に設定します。 次に、コードが SqlFileStream からバッファーにバイトを読み取ります。 次に、バイトがコンソール ウィンドウに書き込まれます。

さらに、このサンプルでは、既存のすべてのデータが上書きされる FILESTREAM にデータを書き込む方法も示しています。 このコードでは、ファイルへの論理パスを取得し、`SqlFileStream` を作成して、`FileAccess` を `Write` に、`FileOptions` を `SequentialScan` に設定します。 1 バイトが `SqlFileStream` に書き込まれ、ファイル内のすべてのデータが置き換えられます。

このサンプルでは、Seek メソッドを使用してファイルの末尾にデータを追加することによって、データを FILESTREAM に書き込む方法も示します。 このコードでは、ファイルへの論理パスを取得し、`SqlFileStream` を作成して、`FileAccess` を `ReadWrite` に、`FileOptions` を `SequentialScan` に設定します。 このコードは、Seek メソッドを使用してファイルの末尾までシークし、既存のファイルに 1 バイトを追加します。

```csharp
using System;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

別のサンプルについては、「[ファイル ストリーム列にバイナリ データをフェッチおよび格納する方法](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str)」を参照してください。

## <a name="resources-in-sql-server-books-online"></a>SQL Server オンライン ブックのリソース

FILESTREAM の詳細なドキュメントは、SQL Server オンライン ブックの次のセクションにあります。

|トピック|説明|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](/sql/relational-databases/blob/filestream-sql-server)|FILESTREAM ストレージを使用するタイミングと、SQL Server データベース エンジンと NTFS ファイル システムを統合する方法について説明します。|
|[FILESTREAM データ用のクライアント アプリケーションの作成](/sql/relational-databases/blob/create-client-applications-for-filestream-data)|FILESTREAM データを操作するための Windows API 関数について説明します。|
|[FILESTREAM と SQL Server のその他の機能](/sql/relational-databases/blob/filestream-compatibility-with-other-sql-server-features)|FILESTREAM データを SQL Server の他の機能と共に使用する際の注意事項、ガイドライン、および制限事項について説明します。|

## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](sql-server-data-types.md)
- [ADO.NET でのデータの取得および変更](../retrieving-and-modifying-data.md)
- [コード アクセス セキュリティと ADO.NET](../code-access-security.md)
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-and-large-value-data.md)
- [ADO.NET の概要](../ado-net-overview.md)
