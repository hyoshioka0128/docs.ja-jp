---
title: 待機ハンドルを使用した ASP.NET アプリケーション
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.openlocfilehash: d354dda05e8353a33c3a64440e5c2bad390743b4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79148856"
---
# <a name="aspnet-applications-using-wait-handles"></a>待機ハンドルを使用した ASP.NET アプリケーション
アプリケーションが一度に 1 つの非同期操作しか処理しない場合は、コールバック モデルとポーリング モデルが非同期操作の処理に役立ちます。 Wait モデルは、複数の非同期操作を処理するための、さらに柔軟な方法を提供します。 2 つの Wait モデルがあり、それを実装するために使用される <xref:System.Threading.WaitHandle> メソッドから、Wait (Any) モデルと Wait (All) モデルという名前が付けられています。  
  
 どちらの Wait モデルを使用する場合でも、<xref:System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:System.Data.SqlClient.SqlCommand.BeginExecuteReader%2A>、または <xref:System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> メソッドによって返される <xref:System.IAsyncResult> オブジェクトの <xref:System.IAsyncResult.AsyncWaitHandle%2A> プロパティを使用する必要があります。 <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドと <xref:System.Threading.WaitHandle.WaitAll%2A> メソッドはどちらも、配列内にグループ化された <xref:System.Threading.WaitHandle> オブジェクトを引数として送信する必要があります。  
  
 どちらの Wait メソッドも、非同期操作を監視し、完了を待機します。 <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドは、いずれか 1 つの操作の完了またはタイムアウトを待機します。特定の操作が完了したことがわかれば、その結果を処理し、引き続き次の操作の完了またはタイムアウトを待機できます。<xref:System.Threading.WaitHandle.WaitAll%2A> メソッドは、<xref:System.Threading.WaitHandle> インスタンスの配列に含まれているすべてのプロセスが完了するかタイムアウトするまで次の操作の監視を開始しません。  
  
 Wait モデルの利点は、ある程度の長さの複数の操作を異なるサーバーで実行する必要がある場合や、サーバーがすべてのクエリを同時に処理するのに十分な性能を備えている場合に最も大きくなります。 ここで示す例では、重要度の低い SELECT クエリにさまざまな長さの WAITFOR コマンドを追加することによって、3 つのクエリが長いプロセスをエミュレートします。  
  
## <a name="example-wait-any-model"></a>例:Wait (Any) モデル  
 次の例は Wait (Any) モデルを示しています。 3 つの非同期プロセスが開始されると、いずれかのプロセスの完了を待つために <xref:System.Threading.WaitHandle.WaitAny%2A> メソッドが呼び出されます。 各プロセスが完了すると、<xref:System.Data.SqlClient.SqlCommand.EndExecuteReader%2A> メソッドが呼び出され、結果の <xref:System.Data.SqlClient.SqlDataReader> オブジェクトが読み取られます。 この時点で、実際のアプリケーションでは、<xref:System.Data.SqlClient.SqlDataReader> を使用してページの一部にデータが入力されることがあります。 この単純な例では、プロセスが完了した時刻が、そのプロセスに対応するテキスト ボックスに追加されます。 このように、テキスト ボックス内の時刻はその時点を示します。プロセスが完了するたびに、コードが実行されます。  
  
 この例を設定するには、新しい ASP.NET Web サイト プロジェクトを作成します。 ページ上に 1 つの <xref:System.Web.UI.WebControls.Button> コントロールと 4 つの <xref:System.Web.UI.WebControls.TextBox> コントロールを配置します (各コントロールの既定の名前をそのまま使用します)。  
  
 フォームのクラスに次のコードを追加し、実際の環境で必要に応じて接続文字列を変更します。  
  
