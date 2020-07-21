---
title: DataReader によるデータの取得
description: ADO.NET で DataReader を使用してデータを取得する方法について、サンプル コードで説明します。 DataReader は、バッファリングされないデータ ストリームを提供します。
ms.date: 10/29/2018
dev_langs:
- csharp
- vb
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.openlocfilehash: 6e5161cc325bf0379bb9241b99c473c539ad1081
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286599"
---
# <a name="retrieve-data-using-a-datareader"></a>DataReader を使用してデータを取得する
**DataReader** を使用してデータを取得するには、**Command** オブジェクトのインスタンスを作成した後、**Command.ExecuteReader** を呼び出して **DataReader** を作成し、データ ソースから行を取得します。 **DataReader** では、手続きロジックがデータ ソースからの結果を順番に効率的に処理できるようにするバッファリングされないデータ ストリームが提供されます。 **DataReader** はデータをメモリにキャッシュしないため、大量のデータを取得する場合に適しています。

**DataReader** を使用する例を次に示します。ここで、`reader` は有効な DataReader を、`command` は有効な Command オブジェクトを表します。  

```csharp
reader = command.ExecuteReader();  
```

```vb
reader = command.ExecuteReader()
```  

クエリ結果から行を取得するには、**DataReader.Read** メソッドを使用します。 返された行の各列にアクセスするには、その列の名前または序数を **DataReader** に渡します。 ただし、**DataReader** では、最適のパフォーマンスが得られるように、ネイティブのデータ型を使用して列の値にアクセスできる一連のメソッド (**GetDateTime**、**GetDouble**、**GetGuid**、**GetInt32** など) が提供されています。 データ プロバイダー固有の **DataReader** に対する型指定されたアクセサー メソッドの一覧については、<xref:System.Data.OleDb.OleDbDataReader> および <xref:System.Data.SqlClient.SqlDataReader> を参照してください。 基になるデータ型がわかっているときは、型指定されたアクセサー メソッドを使用すると、列の値を取得するときに必要な型変換の量が少なくなります。  
  
 次に、**DataReader** オブジェクトを反復処理して各行から 2 つの列を返す例を示します。  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
## <a name="closing-the-datareader"></a>DataReader の終了  
 **DataReader** オブジェクトを使い終えたら、**Close** メソッドを必ず呼び出します。  
  
 **Command** に出力パラメーターまたは戻り値が含まれている場合、**DataReader** が閉じられるまで、それらの値を使用することはできません。  
  
 **DataReader** が開かれている間、**Connection** はその **DataReader** によって排他的に使用されています。 元の **DataReader** が閉じられるまでは、別の **DataReader** の作成など、どのようなコマンドもその **Connection** に対して実行できません。  
  
> [!NOTE]
> クラスの **Finalize** メソッド内では、**Connection**、**DataReader**、またはその他のマネージド オブジェクトに対して、**Close** または **Dispose** を呼び出さないでください。 終了処理では、クラスに直接所有されているアンマネージ リソースだけを解放してください。 クラスがアンマネージド リソースを所有していない場合は、クラス定義に **Finalize** メソッドを含めないでください。 詳しくは、「[ガベージ コレクション](../../../standard/garbage-collection/index.md)」をご覧ください。  
  
## <a name="retrieving-multiple-result-sets-using-nextresult"></a>NextResult による複数の結果セットの取得  
 **DataReader** から複数の結果セットが返される場合は、**NextResult** メソッドを呼び出して、結果セットを順番に反復処理します。 <xref:System.Data.SqlClient.SqlDataReader> メソッドを使用して、2 つの SELECT ステートメントの結果を処理する <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> の例を次に示します。  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## <a name="getting-schema-information-from-the-datareader"></a>DataReader からのスキーマ情報の取得  
 **DataReader** が開かれている間に **GetSchemaTable** メソッドを使用して、現在の結果セットについてのスキーマ情報を取得できます。 **GetSchemaTable** は、現在の結果セットのスキーマ情報を含む行と列が設定されている <xref:System.Data.DataTable> オブジェクトを返します。 **DataTable** には結果セットの列ごとに 1 行が設定されます。 スキーマ テーブルの各列は、結果セットの行で返される列の 1 つのプロパティにマップされます。**ColumnName** はそのプロパティの名前であり、列の値はプロパティの値です。 **DataReader** のスキーマ情報を出力する例を次に示します。  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## <a name="working-with-ole-db-chapters"></a>OLE DB のチャプターの使用  
 階層構造の行セット、つまりチャプター (OLE DB では **DBTYPE_HCHAPTER** 型、ADO では **adChapter** 型) は、<xref:System.Data.OleDb.OleDbDataReader> を使用して取得できます。 チャプターを含むクエリが **DataReader** として返されるとき、チャプターはその **DataReader** の列として返され、**DataReader** オブジェクトとして公開されます。  
  
 ADO.NET の **DataSet** を使用することで、テーブル間の親子のリレーションシップを使用して階層構造の行セットを表すこともできます。 詳しくは、「[DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)」をご覧ください。  
  
 MSDataShape プロバイダーを使用して、顧客リストの顧客別オーダーのチャプター列を生成するコード サンプルを次に示します。  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" &
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")

    Using custCMD As OleDbCommand = New OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " &
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " &
        "RELATE CustomerID TO CustomerID)", connection)

        connection.Open()

        Using custReader As OleDbDataReader = custCMD.ExecuteReader()

            Do While custReader.Read()
                Console.WriteLine("Orders for " & custReader.GetString(1))
                ' custReader.GetString(1) = CompanyName  

                Using orderReader As OleDbDataReader = custReader.GetValue(2)
                    ' custReader.GetValue(2) = Orders chapter as DataReader  

                    Do While orderReader.Read()
                        Console.WriteLine(vbTab & orderReader.GetInt32(1))
                        ' orderReader.GetInt32(1) = OrderID  
                    Loop
                    orderReader.Close()
                End Using
            Loop
            ' Make sure to always close readers and connections.  
            custReader.Close()
        End Using
    End Using
