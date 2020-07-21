---
title: SQL Server のデータベース ミラーリング
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.openlocfilehash: b18c67f5573d375fe0872d76d69a1f0aafa7e7f6
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040439"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server のデータベース ミラーリング
SQL Server のデータベース ミラーリング機能を使用すると、スタンバイ サーバー上に SQL Server データベースのコピー (ミラー) を保持できます。 ミラーリングは、常にデータのコピーが 2 つ別々に存在することを保証し、高可用性とデータの完全な冗長性をもたらします。 .NET Data Provider for SQL Server では、データベース ミラーリングが暗黙的にサポートされているため、SQL Server データベース用に構成されている場合は、開発者が操作を行ったり、コードを作成したりする必要はありません。 さらに、<xref:System.Data.SqlClient.SqlConnection> オブジェクトは、<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 内のフェールオーバー パートナー サーバーの名前を指定できる明示的な接続モードをサポートします。  
  
 簡略化された次の一連のイベントは、ミラーリング用に構成されたデータベースをターゲットにする <xref:System.Data.SqlClient.SqlConnection> オブジェクトに対して発生します。  
  
1. クライアント アプリケーションがプリンシパル データベースに正常に接続し、サーバーがパートナー サーバーの名前を送り返します。その後、その名前がクライアントでキャッシュされます。  
  
2. プリンシパル データベースを含むサーバーに障害が発生、または接続が中断された場合、接続およびトランザクション状態は失われます。 クライアント アプリケーションがプリンシパル データベースへの接続を再確立しようとして失敗します。  
  
3. 次に、クライアント アプリケーションがパートナー サーバー上のミラー データベースへの接続を透過的に確立しようとします。 この処理に成功すると、新しいプリンシパル データベースとなるミラー データベースに、接続がリダイレクトされます。  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>接続文字列でのフェールオーバー パートナーの指定  
 接続文字列でフェールオーバー パートナー サーバーの名前を指定すると、クライアント アプリケーションが最初に接続するときにプリンシパル データベースを使用できない場合、クライアントはフェールオーバー パートナーへの接続を透過的に試行します。  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
 フェールオーバー パートナー サーバーの名前を省略すると、クライアント アプリケーションの最初の接続時にプリンシパル データベースが使用できない場合、<xref:System.Data.SqlClient.SqlException> が生成されます。  
  
 <xref:System.Data.SqlClient.SqlConnection> が正常に開かれた場合は、サーバーからフェールオーバー パートナー名が返され、接続文字列で指定されたすべての値と置き換わります。  
  
> [!NOTE]
> データベース ミラーリングのシナリオでは、接続文字列で初期カタログまたはデータベース名を明示的に指定する必要があります。 クライアントが、初期カタログやデータベースが明示的に指定されていない接続に関するフェールオーバー情報を受信する場合は、このフェールオーバー情報はキャッシュされず、アプリケーションはプリンシパル サーバーでの障害発生時にフェールオーバーを試行しません。 接続文字列にフェールオーバー パートナーの値が含まれていても、初期カタログまたはデータベースの値が含まれていない場合、`InvalidArgumentException` が発生します。  
  
## <a name="retrieving-the-current-server-name"></a>現在のサーバー名の取得  
 フェールオーバーの場合には、<xref:System.Data.SqlClient.SqlConnection.DataSource%2A> オブジェクトの <xref:System.Data.SqlClient.SqlConnection> プロパティを使って、現在の接続が実際に接続されているサーバーの名前を取得できます。 次のコード フラグメントでは、接続変数が開いている <xref:System.Data.SqlClient.SqlConnection> を参照していることを前提として、アクティブなサーバーの名前を取得します。  
  
 フェールオーバー イベントが発生し、接続がミラー サーバーに切り替えられた場合は、**DataSource** プロパティがそのミラー名を反映するように更新されます。  
  
```vb  
Dim activeServer As String = connection.DataSource  
```  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient ミラーリングの動作  
 クライアントは、常に現在のプリンシパル サーバーに接続しようとします。 それが失敗すると、フェールオーバー パートナーを試します。 ミラー データベースが既にパートナー サーバー上のプリンシパル ロールに切り替えられている場合、接続は成功し、新しいプリンシパル/ミラーのマッピングがクライアントに送信され、<xref:System.AppDomain> の呼び出しが有効な間はキャッシュされます。 このマッピングは永続ストレージには格納されないため、別の **AppDomain** 内またはプロセス内で次回の接続に使用することはできません。 ただし、同一の **AppDomain** 内では次回の接続に使用できます。 同一または別のコンピューター上で実行されている、別の **AppDomain** またはプロセスには常に接続のプールがあり、これらの接続はリセットされません。 このとき、プライマリ データベースがダウンし、各プロセスまたは **AppDomain** が失敗した場合、プールは自動的に消去されます。  
  
> [!NOTE]
> サーバー上のミラーリングのサポートは、データベースごとに構成されます。 マルチパート名を使用するか、または現在のデータベースを変更し、プリンシパル/ミラー セットに含まれていない他のデータベースに対してデータ操作が行われた場合、障害が発生したときは、これらの他のデータベースへの変更は伝播されません。 ミラー化されていないデータベースでデータが変更されても、エラーは生成されません。 開発者は、このような操作の考えられる影響を評価する必要があります。  
  
## <a name="database-mirroring-resources"></a>データベース ミラーリングに関するリソース  
 ミラーリングの構成、配置、管理の概念に関するドキュメントや情報については、SQL Server ドキュメントの次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[データベース ミラーリング](/sql/database-engine/database-mirroring/database-mirroring-sql-server)|SQL Server でのミラーリングの設定と構成方法について説明します。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
