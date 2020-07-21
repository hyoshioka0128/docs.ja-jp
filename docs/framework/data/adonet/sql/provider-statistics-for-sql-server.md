---
title: SQL Server のプロバイダー統計情報
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.openlocfilehash: 5e37a04ff731a99664d636e0d4175f99214c2646
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174512"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server のプロバイダー統計情報
.NET Framework version 2.0 以降では、.NET Framework Data Provider for SQL Server によって実行時の統計がサポートされています。 統計情報を有効にするには、有効な接続オブジェクトを作成した後で、<xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> オブジェクトの <xref:System.Data.SqlClient.SqlConnection> プロパティを `True` に設定する必要があります。 統計情報が有効になったら、<xref:System.Data.SqlClient.SqlConnection> オブジェクトの <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> メソッドを使用して、<xref:System.Collections.IDictionary> 参照を取得することにより、それらを "特定の時点のスナップショット" として確認できます。 名前と値のペアの辞書エントリのセットとしてリストを列挙します。 これらの名前と値のペアは順不同です。 カウンターはいつでも、<xref:System.Data.SqlClient.SqlConnection> オブジェクトの <xref:System.Data.SqlClient.SqlConnection.ResetStatistics%2A> メソッドを呼び出してリセットできます。 統計情報の収集が有効にされていない場合、例外は生成されません。 さらに、最初に <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> を呼び出すことなく <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> が呼び出された場合、取得される値は各エントリの初期値になります。 統計を有効にし、アプリケーションをしばらく実行してから統計を無効にした場合、取得される値には、統計を無効にした時点までに収集された値が反映されます。 すべての統計情報の値は、接続ごとに収集されます。  
  
