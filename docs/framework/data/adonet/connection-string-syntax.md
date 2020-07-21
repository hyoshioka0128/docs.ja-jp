---
title: 接続文字列の構文
description: ADO.NET の接続文字列の構文について説明します。 各プロバイダーの構文は、対応する ConnectionString プロパティのトピックで説明されています。
ms.date: 05/22/2018
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
ms.openlocfilehash: bb29365a4729e731ddeffc7cfa61e379c3144a46
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287052"
---
# <a name="connection-string-syntax"></a>接続文字列の構文
すべての .NET Framework データ プロバイダーは、`Connection` を継承する <xref:System.Data.Common.DbConnection> オブジェクトに加え、プロバイダー固有の <xref:System.Data.Common.DbConnection.ConnectionString%2A> プロパティを持ちます。 それぞれのプロバイダーに固有の接続文字列の構文は、対応する `ConnectionString` プロパティのトピックで説明されています。 次の表は、.NET Framework に含まれている 4 つのデータ プロバイダーを一覧にしたものです。  
  
|.NET Framework データ プロバイダー|説明|  
|----------------------------------|-----------------|  
|<xref:System.Data.SqlClient>|Microsoft SQL Server へのデータ アクセスを提供します。 接続文字列の構文の詳細については、「<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。|  
|<xref:System.Data.OleDb>|OLE DB を使って公開されたデータ ソースへのデータ アクセスを提供します。 接続文字列の構文の詳細については、「<xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>」を参照してください。|  
|<xref:System.Data.Odbc>|ODBC を使って公開されたデータ ソースへのデータ アクセスを提供します。 接続文字列の構文の詳細については、「<xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A>」を参照してください。|  
|<xref:System.Data.OracleClient>|Oracle バージョン 8.1.7 以降へのデータ アクセスを提供します。 接続文字列の構文の詳細については、「<xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>」を参照してください。|  
  
## <a name="connection-string-builders"></a>接続文字列ビルダー  
 ADO.NET 2.0 では、.NET Framework データ プロバイダー用の次の接続文字列ビルダーが導入されました。  
  
- <xref:System.Data.SqlClient.SqlConnectionStringBuilder>  
  
- <xref:System.Data.OleDb.OleDbConnectionStringBuilder>  
  
- <xref:System.Data.Odbc.OdbcConnectionStringBuilder>  
  
- <xref:System.Data.OracleClient.OracleConnectionStringBuilder>  
  
 接続文字列ビルダーを使用すると、構文的に正しい接続文字列を実行時に構築できるため、コード内で接続文字列値を手動で連結する必要はありません。 詳細については、「[接続文字列ビルダー](connection-string-builders.md)」をご覧ください。  

## <a name="windows-authentication"></a>Windows 認証  
 データ ソースでサポートされている場合は、Windows 認証 ("*統合セキュリティ*" とも呼ばれます) を使用して接続することをお勧めします。 接続文字列の構文は、プロバイダーによって異なります。 .NET Framework データ プロバイダーで使用されている Windows 認証の構文を次の表に示します。  
  
|プロバイダー|構文|  
|--------------|------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  
|`OleDb`|`Integrated Security=SSPI;`|  
|`Odbc`|`Trusted_Connection=yes;`|  
|`OracleClient`|`Integrated Security=yes;`|  
  
> [!NOTE]
> `Integrated Security=true` プロバイダーで `OleDb` に設定すると例外がスローされます。  
  
## <a name="sqlclient-connection-strings"></a>SqlClient 接続文字列  
<xref:System.Data.SqlClient.SqlConnection> 接続文字列の構文については、<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> プロパティで説明されています。 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> プロパティを使用すると、SQL Server データベースの接続文字列を取得または設定することができます。 以前のバージョンの SQL Server に接続する必要がある場合は、.NET Framework Data Provider for OleDb (<xref:System.Data.OleDb>) を使用する必要があります。 接続文字列のほとんどのキーワードは、<xref:System.Data.SqlClient.SqlConnectionStringBuilder> のプロパティにマップされています。  

