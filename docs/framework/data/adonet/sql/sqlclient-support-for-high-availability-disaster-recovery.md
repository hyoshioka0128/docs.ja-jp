---
title: 高可用性障害復旧のための SqlClient サポート
description: AlwaysOn 可用性グループを使用した、SQL Server での高可用性、ディザスター リカバリーのための SqlClient アプリケーション サポートについて説明します。
ms.date: 03/30/2017
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.openlocfilehash: eba243d37db8262970d161cfa786d3aee4462950
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286211"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>高可用性障害復旧のための SqlClient サポート
このトピックでは、高可用性、ディザスター リカバリーのための SqlClient サポート (.NET Framework 4.5 で追加) である AlwaysOn 可用性グループについて説明します。  AlwaysOn 可用性グループの機能は SQL Server 2012 に追加されています。 AlwaysOn 可用性グループの詳細については、SQL Server オンライン ブックを参照してください。  
  
 現在は、接続プロパティで、(高可用性、障害回復) 可用性グループ (AG) の高可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスを指定できます。 フェールオーバーが発生した AlwaysOn データベースに SqlClient アプリケーションが接続される場合、元の接続が途切れるため、アプリケーションがフェールオーバーの後に処理を続行するには、新しい接続を開く必要があります。  
  
 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続していない場合、複数の IP アドレスがホスト名に関連付けられていると、SqlClient は、DNS エントリに関連付けられたすべての IP アドレスを順に反復処理します。 これは、DNS サーバーによって返された最初の IP アドレスがネットワーク インターフェイス カード (NIC) にバインドされていない場合、時間がかかります。 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する場合、SqlClient ですべての IP アドレスへの接続確立を並列実行しようとして、接続試行が成功すると、ドライバーは保留状態の接続試行を破棄します。  
  
> [!NOTE]
> 接続タイムアウトの増加および接続の再試行ロジックの実装により、アプリケーションが可用性グループに接続する可能性は向上します。 また、接続がフェールオーバーによって失敗する可能性があるので、接続の再試行ロジックの実装は、失敗した接続が再接続するまで試行されるようにする必要があります。  
  
 次の接続プロパティが、.NET Framework 4.5 の SqlClient に追加されました。  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
 プログラムによって、これらの接続文字列キーワードを次のとおりに変更できます。  
  
1. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
2. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  

> [!NOTE]
> .NET Framework 4.6.1 以降のバージョンでは、`MultiSubnetFailover` を `true` に設定する必要はありません。
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続  
 SQL Server 2012 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する際には、必ず `MultiSubnetFailover=True` を指定してください。 `MultiSubnetFailover` を指定することで、SQL Server 2012 のすべての可用性グループとフェールオーバー クラスター インスタンスに対して高速フェールオーバーが有効化され、単一サブネットおよびマルチサブネットの AlwaysOn トポロジにおけるフェールオーバー時間が大幅に短縮されます。 複数のサブネットのフェールオーバーでは、クライアントは並列接続を試みます。 サブネットのフェールオーバー中に、積極的に TCP 接続を再試行します。  
  
 `MultiSubnetFailover` 接続プロパティは、アプリケーションが可用性グループまたは SQL Server 2012 フェールオーバー クラスター インスタンスで展開されていること、およびすべての IP アドレスへの接続を試行することで SqlClient がプライマリ SQL Server インスタンスのデータベースに接続を試行することを示します。 `MultiSubnetFailover=True` を接続に指定すると、クライアントは、オペレーティング システムの既定の TCP 再転送間隔よりも高速に接続試行を再試行します。 これは、AlwaysOn 可用性グループまたは AlwaysOn フェールオーバー クラスター インスタンスのフェールオーバー後のより高速な再接続を可能にし、単一および複数のサブネットの可用性グループおよびフェールオーバー クラスター インスタンスの両方に適用可能です。  
  
 SqlClient の接続文字列キーワードの詳細については、<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> を参照してください。  
  
 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンス以外の何かに接続する場合に `MultiSubnetFailover=True` を指定すると、パフォーマンスに負の影響が及ぶ可能性があるため、サポートされていません。  
  
 可用性グループまたは SQL Server 2012 フェールオーバー クラスター インスタンス内のサーバーに接続する際には、次のガイドラインに従います。  
  
- 単一のサブネットまたは複数のサブネットへの接続時には、`MultiSubnetFailover` 接続プロパティを使用します。これにより、両方の場合でパフォーマンスが向上します。  
  
- 可用性グループに接続するには、使用する接続文字列でサーバーとして可用性グループの可用性グループ リスナーを指定します。  
  
- 64 個を超える数の IP アドレスが構成された SQL Server インスタンスに接続すると、接続エラーが発生します。  
  
- `MultiSubnetFailover` 接続プロパティを使用するアプリケーションの動作は、認証の種類 (SQL Server 認証、Kerberos 認証、または Windows 認証) によって影響を受けません。  
  
