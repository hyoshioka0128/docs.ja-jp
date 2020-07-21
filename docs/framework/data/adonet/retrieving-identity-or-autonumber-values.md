---
title: ID 値および Autonumber 値の取得
description: リレーショナル データベースの主キーの ID 値と Autonumber 値を取得する方法、および ADO.NET で新しい ID 値をマージする方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d6b7f9cb-81be-44e1-bb94-56137954876d
ms.openlocfilehash: dbbc013a5b6c83391a29109beca44120c68d827f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286573"
---
# <a name="retrieving-identity-or-autonumber-values"></a>ID 値および Autonumber 値の取得

リレーショナル データベースの主キーとは、常に一意の値を含んだ列または列の組み合わせをいいます。 主キー値がわかっていれば、それが格納されている行を特定できます。 SQL Server、Oracle、Microsoft Access/Jet などのリレーショナル データベース エンジンは、主キーとして指定可能な自動インクリメント列の作成をサポートしています。 これらの値はテーブルに行を追加するとサーバーによって自動的に生成されます。 SQL Server では列の Identity プロパティを設定し、Oracle では Sequence を作成します。また、Microsoft Access では、AutoNumber 列を作成します。

<xref:System.Data.DataColumn> を使用し、<xref:System.Data.DataColumn.AutoIncrement%2A> プロパティを true に設定することで、インクリメント値を自動的に生成することもできます。 ただし、複数のクライアント アプリケーションがそれぞれ独立して自動インクリメント値を生成した場合、最終的に <xref:System.Data.DataTable> の別々のインスタンスに重複する値が存在することも考えられます。 サーバーで自動的にインクリメント値を生成すると、各ユーザーが、挿入された行ごとに生成された値を取得できるようになるため、競合を未然に防ぐことができます。

ADO.NET アプリケーションでは、`Update` の `DataAdapter` メソッドを呼び出している間、データベースから出力パラメーターとして、または (INSERT ステートメントと同じバッチで実行した) SELECT ステートメントの結果セットの最初に返されたレコードとして、データを取得できます。 これらの値を取得することで、更新対象となる <xref:System.Data.DataRow> 内の対応する列を更新できます。

Microsoft Access Jet データベース エンジンなど、一部のデータベース エンジンは、出力パラメーターをサポートしておらず、複数のステートメントを 1 回のバッチで処理することもできません。 Jet データベース エンジンを使用する場合は、`RowUpdated` の `DataAdapter` イベントのイベント ハンドラーで別途 SELECT コマンドを実行することによって、挿入行に対して生成された新しい AutoNumber 値を取得できます。

> [!NOTE]
> 自動インクリメント値を使用する代わりに、クライアント コンピューター側で <xref:System.Guid.NewGuid%2A> オブジェクトの <xref:System.Guid> メソッドを使用して GUID (グローバルな一意識別子) を生成し、新しい行が挿入されるたびにそれをサーバーにコピーする方法もあります。 `NewGuid` メソッドでは、値の重複を高い確率で防ぐアルゴリズムを使って 16 バイトのバイナリ値が生成されます。 SQL Server データベースでは、Transact-SQL の `uniqueidentifier` 関数を使って自動的に生成される GUID が、`NEWID()` 列に格納されます。 GUID を主キーとして使用すると、パフォーマンスが低下する場合があります。 SQL Server では、シーケンシャルな GUID を生成する `NEWSEQUENTIALID()` 関数がサポートされています。この GUID は、グローバルに一意であることは保証されませんが、より効率的なインデックス処理が可能となります。

## <a name="retrieving-sql-server-identity-column-values"></a>SQL Server の ID 列値の取得

Microsoft SQL Server を使用している場合は、出力パラメーターを持ったストアド プロシージャを作成して、挿入された行の ID 値を取得できます。 次の表は、SQL Server で ID 列値の取得に使用できる 3 つの Transact-SQL 関数を示しています。