> [!IMPORTANT]
> `Persist Security Info` キーワードの既定の設定は `false` です。 このキーワードを `true` または `yes` に設定すると、ユーザー ID やパスワードなどのセキュリティ関連情報を、接続を開いた後にその接続から取得できます。 機密を要する接続文字列情報が、信頼できないソースによってアクセスされることのないよう、`Persist Security Info` は必ず `false` にしてください。  

### <a name="windows-authentication-with-sqlclient"></a>SqlClient での Windows 認証
 次の構文のフォームはそれぞれ、Windows 認証を使用してローカル サーバー上の **AdventureWorks** データベースに接続します。  
  
```csharp  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  
  
### <a name="sql-server-authentication-with-sqlclient"></a>SqlClient での SQL Server 認証
 SQL Server への接続には Windows 認証の使用をお勧めします。 ただし、どうしても SQL Server 認証を使用する必要がある場合は、次の構文に従ってユーザー名とパスワードを指定してください。 この例では、アスタリスクを使用して有効なユーザー名とパスワードを表しています。  
  
```csharp  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  

Azure SQL Database または Azure SQL Data Warehouse に接続し、`user@servername` の形式でログインを指定する場合は、ログインの `servername` の値が `Server=` に指定されている値と一致することを確認します。

> [!NOTE]
> Windows 認証は SQL Server ログインよりも優先されます。 Integrated Security を true に指定し、ユーザー名とパスワードも指定した場合、ユーザー名とパスワードは無視され、Windows 認証が使用されます。  

### <a name="connect-to-a-named-instance-of-sql-server"></a>SQL Server の名前付きインスタンスに接続する
SQL Server の名前付きインスタンスに接続するには、*server name\instance name* 構文を使用します。  
  
```csharp  
"Data Source=MySqlServer\MSSQL1;"  
```  

接続文字列の作成時に、<xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> の `SqlConnectionStringBuilder` プロパティをインスタンス名に設定することもできます。 <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> オブジェクトの <xref:System.Data.SqlClient.SqlConnection> プロパティは読み取り専用です。  
  
### <a name="type-system-version-changes"></a>Type System Version の変更  
 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> の `Type System Version` キーワードは、クライアント側での SQL Server 型の表現を指定します。 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> キーワードの詳細については、`Type System Version` のトピックを参照してください。  
  
## <a name="connecting-and-attaching-to-sql-server-express-user-instances"></a>SQL Server Express ユーザー インスタンスへの接続とアタッチ  
 ユーザー インスタンスは、SQL Server Express の機能の 1 つです。 最小限の特権しか持たないローカル Windows アカウントで実行しているユーザーが、SQL Server データベースにアタッチできます。この場合、管理特権は不要です。 ユーザー インスタンスは、サービスとしてではなく、ユーザーの Windows 資格情報で実行されます。  
  
 ユーザー インスタンスの使用について詳しくは、「[SQL Server Express ユーザー インスタンス](./sql/sql-server-express-user-instances.md)」をご覧ください。  
  
## <a name="using-trustservercertificate"></a>TrustServerCertificate の使用  
 `TrustServerCertificate` キーワードは、有効な証明書を使用して SQL Server インスタンスに接続する場合にのみ使用できます。 `TrustServerCertificate` を `true` に設定した場合、トランスポート層に SSL が使用されてチャネルが暗号化されます。また、証明書チェーンをたどることによる信頼性の検証は省略されます。  
  
```csharp  
"TrustServerCertificate=true;"
```  
  
> [!NOTE]
> `TrustServerCertificate` を `true` に設定して暗号化を有効にした場合、接続文字列で `Encrypt` を `false` に設定したとしても、サーバーで指定された暗号化レベルが使用されます。 それ以外の場合、接続は失敗します。  
  