- フェールオーバー時に対応し、アプリケーションの接続の再試行を減らすには、`Connect Timeout` の値を増やします。  
  
- 分散トランザクションはサポートされていません。  
  
 読み取り専用のルーティングが有効でない場合は、セカンダリ レプリカの場所への接続は、次の場合に失敗します。  
  
1. セカンダリ レプリカの場所が接続を受け入れないように構成されている場合。  
  
2. アプリケーションが `ApplicationIntent=ReadWrite` (後で説明) を使用している場合、セカンダリ レプリカの場所は読み取り専用アクセスとして構成されます。  
  
 <xref:System.Data.SqlClient.SqlDependency> は、読み取り専用セカンダリ レプリカではサポートされていません。  
  
 プライマリ レプリカが読み取り専用のワークロードを拒否するように設定され、接続文字列が  `ApplicationIntent=ReadOnly` を含んでいる場合、接続は失敗します。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングから複数のサブネット クラスターを使用するためのアップグレード  
 接続エラー (<xref:System.ArgumentException>) は、`MultiSubnetFailover` および `Failover Partner` 接続のキーワードが接続文字列内に存在する場合や、`MultiSubnetFailover=True` および TCP 以外のプロトコルが使用された場合に発生します。 また、`MultiSubnetFailover` が使用されているとき、SQL Server から、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナー応答が返された場合にも、エラー (<xref:System.Data.SqlClient.SqlException>) が発生します。  
  
 現在データベース ミラーリングを使用している SqlClient アプリケーションを複数のサブネットのシナリオへとアップグレードする場合、`Failover Partner` 接続プロパティを削除し、`MultiSubnetFailover` に設定した `True` で置き換え、接続文字列のサーバー名を可用性グループ リスナーと置き換える必要があります。 接続文字列が `Failover Partner` および `MultiSubnetFailover=True` を使用していると、ドライバーがエラーを生成します。 ただし、接続文字列が `Failover Partner` および `MultiSubnetFailover=False` (または  `ApplicationIntent=ReadWrite`) を使用している場合、アプリケーションはデータベース ミラーリングを使用します。  
  
 データベース ミラーリングが AG のプライマリ データベースで使用される場合、および  `MultiSubnetFailover=True` が可用性グループ リスナーではなくプライマリ データベースに接続する接続文字列で使用される場合、ドライバーはエラーを返します。  
  
## <a name="specifying-application-intent"></a>アプリケーションの目的の指定  
 `ApplicationIntent=ReadOnly` の場合、クライアントは AlwaysOn が有効になったデータベースに接続する場合に、読み取られたワークロードを要求します。 サーバーは、接続時および USE データベース ステートメントの間、その目的を強制しますが、AlwaysOn が有効になったデータベースに対してのみ、これを行います。  
  
 `ApplicationIntent` キーワードは従来の読み取り専用のデータベースでは機能しません。  
  
 データベースは、対象となる AlwaysOn データベースのワークロードの読み取りを許可または拒否できます。 (これは、`PRIMARY_ROLE` および `SECONDARY_ROLE` Transact-SQL ステートメントの `ALLOW_CONNECTIONS` 句を使用して実行されます。)  
  
 `ApplicationIntent` キーワードは、読み取り専用のルーティングを有効にするために使用されます。  
  
## <a name="read-only-routing"></a>読み取り専用ルーティング  
 読み取り専用のルーティングはデータベースの読み取り専用のレプリカの可用性を確保できる機能です。 読み取り専用のルーティングを有効にするには次のことが必要です。  
  
1. AlwaysOn 可用性グループの可用性グループ リスナーに接続する必要があります。  
  
2. `ApplicationIntent` 接続文字列キーワードを `ReadOnly` に設定する必要があります。  
  
3. 可用性グループは、データベース管理者によって、読み取り専用のルーティングを有効にするように構成される必要があります。  
  
 読み取り専用のルーティングを使用する複数の接続のすべてが、同じ読み取り専用のレプリカに接続しないようにすることができます。 データベースの同期変更またはサーバーのルーティング構成の変更は、異なる読み取り専用のレプリカに対するクライアントの接続につながることがあります。 すべての読み取り専用の要求が、確実に同じ読み取り専用のレプリカに接続するようにするには、`Data Source` 接続文字列キーワードに可用性グループ リスナーを渡さないでください。 代わりに、読み取り専用のインスタンスの名前を指定します。  
  
 読み取り専用のルーティングでは、最初にプライマリに接続し、最適な可用性の読み取り可能なセカンダリを検索するため、プライマリに接続するよりも時間がかかる場合があります。 そのため、ログインのタイムアウトを増やす必要があります。  
  
## <a name="see-also"></a>関連項目

- [SQL Server の機能と ADO.NET](sql-server-features-and-adonet.md)
- [ADO.NET の概要](../ado-net-overview.md)
