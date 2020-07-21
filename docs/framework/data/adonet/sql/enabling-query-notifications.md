---
title: クエリ通知の有効化
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.openlocfilehash: 84048a3fba2b32b1ae745160e2b405c04b738c65
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040235"
---
# <a name="enabling-query-notifications"></a>クエリ通知の有効化
クエリ通知を使用するアプリケーションには、いくつか共通する要件があります。 SQL クエリ通知をサポートするには、データ ソースが正しく設定され、ユーザーがクライアント側およびサーバー側の正しい権限を所有している必要があります。  
  
 クエリ通知を使用するためには、次のことが必要です。  
  
- データベースのクエリ通知を有効にします。  
  
- データベースへの接続に使用するユーザー ID に必要なアクセス許可があることを確認します。  
  
- <xref:System.Data.SqlClient.SqlCommand> オブジェクトを使用して、通知オブジェクト (<xref:System.Data.SqlClient.SqlDependency> または <xref:System.Data.Sql.SqlNotificationRequest> のいずれか) が関連付けられている有効な SELECT ステートメントを実行します。  
  
- 監視対象のデータが変更された場合に通知を処理するコードを設定する  
  
## <a name="query-notifications-requirements"></a>クエリ通知の要件  
 クエリ通知は、特定の要件を満たす SELECT ステートメントでのみサポートされます。 次の表に、SQL Server オンライン ブックの Service Broker とクエリ通知のドキュメントへのリンクを示します。  
  
 **SQL Server のドキュメント**  
  
- [通知のためのクエリの作成](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker のセキュリティに関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [セキュリティと保護 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services のセキュリティに関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [クエリ通知の権限](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker の国際化に関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [ソリューション設計に関する考慮事項 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 開発者向けの情報](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開発者ガイド (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>サンプル コードを実行するためのクエリ通知の有効化  
 **AdventureWorks** データベースで Service Broker を有効にするには、SQL Server Management Studio を通じて、次の Transact-SQL ステートメントを実行します。  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 クエリ通知のサンプルを正しく実行するには、次の Transact-SQL ステートメントをデータベース サーバー上で実行する必要があります。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>クエリ通知のアクセス許可  
 通知を要求するコマンドを実行するユーザーは、特定のサーバーに対する SUBSCRIBE QUERY NOTIFICATIONS データベース アクセス許可を必要とします。  
  
 部分的に信頼される状況で実行されるクライアント側のコードには <xref:System.Data.SqlClient.SqlClientPermission> が必要です。  
  
 次のコードは <xref:System.Data.SqlClient.SqlClientPermission> オブジェクトを作成し、<xref:System.Security.Permissions.PermissionState> を <xref:System.Security.Permissions.PermissionState.Unrestricted> に設定します。 <xref:System.Security.CodeAccessPermission.Demand%2A> を指定すると、呼び出し履歴の上流に、権限の付与されていない呼び出し元が 1 つでも存在した場合、実行時に強制的に <xref:System.Security.SecurityException> が発生します。  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## <a name="choosing-a-notification-object"></a>通知オブジェクトの選択  
 クエリ通知 API は、通知を処理するために <xref:System.Data.SqlClient.SqlDependency> と <xref:System.Data.Sql.SqlNotificationRequest> という 2 つのオブジェクトを提供します。 通常、ASP.NET 以外のほとんどのアプリケーションでは、<xref:System.Data.SqlClient.SqlDependency> オブジェクトを使用する必要があります。 ASP.NET アプリケーションは、高レベルの <xref:System.Web.Caching.SqlCacheDependency> を使用する必要があります。これは <xref:System.Data.SqlClient.SqlDependency> をラップし、通知オブジェクトとキャッシュ オブジェクトを管理するためのフレームワークになります。  
  
### <a name="using-sqldependency"></a>SqlDependency の使用  
 <xref:System.Data.SqlClient.SqlDependency> を使用するには、使用する SQL Server データベースに対して Service Broker を有効にし、通知を受け取るためのアクセス許可をユーザーに与える必要があります。 通知キューなどの Service Broker オブジェクトは事前に定義されています。  
  
 さらに、<xref:System.Data.SqlClient.SqlDependency> によってワーカー スレッドが自動的に起動し、キューにポストされた通知が処理されます。また、Service Broker メッセージも解析され、情報がイベント引数データとして公開されます。 <xref:System.Data.SqlClient.SqlDependency> は、`Start` メソッドを呼び出し、データベースに対する依存関係を確立して初期化する必要があります。 これは、必要となる各データベース接続に対するアプリケーションの初期化中に、1 回だけ呼び出す必要のある静的メソッドです。 `Stop` メソッドは、作成された依存関係の接続ごとにアプリケーションの終了時に呼び出す必要があります。  
  
### <a name="using-sqlnotificationrequest"></a>SqlNotificationRequest の使用  
 これに対して、<xref:System.Data.Sql.SqlNotificationRequest> では、リッスンしているインフラストラクチャ全体を自分で実装する必要があります。 さらに、キュー、サービス、およびキューでサポートされているメッセージの種類など、サポート対象となるすべての Service Broker オブジェクトを定義する必要があります。 手動によるこの方法は、使用しているアプリケーションで特殊な通知メッセージや通知動作が必要な場合、またはそのアプリケーションが Service Broker アプリケーションの一部である場合に使用すると便利です。  
  
## <a name="see-also"></a>関連項目

- [SQL Server のクエリ通知](query-notifications-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