### <a name="enabling-encryption"></a>暗号化の有効化  
 サーバー証明書がプロビジョニングされていない場合、暗号化を有効にするには、SQL Server 構成マネージャーで **[プロトコルの暗号化を設定する]** オプションと **[サーバー証明書を信頼する]** オプションを設定する必要があります。 このように、検証可能なサーバー証明書がプロビジョニングされていない場合、暗号化には検証を伴わない自己署名入りのサーバー証明書が使用されます。  
  
 SQL Server で構成されたセキュリティのレベルを、アプリケーションの設定によって緩和することはできません。ただし、必要に応じて厳密にすることはできます。 アプリケーションから暗号化を要求するには、`TrustServerCertificate` キーワードおよび `Encrypt` キーワードを `true` に設定します。こうすることで、サーバー証明書がプロビジョニングされておらず、なおかつ、クライアントで **[プロトコルの暗号化を設定する]** が構成されていない場合でも常に暗号化が行われます。 ただし、クライアントの構成で `TrustServerCertificate` を有効にしなかった場合は、プロビジョニングされたサーバー証明書が必要です。  
  
 次の表ですべてのケースを説明します。  
  
|[プロトコルの暗号化を設定する] クライアント設定|[サーバー証明書を信頼する] クライアント設定|Encrypt/Use Encryption for Data 接続文字列/属性|Trust Server Certificate 接続文字列/属性|結果|  
|----------------------------------------------|---------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|------------|  
|いいえ|N/A|無効 (既定値)|無視|暗号化は行われません。|  
|いいえ|N/A|はい|無効 (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|いいえ|N/A|はい|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|いいえ|無視|無視|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|はい|無効 (既定値)|無視|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|はい|はい|無効 (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|はい|はい|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
  
 詳細については、「[検証を伴わない暗号化の使用](/sql/relational-databases/native-client/features/using-encryption-without-validation)」を参照してください。
  
## <a name="oledb-connection-strings"></a>OleDb 接続文字列  
 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> の <xref:System.Data.OleDb.OleDbConnection> プロパティを使用すると、Microsoft Access などの OLE DB データ ソースの接続文字列を取得または設定することができます。 `OleDb` クラスを使用して、実行時に <xref:System.Data.OleDb.OleDbConnectionStringBuilder> 接続文字列を作成することもできます。  
  
### <a name="oledb-connection-string-syntax"></a>OleDb 接続文字列の構文  
 <xref:System.Data.OleDb.OleDbConnection> 接続文字列では、プロバイダー名を指定する必要があります。 次の接続文字列は、Jet プロバイダーを使用して Microsoft Access データベースに接続します。 `User ID` および `Password` キーワードは、データベースがセキュリティ保護されていない場合は省略できます (既定)。  
  
```csharp
Provider=Microsoft.Jet.OLEDB.4.0; Data Source=d:\Northwind.mdb;User ID=Admin;Password=;
```  
  
 ユーザー レベルのセキュリティを使用して Jet データベースがセキュリティ保護されている場合は、ワークグループ情報ファイル (.mdw) の場所を指定する必要があります。 ワークグループ情報ファイルを使用して接続文字列に表示された資格情報を検証します。  
  
```csharp
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=d:\Northwind.mdb;Jet OLEDB:System Database=d:\NorthwindSystem.mdw;User ID=*****;Password=*****;  
```  
  
> [!IMPORTANT]
> **OleDbConnection** の接続情報は、UDL (Universal Data Link) ファイルを使用して提供できますが、このファイルは使用しないでください。 UDL ファイルは暗号化されないため、接続文字列をテキスト形式で表現してしまいます。 UDL ファイルは、アプリケーションにとって外部ファイルをベースにしたリソースであるため、.NET Framework でセキュリティ保護できません。 UDL ファイルは **SqlClient** ではサポートされていません。  
  
### <a name="using-datadirectory-to-connect-to-accessjet"></a>DataDirectory を使用した Access/Jet との接続  
 `DataDirectory` の使用は `SqlClient` に限定されません。 <xref:System.Data.OleDb> および <xref:System.Data.Odbc> .NET データ プロバイダーでも使用できます。 アプリケーションの app_data フォルダーに格納された Northwind.mdb に接続するための <xref:System.Data.OleDb.OleDbConnection> 文字列の構文を次の例に示します。 この場所には、システム データベース (System.mdw) も格納されています。  
  
```csharp  
"Provider=Microsoft.Jet.OLEDB.4.0;  
Data Source=|DataDirectory|\Northwind.mdb;  
Jet OLEDB:System Database=|DataDirectory|\System.mdw;"  
```  
  
> [!IMPORTANT]
> Access/Jet データベースをセキュリティで保護しない場合は、接続文字列にシステム データベースの場所を指定する必要はありません。 既定では、セキュリティが無効になります。すべてのユーザーが、空のパスワードで組み込みの Admin ユーザーとして接続することになります。 ユーザー レベルのセキュリティを正しく実装したとしても、Jet データベースは攻撃に対して無防備です。 ファイル ベースのセキュリティでは克服できない限界があるため、Access/Jet データベースに機密情報を格納することはお勧めできません。  
  
### <a name="connecting-to-excel"></a>Excel への接続  
 Excel ワークブックへの接続には、Microsoft Jet プロバイダーが使用されます。 次の接続文字列では、`Extended Properties` キーワードは Excel に固有のプロパティを設定しています。 「HDR=Yes;」は最初の列にデータではなく行の名前が含まれていることを示し、「IMEX=1;」は "intermixed" データ行を常にテキストとして読み取ることをドライバーに指示しています。  
  
```csharp
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\MyExcel.xls;Extended Properties=""Excel 8.0;HDR=Yes;IMEX=1""  
```  
  
 `Extended Properties` を二重引用符で囲む必要があることに注意してください。  
  
### <a name="data-shape-provider-connection-string-syntax"></a>Data Shape プロバイダーの接続文字列の構文  
 Microsoft Data Shape プロバイダーを使用するときは、`Provider` および `Data Provider` キーワードを両方使用してください。 Shape プロバイダーを使用して SQL Server のローカル インスタンスに接続する例を次に示します。  
  
```csharp  
"Provider=MSDataShape;Data Provider=SQLOLEDB;Data Source=(local);Initial Catalog=pubs;Integrated Security=SSPI;"
```  
  
## <a name="odbc-connection-strings"></a>Odbc 接続文字列  
 <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A> の <xref:System.Data.Odbc.OdbcConnection> プロパティを使用すると、OLE DB データベースで接続文字列を取得または設定することができます。 <xref:System.Data.Odbc.OdbcConnectionStringBuilder> は、Odbc の接続文字列もサポートしています。  
  
 次の接続文字列では、Microsoft Text Driver を使用しています。  
  
```csharp  
Driver={Microsoft Text Driver (*.txt; *.csv)};DBQ=d:\bin  
```  
  
### <a name="using-datadirectory-to-connect-to-visual-foxpro"></a>DataDirectory を使用した Visual FoxPro との接続  
 次の <xref:System.Data.Odbc.OdbcConnection> 接続文字列は、`DataDirectory` を使用して Microsoft Visual FoxPro ファイルに接続する例を示しています。  
  
```csharp  
"Driver={Microsoft Visual FoxPro Driver};  
SourceDB=|DataDirectory|\MyData.DBC;SourceType=DBC;"  
```  
  
## <a name="oracle-connection-strings"></a>Oracle 接続文字列  
 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> の <xref:System.Data.OracleClient.OracleConnection> プロパティを使用すると、OLE DB データベースで接続文字列を取得または設定することができます。 <xref:System.Data.OracleClient.OracleConnectionStringBuilder> は、Oracle の接続文字列もサポートしています。  
  
```csharp
Data Source=Oracle9i;User ID=*****;Password=*****;  
```  
  
 ODBC 接続文字列の構文の詳細については、「<xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [接続文字列](connection-strings.md)
- [データ ソースへの接続](connecting-to-a-data-source.md)
- [ADO.NET の概要](ado-net-overview.md)
