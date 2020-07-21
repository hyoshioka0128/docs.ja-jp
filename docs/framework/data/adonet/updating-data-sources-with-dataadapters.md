---
title: DataAdapter によるデータ ソースの更新
description: DataAdapter の Update メソッドが、DataSet からの変更を ADO.NET アプリケーションのデータ ソースに反映させて解決する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.openlocfilehash: e2348a3a89aa1c28856bfc21aaa25f2c8327aac7
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286185"
---
# <a name="updating-data-sources-with-dataadapters"></a>DataAdapter によるデータ ソースの更新

`Update` の <xref:System.Data.Common.DataAdapter> メソッドを呼び出して、変更を <xref:System.Data.DataSet> からデータ ソースに反映します。 `Update` メソッドは、`Fill` メソッドと同様に、引数として `DataSet` のインスタンスおよびオプションの <xref:System.Data.DataTable> オブジェクトまたは `DataTable` 名を受け取ります。 `DataSet` のインスタンスは、行われた変更点を格納する `DataSet` です。`DataTable` は、変更点の取得元のテーブルです。 `DataTable` を指定しなかった場合、`DataTable` 内の最初の `DataSet` が使用されます。

`Update` メソッドを呼び出すと、`DataAdapter` は、既に加えられた変更を解析し、適切なコマンド (INSERT、UPDATE、または DELETE) を実行します。 `DataAdapter` は <xref:System.Data.DataRow> へ加えられた変更を検出すると、<xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>、<xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>、または <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> を使用してその変更を処理します。 その結果、デザイン時にコマンド構文を指定し、可能な場合はストアド プロシージャを使用することにより、ADO.NET アプリケーションのパフォーマンスを最適化できます。 コマンドは `Update` を呼び出す前に明示的に設定する必要があります。 `Update` を呼び出し、その更新に関連する適切なコマンドが存在しない場合 (たとえば、削除済みの行に関連する `DeleteCommand` が存在しない場合) は、例外がスローされます。

> [!NOTE]
> SQL Server のストアド プロシージャで、`DataAdapter` を使用してデータを編集または削除する場合、ストアド プロシージャの定義に SET NOCOUNT ON は使用しないでください。 処理された行数がゼロとして返され、`DataAdapter` によってコンカレンシーの競合として解釈されてしまいます。 この場合、<xref:System.Data.DBConcurrencyException> がスローされます。

Command パラメーターを使用して、`DataSet` 内の各変更行に対する SQL ステートメントまたはストアド プロシージャに入力値と出力値を指定できます。 詳しくは、「[DataAdapter パラメーター](dataadapter-parameters.md)」をご覧ください。

> [!NOTE]
> <xref:System.Data.DataTable> の行を Delete することと、行を Remove することの違いを理解することが大切です。 `Remove` メソッドまたは `RemoveAt` メソッドを呼び出した場合、行は直ちに削除されます。 その後、`DataTable` または `DataSet` を `DataAdapter` に渡し、`Update` を呼び出しても、バックエンド データ ソースの対応する行には影響しません。 `Delete` メソッドを使用した場合、行はそのまま `DataTable` 内に維持され、削除対象としてマークされます。 その後、`DataTable` または `DataSet` を `DataAdapter` に渡し、`Update` を呼び出すと、バックエンド データ ソースから対応する行が削除されます。

`DataTable` を単一データベース テーブルに割り当てたり、単一データベースから生成する場合は、<xref:System.Data.Common.DbCommandBuilder> オブジェクトを利用して自動的に `DeleteCommand` の `InsertCommand` オブジェクト、`UpdateCommand` オブジェクト、および `DataAdapter` オブジェクトを生成できます。 詳細については、「[CommandBuilder でのコマンドの生成](generating-commands-with-commandbuilders.md)」を参照してください。

## <a name="using-updatedrowsource-to-map-values-to-a-dataset"></a>UpdatedRowSource を使用した値の DataSet への割り当て

