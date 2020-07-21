---
title: SQL Server Express ユーザー インスタンス
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.openlocfilehash: 2bd67a9315eda4161d4b76e1638f5c08f9598a52
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174486"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express ユーザー インスタンス
Microsoft SQL Server Express Edition (SQL Server Express) でサポートされる機能に、ユーザー インスタンスがあります。ユーザー インスタンスは、.NET Framework Data Provider for SQL Server (`SqlClient`) を使用している場合にしか利用できません。 ユーザー インスタンスは、親インスタンスによって生成される SQL Server Express データベース エンジンの独立したインスタンスです。 ユーザー インスタンスを使用すると、ローカル コンピューター上の管理者以外のユーザーが、SQL Server Express データベースにアタッチして接続することができます。 それぞれのインスタンスは、1 ユーザーあたり 1 インスタンスの原則に基づいて、個々のユーザーのセキュリティ コンテキストで実行されます。  
  
## <a name="user-instance-capabilities"></a>ユーザー インスタンスの機能  
 ユーザー インスタンスは、最小特権のユーザー アカウント (LUA) で Windows を実行しているユーザーに役立ちます。 各ユーザーは、Windows 管理者として実行する必要なしに、コンピューター上で実行されているインスタンスに対して SQL Server システム管理者 (`sysadmin`) の特権を持ちます。 SQL Server Express のユーザー インスタンスは、サービスではなく、そのユーザーの非管理者 Windows アカウントで実行されるため、ユーザー インスタンス上で実行されているソフトウェアは権限が限定され、システム全体に及ぶ変更を行うことはできません。 各ユーザー インスタンスは、その親インスタンスや同じコンピューター上で実行されている他のユーザー インスタンスとは分離されます。 ユーザー インスタンスで実行されるデータベースはシングル ユーザー モードでのみ開かれるので、ユーザー インスタンスで実行されているデータベースに複数のユーザーが接続することはできません。 ユーザー インスタンスでは、レプリケーションと分散クエリも無効になります。
  
> [!NOTE]
> 既にコンピューターの管理者であるユーザーが、ユーザー インスタンスを使用する必要はありません。また、複数のデータベース ユーザーが関係する場合もユーザー インスタンスは不要です。  
  
## <a name="enabling-user-instances"></a>ユーザー インスタンスの有効化  
 ユーザー インスタンスを生成するには、SQL Server Express の親インスタンスが実行されている必要があります。 SQL Server Express がインストールされている場合は、ユーザー インスタンスが既定で有効になります。また、システム管理者は、親インスタンスに対して **sp_configure** システム ストアド プロシージャを実行することで、ユーザー インスタンスの有効と無効を明示的に切り替えることもできます。  
  
```sql  
-- Enable user instances.  
sp_configure 'user instances enabled','1'
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
 ユーザー インスタンスのネットワーク プロトコルは、ローカルの名前付きパイプである必要があります。 ユーザー インスタンスを SQL Server のリモート インスタンスで開始することはできません。また、SQL Server ログインは許可されません。  
  
## <a name="connecting-to-a-user-instance"></a>ユーザー インスタンスへの接続  
 `User Instance` および `AttachDBFilename`<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> キーワードによって、<xref:System.Data.SqlClient.SqlConnection> でユーザー インスタンスに接続できます。 ユーザー インスタンスは、<xref:System.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` および `AttachDBFilename` プロパティによってもサポートされています。  
  
 下に示す接続文字列の例については、次の点に注意してください。  
  
- `Data Source` キーワードは、ユーザー インスタンスを生成している SQL Server Express の親インスタンスを参照します。 既定のインスタンスは .\sqlexpress です。  
  
- `Integrated Security` が `true` に設定されます。 ユーザー インスタンスに接続するには、Windows 認証が必要です。SQL Server ログインはサポートされていません。  
  
- `User Instance` は `true` に設定されます。これにより、ユーザー インスタンスが呼び出されます。 既定値は `false` です。  
  
- `AttachDbFileName` 接続文字列キーワードは、プライマリ データベース ファイル (.mdf) をアタッチするために使用されます。これには、完全なパス名を含める必要があります。 また、`AttachDbFileName` は <xref:System.Data.SqlClient.SqlConnection> 接続文字列内の "extended properties" キーと "initial file name" キーにも対応しています。  
  
