---
title: パラメーターおよびパラメーター データ型の構成
description: コマンド オブジェクトは、パラメーターを使用して SQL ステートメントまたはストアド プロシージャに値を渡すことによって、ADO.NET での型チェックと検証の機能を実現します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 537d8a2c-d40b-4000-83eb-bc1fcc93f707
ms.openlocfilehash: a426eeae785274b0484a84a2fae2dce4572fb4c4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287117"
---
# <a name="configuring-parameters-and-parameter-data-types"></a>パラメーターおよびパラメーター データ型の構成

コマンド オブジェクトは、パラメーターを使用して SQL ステートメントまたはストアド プロシージャに値を渡すことによって、型チェックと検証の機能を実現します。 コマンド テキストとは異なり、パラメーターの入力は実行可能なコードとしてではなく、リテラル値として扱われます。 これにより、攻撃者がサーバーのセキュリティを侵害するコマンドを SQL ステートメントに "注入" する SQL インジェクション攻撃を防ぐことができます。

パラメーター化コマンドによりクエリ実行パフォーマンスも向上します。これは、データベース サーバーが入力コマンドを適切なキャッシュ済みクエリ プランに正確に一致させるのに役立つためです。 詳細については、「[実行プランのキャッシュと再利用](/sql/relational-databases/query-processing-architecture-guide#execution-plan-caching-and-reuse)」および「[パラメーターと実行プランの再利用](/sql/relational-databases/query-processing-architecture-guide#PlanReuse)」を参照してください。 セキュリティおよびパフォーマンス上の利点に加え、パラメーター化コマンドを使用すると、データ ソースに渡す値を簡単に扱うことができます。

<xref:System.Data.Common.DbParameter> オブジェクトは、コンストラクターを使って作成できるほか、 <xref:System.Data.Common.DbCommand.DbParameterCollection%2A> コレクションの `Add` メソッドを呼び出し、 <xref:System.Data.Common.DbParameterCollection> にオブジェクトを追加することによって作成することもできます。 `Add` メソッドは、コンストラクター引数または既存のパラメーター オブジェクトを入力として受け取ります。この点はデータ プロバイダーによっても異なります。

## <a name="supplying-the-parameterdirection-property"></a>ParameterDirection プロパティの指定

パラメーターを追加する際は、入力パラメーターとは別に、パラメーターの <xref:System.Data.ParameterDirection> プロパティを指定する必要があります。 `ParameterDirection` で使用できる <xref:System.Data.ParameterDirection> の値を次の表に示します。

|メンバー名|説明|
|-----------------|-----------------|
|<xref:System.Data.ParameterDirection.Input>|このパラメーターは入力パラメーターです。 既定値です。|
|<xref:System.Data.ParameterDirection.InputOutput>|このパラメーターは入力と出力の両方の機能を持っています。|
|<xref:System.Data.ParameterDirection.Output>|このパラメーターは出力パラメーターです。|
|<xref:System.Data.ParameterDirection.ReturnValue>|パラメーターは、ストアド プロシージャ、組み込み関数、ユーザー定義関数などの操作からの戻り値を表します。|

## <a name="working-with-parameter-placeholders"></a>パラメーターのプレースホルダーの使用

パラメーターのプレースホルダーの構文はデータ ソースに依存します。 .NET Framework のデータ プロバイダーによって、パラメーターおよびパラメーターのプレースホルダーの名前付けや指定方法が異なります。 次の表に示すように、データ ソースごとに固有の構文が採用されています。

|データ プロバイダー|パラメーターの名前付け構文|
|-------------------|-----------------------------|
|<xref:System.Data.SqlClient>|`@`*parametername*形式の名前付きパラメーターが使用されます。|
|<xref:System.Data.OleDb>|疑問符 (`?`) で指定される位置パラメーター マーカーが使用されます。|
|<xref:System.Data.Odbc>|疑問符 (`?`) で指定される位置パラメーター マーカーが使用されます。|
|<xref:System.Data.OracleClient>|`:`*parmname* (または *parmname*) 形式の名前付きパラメーターが使用されます。|

## <a name="specifying-parameter-data-types"></a>パラメーターのデータ型の指定

パラメーターのデータ型は .NET Framework データ プロバイダーに固有です。 型が指定されている場合は、`Parameter` の値がデータ ソースに渡される前に、その値が .NET Framework データ プロバイダー型に変換されます。 `Parameter` オブジェクトの `DbType` プロパティを特定の `Parameter` に設定する一般的な方法で <xref:System.Data.DbType>の型を指定することもできます。

`Parameter` オブジェクトの .NET Framework データ プロバイダー型は、`Parameter` オブジェクトの `Value` の .NET Framework 型、または `Parameter` オブジェクトの `DbType` から推論されます。 `Parameter` 値として渡されるオブジェクトまたは指定された `Parameter` に基づいて推論される `DbType`型を、次の表に示します。

|.NET Framework 型|DbType|SqlDbType|OleDbType|OdbcType|OracleType|
|-------------------------|------------|---------------|---------------|--------------|----------------|
|<xref:System.Boolean>|ブール型|ビット|ブール型|ビット|Byte|
|<xref:System.Byte>|Byte|TinyInt|UnsignedTinyInt|TinyInt|Byte|
|byte[]|2 項|VarBinary。 バイト配列が VarBinary の最大サイズ (8000 バイト) より大きい場合、この暗黙の変換はエラーになります。8000 バイトを超えるバイト配列の場合は、明示的に <xref:System.Data.SqlDbType> を設定してください。|VarBinary|2 項|Raw|
|<xref:System.Char>| |char から <xref:System.Data.SqlDbType> への推論はサポートされていません。|Char|Char|Byte|
|<xref:System.DateTime>|DateTime|DateTime|DBTimeStamp|DateTime|DateTime|
|<xref:System.DateTimeOffset>|DateTimeOffset|SQL Server 2008 の DateTimeOffset。 SQL Server 2008 より前のバージョンの SQL Server では、DateTimeOffset から <xref:System.Data.SqlDbType> への推論はサポートされていません。|||DateTime|
|<xref:System.Decimal>|Decimal (10 進数型)|Decimal (10 進数型)|Decimal (10 進数型)|数字|数値|
|<xref:System.Double>|Double|Float|Double|Double|Double|
|<xref:System.Single>|Single|Real|Single|Real|Float|
|<xref:System.Guid>|GUID|UniqueIdentifier|GUID|UniqueIdentifier|Raw|
|<xref:System.Int16>|Int16|SmallInt|SmallInt|SmallInt|Int16|
|<xref:System.Int32>|Int32|Int|Int|Int|Int32|
|<xref:System.Int64>|Int64|BigInt|BigInt|BigInt|Number|
|<xref:System.Object>|Object|バリアント|バリアント|Object から OdbcType への推論はサポートされていません。|Blob|
|<xref:System.String>|String|NVarChar。 文字列が NVarChar の最大サイズ (4000 文字) より大きい場合、この暗黙の変換はエラーになります。 4000 文字を超える文字列の場合は、明示的に <xref:System.Data.SqlDbType>を設定してください。|VarWChar|NVarChar|NVarChar|
|<xref:System.TimeSpan>|時刻|SQL Server 2008 の Time。 SQL Server 2008 より前のバージョンの SQL Server では、TimeSpan から <xref:System.Data.SqlDbType> への推論はサポートされていません。|DBTime|時刻|DateTime|
|<xref:System.UInt16>|UInt16|UInt16 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|UnsignedSmallInt|Int|UInt16|
|<xref:System.UInt32>|UInt32|UInt32 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|UnsignedInt|BigInt|UInt32|
|<xref:System.UInt64>|UInt64|UInt64 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|UnsignedBigInt|数字|数値|
||AnsiString|VarChar|VarChar|VarChar|VarChar|
||AnsiStringFixedLength|Char|Char|Char|Char|
||通貨|通貨|通貨|`OdbcType` から `Currency` への推論はサポートされていません。|数値|
||Date|SQL Server 2008 の Date。 SQL Server 2008 より前のバージョンの SQL Server では、Date から <xref:System.Data.SqlDbType> への推論はサポートされていません。|DBDate|Date|DateTime|
||SByte|SByte から <xref:System.Data.SqlDbType> への推論はサポートされていません。|TinyInt|SByte から `OdbcType` への推論はサポートされていません。|SByte|
||StringFixedLength|NChar|WChar|NChar|NChar|
||時刻|SQL Server 2008 の Time。 SQL Server 2008 より前のバージョンの SQL Server では、Time から <xref:System.Data.SqlDbType> への推論はサポートされていません。|DBTime|時刻|DateTime|
||VarNumeric|VarNumeric から <xref:System.Data.SqlDbType> への推論はサポートされていません。|VarNumeric|VarNumeric から `OdbcType` への推論はサポートされていません。|数値|
|ユーザー定義型 ( <xref:Microsoft.SqlServer.Server.SqlUserDefinedAggregateAttribute>を持つオブジェクト)|プロバイダーに応じて Object または String (SqlClient は常に Object を返し、Odbc は常に String を返します。OleDb マネージド データ プロバイダーはいずれかを表示できます)。|<xref:Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute> がある場合は SqlDbType.Udt、それ以外の場合は Variant。|OleDbType.VarWChar (値が null の場合)、それ以外の場合は OleDbType.Variant。|OdbcType.NVarChar|サポート外|

> [!NOTE]
> decimal から他の型への変換は縮小変換になるため、decimal 値は最も近い整数値に切り捨てられます。 変換結果が対象の型にならなかった場合、 <xref:System.OverflowException> がスローされます。

> [!NOTE]
> サーバーに NULL パラメーター値を送信する場合は、`null` (Visual Basic の場合は `Nothing`) ではなく、<xref:System.DBNull> を指定する必要があります。 システムの null 値は、値のない空オブジェクトです。 <xref:System.DBNull> は、null 値を表すために使用します。 データベースの NULL 値の詳細については、「 [Handling Null Values](./sql/handling-null-values.md)」を参照してください。

## <a name="deriving-parameter-information"></a>パラメーター情報の派生

`DbCommandBuilder` クラスを使用してストアド プロシージャからパラメーターを派生させることができます。 `SqlCommandBuilder` クラスと `OleDbCommandBuilder` クラスはどちらも静的メソッド `DeriveParameters`を提供します。このメソッドは、ストアド プロシージャから得られたパラメーター情報を使用して、コマンド オブジェクトのパラメーター コレクションを設定します。 `DeriveParameters` はコマンドの既存のパラメーター情報を上書きします。

> [!NOTE]
> パラメーター情報を派生させた場合、情報を取得するためにデータ ソースへのラウンド トリップが 1 つ増えるため、パフォーマンスが低下します。 パラメーター情報がデザイン時にわかっている場合は、パラメーターを明示的に設定することでアプリケーションのパフォーマンスを改善できます。

詳細については、「[CommandBuilder でのコマンドの生成](generating-commands-with-commandbuilders.md)」を参照してください。

## <a name="using-parameters-with-a-sqlcommand-and-a-stored-procedure"></a>SqlCommand およびストアド プロシージャでのパラメーターの使用

ストアド プロシージャは、データドリブンのアプリケーションに多くの利点を提供します。 ストアド プロシージャを使用すると、データベースの操作を単一のコマンドにカプセル化し、最大のパフォーマンスが得られるように最適化し、さらに追加のセキュリティ機能を使用して、セキュリティを強化することができます。 ストアド プロシージャは、ストアド プロシージャ名の後にパラメーター引数を記述して SQL ステートメントとして渡すことで呼び出すことができますが、ADO.NET の <xref:System.Data.Common.DbCommand> オブジェクトの <xref:System.Data.Common.DbCommand.Parameters%2A> コレクションを使用すると、ストアド プロシージャ パラメーターをより明示的に定義でき、出力パラメーターや戻り値にもアクセスできます。

> [!NOTE]
> パラメーター化ステートメントは、 `sp_executesql,` を使ってサーバー上で実行されるため、クエリ プランの再利用が可能になります。 `sp_executesql` バッチ内のローカル カーソルまたはローカル変数は、 `sp_executesql`を呼び出すバッチでは認識されません。 データベース コンテキストの変更は、 `sp_executesql` ステートメント終了時まで有効です。 詳細については、「[sp_executesql (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql)」を参照してください。

<xref:System.Data.SqlClient.SqlCommand> でパラメーターを使用して SQL Server のストアド プロシージャを実行する場合は、 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> コレクションに追加したパラメーターの名前が、ストアド プロシージャ内のパラメーター マーカーの名前と一致している必要があります。 .NET Framework Data Provider for SQL Server は、SQL ステートメントまたはストアド プロシージャにパラメーターを渡す場合の疑問符 (?) プレースホルダーをサポートしていません。 ストアド プロシージャ内のパラメーターは名前付きのパラメーターと見なされ、一致するパラメーター マーカーが検索されます。 たとえば、 `CustOrderHist` ストアド プロシージャが、 `@CustomerID`という名前のパラメーターで定義されているとします。 このストアド プロシージャを実行する場合、実行元のコードでも `@CustomerID`という名前のパラメーターを使用する必要があります。

```sql
CREATE PROCEDURE dbo.CustOrderHist @CustomerID varchar(5)
```

### <a name="example"></a>例

次の例では、 `Northwind` サンプル データベースにある SQL Server ストアド プロシージャを呼び出す方法を説明します。 ストアド プロシージャの名前は `dbo.SalesByCategory` で、 `@CategoryName` データ型の `nvarchar(15)`という名前の入力パラメーターを持ちます。 このコードでは、プロシージャの終了時に接続が破棄されるように、using ブロック内で新しい <xref:System.Data.SqlClient.SqlConnection> を作成しています。 <xref:System.Data.SqlClient.SqlCommand> オブジェクトおよび <xref:System.Data.SqlClient.SqlParameter> オブジェクトが作成され、それぞれのプロパティが設定されます。 <xref:System.Data.SqlClient.SqlDataReader> によって `SqlCommand` が実行された後、ストアド プロシージャから結果セットが返されて、出力がコンソール ウィンドウに表示されます。

> [!NOTE]
> `SqlCommand` オブジェクトと `SqlParameter` オブジェクトを作成してから別個のステートメントでプロパティを設定する代わりに、オーバーロード コンストラクターを使用して複数のプロパティを 1 つのステートメントで設定することもできます。

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]

## <a name="using-parameters-with-an-oledbcommand-or-odbccommand"></a>OleDbCommand または OdbcCommand によるパラメーターの使用

<xref:System.Data.OleDb.OleDbCommand> または <xref:System.Data.Odbc.OdbcCommand>でパラメーターを使用するときは、 `Parameters` コレクションにパラメーターが追加されている順序が、ストアド プロシージャ内でパラメーターが定義されている順序と一致している必要があります。 .NET Framework Data Provider for OLE DB と .NET Framework Data Provider for ODBC は、ストアド プロシージャ内のパラメーターをプレースホルダーとして処理し、順にパラメーター値を適用します。 また、戻り値パラメーターは、 `Parameters` コレクションに最初に追加されたパラメーターにする必要があります。

.NET Framework Data Provider for OLE DB と .NET Framework Data Provider for ODBC は、SQL ステートメントまたはストアド プロシージャにパラメーターを渡す場合の名前付きのパラメーターをサポートしていません。 この場合は、次の例に示すように、疑問符 (?) プレースホルダーを使用する必要があります。

```sql
SELECT * FROM Customers WHERE CustomerID = ?
```

したがって、 `Parameter` コレクションに `Parameters` オブジェクトを追加する順序は、パラメーターの疑問符 (?) プレースホルダーの位置と完全に対応している必要があります。

### <a name="oledb-example"></a>OleDb の例

```vb
Dim command As OleDbCommand = New OleDbCommand( _
  "SampleProc", connection)
command.CommandType = CommandType.StoredProcedure

Dim parameter As OleDbParameter = command.Parameters.Add( _
  "RETURN_VALUE", OleDbType.Integer)
parameter.Direction = ParameterDirection.ReturnValue

parameter = command.Parameters.Add( _
  "@InputParm", OleDbType.VarChar, 12)
parameter.Value = "Sample Value"

parameter = command.Parameters.Add( _
  "@OutputParm", OleDbType.VarChar, 28)
parameter.Direction = ParameterDirection.Output
```

```csharp
OleDbCommand command = new OleDbCommand("SampleProc", connection);
command.CommandType = CommandType.StoredProcedure;

OleDbParameter parameter = command.Parameters.Add(
  "RETURN_VALUE", OleDbType.Integer);
parameter.Direction = ParameterDirection.ReturnValue;

parameter = command.Parameters.Add(
  "@InputParm", OleDbType.VarChar, 12);
parameter.Value = "Sample Value";

parameter = command.Parameters.Add(
  "@OutputParm", OleDbType.VarChar, 28);
parameter.Direction = ParameterDirection.Output;
```

## <a name="odbc-example"></a>Odbc の例

```vb
Dim command As OdbcCommand = New OdbcCommand( _
  "{ ? = CALL SampleProc(?, ?) }", connection)
command.CommandType = CommandType.StoredProcedure

Dim parameter As OdbcParameter = command.Parameters.Add("RETURN_VALUE", OdbcType.Int)
parameter.Direction = ParameterDirection.ReturnValue

parameter = command.Parameters.Add( _
  "@InputParm", OdbcType.VarChar, 12)
parameter.Value = "Sample Value"

parameter = command.Parameters.Add( _
  "@OutputParm", OdbcType.VarChar, 28)
parameter.Direction = ParameterDirection.Output
```

```csharp
OdbcCommand command = new OdbcCommand( _
  "{ ? = CALL SampleProc(?, ?) }", connection);
command.CommandType = CommandType.StoredProcedure;

OdbcParameter parameter = command.Parameters.Add( _
  "RETURN_VALUE", OdbcType.Int);
parameter.Direction = ParameterDirection.ReturnValue;

parameter = command.Parameters.Add( _
  "@InputParm", OdbcType.VarChar, 12);
parameter.Value = "Sample Value";

parameter = command.Parameters.Add( _
  "@OutputParm", OdbcType.VarChar, 28);
parameter.Direction = ParameterDirection.Output;
```

## <a name="see-also"></a>関連項目

- [コマンドおよびパラメーター](commands-and-parameters.md)
- [DataAdapter パラメーター](dataadapter-parameters.md)
- [ADO.NET でのデータ型のマッピング](data-type-mappings-in-ado-net.md)
- [ADO.NET の概要](ado-net-overview.md)
