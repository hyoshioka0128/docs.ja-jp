---
title: テーブル値パラメーター
description: テーブル値パラメーターを使用することにより、複数行のデータをクライアント アプリケーションから SQL Server にマーシャリングする方法について説明します。
ms.date: 10/12/2018
dev_langs:
- csharp
- vb
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.openlocfilehash: 7b1f0a6c416f660f06cea099197ba136f84407f9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286198"
---
# <a name="table-valued-parameters"></a>テーブル値パラメーター
テーブル値パラメーターを使用すると、ラウンド トリップを何度も繰り返したり、サーバー側にデータを処理するための特殊なロジックを組み込んだりすることなく、複数行のデータをクライアント アプリケーションから SQL Server へと簡単にマーシャリングできます。 テーブル値パラメーターを使用すると、クライアント アプリケーションのデータ行をカプセル化して単一のパラメーター化コマンドでサーバーに送ることができます。 受信データ行はテーブル変数に格納され、Transact-SQL によって操作できるようになります。  
  
 テーブル値パラメーターの列値には、Transact-SQL の標準的な SELECT ステートメントを使ってアクセスできます。 テーブル値パラメーターは厳密に型指定されており、その構造は自動的に検証されます。 テーブル値パラメーターのサイズは、サーバーのメモリによってのみ制限されます。  
  
> [!NOTE]
> テーブル値パラメーターでデータを返すことはできません。 テーブル値パラメーターは入力専用です。OUTPUT キーワードはサポートされていません。  
  
 テーブル値パラメーターの詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[テーブル値パラメーターの使用 (データベース エンジン)](/sql/relational-databases/tables/use-table-valued-parameters-database-engine)|テーブル値パラメーターの作成方法および使用方法について説明します。|  
|[ユーザー定義テーブル型](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/bb522526(v=sql.100))|テーブル値パラメーターを宣言する際に使用するユーザー定義テーブル型について説明します。|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>旧バージョンの SQL Server での複数行の受け渡し  
 SQL Server 2008 にテーブル値パラメーターが導入されるまでは、複数行データをストアド プロシージャまたはパラメーター化 SQL コマンドに渡す方法は限られていました。 開発者が選択できる複数の行をサーバーに渡すためのオプションを次に示します。  
  
- 複数のデータ列とデータ行の値を表すには、一連の個別のパラメーターを使用します。 このメソッドを使用して渡すことができるデータの量は、許可されているパラメーター数によって制限されます。 SQL Server プロシージャが持つことのできるパラメーター数は最大 2,100 です。 これらの個々の値をテーブル変数または一時テーブルにまとめて処理するには、サーバー側ロジックが必要です。  
  
- 複数のデータ値を区切り文字列または XML ドキュメントにバンドルし、それらのテキスト値をプロシージャまたはステートメントに渡します。 これを行うには、そのプロシージャまたはステートメントに、データ構造の検証と値のバンドルの解除に必要なロジックが含まれている必要があります。  
  
- 複数の行 (<xref:System.Data.SqlClient.SqlDataAdapter> の `Update` メソッドを呼び出すことによって作成された行など) に影響を及ぼす、データを変更するための一連の個別 SQL ステートメントを作成します。 サーバーへの変更の送信は個別に行うことも、グループにまとめることもできます。 ただし、複数のステートメントをまとめてバッチ送信しても、サーバーで実行されるときはそれぞれ個別に処理されます。  
  
- `bcp` ユーティリティ プログラムまたは <xref:System.Data.SqlClient.SqlBulkCopy> オブジェクトを使用して、多数のデータ行をテーブルに読み込みます。 この方法は効率的ですが、データが一時テーブルまたはテーブル変数に読み込まれなければ、サーバー側での処理がサポートされません。  
  
## <a name="creating-table-valued-parameter-types"></a>テーブル値パラメーター型の作成  
 テーブル値パラメーターは、Transact-SQL の CREATE TYPE ステートメントを使用して定義された厳密に型指定されたテーブルの構造に基づいています。 クライアント アプリケーションでテーブル値パラメーターを使用するには、まず SQL Server でテーブル型を作成し、その構造を定義する必要があります。 テーブル型の作成の詳細については、「[ユーザー定義テーブル型](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/bb522526(v=sql.100))」を参照してください。  
  
 次のステートメントは、CategoryID と CategoryName 列から成る CategoryTableType というテーブル型を作成します。  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 テーブル型を作成したら、その型に基づいてテーブル値パラメーターを宣言できます。 次の Transact-SQL フラグメントは、ストアド プロシージャ定義の中でテーブル値パラメーターを宣言する方法を示しています。 テーブル値パラメーターの宣言には READONLY キーワードが必要であることに注意してください。  
  