```vb  
' Add these to the top of the class  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Threading  
  
' Add this code to the page's class:  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,
        ' you can retrieve it from a configuration file.
  
        ' If you have not included "Asynchronous Processing=true"
        ' in the connection string, the command will not be able  
        ' to execute asynchronously.  
        Return "Data Source=(local);Integrated Security=SSPI;" & _  
          "Initial Catalog=AdventureWorks;" & _  
          "Asynchronous Processing=true"  
    End Function
  
    Sub Button1_Click( _  
     ByVal sender As Object, ByVal e As System.EventArgs)  
  
        ' In a real-world application, you might be connecting to
        '  three different servers or databases. For the example,  
        '  we connect to only one.  
        Dim connection1 As New SqlConnection(GetConnectionString())  
        Dim connection2 As New SqlConnection(GetConnectionString())  
        Dim connection3 As New SqlConnection(GetConnectionString())  
  
        ' To keep the example simple, all three asynchronous
        ' processes select a row from the same table. WAITFOR  
        ' commands are used to emulate long-running processes  
        ' that complete after different periods of time.  
        Dim commandText1 As String = _  
            "WAITFOR DELAY '0:0:01';" & _  
            "SELECT * FROM Production.Product " & _  
            "WHERE ProductNumber = 'BL-2036'"  
  
        Dim commandText2 As String = _  
            "WAITFOR DELAY '0:0:05';" & _  
            "SELECT * FROM Production.Product " & _  
            "WHERE ProductNumber = 'BL-2036'"  
  
        Dim commandText3 As String = _  
            "WAITFOR DELAY '0:0:10';" & _  
            "SELECT * FROM Production.Product " & _  
            "WHERE ProductNumber = 'BL-2036'"  
  
        Dim waitHandles(2) As WaitHandle  
        Try  
            ' For each process, open a connection and begin execution.  
            ' Use the IAsyncResult object returned by
            ' BeginExecuteReader to add a WaitHandle for the process  
            ' to the array.  
            connection1.Open()  
            Dim command1 As New SqlCommand(commandText1, connection1)  
            Dim result1 As IAsyncResult = _  
             command1.BeginExecuteReader()  
            waitHandles(0) = result1.AsyncWaitHandle  
  
            connection2.Open()  
            Dim command2 As New SqlCommand(commandText2, connection2)  
            Dim result2 As IAsyncResult = _  
             command2.BeginExecuteReader()  
            waitHandles(1) = result2.AsyncWaitHandle  
  
            connection3.Open()  
            Dim command3 As New SqlCommand(commandText3, connection3)  
            Dim result3 As IAsyncResult = _  
             command3.BeginExecuteReader()  
            waitHandles(2) = result3.AsyncWaitHandle  
  
            Dim index As Integer  
            For countWaits As Integer = 1 To 3  
                ' WaitAny waits for any of the processes to complete.  
                ' The return value is either the index of the  
                ' array element whose process just completed, or  
                ' the WaitTimeout value.  
                index = WaitHandle.WaitAny(waitHandles, 60000, False)  
                ' This example doesn't actually do anything with the
                ' data returned by the processes, but the code opens
                ' readers for each just to demonstrate the concept.  
                ' Instead of using the returned data to fill the
                ' controls on the page, the example adds the time  
                ' the process was completed to the corresponding  
                ' text box.  
                Select Case index  
                    Case 0  
                        Dim reader1 As SqlDataReader  
                        reader1 = command1.EndExecuteReader(result1)  
                        If reader1.Read Then  
                            TextBox1.Text = _  
                             "Completed " & _  
                             System.DateTime.Now.ToLongTimeString()  
                        End If  
                        reader1.Close()  
  
                    Case 1  
                        Dim reader2 As SqlDataReader  
                        reader2 = command2.EndExecuteReader(result2)  
                        If reader2.Read Then  
                            TextBox2.Text = _  
                             "Completed " & _  
                             System.DateTime.Now.ToLongTimeString()  
                        End If  
                        reader2.Close()  
                    Case 2  
                        Dim reader3 As SqlDataReader  
                        reader3 = command3.EndExecuteReader(result3)  
                        If reader3.Read Then  
                            TextBox3.Text = _  
                             "Completed " & _  
                             System.DateTime.Now.ToLongTimeString()  
                        End If  
                        reader3.Close()  
                    Case WaitHandle.WaitTimeout  
                        Throw New Exception("Timeout")  
                End Select  
  
            Next  
        Catch ex As Exception  
            TextBox4.Text = ex.ToString  
        End Try  
        connection1.Close()  
        connection2.Close()  
        connection3.Close()  
  
    End Sub  
```  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using System.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,
     //  you can retrieve it from a configuration file.
     //  If you have not included "Asynchronous Processing=true"
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +
          "SELECT * FROM Production.Product " +
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +
          "SELECT * FROM Production.Product " +
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +
          "SELECT * FROM Production.Product " +
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin
          //  execution. Use the IAsyncResult object returned by
          //  BeginExecuteReader to add a WaitHandle for the
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to
               //  complete. The return value is either the index
               //  of the array element whose process just
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,
                    60000, false);  
               //  This example doesn't actually do anything with
               //  the data returned by the processes, but the
               //  code opens readers for each just to demonstrate
               //  the concept.  
               //  Instead of using the returned data to fill the
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>例:Wait (All) モデル  
 次の例は Wait (All) モデルを示しています。 3 つの非同期プロセスが開始されると、プロセスの完了またはタイムアウトを待つ <xref:System.Threading.WaitHandle.WaitAll%2A> メソッドが呼び出されます。  
  
 Wait (Any) モデルの例と同様に、プロセスが完了した時刻が、そのプロセスに対応するテキスト ボックスに追加されます。 ここでも、テキスト ボックス内の時刻がその時点を示します。<xref:System.Threading.WaitHandle.WaitAny%2A> メソッドに続くコードは、すべてのプロセスが完了した後でのみ実行されます。  
  
 この例を設定するには、新しい ASP.NET Web サイト プロジェクトを作成します。 ページ上に 1 つの <xref:System.Web.UI.WebControls.Button> コントロールと 4 つの <xref:System.Web.UI.WebControls.TextBox> コントロールを配置します (各コントロールの既定の名前をそのまま使用します)。  
  
 お使いの環境に応じて接続文字列を変更し、次のコードをフォームのクラスに追加します。  
  