|関数|説明|
|--------------|-----------------|
|SCOPE_IDENTITY|現在の実行スコープ内の最後の ID 値を返します。 通常は、SCOPE_IDENTITY を使用することをお勧めします。|
|@@IDENTITY|現在のセッション内の任意のテーブルで生成された最後の ID 値を保持します。 @@IDENTITY はトリガーの影響を受けるため、期待した ID 値が返されない場合があります。|
|IDENT_CURRENT|任意のセッションとスコープ内の特定のテーブルに対して生成された最後の ID 値を返します。|

 次のストアド プロシージャでは、**Categories** テーブルに行を挿入し、Transact-SQL の SCOPE_IDENTITY() 関数によって生成された新しい ID 値を出力パラメーターとして取得する方法が示されています。

```sql
CREATE PROCEDURE dbo.InsertCategory
  @CategoryName nvarchar(15),
  @Identity int OUT
AS
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)
SET @Identity = SCOPE_IDENTITY()
```

このストアド プロシージャは <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> オブジェクトの <xref:System.Data.SqlClient.SqlDataAdapter> のソースとして指定できます。 <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> の <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> プロパティには、有効な <xref:System.Data.CommandType.StoredProcedure> を設定する必要があります。 ID の出力を取得するには、<xref:System.Data.SqlClient.SqlParameter> を <xref:System.Data.ParameterDirection> に設定した <xref:System.Data.ParameterDirection.Output> を作成します。 挿入コマンドの <xref:System.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> プロパティを `UpdateRowSource.OutputParameters` または `UpdateRowSource.Both` に設定した場合、`InsertCommand` が処理されるときに、自動的にインクリメントされた ID 値が返され、現在の行の **CategoryID** 列に設定されます。

挿入コマンドで、INSERT ステートメントと (新しい ID 値を返す) SELECT ステートメントの両方を含むバッチを実行した場合、挿入コマンドの `UpdatedRowSource` プロパティを `UpdateRowSource.FirstReturnedRecord` に設定することによって新しい値を取得できます。

