---
title: Oracle シーケンス
ms.date: 03/30/2017
ms.assetid: 27cd371d-8252-414d-b5b2-5d31fa44b585
ms.openlocfilehash: d6e6bb51b8bd317c7161500b89993be689659fad
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149415"
---
# <a name="oracle-sequences"></a>Oracle シーケンス
.NET Framework Data Provider for Oracle では、<xref:System.Data.OracleClient.OracleDataAdapter> を使用して挿入操作を実行した後、サーバーによって生成されたキー値 (Oracle シーケンス) を取得できます。  
  
 SQL Server および Oracle は、主キーとして指定できる自動増分列の作成をサポートします。 これらの値はテーブルに行を追加するとサーバーによって自動的に生成されます。 SQL Server では列の Identity プロパティを設定し、Oracle では Sequence を作成します。 SQL Server の自動増分列と Oracle シーケンスの違いは、次のとおりです。  
  
- SQL Server では列を自動増分列として指定すると、新しい行を挿入するたびに SQL Server によって新しい列値が自動的に生成されます。  
  
- Oracle ではシーケンスを作成することによって、テーブルに新しい列値を生成します。ただし、シーケンスとテーブルまたはシーケンスと列の間に直接的な関係はありません。 Oracle シーケンスは、テーブルやストアド プロシージャと同様のオブジェクトです。  
  
 Oracle データベースにシーケンスを作成する場合は、初期値と増分値を定義できます。 新しい行を送信する前に、新しい値のシーケンスを照会することもできます。 つまり、コードでデータベースに行を挿入する前に、新しい行のキー値を調べることができます。  
  
 SQL Server と ADO.NET を使用した自動増加列の作成について詳しくは、「[ID 値および Autonumber 値の取得](retrieving-identity-or-autonumber-values.md)」および「[AutoIncrement 列の作成](./dataset-datatable-dataview/creating-autoincrement-columns.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の C# コードは、Oracle データベースから新しいシーケンス値を取得する例です。 新しい行を送信する INSERT INTO クエリでシーケンスを参照した後、Oracle10g で導入された RETURNING 句を使って、生成されたシーケンス値を返します。 この例では、保留状態の一連の新しい行を、ADO.NET の自動増分機能を使って <xref:System.Data.DataTable> に追加し、"プレースホルダー" の主キー値を生成します。 ADO.NET が新しい行に対して生成した増分値は、単なる "プレースホルダー" である点に注意してください。 つまり、データベースで生成される値は、ADO.NET によって生成された値とは必ずしも一致しません。  
  
 この例では、保留中の挿入をデータベースに送信する前に行の内容を表示します。 次に、新しい <xref:System.Data.OracleClient.OracleDataAdapter> オブジェクトを作成して、その <xref:System.Data.OracleClient.OracleDataAdapter.InsertCommand%2A> プロパティと <xref:System.Data.OracleClient.OracleDataAdapter.UpdateBatchSize%2A> プロパティを設定します。 この例では、サーバーによって生成された値を、出力パラメーターを使って返すロジックも使用されています。 その後、更新操作を実行し、保留中の行を送信して、<xref:System.Data.DataTable> の内容を表示します。  
  
```csharp  
public void OracleSequence(String connectionString)  
{  
   String insertString =
      "INSERT INTO SequenceTest_Table (ID, OtherColumn)" +  
      "VALUES (SequenceTest_Sequence.NEXTVAL, :OtherColumn)" +  
      "RETURNING ID INTO :ID";  
  
   using (OracleConnection conn = new OracleConnection(connectionString))  
   {  
      //Open a connection.  
      conn.Open();  
      OracleCommand cmd = conn.CreateCommand();  
  
      // Prepare the database.  
      cmd.CommandText = "DROP SEQUENCE SequenceTest_Sequence";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "DROP TABLE SequenceTest_Table";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "CREATE TABLE SequenceTest_Table " +  
                     "(ID int PRIMARY KEY, OtherColumn varchar(255))";  
      cmd.ExecuteNonQuery();  
  
      cmd.CommandText = "CREATE SEQUENCE SequenceTest_Sequence " +  
                        "START WITH 100 INCREMENT BY 5";  
      cmd.ExecuteNonQuery();  
  
      DataTable testTable = new DataTable();  
      DataColumn column = testTable.Columns.Add("ID", typeof(int));  
      column.AutoIncrement = true;  
      column.AutoIncrementSeed = -1;  
      column.AutoIncrementStep = -1;  
      testTable.PrimaryKey = new DataColumn[] { column };  
      testTable.Columns.Add("OtherColumn", typeof(string));  
      for (int rowCounter = 1; rowCounter <= 15; rowCounter++)  
      {  
         testTable.Rows.Add(null, "Row #" + rowCounter.ToString());  
      }  
  
      Console.WriteLine("Before Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      Console.WriteLine();  
  
      cmd.CommandText =
        "SELECT ID, OtherColumn FROM SequenceTest_Table";  
      OracleDataAdapter da = new OracleDataAdapter(cmd);  
      da.InsertCommand = new OracleCommand(insertString, conn);  
      da.InsertCommand.Parameters.Add(":ID", OracleType.Int32, 0, "ID");  
      da.InsertCommand.Parameters[0].Direction = ParameterDirection.Output;  
      da.InsertCommand.Parameters.Add(":OtherColumn", OracleType.VarChar, 255, "OtherColumn");  
      da.InsertCommand.UpdatedRowSource = UpdateRowSource.OutputParameters;  
      da.UpdateBatchSize = 10;  
  
      da.Update(testTable);  
  
      Console.WriteLine("After Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      // Close the connection.  
      conn.Close();  
   }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [Oracle および ADO.NET](oracle-and-adonet.md)
- [ADO.NET の概要](ado-net-overview.md)
