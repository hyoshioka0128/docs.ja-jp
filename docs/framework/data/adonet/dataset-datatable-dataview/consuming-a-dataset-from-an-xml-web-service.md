---
title: XML Web サービスからの DataSet の使用
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9edd6b71-0fa5-4649-ae1d-ac1c12541019
ms.openlocfilehash: d7328949e3eb4822b1a645bb5f0c1866f01ecb0a
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389742"
---
# <a name="consume-a-dataset-from-an-xml-web-service"></a>XML Web サービスからの DataSet の使用

<xref:System.Data.DataSet> は、非接続型デザインで設計されています。インターネットで簡単にデータを転送するのが目的の一部です。 **DataSet** は、**DataSet** の内容を XML Web サービスからクライアントに (およびその逆方向に) ストリーム転送するためのコードを追加せずに XML Web サービスへの入力または出力として指定できるという点で、"シリアル化可能" です。 **DataSet** は、DiffGram 形式を使用して暗黙に XML ストリームに変換され、ネットワーク経由で送信されます。その後、受信側で XML ストリームから **DataSet** として再構築されます。 これにより、XML Web サービスを使用してリレーショナル データを送信および返送する、たいへん簡単で柔軟性のある方法が提供されます。 DiffGram 形式の詳細については、「[DiffGrams](diffgrams.md)」を参照してください。  
  
 **DataSet** を使用してリレーショナル データ (変更データを含む) を転送し、更新内容を元のデータ ソースに反映させる XML Web サービスと XML Web サービスのクライアントを作成する手順を次の例に示します。  
  
> [!NOTE]
> XML Web サービスを作成する場合は、常にセキュリティへの影響を考慮することをお勧めします。 XML Web サービスのセキュリティ保護については、「[ASP.NET を使用して作成した XML Web サービスのセキュリティ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w67h0dw7(v=vs.100))」を参照してください。  
  
## <a name="create-an-xml-web-service"></a>XML Web サービスの作成
  
1. XML Web サービスを作成します。  
  
     この例では、データ (ここでは、**Northwind** データベースの顧客リスト) を返し、元のデータ ソースに反映させるデータ更新が格納されている **DataSet** を受け取る XML Web サービスを作成します。  
  
     この XML Web サービスでは 2 つのメソッドが公開されています。顧客リストを返す **GetCustomers** と、更新をデータ ソースに反映させる **UpdateCustomers** です。 この XML Web サービスは、Web サーバー上の DataSetSample.asmx というファイルに格納されます。 次のコードは、DataSetSample.asmx の内容の概要を示しています。  
  
    ```vb  
    <% @ WebService Language = "vb" Class = "Sample" %>  
    Imports System  
    Imports System.Data  
    Imports System.Data.SqlClient  
    Imports System.Web.Services  
  
    <WebService(Namespace:="http://microsoft.com/webservices/")> _  
    Public Class Sample  
  
    Public connection As SqlConnection = New SqlConnection("Data Source=(local);Integrated Security=SSPI;Initial Catalog=Northwind")  
  
      <WebMethod( Description := "Returns Northwind Customers", EnableSession := False )> _  
      Public Function GetCustomers() As DataSet  
        Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
          "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
        Dim custDS As DataSet = New DataSet()  
        adapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
        adapter.Fill(custDS, "Customers")  
  
        Return custDS  
      End Function  
  
      <WebMethod( Description := "Updates Northwind Customers", EnableSession := False )> _  
      Public Function UpdateCustomers(custDS As DataSet) As DataSet  
        Dim adapter As SqlDataAdapter = New SqlDataAdapter()  
  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Customers (CustomerID, CompanyName) " & _  
          "Values(@CustomerID, @CompanyName)", connection)  
        adapter.InsertCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        adapter.InsertCommand.Parameters.Add( _  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Customers Set CustomerID = @CustomerID, " & _  
          "CompanyName = @CompanyName WHERE CustomerID = " & _  
          @OldCustomerID", connection)  
        adapter.UpdateCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        adapter.UpdateCommand.Parameters.Add( _  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
  
        Dim parameter As SqlParameter = _  
          adapter.UpdateCommand.Parameters.Add( _  
          "@OldCustomerID", SqlDbType.NChar, 5, "CustomerID")  
        parameter.SourceVersion = DataRowVersion.Original  
  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Customers WHERE CustomerID = @CustomerID", _  
          connection)  
        parameter = adapter.DeleteCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        parameter.SourceVersion = DataRowVersion.Original  
  
        adapter.Update(custDS, "Customers")  
  
        Return custDS  
      End Function  
    End Class  
    ```  
  
    ```csharp  
    <% @ WebService Language = "C#" Class = "Sample" %>  
    using System;  
    using System.Data;  
    using System.Data.SqlClient;  
    using System.Web.Services;  
  
    [WebService(Namespace="http://microsoft.com/webservices/")]  
    public class Sample  
    {  
      public SqlConnection connection = new SqlConnection("Data Source=(local);Integrated Security=SSPI;Initial Catalog=Northwind");  
  
      [WebMethod( Description = "Returns Northwind Customers", EnableSession = false )]  
      public DataSet GetCustomers()  
      {  
        SqlDataAdapter adapter = new SqlDataAdapter(  
          "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
        DataSet custDS = new DataSet();  
        adapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
        adapter.Fill(custDS, "Customers");  
  
        return custDS;  
      }  
  
      [WebMethod( Description = "Updates Northwind Customers",  
        EnableSession = false )]  
      public DataSet UpdateCustomers(DataSet custDS)  
      {  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        adapter.InsertCommand = new SqlCommand(  
          "INSERT INTO Customers (CustomerID, CompanyName) " +  
          "Values(@CustomerID, @CompanyName)", connection);  
        adapter.InsertCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        adapter.InsertCommand.Parameters.Add(  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName");  
  
        adapter.UpdateCommand = new SqlCommand(  
          "UPDATE Customers Set CustomerID = @CustomerID, " +  
          "CompanyName = @CompanyName WHERE CustomerID = " +  
          "@OldCustomerID", connection);  
        adapter.UpdateCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        adapter.UpdateCommand.Parameters.Add(  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName");  
        SqlParameter parameter = adapter.UpdateCommand.Parameters.Add(  
          "@OldCustomerID", SqlDbType.NChar, 5, "CustomerID");  
        parameter.SourceVersion = DataRowVersion.Original;  
  
        adapter.DeleteCommand = new SqlCommand(  
        "DELETE FROM Customers WHERE CustomerID = @CustomerID",  
         connection);  
        parameter = adapter.DeleteCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        parameter.SourceVersion = DataRowVersion.Original;  
  
        adapter.Update(custDS, "Customers");  
  
        return custDS;  
      }  
    }  
    ```  
  
     代表的なシナリオでは、**UpdateCustomers** メソッドはオプティミスティック コンカレンシー違反をキャッチするように記述されます。 説明を簡単にするために、この例では UpdateCustmoers メソッドを省略しています。 オプティミスティック コンカレンシーについて詳しくは、「[オプティミスティック コンカレンシー](../optimistic-concurrency.md)」を参照してください。  
  