End Using
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" +
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"))
{
    using (OleDbCommand custCMD = new OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +
        "RELATE CustomerID TO CustomerID)", connection))
    {
        connection.Open();

        using (OleDbDataReader custReader = custCMD.ExecuteReader())
        {

            while (custReader.Read())
            {
                Console.WriteLine("Orders for " + custReader.GetString(1));
                // custReader.GetString(1) = CompanyName  

                using (OleDbDataReader orderReader = (OleDbDataReader)custReader.GetValue(2))
                {
                    // custReader.GetValue(2) = Orders chapter as DataReader  

                    while (orderReader.Read())
                        Console.WriteLine("\t" + orderReader.GetInt32(1));
                    // orderReader.GetInt32(1) = OrderID  
                    orderReader.Close();
                }
            }
            // Make sure to always close readers and connections.  
            custReader.Close();
        }
    }
}
```  
  
## <a name="returning-results-with-oracle-ref-cursors"></a>Oracle REF CURSOR による結果の取得  
 .NET Framework Data Provider for Oracle は、クエリ結果を返すために、Oracle REF CURSOR の使用をサポートしています。 Oracle REF CURSOR は <xref:System.Data.OracleClient.OracleDataReader> として返されます。  
  
 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> メソッドを使用して、Oracle の REF CURSOR を表す <xref:System.Data.OracleClient.OracleDataReader> オブジェクトを取得できます。 <xref:System.Data.DataSet> を設定するために使用される <xref:System.Data.OracleClient.OracleDataAdapter> に対する **SelectCommand** として 1 つまたは複数の Oracle の REF CURSOR を返す <xref:System.Data.OracleClient.OracleCommand> を指定することもできます。  
  
 Oracle データ ソースから返された REF CURSOR にアクセスするには、クエリ用の <xref:System.Data.OracleClient.OracleCommand> を作成し、<xref:System.Data.OracleClient.OracleCommand> の <xref:System.Data.OracleClient.OracleCommand.Parameters> コレクションに、REF CURSOR を参照する出力パラメーターを追加します。 パラメーターの名前は、クエリの REF CURSOR パラメーターの名前と一致させる必要があります。 パラメーターの型を <xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType> に設定します。 <xref:System.Data.OracleClient.OracleCommand> の <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> メソッドでは、REF CURSOR に対する <xref:System.Data.OracleClient.OracleDataReader> が返されます。  
  
 <xref:System.Data.OracleClient.OracleCommand> で複数の REF CURSOR が返される場合は、複数の出力パラメーターを追加します。 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> メソッドを呼び出すことにより、異なる REF CURSOR にアクセスできます。 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader> を呼び出すと、最初の REF CURSOR を参照している <xref:System.Data.OracleClient.OracleDataReader> が返されます。 次に <xref:System.Data.OracleClient.OracleDataReader.NextResult?displayProperty=nameWithType> メソッドを呼び出すと、後続の REF CURSOR にアクセスできます。 <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> コレクションのパラメーターが REF CURSOR 出力パラメーターの名前と一致していても、<xref:System.Data.OracleClient.OracleDataReader> は、<xref:System.Data.OracleClient.OracleCommand.Parameters> コレクションに追加された順に出力パラメーターにアクセスします。  
  
 たとえば、次のような Oracle パッケージとパッケージ本体があるとします。  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS
  TYPE T_CURSOR IS REF CURSOR;
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,
    DEPTCURSOR OUT T_CURSOR);
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,
    DEPTCURSOR OUT T_CURSOR)
  IS
  BEGIN
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;
  END OPEN_TWO_CURSORS;
END CURSPKG;
```  
  
 次のコードで作成する <xref:System.Data.OracleClient.OracleCommand> では、<xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType> 型の 2 つのパラメーターを <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> コレクションに追加することで、上の Oracle パッケージから REF CURSOR を返します。  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 <xref:System.Data.OracleClient.OracleDataReader> の <xref:System.Data.OracleClient.OracleDataReader.Read> メソッドと <xref:System.Data.OracleClient.OracleDataReader.NextResult> メソッドを使用して、上のコマンドの結果を返すコードを次に示します。 REF CURSOR パラメーターは順番に返されます。  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 上のコマンドを使用して、Oracle パッケージの結果を <xref:System.Data.DataSet> に設定する例を次に示します。  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```

> [!NOTE]
> **OverflowException** が発生しないようにするため、<xref:System.Data.DataRow> に値を格納する前に、Oracle の NUMBER 型を有効な .NET Framework のデータ型に変換することをお勧めします。 <xref:System.Data.Common.DataAdapter.FillError> イベントを使用して、**OverflowException** が発生したかどうかを確認できます。 <xref:System.Data.Common.DataAdapter.FillError> イベントについて詳しくは、「[DataAdapter のイベント処理](handling-dataadapter-events.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [コマンドおよびパラメーター](commands-and-parameters.md)
- [データベース スキーマ情報の取得](retrieving-database-schema-information.md)
- [ADO.NET の概要](ado-net-overview.md)