- パイプ記号で囲まれた `|DataDirectory|` 置換文字列は、接続を開いているアプリケーションのデータ ディレクトリを参照しするもので、.mdf (データベース ファイル) および .ldf (ログ ファイル) の場所を示す相対パスを指定します。 これらのファイルを別の場所に配置する場合は、ファイルへの完全なパスを指定する必要があります。  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
> 実行時に接続文字列を作成するために <xref:System.Data.SqlClient.SqlConnectionStringBuilder><xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> および <xref:System.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> プロパティを使用することもできます。  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>&#124;DataDirectory&#124; 置換文字列の使用  
 ADO.NET 2.0 では、`AttachDbFileName` が拡張されて、`|DataDirectory|` というパイプ記号で囲まれた置換文字列が導入されました。 `DataDirectory` に `AttachDbFileName` を組み合わせて使用することで、データ ファイルへの相対パスを指定でき、完全パスを使用する代わりに、データ ソースの相対パスに基づいて接続文字列を作成できます。  
  
 `DataDirectory` が参照する物理的な場所は、アプリケーションの種類によって異なります。 この例では、アタッチする Northwind.mdf ファイルは、アプリケーションの \app_data フォルダーにあります。  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
 `DataDirectory` を使用する場合、結果として得られるファイル パスは、置換文字列によって参照されるディレクトリよりもディレクトリ構造の上位に配置することはできません。 たとえば、完全に展開された `DataDirectory` が C:\AppDirectory\app_data である場合、上記の例の接続文字列は C:\AppDirectory より下位であるため機能します。 しかし、`DataDirectory` を「`|DataDirectory|\..\data`」として指定すると、\data が \AppDirectory のサブディレクトリではないため、エラーが発生します。  
  
 接続文字列に不適切な形式の置換文字列が含まれている場合、<xref:System.ArgumentException> がスローされます。  
  
> [!NOTE]
> <xref:System.Data.SqlClient> により、置換文字列がローカル コンピューターのファイル システムに対して完全パスに解決されます。 そのため、リモート サーバー、HTTP、および UNC の各パス名はサポートされていません。 サーバーがローカル コンピューターに配置されていない場合、接続が開かれると例外がスローされます。  
  
 <xref:System.Data.SqlClient.SqlConnection> が開かれると、既定の SQL Server Express インスタンスから、実行時に開始された (呼び出し元アカウントで実行される) インスタンスへとリダイレクトされます。  
  
> [!NOTE]
> ユーザー インスタンスは通常のインスタンスよりも読み込みに時間がかかるため、<xref:System.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> の値を大きくすることが必要になる場合があります。  
  
 次のコード フラグメントでは、新しい `SqlConnection`が開かれ、コンソール ウィンドウに接続文字列が表示された後、`using` コードブロックが終了した時点で接続が閉じられます。  
  
```vb  
Private Sub OpenSqlConnection()  
    ' Retrieve the connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    Using connection As New SqlConnection(connectionString)  
        connection.Open()  
        Console.WriteLine("ConnectionString: {0}", _  
           connection.ConnectionString)  
    End Using  
End Sub  
```  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
> ユーザー インスタンスは、SQL Server 内で実行されている共通言語ランタイム (CLR) コードではサポートされていません。 <xref:System.InvalidOperationException> の接続文字列で `Open` を指定して <xref:System.Data.SqlClient.SqlConnection> を呼び出すと、`User Instance=true` がスローされます。  
  
## <a name="lifetime-of-a-user-instance-connection"></a>ユーザー インスタンスの接続の有効期間  
 SQL Server にはサービスとして実行されるバージョンもありますが、それらのバージョンとは異なり、SQL Server Express のインスタンスは、開始と停止を手動で行う必要はありません。 ユーザーがログインしてユーザー インスタンスに接続するたびに、ユーザー インスタンスが起動されます (まだ実行されていない場合)。 ユーザー インスタンス データベースでは `AutoClose` オプションが設定されており、非アクティブな状態が一定期間続くとデータベースが自動的にシャットダウンされます。 開始された sqlservr.exe プロセスは、インスタンスへの最後の接続が終了した後、一定のタイムアウト期間、実行されたままになります。そのため、タイムアウトの期限が切れる前であれば、別の接続を開いても再起動する必要がありません。 タイムアウト期間が過ぎるまでに新しい接続が開かれないと、ユーザー インスタンスは自動的にシャットダウンされます。 親インスタンスのシステム管理者は、**sp_configure** を使用し、**user instance timeout** オプションを変更することにより、ユーザー インスタンスのタイムアウト期間を設定できます。 既定値は、60 分です。  
  
> [!NOTE]
> 接続文字列の `Min Pool Size` に 0 を超える値を指定した場合、接続プーラーは、開かれているいくつかの接続を常に保持するようになります。この場合、ユーザー インスタンスは自動的にはシャットダウンされません。  
  