```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>テーブル値パラメーターによるデータの変更 (Transact-SQL)  
 テーブル値パラメーターは、単一のステートメントを実行して複数行を操作する、セット ベースのデータ変更の中で使用できます。 たとえば、テーブル値パラメーター内のすべての行を選択して、データベース テーブルに挿入できます。また、テーブル値パラメーターを更新対象テーブルに結合して、更新ステートメントを作成することもできます。  
  
 次の Transact-SQL UPDATE ステートメントは、テーブル値パラメーターを Categories テーブルに結合して使用する方法を示しています。 FROM 句の中でテーブル値パラメーターを JOIN と共に使用する場合は、次に示すように、別名も使用する必要があります。ここでは、テーブル値パラメーターは "ec" という別名になっています。  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 この Transact-SQL の例は、単一のセット ベース操作で INSERT を実行するためにテーブル値パラメーターから行を選択する方法を示しています。  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>テーブル値パラメーターの制限  
 テーブル値パラメーターにはいくつかの制限があります。  
  
- テーブル値パラメーターを [CLR ユーザー定義の関数](/sql/relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions)に渡すことはできません。  
  
- テーブル値パラメーターには、UNIQUE 制約または PRIMARY KEY 制約に対応する目的でのみインデックスを設定できます。 SQL Server はテーブル値パラメーターの統計を保持しません。  
  
- テーブル値パラメーターは Transact-SQL コードの中では読み取り専用です。 テーブル値パラメーターの行の列値は更新できません。また、行の挿入や削除もできません。 テーブル値パラメーターのストアド プロシージャまたはパラメーター化されたステートメントに渡すデータを変更するには、そのデータを一時テーブルまたはテーブル変数に挿入する必要があります。  
  
- ALTER TABLE ステートメントをテーブル値パラメーターの設計変更に使用することはできません。  
  
## <a name="configuring-a-sqlparameter-example"></a>SqlParameter の構成例  
 <xref:System.Data.SqlClient> では、テーブル値パラメーターのデータを <xref:System.Data.DataTable>、<xref:System.Data.Common.DbDataReader>、または <xref:System.Collections.Generic.IEnumerable%601> \ <xref:Microsoft.SqlServer.Server.SqlDataRecord> オブジェクトから読み込むことができます。 <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> の <xref:System.Data.SqlClient.SqlParameter> プロパティを使用して、テーブル値パラメーターの型名を指定する必要があります。 `TypeName` は、サーバーで以前に作成した互換性のある型の名前と一致する必要があります。 次のコード フラグメントは、データを挿入するために <xref:System.Data.SqlClient.SqlParameter> を構成する方法を示しています。  

次の例では、`addedCategories` 変数に <xref:System.Data.DataTable> が含まれています。 変数がどのように設定されているかを確認するには、次の「[ストアド プロシージャへのテーブル値パラメーターの受け渡し](#passing)」を参照してください。

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```  
  
```vb  
' Configure the command and parameter.  
Dim insertCommand As New SqlCommand(sqlInsert, connection)  
Dim tvpParam As SqlParameter = _  
   insertCommand.Parameters.AddWithValue( _  
  "@tvpNewCategories", addedCategories)  
tvpParam.SqlDbType = SqlDbType.Structured  
tvpParam.TypeName = "dbo.CategoryTableType"  
```  
  
 <xref:System.Data.Common.DbDataReader> から派生した任意のオブジェクトを使用して、一連の行データをテーブル値パラメーターに挿入することもできます。その方法を次のフラグメントに示します。  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
```vb  
' Configure the SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  dataReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
```  
  
## <a name="passing-a-table-valued-parameter-to-a-stored-procedure"></a><a name="passing"></a> ストアド プロシージャへのテーブル値パラメーターの受け渡し  
 この例は、テーブル値パラメーターのデータをストアド プロシージャに渡す方法を示しています。 追加された行が、<xref:System.Data.DataTable.GetChanges%2A> メソッドを使って新しい <xref:System.Data.DataTable> に抽出された後、 <xref:System.Data.SqlClient.SqlCommand> が定義され、<xref:System.Data.SqlClient.SqlCommand.CommandType%2A> プロパティが <xref:System.Data.CommandType.StoredProcedure> に設定されます。 <xref:System.Data.SqlClient.SqlParameter> は <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> メソッドを使って設定され、<xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> は `Structured` に設定されます。 次に <xref:System.Data.SqlClient.SqlCommand> メソッドを使用して <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> が実行されます。  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection object.  