```vb  
' Add these to the top of the class  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Threading  
  
' Add this code to the page's class:  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,
        ' you can retrieve it from a configuration file.
  
        ' If you have not included "Asynchronous Processing=true"
        ' in the connection string, the command will not be able  
        ' to execute asynchronously.  
        Return "Data Source=(local);Integrated Security=SSPI;" & _  
          "Initial Catalog=AdventureWorks;" & _  
          "Asynchronous Processing=true"  
    End Function
    Sub Button1_Click( _  
     ByVal sender As Object, ByVal e As System.EventArgs)  
  
        ' In a real-world application, you might be connecting to
        '  three different servers or databases. For the example,  
        '  we connect to only one.  
        Dim connection1 As New SqlConnection(GetConnectionString())  
        Dim connection2 As New SqlConnection(GetConnectionString())  
        Dim connection3 As New SqlConnection(GetConnectionString())  
  
        ' To keep the example simple, all three asynchronous
        ' processes select a row from the same table. WAITFOR  
        ' commands are used to emulate long-running processes  
        ' that complete after different periods of time.  
        Dim commandText1 As String = _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint + 1 " & _  
         "WHERE ReorderPoint Is Not Null;" & _  
         "WAITFOR DELAY '0:0:01';" & _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint - 1 " & _  
         "WHERE ReorderPoint Is Not Null"  
  
        Dim commandText2 As String = _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint + 1 " & _  
         "WHERE ReorderPoint Is Not Null;" & _  
         "WAITFOR DELAY '0:0:05';" & _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint - 1 " & _  
         "WHERE ReorderPoint Is Not Null"  
  
        Dim commandText3 As String = _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint + 1 " & _  
         "WHERE ReorderPoint Is Not Null;" & _  
         "WAITFOR DELAY '0:0:10';" & _  
         "UPDATE Production.Product " & _  
         "SET ReorderPoint = ReorderPoint - 1 " & _  
         "WHERE ReorderPoint Is Not Null"  
  
        Dim waitHandles(2) As WaitHandle  
  
        Try  
            ' For each process, open a connection and begin execution.  
            ' Use the IAsyncResult object returned by
            ' BeginExecuteReader to add a WaitHandle for the process  
            ' to the array.  
            connection1.Open()  
            Dim command1 As New SqlCommand(commandText1, connection1)  
            Dim result1 As IAsyncResult = _  
             command1.BeginExecuteNonQuery()  
            waitHandles(0) = result1.AsyncWaitHandle  
  
            connection2.Open()  
            Dim command2 As New SqlCommand(commandText2, connection2)  
            Dim result2 As IAsyncResult = _  
             command2.BeginExecuteNonQuery()  
            waitHandles(1) = result2.AsyncWaitHandle  
  
            connection3.Open()  
            Dim command3 As New SqlCommand(commandText3, connection3)  
            Dim result3 As IAsyncResult = _  
             command3.BeginExecuteNonQuery()  
            waitHandles(2) = result3.AsyncWaitHandle  
  
            ' WaitAll waits for all of the processes to complete.  
            ' The return value is True if all processes completed,
            ' False if any process timed out.  
            Dim result As Boolean = _  
             WaitHandle.WaitAll(waitHandles, 60000, False)  
            If result Then  
                Dim rowCount1 As Long = _  
                 command1.EndExecuteNonQuery(result1)  
                TextBox1.Text = _  
                 "Completed " & _  
                 System.DateTime.Now.ToLongTimeString()  
  
                Dim rowCount2 As Long = _  
                 command2.EndExecuteNonQuery(result2)  
                TextBox2.Text = _  
                 "Completed " & _  
                 System.DateTime.Now.ToLongTimeString()  
  
                Dim rowCount3 As Long = _  
                 command3.EndExecuteNonQuery(result3)  
                TextBox3.Text = _  
                 "Completed " & _  
                 System.DateTime.Now.ToLongTimeString()  
            Else  
                Throw New Exception("Timeout")  
            End If  
        Catch ex As Exception  
            TextBox4.Text = ex.ToString  
        End Try  
        connection1.Close()  
        connection2.Close()  
        connection3.Close()  
  
    End Sub  
```  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using System.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,
    //  you can retrieve it from a configuration file.
    //  If you have not included "Asynchronous Processing=true"
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin
        //  execution. Use the IAsyncResult object returned by
        //  BeginExecuteReader to add a WaitHandle for the
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="see-also"></a>関連項目

- [非同期操作](asynchronous-operations.md)
- [ADO.NET の概要](../ado-net-overview.md)