[!code-csharp[DataWorks SqlClient.RetrieveIdentityStoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.RetrieveIdentityStoredProcedure/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.RetrieveIdentityStoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.RetrieveIdentityStoredProcedure/VB/source.vb#1)]

## <a name="merging-new-identity-values"></a>新しい ID 値の結合

`GetChanges` の `DataTable` は、変更行だけを含んだコピーを作成するメソッドです。作成した新しいコピーは `Update` の `DataAdapter` メソッドの呼び出し時に使用できます。 この方法を用いると、変更された行を別のコンポーネントにマーシャリングして更新を実行できます。 更新後、このコピーには、元の `DataTable` に再び結合する必要のある新しい ID 値が格納されている可能性もあります。 新しい ID 値は、おそらく `DataTable` 内の元の値とは異なります。 マージを実行するには、新しい ID 値を含んだ新しい行を追加するのではなく、コピー内の **AutoIncrement** 列の元の値を保持しておき、元の `DataTable` から既存の行を特定して更新する必要があります。 しかし、既定では、`Update` の `DataAdapter` メソッドを呼び出した後、元の値は失われてしまいます。更新された `AcceptChanges` ごとに `DataRow` が暗黙的に呼び出されるためです。

`DataColumn` の更新処理中、`DataRow` の `DataAdapter` に格納されていた元の値を保持するには、次の 2 とおりの方法があります。

- 元の値を保持する 1 つ目の方法は、`AcceptChangesDuringUpdate` の `DataAdapter` プロパティを `false` に設定することです。 この設定は、更新対象となる `DataRow` のすべての `DataTable` に影響します。 コード例および詳細については、「<xref:System.Data.Common.DataAdapter.AcceptChangesDuringUpdate%2A>」を参照してください。

- 2 つ目は、`RowUpdated` の `DataAdapter` イベント ハンドラーに、<xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> を <xref:System.Data.UpdateStatus.SkipCurrentRow> に設定するコードを記述する方法です。 `DataRow` が更新されても、各 `DataColumn` の元の値は保持されます。 この方法を使用した場合、一部の行についてのみ元の値を保持するといったことも可能です。 たとえば、最初に <xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A> を調べ、<xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> が <xref:System.Data.UpdateStatus.SkipCurrentRow> である行に限定して `StatementType` を `Insert` に設定することで、追加された行については元の値を保持し、編集または削除された行については元の値を保持しないようなコードを作成できます。

`DataRow` の更新処理中、上記のいずれかの方法で `DataAdapter` の元の値を保持した場合、ADO.NET は、各 `DataRow` の元の値を保持する一方で、`DataColumn` の現在の値を新しい値 (つまり、出力パラメーターまたは結果セットの先頭行として返された値) に設定するための一連の処理を実行します。 最初に `AcceptChanges` の `DataRow` メソッドが呼び出され、現在の値が元の値として保持された後、新しい値が割り当てられます。 これらの処理に続けて、`DataRows` プロパティが <xref:System.Data.DataRow.RowState%2A> に設定されていた <xref:System.Data.DataRowState.Added> については、`RowState` プロパティが <xref:System.Data.DataRowState.Modified> に設定されます。これはユーザーが想定していない可能性があります。

更新対象の各 <xref:System.Data.DataRow> に対し、コマンドの結果がどのように適用されるかは、各 <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> の <xref:System.Data.Common.DbCommand> プロパティによって決まります。 このプロパティは、`UpdateRowSource` 列挙型のいずれかの値に設定されます。

次の表では、`UpdateRowSource` 列挙型の各値が、更新対象の行の <xref:System.Data.DataRow.RowState%2A> プロパティにどのように影響するかを説明します。

|メンバー名|説明|
|-----------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|`AcceptChanges` が呼び出され、出力パラメーターの値と、返された結果セットの先頭行が、どちらも更新対象の `DataRow` に格納されます。 適用する値が存在しない場合、`RowState` は <xref:System.Data.DataRowState.Unchanged> になります。|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|行が返された場合、`AcceptChanges` が呼び出され、その行が `DataTable` の変更行にマップされて、`RowState` が `Modified` に設定されます。 行が返されなかった場合、`AcceptChanges` は呼び出されず、`RowState` は `Added` のままになります。|
|<xref:System.Data.UpdateRowSource.None>|返されたパラメーターまたは行はすべて無視されます。 `AcceptChanges` は呼び出されず、`RowState` は `Added` のままになります。|
|<xref:System.Data.UpdateRowSource.OutputParameters>|`AcceptChanges` が呼び出され、出力パラメーターがある場合は `DataTable` の変更行にマップされて、`RowState` が `Modified` に設定されます。 出力パラメーターがない場合は、`RowState` は `Unchanged` になります。|

### <a name="example"></a>例

次の例では、`DataTable` から変更行を抽出し、<xref:System.Data.SqlClient.SqlDataAdapter> でデータ ソースを更新して、新しい ID 列値を取得します。 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> は、2 つの Transact-SQL ステートメントを実行します。1 つは INSERT ステートメントで、もう 1 つは、SCOPE_IDENTITY 関数を使って ID 値を取得する SELECT ステートメントです。

```sql
INSERT INTO dbo.Shippers (CompanyName)
VALUES (@CompanyName);
SELECT ShipperID, CompanyName FROM dbo.Shippers
WHERE ShipperID = SCOPE_IDENTITY();
```

挿入コマンドの `UpdatedRowSource` プロパティは `UpdateRowSource.FirstReturnedRow` に、<xref:System.Data.MissingSchemaAction> の `DataAdapter` プロパティは `MissingSchemaAction.AddWithKey` に設定します。 `DataTable` にデータを格納した後、新しい行を `DataTable` に追加します。 次に、変更行を抽出して新しい `DataTable` に格納します。このデータ テーブルが `DataAdapter` に渡され、サーバー側が更新されます。

[!code-csharp[DataWorks SqlClient.MergeIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.MergeIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/VB/source.vb#1)]

`OnRowUpdated` イベント ハンドラーでは、<xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A> の <xref:System.Data.SqlClient.SqlRowUpdatedEventArgs> をチェックして、行が挿入であるかどうかを調べています。 挿入である場合は、<xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> プロパティを <xref:System.Data.UpdateStatus.SkipCurrentRow> に設定します。 行は更新されますが、その行の元の値は保持されます。 プロシージャの本体では、<xref:System.Data.DataSet.Merge%2A> メソッドを呼び出すことによって、新しい ID 値を元の `DataTable` に結合し、最後に `AcceptChanges` を呼び出します。

[!code-csharp[DataWorks SqlClient.MergeIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/CS/source.cs#2)]
[!code-vb[DataWorks SqlClient.MergeIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/VB/source.vb#2)]

## <a name="retrieving-microsoft-access-autonumber-values"></a>Microsoft Access の Autonumber 値の取得

このセクションでは、Jet 4.0 データベースから `Autonumber` 値を取得する方法を例で示します。 Jet データベース エンジンは、複数のステートメントをバッチとして実行することも、出力パラメーターを使用することもできません。そのため、前述した方法では、挿入行に割り当てられた新しい `Autonumber` 値を取得することはできません。 ただし、`RowUpdated` イベント ハンドラーにコードを追加し、別の SELECT @@IDENTITY ステートメントを実行することによって、新しい `Autonumber` の値を取得できます。

### <a name="example"></a>例

この例では、`MissingSchemaAction.AddWithKey` を使ってスキーマ情報を追加する代わりに、あらかじめ適切なスキーマで `DataTable` を構成した後、<xref:System.Data.OleDb.OleDbDataAdapter> を呼び出して `DataTable` にデータを格納しています。 この場合、<xref:System.Data.DataColumn.AutoIncrement%2A> を `true` に、<xref:System.Data.DataColumn.AutoIncrementSeed%2A> を 0 に、<xref:System.Data.DataColumn.AutoIncrementStep%2A> を -1 に設定することにより、行が挿入されるたびに割り当てられる 0 から始まる値をデクリメントするように、**CategoryID** 列を構成します。 その後、2 つの新しい行を追加し、`GetChanges` を使って変更行を新しい `DataTable` に追加します。`Update` メソッドには、このデータ テーブルが渡されます。

[!code-csharp[DataWorks OleDb.JetAutonumberMerge#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/CS/source.cs#1)]
[!code-vb[DataWorks OleDb.JetAutonumberMerge#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/VB/source.vb#1)]

`RowUpdated` イベント ハンドラーでは、<xref:System.Data.OleDb.OleDbConnection> の `Update` ステートメントと同じ、開いている `OleDbDataAdapter` を使用します。 このハンドラーでは、挿入された行について、`StatementType` の <xref:System.Data.OleDb.OleDbRowUpdatedEventArgs> をチェックします。 挿入された行ごとに、新しい <xref:System.Data.OleDb.OleDbCommand> を作成し、接続に対して SELECT @@IDENTITY ステートメントを実行して、`Autonumber` の新しい値を取得します。取得した値は、`DataRow` の **CategoryID** 列に格納します。 次に、`Status` の暗黙的な呼び出しを抑制するため、`UpdateStatus.SkipCurrentRow` プロパティを `AcceptChanges` に設定しています。 プロシージャの本体では、`Merge` メソッドを呼び出すことによって、2 つの `DataTable` を結合し、最後に `AcceptChanges` を呼び出します。

[!code-csharp[DataWorks OleDb.JetAutonumberMerge#2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/CS/source.cs#2)]
[!code-vb[DataWorks OleDb.JetAutonumberMerge#2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/VB/source.vb#2)]

### <a name="retrieving-identity-values"></a>ID 値の取得

列内の値が一意である必要がある場合、列を ID として設定することがあります。 新しいデータの ID 値が必要となる場合があります。 次のサンプルは、ID 値を取得する方法を示しています。

- データを挿入して ID 値を返すストアド プロシージャを作成します。

- 新しいデータを挿入して結果を表示するコマンドを実行します。

- <xref:System.Data.SqlClient.SqlDataAdapter> を使用し、新しいデータを挿入して結果を表示します。

サンプルをコンパイルして実行する前に、次のスクリプトを使用してサンプル データベースを作成する必要があります。

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
CREATE procedure [dbo].[CourseExtInfo] @CourseId int
as
select c.CourseID,c.Title,c.Credits,d.Name as DepartmentName
from Course as c left outer join Department as d on c.DepartmentID=d.DepartmentID
where c.CourseID=@CourseId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create procedure [dbo].[DepartmentInfo] @DepartmentId int,@CourseCount int output
as
select @CourseCount=Count(c.CourseID)
from course as c
where c.DepartmentID=@DepartmentId

select d.DepartmentID,d.Name,d.Budget,d.StartDate,d.Administrator
from Department as d
where d.DepartmentID=@DepartmentId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
Create PROCEDURE [dbo].[GetDepartmentsOfSpecifiedYear]
@Year int,@BudgetSum money output
AS
BEGIN
        SELECT @BudgetSum=SUM([Budget])
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

SELECT [DepartmentID]
      ,[Name]
      ,[Budget]
      ,[StartDate]
      ,[Administrator]
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[GradeOfStudent]
-- Add the parameters for the stored procedure here
@CourseTitle nvarchar(100),@FirstName nvarchar(50),
@LastName nvarchar(50),@Grade decimal(3,2) output
AS
BEGIN
select @Grade=Max(Grade)
from [dbo].[StudentGrade] as s join [dbo].[Course] as c on
s.CourseID=c.CourseID join [dbo].[Person] as p on s.StudentID=p.PersonID
where c.Title=@CourseTitle and p.FirstName=@FirstName
and p.LastName= @LastName
END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[InsertPerson]
-- Add the parameters for the stored procedure here
@FirstName nvarchar(50),@LastName nvarchar(50),
@PersonID int output
AS
BEGIN
    insert [dbo].[Person](LastName,FirstName) Values(@LastName,@FirstName)

    set @PersonID=SCOPE_IDENTITY()
END
Go

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

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[Person]([PersonID] [int] IDENTITY(1,1) NOT NULL,
[LastName] [nvarchar](50) NOT NULL,
[FirstName] [nvarchar](50) NOT NULL,
[HireDate] [datetime] NULL,
[EnrollmentDate] [datetime] NULL,
[Picture] [varbinary](max) NULL,
 CONSTRAINT [PK_School.Student] PRIMARY KEY CLUSTERED
(
[PersonID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[StudentGrade]([EnrollmentID] [int] IDENTITY(1,1) NOT NULL,
[CourseID] [nvarchar](10) NOT NULL,
[StudentID] [int] NOT NULL,
[Grade] [decimal](3, 2) NOT NULL,
 CONSTRAINT [PK_StudentGrade] PRIMARY KEY CLUSTERED
(
[EnrollmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create view [dbo].[EnglishCourse]
as
select c.CourseID,c.Title,c.Credits,c.DepartmentID
from Course as c join Department as d on c.DepartmentID=d.DepartmentID
where d.Name=N'English'

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
SET IDENTITY_INSERT [dbo].[Person] ON

INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (1, N'Hu', N'Nan', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (2, N'Norman', N'Laura', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (3, N'Olivotto', N'Nino', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (4, N'Anand', N'Arturo', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (5, N'Jai', N'Damien', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (6, N'Holt', N'Roger', CAST(0x000097F100000000 AS DateTime), NULL)
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (7, N'Martin', N'Randall', CAST(0x00008B1A00000000 AS DateTime), NULL)
SET IDENTITY_INSERT [dbo].[Person] OFF
SET IDENTITY_INSERT [dbo].[StudentGrade] ON

INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (1, N'C1045', 1, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (2, N'C1045', 2, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (3, N'C1045', 3, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (4, N'C1045', 4, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (5, N'C1045', 5, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (6, N'C1061', 1, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (7, N'C1061', 3, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (8, N'C1061', 4, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (9, N'C1061', 5, CAST(1.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (10, N'C2021', 1, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (11, N'C2021', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (12, N'C2021', 4, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (13, N'C2021', 5, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (14, N'C2042', 1, CAST(2.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (15, N'C2042', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (16, N'C2042', 3, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (17, N'C2042', 5, CAST(3.00 AS Decimal(3, 2)))
SET IDENTITY_INSERT [dbo].[StudentGrade] OFF
ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
ALTER TABLE [dbo].[StudentGrade]  WITH CHECK ADD  CONSTRAINT [FK_StudentGrade_Student] FOREIGN KEY([StudentID])
REFERENCES [dbo].[Person] ([PersonID])
GO
ALTER TABLE [dbo].[StudentGrade] CHECK CONSTRAINT [FK_StudentGrade_Student]
GO
```

コード リストを次に示します。

> [!TIP]
> このコード リストは、MySchool.mdb という名前の Access データベース ファイルを参照します。 MySchool.mdb は、[code.msdn.microsoft.com](https://code.msdn.microsoft.com/How-to-Retrieve-the-511acece) から (完全な C# または Visual Basic サンプル プロジェクトの一部として) ダウンロードできます。

```csharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Data.SqlClient;

class Program {
   static void Main(string[] args) {
      String SqlDbConnectionString = "Data Source=(local);Initial Catalog=MySchool;Integrated Security=True;Asynchronous Processing=true;";

      InsertPerson(SqlDbConnectionString, "Janice", "Galvin");
      Console.WriteLine();

      InsertPersonInAdapter(SqlDbConnectionString, "Peter", "Krebs");
      Console.WriteLine();

      String oledbConnectionString = "Provider=Microsoft.Jet.OLEDB.4.0; Data Source=Database\\MySchool.mdb";
      InsertPersonInJet4Database(oledbConnectionString, "Janice", "Galvin");
      Console.WriteLine();

      Console.WriteLine("Please press any key to exit.....");
      Console.ReadKey();
   }

   // Using stored procedure to insert a new row and retrieve the identity value
   static void InsertPerson(String connectionString, String firstName, String lastName) {
      String commandText = "dbo.InsertPerson";

      using (SqlConnection conn = new SqlConnection(connectionString)) {
         using (SqlCommand cmd = new SqlCommand(commandText, conn)) {
            cmd.CommandType = CommandType.StoredProcedure;

            cmd.Parameters.Add(new SqlParameter("@FirstName", firstName));
            cmd.Parameters.Add(new SqlParameter("@LastName", lastName));
            SqlParameter personId = new SqlParameter("@PersonID", SqlDbType.Int);
            personId.Direction = ParameterDirection.Output;
            cmd.Parameters.Add(personId);

            conn.Open();
            cmd.ExecuteNonQuery();

            Console.WriteLine("Person Id of new person:{0}", personId.Value);
         }
      }
   }

   // Using stored procedure in adapter to insert new rows and update the identity value.
   static void InsertPersonInAdapter(String connectionString, String firstName, String lastName) {
      String commandText = "dbo.InsertPerson";
      using (SqlConnection conn = new SqlConnection(connectionString)) {
         SqlDataAdapter mySchool = new SqlDataAdapter("Select PersonID,FirstName,LastName from [dbo].[Person]", conn);

         mySchool.InsertCommand = new SqlCommand(commandText, conn);
         mySchool.InsertCommand.CommandType = CommandType.StoredProcedure;

         mySchool.InsertCommand.Parameters.Add(
             new SqlParameter("@FirstName", SqlDbType.NVarChar, 50, "FirstName"));
         mySchool.InsertCommand.Parameters.Add(
             new SqlParameter("@LastName", SqlDbType.NVarChar, 50, "LastName"));

         SqlParameter personId = mySchool.InsertCommand.Parameters.Add(new SqlParameter("@PersonID", SqlDbType.Int, 0, "PersonID"));
         personId.Direction = ParameterDirection.Output;

         DataTable persons = new DataTable();
         mySchool.Fill(persons);

         DataRow newPerson = persons.NewRow();
         newPerson["FirstName"] = firstName;
         newPerson["LastName"] = lastName;
         persons.Rows.Add(newPerson);

         mySchool.Update(persons);
         Console.WriteLine("Show all persons:");
         ShowDataTable(persons, 14);
      }
   }

   /// For a Jet 4.0 database, we need use the single statement and event handler to insert new rows and retrieve the identity value.
   static void InsertPersonInJet4Database(String connectionString, String firstName, String lastName) {
      String commandText = "Insert into Person(FirstName,LastName) Values(?,?)";
      using (OleDbConnection conn = new OleDbConnection(connectionString)) {
         OleDbDataAdapter mySchool = new OleDbDataAdapter("Select PersonID,FirstName,LastName from Person", conn);

         // Create Insert Command
         mySchool.InsertCommand = new OleDbCommand(commandText, conn);
         mySchool.InsertCommand.CommandType = CommandType.Text;

         mySchool.InsertCommand.Parameters.Add(new OleDbParameter("@FirstName", OleDbType.VarChar, 50, "FirstName"));
         mySchool.InsertCommand.Parameters.Add(new OleDbParameter("@LastName", OleDbType.VarChar, 50, "LastName"));
         mySchool.InsertCommand.UpdatedRowSource = UpdateRowSource.Both;

         DataTable persons = CreatePersonsTable();

         mySchool.Fill(persons);

         DataRow newPerson = persons.NewRow();
         newPerson["FirstName"] = firstName;
         newPerson["LastName"] = lastName;
         persons.Rows.Add(newPerson);

         DataTable dataChanges = persons.GetChanges();

         mySchool.RowUpdated += OnRowUpdated;

         mySchool.Update(dataChanges);

         Console.WriteLine("Data before merging:");
         ShowDataTable(persons, 14);
         Console.WriteLine();

         persons.Merge(dataChanges);
         persons.AcceptChanges();

         Console.WriteLine("Data after merging");
         ShowDataTable(persons, 14);
      }
   }

   static void OnRowUpdated(object sender, OleDbRowUpdatedEventArgs e) {
      if (e.StatementType == StatementType.Insert) {
         // Retrieve the identity value
         OleDbCommand cmdNewId = new OleDbCommand("Select @@IDENTITY", e.Command.Connection);
         e.Row["PersonID"] = (Int32)cmdNewId.ExecuteScalar();

         // After the status is changed, the original values in the row are preserved. And the
         // Merge method will be called to merge the new identity value into the original DataTable.
         e.Status = UpdateStatus.SkipCurrentRow;
      }
   }

   // Create the Persons table before filling.
   private static DataTable CreatePersonsTable() {
      DataTable persons = new DataTable();

      DataColumn personId = new DataColumn();
      personId.DataType = Type.GetType("System.Int32");
      personId.ColumnName = "PersonID";
      personId.AutoIncrement = true;
      personId.AutoIncrementSeed = 0;
      personId.AutoIncrementStep = -1;
      persons.Columns.Add(personId);

      DataColumn firstName = new DataColumn();
      firstName.DataType = Type.GetType("System.String");
      firstName.ColumnName = "FirstName";
      persons.Columns.Add(firstName);

      DataColumn lastName = new DataColumn();
      lastName.DataType = Type.GetType("System.String");
      lastName.ColumnName = "LastName";
      persons.Columns.Add(lastName);

      DataColumn[] pkey = { personId };
      persons.PrimaryKey = pkey;

      return persons;
   }

   private static void ShowDataTable(DataTable table, Int32 length) {
      foreach (DataColumn col in table.Columns) {
         Console.Write("{0,-" + length + "}", col.ColumnName);
      }
      Console.WriteLine();

      foreach (DataRow row in table.Rows) {
         foreach (DataColumn col in table.Columns) {
            if (col.DataType.Equals(typeof(DateTime)))
               Console.Write("{0,-" + length + ":d}", row[col]);
            else if (col.DataType.Equals(typeof(Decimal)))
               Console.Write("{0,-" + length + ":C}", row[col]);
            else
               Console.Write("{0,-" + length + "}", row[col]);
         }

         Console.WriteLine();
      }
   }
}
```

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [行の状態とバージョン](./dataset-datatable-dataview/row-states-and-row-versions.md)
- [AcceptChange と RejectChange](./dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)
- [DataSet の内容のマージ](./dataset-datatable-dataview/merging-dataset-contents.md)
- [DataAdapter によるデータ ソースの更新](updating-data-sources-with-dataadapters.md)
- [ADO.NET の概要](ado-net-overview.md)