Using connection  
   '  Create a DataTable with the modified rows.  
   Dim addedCategories As DataTable = _  
     CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Configure the SqlCommand and SqlParameter.  
   Dim insertCommand As New SqlCommand( _  
     "usp_InsertCategories", connection)  
   insertCommand.CommandType = CommandType.StoredProcedure  
   Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
     "@tvpNewCategories", addedCategories)  
   tvpParam.SqlDbType = SqlDbType.Structured  
  
   '  Execute the command.  
   insertCommand.ExecuteNonQuery()  
End Using  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>パラメーター化 SQL ステートメントへのテーブル値パラメーターの受け渡し  
 次の例は、データ ソースとしてテーブル値パラメーターを持つ SELECT サブクエリ付きの INSERT ステートメントを使用して、dbo.Categories テーブルにデータを挿入する方法を示しています。 テーブル値パラメーターをパラメーター化 SQL ステートメントに渡すときは、<xref:System.Data.SqlClient.SqlParameter> の新しい <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> プロパティを使用して、テーブル値パラメーターの型名を指定する必要があります。 この `TypeName` は、サーバーで以前に作成した互換性のある型の名前と一致する必要があります。 この例のコードは、`TypeName` プロパティを使用して、dbo.CategoryTableType で定義されている型構造体を参照しています。  
  
> [!NOTE]
> テーブル値パラメーターで ID 列の値を指定する場合は、そのセッションの SET IDENTITY_INSERT ステートメントを実行する必要があります。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
Using connection  
  ' Create a DataTable with the modified rows.  
  Dim addedCategories As DataTable = _  
    CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Define the INSERT-SELECT statement.  
  Dim sqlInsert As String = _  
  "INSERT INTO dbo.Categories (CategoryID, CategoryName)" _  
  & " SELECT nc.CategoryID, nc.CategoryName" _  
  & " FROM @tvpNewCategories AS nc;"  
  
  ' Configure the command and parameter.  
  Dim insertCommand As New SqlCommand(sqlInsert, connection)  
  Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
    "@tvpNewCategories", addedCategories)  
  tvpParam.SqlDbType = SqlDbType.Structured  
  tvpParam.TypeName = "dbo.CategoryTableType"  
  
  ' Execute the query  
  insertCommand.ExecuteNonQuery()  
End Using  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>DataReader による行のストリーミング  
 テーブル値パラメーターにデータ行をストリーム出力するには、<xref:System.Data.Common.DbDataReader> から派生したオブジェクトを使用します。 次のコード フラグメントは、<xref:System.Data.OracleClient.OracleCommand> と <xref:System.Data.OracleClient.OracleDataReader> を使用して、Oracle データベースからデータを取得する方法を示しています。 その後、<xref:System.Data.SqlClient.SqlCommand> を、1 つの入力パラメーターを使用してストアド プロシージャを呼び出すように構成します。 <xref:System.Data.SqlClient.SqlParameter> の <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> プロパティは `Structured` に設定されます。 <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> は `OracleDataReader` の結果セットをテーブル値パラメーターとしてストアド プロシージャに渡します。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
' Retrieve data from Oracle.  
Dim selectCommand As New OracleCommand( _  
  "Select CategoryID, CategoryName FROM Categories;", _  
  oracleConnection)  
Dim oracleReader As OracleDataReader = _  
  selectCommand.ExecuteReader(CommandBehavior.CloseConnection)  
  
' Configure SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  oracleReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
' Execute the command.  
insertCommand.ExecuteNonQuery()  
```  
  
## <a name="see-also"></a>関連項目

- [パラメーターおよびパラメーター データ型の構成](../configuring-parameters-and-parameter-data-types.md)
- [コマンドおよびパラメーター](../commands-and-parameters.md)
- [DataAdapter パラメーター](../dataadapter-parameters.md)
- [ADO.NET における SQL Server データ操作](sql-server-data-operations.md)
- [ADO.NET の概要](../ado-net-overview.md)