## <a name="how-user-instances-work"></a>ユーザー インスタンスの動作  
 各ユーザーに対して最初にユーザー インスタンスが生成された時点で、そのユーザー インスタンスによって排他的に使用されるユーザーのローカル アプリケーション データ リポジトリ ディレクトリの下位パスに、Template Data フォルダーからシステム データベース **master** および **msdb** がコピーされます。 通常、このパスは `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS` です。 ユーザー インスタンスが開始されると、**tempdb**、ログ、トレース ファイルもこのディレクトリに書き込まれます。 インスタンスに対して名前が生成され、この名前はユーザーごとに一意であることが保証されます。  
  
 既定では、Windows Builtin\Users グループのすべてのメンバーには、ローカル インスタンスで接続するためのアクセス許可と、SQL Server バイナリに対する読み取りおよび実行のアクセス許可が付与されます。 ユーザー インスタンスをホストしている呼び出し元ユーザーの資格情報が検証されると、そのユーザーはそのインスタンスの `sysadmin` になります。 ユーザー インスタンスに対しては共有メモリのみが有効になっています。つまり、ローカル コンピューター上での操作のみを行うことができます。  
  
 ユーザーには、接続文字列で指定された .mdf ファイルと .ldf ファイルに対する読み取りと書き込みの両方のアクセス許可が付与されている必要があります。  
  
> [!NOTE]
> .mdf ファイルと .ldf ファイルは、それぞれデータベース ファイルとログ ファイルを表します。 これら 2 つのファイルは対応したセットであるため、バックアップ操作と復元操作では注意する必要があります。 データベース ファイルには、ログ ファイルの正確なバージョンに関する情報が含まれているため、不適切なログ ファイルと組み合わせるとデータベースは開かれません。  
  
 データの破損を防ぐために、ユーザー インスタンス内のデータベースは排他アクセスで開かれます。 同じコンピューター上の同じデータベースを 2 つの異なるユーザー インスタンスで共有する場合は、一方のインスタンスのユーザーがデータベースを閉じる必要があります。データベースを閉じない限り、もう一方のインスタンスでそのデータベースを開くことはできません。  
  
## <a name="user-instance-scenarios"></a>ユーザー インスタンスのシナリオ  
 データベース アプリケーションの開発者は、ユーザー インスタンスを使用することで、開発コンピューター上に自分の管理者アカウントがなくても、SQL Server のデータ ストアを自由に利用できるようになります。 ユーザー インスタンスは Access/Jet モデルに基づいています。このモデルでは、データベース アプリケーションは単純にファイルに接続し、ユーザーはすべてのデータベース オブジェクトに対する完全なアクセス許可を自動的に付与されます。つまり、システム管理者が介入してアクセス許可を付与する必要はありません。 これは、ユーザーが最小限の特権を持つユーザー アカウント (LUA) で実行しており、サーバーまたはローカル コンピューターに対する管理特権を持っていないが、データベース オブジェクトおよびアプリケーションを作成する必要がある状況で機能することを目的としています。 ユーザー インスタンスを使用すると、より高い特権を持つシステム サービスのセキュリティ コンテキストではなく、ユーザー自身のセキュリティ コンテキストで実行されるインスタンスを実行時に作成できます。  
  
> [!IMPORTANT]
> ユーザー インスタンスは、それを使用するすべてのアプリケーションが完全に信頼されているシナリオでのみ使用してください。  
  
 ユーザー インスタンスのシナリオには、次のようなものがあります。  
  
- データを共有する必要がないシングル ユーザー アプリケーション。  
  
- ClickOnce 配置。 .NET Framework 2.0 以降および SQL Server Express が既にターゲット コンピューターにインストールされている場合、管理者以外のユーザーでも、ClickOnce アクションの結果としてダウンロードされたインストール パッケージをインストールして使用できます。 ただし、SQL Server Express がセットアップの一部として含まれている場合は、管理者が SQL Server Express をインストールする必要があります。 詳細については、「[Windows フォーム用の ClickOnce 配置](../../../winforms/clickonce-deployment-for-windows-forms.md)」を参照してください。
  
- Windows 認証を使用した専用 ASP.NET ホスティング。 1 つの SQL Server Express インスタンスをイントラネット上でホストできます。 アプリケーションは、偽装を使用するのではなく、ASPNET Windows アカウントを使用して接続します。 サードパーティ製品を使ったホスティングや共有ホスティングのシナリオでユーザー インスタンスを使用することは避けてください。すべてのアプリケーションで同じユーザー インスタンスが使用され、アプリケーションを互いに分離することができなくなります。  
  
## <a name="see-also"></a>関連項目

- [SQL Server と ADO.NET](index.md)
- [接続文字列](../connection-strings.md)
- [データ ソースへの接続](../connecting-to-a-data-source.md)
- [ADO.NET の概要](../ado-net-overview.md)