`DataTable` オブジェクトの `DataAdapter` プロパティを使用すると、<xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> の Update メソッドを呼び出した後、データ ソースから返された値を <xref:System.Data.Common.DbCommand> に割り当てる方法を制御できます。 `UpdatedRowSource` プロパティを <xref:System.Data.UpdateRowSource> 列挙型の値の 1 つに設定することで、`DataAdapter` コマンドが返した出力パラメーターを無視するか、`DataSet` 内の変更行に適用するかを制御できます。 最初に返された行 (存在する場合) を、`DataTable` 内の変更行に適用するかどうかを指定することもできます。

`UpdateRowSource` 列挙型のさまざまの値と、それらの値が `DataAdapter` で使用されるコマンドの動作にどのように影響するかを次の表で説明します。

|UpdatedRowSource 列挙型|説明|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|出力パラメーターと返された結果セットの最初の行を `DataSet` 内の変更行に割り当てます。|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|返された結果セットの最初の行のデータだけを `DataSet` 内の変更行に割り当てます。|
|<xref:System.Data.UpdateRowSource.None>|出力パラメーターまたは返された結果セットの行が無視されます。|
|<xref:System.Data.UpdateRowSource.OutputParameters>|出力パラメーターだけを `DataSet` 内の変更行に割り当てます。|

`Update` メソッドは変更点を元のデータ ソースに反映させますが、`DataSet` に最後にデータを格納した後、他のクライアントがデータ ソースのデータを変更した可能性もあります。 `DataSet` を現在のデータで更新するには、`DataAdapter` および `Fill` メソッドを使用します。 新しい行がテーブルに追加され、更新された情報が既存の行に取り込まれます。 `Fill` メソッドは、`DataSet` の行と `SelectCommand` によって返された行の主キーの値を調べて、新しい行が追加されたか、または既存の行が更新されたかを判断します。 `Fill` メソッドは、`DataSet` によって返された結果の行に一致する主キーの値を持つ `SelectCommand` の行を見つけた場合、`SelectCommand` によって返された行の情報で既存の行を更新して、既存の行の <xref:System.Data.DataRow.RowState%2A> を `Unchanged` に設定します。 `SelectCommand` によって返された行の主キーの値が、`DataSet` のどの行の主キーの値にも一致しない場合、`Fill` メソッドは、`RowState` が `Unchanged` の新しい行を追加します。

> [!NOTE]
> `SelectCommand` が OUTER JOIN の結果を返す場合、`DataAdapter` は、生成される `PrimaryKey` に `DataTable` 値を設定しません。 自分で `PrimaryKey` を定義して、重複行が正しく反映されるようにする必要があります。 詳しくは、「[主キーの定義](./dataset-datatable-dataview/defining-primary-keys.md)」をご覧ください。

`Update` メソッド呼び出すときに発生する可能性がある例外を処理するには、行更新エラーが発生したときに `RowUpdated` イベントを使用して応答するか (「[DataAdapter のイベント処理](handling-dataadapter-events.md)」を参照)、または `Update` メソッドを呼び出す前に `DataAdapter.ContinueUpdateOnError` を `true` に設定し、更新が完了した時点で特定の行の `RowError` プロパティに格納されているエラー情報に応答します (「[行エラー情報](./dataset-datatable-dataview/row-error-information.md)」を参照)。

> [!NOTE]
> `DataSet`、`DataTable`、または `DataRow` に対して `AcceptChanges` を呼び出すと、`DataRow` に対するすべての `Original` の値が、`DataRow` に対する `Current` の値で上書きされます。 行を一意に識別するフィールド値が変更された場合は、`AcceptChanges` 呼び出しの後に `Original` 値がデータ ソースの値と一致しなくなります。 `AcceptChanges` は、`DataAdapter` の Update メソッドを呼び出す間に、各行について自動的に呼び出されます。 Update メソッドの呼び出し中に元の値を維持するには、まず `AcceptChangesDuringUpdate` の `DataAdapter` プロパティを false に設定するか、`RowUpdated` イベントのイベント ハンドラーを作成し、その <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> を <xref:System.Data.UpdateStatus.SkipCurrentRow> に設定します。 詳しくは、「[DataSet の内容のマージ](./dataset-datatable-dataview/merging-dataset-contents.md)」および「[DataAdapter のイベント処理](handling-dataadapter-events.md)」をご覧ください。