## <a name="statistical-values-available"></a>使用できる統計情報の値  
 現在、Microsoft SQL Server プロバイダーから使用できる項目は 18 種類あります。 使用できる項目の数を確認するには、<xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> により返される <xref:System.Collections.IDictionary> インターフェイス参照の **Count** プロパティを使用します。 プロバイダーの統計情報のカウンターはすべて、64 ビット幅である共通言語ランタイムの <xref:System.Int64> 型 (C# と Visual Basic の場合は **long**) を使用します。 **int64** データ型の最大値は、**int64.MaxValue** フィールドにより定義されているように、((2^63)-1)) です。 カウンターの値がこの最大値に達すると、正確であると見なされなくなります。 つまり、**int64.MaxValue**-1((2^63)-2) は、事実上、すべての統計情報について有効な値の最大値になります。  
  
> [!NOTE]
> 返される統計の数、名前、および順序は将来変更される可能性があるため、プロバイダー統計情報を返す場合には、辞書を使用します。 アプリケーションでは、辞書にある特定の値に依存しないようにする必要がありますが、その値が存在するかどうかを確認し、それに応じて分岐する必要があります。  
  
 次の表では、使用可能な現在の統計情報の値が説明されています。 個々の値のキー名は、Microsoft .NET Framework の地域別バージョン全体でローカライズされているわけではないことに注意してください。  
  
|キー名|説明|  
|--------------|-----------------|  
|`BuffersReceived`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、SQL Server からプロバイダーが受信した表形式データ ストリーム (TDS) パケットの数を返します。|  
|`BuffersSent`|統計が有効になった後にプロバイダーから SQL Server に送信された TDS パケットの数を返します。 大規模なコマンドでは、複数のバッファーが必要になる場合があります。 たとえば、大規模なコマンドがサーバーに送信され、6 個のパケットが必要な場合、`ServerRoundtrips` は 1 ずつ増え、`BuffersSent` は 6 ずつ増えます。|  
|`BytesReceived`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、SQL Server からプロバイダーが受信した TDS パケット内のデータのバイト数を返します。|  
|`BytesSent`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、TDS パケットで SQL Server に送信されるデータのバイト数を返します。|  
|`ConnectionTime`|統計情報が有効になった後に接続が開かれている時間 (ミリ秒) を示します (接続が開かれる前に統計情報が有効になっていた場合は、合計接続時間を示します)。|  
|`CursorOpens`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由でカーソルが開かれた回数を返します。<br /><br /> SELECT ステートメントから返された読み取り専用/順方向専用の結果は、カーソルとは見なされないため、このカウンターには影響しません。|  
|`ExecutionTime`|統計情報が有効になってから、プロバイダーが処理に費やした累計時間 (ミリ秒) を返します。この時間には、サーバーからの応答を待つために費やされた時間と、プロバイダー自体がコードを実行するために費やした時間が含まれます。<br /><br /> タイミング コードが含まれるクラスは次のとおりです。<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> パフォーマンスが重視されるメンバーをできるだけ小規模に保つため、次のメンバーは時刻指定されません。<br /><br /> SqlDataReader<br /><br /> this[] operator (all overloads)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由で実行された INSERT、DELETE、および UPDATE ステートメントの合計数を返します。|  
|`IduRows`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由で実行された INSERT、DELETE、および UPDATE ステートメントによって影響を受ける行の合計数を返します。|  
|`NetworkServerTime`|アプリケーションがプロバイダーを使って開始され、統計情報が有効になった後にプロバイダーがサーバーからの応答を待つために費やした累計時間 (ミリ秒) を返します。|  
|`PreparedExecs`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由で実行された準備済みコマンドの数を返します。|  
|`Prepares`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由で準備されたステートメントの数を返します。|  
|`SelectCount`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続経由で実行された SELECT ステートメントの数を返します。 これには、カーソルから行を取得するための FETCH ステートメントが含まれ、<xref:System.Data.SqlClient.SqlDataReader> の末尾に達したときに SELECT ステートメントの数が更新されます。|  
|`SelectRows`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、選択された行の数を返します。 この数には、SQL ステートメントによって生成されたすべての行が反映され、呼び出し元によって実際に使用されなかった行も含まれます。 たとえば、結果セット全体を読み取る前にデータ リーダーを終了しても、数には影響しません。 これには、FETCH ステートメントによってカーソルから取得された行が含まれます。|  
|`ServerRoundtrips`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、接続によってコマンドがサーバーに送信され、応答が返された回数を返します。|  
|`SumResultSets`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、使用された結果セットの数を返します。 たとえば、これにはクライアントに返される結果セットが含まれます。 カーソルの場合、各フェッチまたはブロックフェッチ操作は、独立した結果セットと見なされます。|  
|`Transactions`|アプリケーションがプロバイダーの使用を開始し、統計情報が有効になった後に、ロールバックを含む開始されたユーザー トランザクションの数を返します。 自動コミットをオンにして接続が実行されている場合、各コマンドはトランザクションと見なされます。<br /><br /> このカウンターでは、後でトランザクションがコミットされるか、ロール バックされるかに関係なく、BEGIN TRAN ステートメントが実行されるとすぐにトランザクション数が増えます。|  
|`UnpreparedExecs`|アプリケーションがプロバイダーを使って開始され、統計情報が有効になった後に接続を通じて準備解除された、ステートメントの数を返します。|  
  
### <a name="retrieving-a-value"></a>値の取得  
 次のコンソール アプリケーションは、接続で統計情報を有効にして、4 つの各統計情報の値を取得し、コンソール ウィンドウに出力する方法を示します。  
  
> [!NOTE]
> 次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプル コードに示されている接続文字列は、データベースがローカル コンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、お使いの環境に合わせて接続文字列を変更してください。  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      ' Retrieve a few individual values  
      ' related to the previous command.  
      Dim bytesReceived As Long = _  
          CLng(currentStatistics.Item("BytesReceived"))  
      Dim bytesSent As Long = _  
          CLng(currentStatistics.Item("BytesSent"))  
      Dim selectCount As Long = _  
          CLng(currentStatistics.Item("SelectCount"))  
      Dim selectRows As Long = _  
          CLng(currentStatistics.Item("SelectRows"))  
  
      Console.WriteLine("BytesReceived: " & bytesReceived.ToString())  
      Console.WriteLine("BytesSent: " & bytesSent.ToString())  
      Console.WriteLine("SelectCount: " & selectCount.ToString())  
      Console.WriteLine("SelectRows: " & selectRows.ToString())  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrieve it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>すべての値の取得  
 次のコンソール アプリケーションは、接続で統計情報を有効にし、使用可能なすべての統計情報の値を列挙子を使って取得して、コンソール ウィンドウに出力する方法を示します。  
  
> [!NOTE]
> 次の例では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 サンプル コードに示されている接続文字列は、データベースがローカル コンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、お使いの環境に合わせて接続文字列を変更してください。  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      Console.WriteLine("Key Name and Value")  
  
      ' Note the entries are unsorted.  
      For Each entry As DictionaryEntry In currentStatistics  
        Console.WriteLine(entry.Key.ToString() & _  
            ": " & entry.Value.ToString())  
      Next  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrieve it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [SQL Server と ADO.NET](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