2. XML Web サービス プロキシを作成します。  
  
     XML Web サービスのクライアントは、公開されたメソッドを使用するために SOAP プロキシを必要とします。 このプロキシは、Visual Studio を使用して生成することができます。 Visual Studio から既存の Web サービスへの Web 参照を設定することにより、この手順で説明されているすべての動作が自動的に実行されます。 プロキシ クラスを手動で作成する場合は、後述の手順を参照してください。 ほとんどの場合、Visual Studio による、クライアント アプリケーションのプロキシ クラスの作成で十分です。  
  
     プロキシは、Web サービス記述言語ツールを使用して作成できます。 たとえば、XML Web サービスを `http://myserver/data/DataSetSample.asmx` の URL に公開する場合は、次のようなコマンドを実行して、名前空間 **WebData.DSSample** を指定した Visual Basic .NET プロキシを作成し、それをファイル sample.vb に格納します。  
  
    ```console
    wsdl /l:VB -out:sample.vb http://myserver/data/DataSetSample.asmx /n:WebData.DSSample  
    ```  
  
     ファイル sample.cs に C# プロキシを作成するには、次のコマンドを実行します。  
  
    ```console
    wsdl -l:CS -out:sample.cs http://myserver/data/DataSetSample.asmx -n:WebData.DSSample  
    ```  
  
     その後、プロキシをライブラリとしてコンパイルし、XML Web サービスのクライアントにインポートします。 sample.vb に格納されている Visual Basic .NET プロキシ コードを sample.dll としてコンパイルするには次のコマンドを実行します。  
  
    ```console  
    vbc -t:library -out:sample.dll sample.vb -r:System.dll -r:System.Web.Services.dll -r:System.Data.dll -r:System.Xml.dll  
    ```  
  
     sample.cs に格納されている C# プロキシ コードを sample.dll としてコンパイルするには次のコマンドを実行します。  
  
    ```console
    csc -t:library -out:sample.dll sample.cs -r:System.dll -r:System.Web.Services.dll -r:System.Data.dll -r:System.Xml.dll  
    ```  
  