## <a name="example"></a>例

次の例では、`DataAdapter` の `UpdateCommand` を明示的に設定し、その `Update` メソッドを呼び出すことにより、変更済みの行に対して更新を実行する方法を示します。 UPDATE ステートメントの WHERE 句に指定したパラメーターが `Original` の `SourceColumn` 値を使用するように設定されていることに注意してください。 `Current` 値が既に変更されている可能性、そしてデータ ソースの値と一致していない可能性があるため、この設定は重要です。 `Original` 値は、データ ソースから `DataTable` にデータを取得するために使用された値です。

[!code-csharp[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/VB/source.vb#1)]

## <a name="autoincrement-columns"></a>AutoIncrement 列

データ ソースから取得したテーブルに自動インクリメント列がある場合、自動インクリメント値をストアド プロシージャの出力パラメーターとして取得してそれをテーブルの列に割り当てるか、ストアド プロシージャまたは SQL ステートメントによって返された結果セットの最初の行の自動インクリメント値を取得するか、または `DataSet` の `RowUpdated` イベントを使用して追加の SELECT コマンドを実行することによって、`DataAdapter` の列に値を格納できます。 詳細と例については、「[ID 値および Autonumber 値の取得](retrieving-identity-or-autonumber-values.md)」をご覧ください。

## <a name="ordering-of-inserts-updates-and-deletes"></a>挿入、更新、削除の順序

通常の条件下では、`DataSet` を使用して行う変更の順序をデータ ソースに送信することが重要です。 たとえば、既存の行の主キーの値を更新し、その新しい主キーの値を外部キーとして新しい行を追加する場合、更新は挿入の前に処理する必要があります。

`Select` の `DataTable` メソッドを使用すると、特定の `DataRow` を持つ行だけを参照する `RowState` 配列を返すことができます。 その後で、返された `DataRow` 配列を `Update` の `DataAdapter` メソッドに渡して変更行を処理できます。 更新する行のサブセットを指定することで、挿入、更新、および削除の処理順序を制御できます。

## <a name="example"></a>例

たとえば次のコードでは、テーブルの削除行を最初に処理し、次に更新行、最後に挿入行を処理します。

```vb
Dim table As DataTable = dataSet.Tables("Customers")

' First process deletes.
dataSet.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Deleted))

' Next process updates.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.ModifiedCurrent))

' Finally, process inserts.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Added))
```

```csharp
DataTable table = dataSet.Tables["Customers"];

// First process deletes.
adapter.Update(table.Select(null, null, DataViewRowState.Deleted));

// Next process updates.
adapter.Update(table.Select(null, null,
  DataViewRowState.ModifiedCurrent));

// Finally, process inserts.
adapter.Update(table.Select(null, null, DataViewRowState.Added));
```

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a>DataAdapter を使用したデータの取得と更新

DataAdapter を使用すると、データを取得および更新できます。

- このサンプルでは、DataAdapter.AcceptChangesDuringFill を使用してデータベース内のデータを複製します。 このプロパティが false として設定されている場合、AcceptChanges はテーブルにデータを格納するときに呼び出されず、新しく追加された行が挿入された行として処理されます。 そのため、このサンプルでは、これらの行を使用して、データベースに新しい行を挿入します。

- このサンプルでは、DataAdapter.TableMappings を使用して、ソース テーブルと DataTable 間のマッピングを定義します。

- このサンプルでは、DataAdapter.FillLoadOption を使用して、アダプターが DbDataReader から DataTable にデータを設定する方法を決定します。 DataTable を作成するときに、プロパティを LoadOption.Upsert または LoadOption.PreserveChanges として設定した場合のみ、データベースのデータを現在のバージョンまたは元のバージョンに書き込むことができます。

- このサンプルでは、DbDataAdapter.UpdateBatchSize を使用してバッチ操作を実行することにより、テーブルを更新します。

サンプルをコンパイルして実行する前に、サンプル データベースを作成する必要があります。

```sql
USE [master]
GO

CREATE DATABASE [MySchool]

GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)

SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

このコード サンプルを含む C# プロジェクトと Visual Basic プロジェクトは、[開発者コード サンプル](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=How%20to%20use%20DataAdapter%20to%20retrieve%20and%20update%20data&f%5B1%5D)のページにあります。

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.SqlClient;
using System.Linq;
using CSDataAdapterOperations.Properties;

namespace CSDataAdapterOperations.Properties {
   internal sealed partial class Settings : global::System.Configuration.ApplicationSettingsBase {

      private static Settings defaultInstance = ((Settings)(global::System.Configuration.ApplicationSettingsBase.Synchronized(new Settings())));

      public static Settings Default {
         get {
            return defaultInstance;
         }
      }

      [global::System.Configuration.ApplicationScopedSettingAttribute()]
      [global::System.Configuration.DefaultSettingValueAttribute("Data Source=(local);Initial Catalog=MySchool;Integrated Security=True")]
      public string MySchoolConnectionString {
         get {
            return ((string)(this["MySchoolConnectionString"]));
         }
      }
   }
}

class Program {
   static void Main(string[] args) {
      Settings settings = new Settings();

      // Copy the data from the database.  Get the table Department and Course from the database.
      String selectString = @"SELECT [DepartmentID],[Name],[Budget],[StartDate],[Administrator]
                                     FROM [MySchool].[dbo].[Department];

                                   SELECT [CourseID],@Year as [Year],Max([Title]) as [Title],
                                   Max([Credits]) as [Credits],Max([DepartmentID]) as [DepartmentID]
                                   FROM [MySchool].[dbo].[Course]
                                   Group by [CourseID]";

      DataSet mySchool = new DataSet();

      SqlCommand selectCommand = new SqlCommand(selectString);
      SqlParameter parameter = selectCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2);
      parameter.Value = new Random(DateTime.Now.Millisecond).Next(9999);

      // Use DataTableMapping to map the source tables and the destination tables.
      DataTableMapping[] tableMappings = {new DataTableMapping("Table", "Department"), new DataTableMapping("Table1", "Course")};
      CopyData(mySchool, settings.MySchoolConnectionString, selectCommand, tableMappings);

      Console.WriteLine("The following tables are from the database.");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      // Roll back the changes
      DataTable department = mySchool.Tables["Department"];
      DataTable course = mySchool.Tables["Course"];

      department.Rows[0]["Name"] = "New" + department.Rows[0][1];
      course.Rows[0]["Title"] = "New" + course.Rows[0]["Title"];
      course.Rows[0]["Credits"] = 10;

      Console.WriteLine("After we changed the tables:");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      department.RejectChanges();
      Console.WriteLine("After use the RejectChanges method in Department table to roll back the changes:");
      ShowDataTable(department);

      DataColumn[] primaryColumns = { course.Columns["CourseID"] };
      DataColumn[] resetColumns = { course.Columns["Title"] };
      ResetCourse(course, settings.MySchoolConnectionString, primaryColumns, resetColumns);
      Console.WriteLine("After use the ResetCourse method in Course table to roll back the changes:");
      ShowDataTable(course);

      // Batch update the table.
      String insertString = @"Insert into [MySchool].[dbo].[Course]([CourseID],[Year],[Title],
                                   [Credits],[DepartmentID])
             values (@CourseID,@Year,@Title,@Credits,@DepartmentID)";
      SqlCommand insertCommand = new SqlCommand(insertString);
      insertCommand.Parameters.Add("@CourseID", SqlDbType.NVarChar, 10, "CourseID");
      insertCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2, "Year");
      insertCommand.Parameters.Add("@Title", SqlDbType.NVarChar, 100, "Title");
      insertCommand.Parameters.Add("@Credits", SqlDbType.Int, 4, "Credits");
      insertCommand.Parameters.Add("@DepartmentID", SqlDbType.Int, 4, "DepartmentID");

      const Int32 batchSize = 10;
      BatchInsertUpdate(course, settings.MySchoolConnectionString, insertCommand, batchSize);
   }

   private static void CopyData(DataSet dataSet, String connectionString, SqlCommand selectCommand, DataTableMapping[] tableMappings) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {adapter.TableMappings.AddRange(tableMappings);
            // If set the AcceptChangesDuringFill as the false, AcceptChanges will not be called on a
            // DataRow after it is added to the DataTable during any of the Fill operations.
            adapter.AcceptChangesDuringFill = false;

            adapter.Fill(dataSet);
         }
      }
   }

   // Roll back only one column or several columns data of the Course table by call ResetDataTable method.
   private static void ResetCourse(DataTable table, String connectionString,
       DataColumn[] primaryColumns, DataColumn[] resetColumns) {
      table.PrimaryKey = primaryColumns;

      // Build the query string
      String primaryCols = String.Join(",", primaryColumns.Select(col => col.ColumnName));
      String resetCols = String.Join(",", resetColumns.Select(col => $"Max({col.ColumnName}) as {col.ColumnName}"));

      String selectString = $"Select {primaryCols},{resetCols} from Course Group by {primaryCols}");

      SqlCommand selectCommand = new SqlCommand(selectString);

      ResetDataTable(table, connectionString, selectCommand);
   }

   // RejectChanges will roll back all changes made to the table since it was loaded, or the last time AcceptChanges
   // was called. When you copy from the database, you can lose all the data after calling RejectChanges
   // The ResetDataTable method rolls back one or more columns of data.
   private static void ResetDataTable(DataTable table, String connectionString,
       SqlCommand selectCommand) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {
            // The incoming values for this row will be written to the current version of each
            // column. The original version of each column's data will not be changed.
            adapter.FillLoadOption = LoadOption.Upsert;

            adapter.Fill(table);
         }
      }
   }

   private static void BatchInsertUpdate(DataTable table, String connectionString,
       SqlCommand insertCommand, Int32 batchSize) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         insertCommand.Connection = connection;
         // When setting UpdateBatchSize to a value other than 1, all the commands
         // associated with the SqlDataAdapter have to have their UpdatedRowSource
         // property set to None or OutputParameters. An exception is thrown otherwise.
         insertCommand.UpdatedRowSource = UpdateRowSource.None;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter()) {
            adapter.InsertCommand = insertCommand;
            // Gets or sets the number of rows that are processed in each round-trip to the server.
            // Setting it to 1 disables batch updates, as rows are sent one at a time.
            adapter.UpdateBatchSize = batchSize;

            adapter.Update(table);

            Console.WriteLine("Successfully to update the table.");
         }
      }
   }

   private static void ShowDataTable(DataTable table) {
      foreach (DataColumn col in table.Columns) {
         Console.Write("{0,-14}", col.ColumnName);
      }
      Console.WriteLine("{0,-14}", "RowState");

      foreach (DataRow row in table.Rows) {
         foreach (DataColumn col in table.Columns) {
            if (col.DataType.Equals(typeof(DateTime)))
               Console.Write("{0,-14:d}", row[col]);
            else if (col.DataType.Equals(typeof(Decimal)))
               Console.Write("{0,-14:C}", row[col]);
            else
               Console.Write("{0,-14}", row[col]);
         }
         Console.WriteLine("{0,-14}", row.RowState);
      }
   }
}
```

## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [行の状態とバージョン](./dataset-datatable-dataview/row-states-and-row-versions.md)
- [AcceptChange と RejectChange](./dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)
- [DataSet の内容のマージ](./dataset-datatable-dataview/merging-dataset-contents.md)
- [ID 値および Autonumber 値の取得](retrieving-identity-or-autonumber-values.md)
- [ADO.NET の概要](ado-net-overview.md)