3. XML Web サービスのクライアントを作成します。  
  
     Visual Studio で Web サービスのプロキシ クラスを生成する場合は、クライアント プロジェクトを作成し、ソリューション エクスプローラー ウィンドウで、そのプロジェクトを右クリックし、 **[追加]**  >  **[サービス参照]** を選択します。 **[サービス参照の追加]** ダイアログ ボックスで、 **[詳細設定]** を選択し、 **[Web 参照の追加]** を選択します。 使用可能な Web サービスの一覧から Web サービスを選択します (ただし、Web サービスが現行ソリューション内または現在のコンピューター上で使用できない場合は、Web サービス エンドポイントのアドレスを指定する必要があります)。 (上記の手順に従って) XML Web サービス プロキシを作成した場合は、それをクライアント コードにインポートし、XML Web サービスのメソッドを処理できます。

     プロキシ ライブラリをインポートし、**GetCustomers** を呼び出して顧客リストを取得し、新しい顧客を追加した後、更新内容が格納された **DataSet** を **UpdateCustomers** に返すサンプル コードを次に示します。  
  
     この例では、変更された行だけを **UpdateCustomers** に渡す必要があるため、**UpdateCustomers** には、**DataSet.GetChanges** によって返された **DataSet** が渡されます。 **UpdateCustomers** は解決された **DataSet** を返します。その後、この DataSet を既存の **DataSet** に **Merge** して、解決された変更と更新からの行エラー情報を取り込むことができます。 次のコードは、Visual Studio を使用して Web 参照が作成済みで、かつ、 **[Web 参照の追加]** ダイアログ ボックスでその Web 参照の名前が DsSample に変更済みであることが前提となっています。  
  
    ```vb  
    Imports System  
    Imports System.Data  
  
    Public Class Client  
  
      Public Shared Sub Main()  
        Dim proxySample As New DsSample.Sample ()  ' Proxy object.  
        Dim customersDataSet As DataSet = proxySample.GetCustomers()  
        Dim customersTable As DataTable = _  
          customersDataSet.Tables("Customers")  
  
        Dim rowAs DataRow = customersTable.NewRow()  
        row("CustomerID") = "ABCDE"  
        row("CompanyName") = "New Company Name"  
        customersTable.Rows.Add(row)  
  
        Dim updateDataSet As DataSet = _  
          proxySample.UpdateCustomers(customersDataSet.GetChanges())  
  
        customersDataSet.Merge(updateDataSet)  
        customersDataSet.AcceptChanges()  
      End Sub  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using System.Data;  
  
    public class Client  
    {  
      public static void Main()  
      {  
        Sample proxySample = new DsSample.Sample();  // Proxy object.  
        DataSet customersDataSet = proxySample.GetCustomers();  
        DataTable customersTable = customersDataSet.Tables["Customers"];  
  
        DataRow row = customersTable.NewRow();  
        row["CustomerID"] = "ABCDE";  
        row["CompanyName"] = "New Company Name";  
        customersTable.Rows.Add(row);  
  
        DataSet updateDataSet = new DataSet();  
  
        updateDataSet =
          proxySample.UpdateCustomers(customersDataSet.GetChanges());  
  
        customersDataSet.Merge(updateDataSet);  
        customersDataSet.AcceptChanges();  
      }  
    }  
    ```  
  
     プロキシ クラスを手動で作成する場合は、次の手順に従ってください。 このサンプルをコンパイルするには、作成したプロキシ ライブラリ (sample.dll) および関連する .NET ライブラリを指定します。 ファイル client.vb に格納されている Visual Basic .NET バージョンのサンプルをコンパイルするには次のコマンドを実行します。  
  
    ```console
    vbc client.vb -r:sample.dll -r:System.dll -r:System.Data.dll -r:System.Xml.dll -r:System.Web.Services.dll  
    ```  
  
     ファイル client.cs に格納されている C# バージョンのサンプルをコンパイルするには、次のコマンドを実行します。  
  
    ```console
    csc client.cs -r:sample.dll -r:System.dll -r:System.Data.dll -r:System.Xml.dll -r:System.Web.Services.dll  
    ```  
  
## <a name="see-also"></a>関連項目

- [ADO.NET](../index.md)
- [DataSet、DataTable、および DataView](index.md)
- [DataTables](datatables.md)
- [DataAdapter からの DataSet の読み込み](../populating-a-dataset-from-a-dataadapter.md)
- [DataAdapter によるデータ ソースの更新](../updating-data-sources-with-dataadapters.md)
- [DataAdapter パラメーター](../dataadapter-parameters.md)
- [Web サービス記述言語ツール (Wsdl.exe)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7h3ystb6(v=vs.100))
- [ADO.NET の概要](../ado-net-overview.md)
