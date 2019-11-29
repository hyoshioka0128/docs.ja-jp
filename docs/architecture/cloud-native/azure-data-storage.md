---
title: Azure のデータストレージ
description: Azure 向けのクラウドネイティブ .NET アプリの設計 |Azure のデータストレージ
ms.date: 06/30/2019
ms.openlocfilehash: 1a86cecf005c6dbdfda5cf4cacfafaad4711c076
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73841895"
---
# <a name="data-storage-in-azure"></a>Azure のデータストレージ

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

この書籍全体で見てきたように、クラウドでは、アプリケーションの設計、展開、および管理の方法が変更されています。 クラウドへの移行時には、データをどのように移動するかという重要な質問がありますか。 幸い、Azure クラウドには多くのオプションが用意されています。

Azure 仮想マシンをプロビジョニングし、任意のデータベースをインストールするだけで済みます。 これは[、サービスとしてのインフラストラクチャ (IaaS)](https://www.techopedia.com/definition/141/infrastructure-as-a-service-iaas)と呼ばれます。 この方法を使用すると、オンプレミスのデータベースをそのままクラウドに移行することが簡単になりますが、仮想マシンとデータベースの管理の負担が軽減されます。

代わりに、完全に管理された[サービスとしてのデータベース (DBaaS)](https://www.stratoscale.com/blog/dbaas/what-is-database-as-a-service/)が適切なオプションです。 多くの組み込み機能を利用できますが、ホスティング、保守、ライセンスは Microsoft によって管理されています。 Azure では、さまざまな種類の完全管理データストレージオプションが用意されており、それぞれに特定の利点があります。 これらはすべて、ジャストインタイム容量と従量課金制モデルをサポートしています。

次に、Azure で使用可能な DBaaS オプションについて見ていきます。 Microsoft は、Azure を "オープンプラットフォーム" にして、さまざまなオープンソースのリレーショナルデータベースと NoSQL データベースの管理されたサポートを提供し、さまざまなオープンソースの基礎に対する重要な貢献をアクティブメンバーとして提供するという取り組みを続けています。

## <a name="azure-sql-database"></a>Azure SQL データベース

[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)は、Microsoft SQL Server データベースエンジンに基づいて、機能豊富で汎用的なサービスとしてのリレーショナルデータベース (dbaas) です。 これは、Microsoft によって完全に管理され、高パフォーマンスで信頼性の高い、セキュリティで保護されたクラウドデータベースです。 このサービスは、オンプレミスバージョンの SQL Server で検出された多くの機能を共有します。

SQL Database サーバーとデータベースを数分でプロビジョニングできます。 アプリケーションの需要が少数の顧客から何百万に増加した場合、最小限のダウンタイムですぐにスケール Azure SQL Database できます。 リソースを動的に追加または削除できます。これには、データベースに割り当てられた CPU 電力、メモリ、IO スループット、ストレージなどが含まれます。

図5-12 に、Azure SQL Database の配置オプションを示します。

![Azure SQL の配置オプション](./media/azure-sql-database-deployment-options.png)

**図 5-12** Azure SQL の配置オプション

SQL Database をデプロイする場合は、前の図の代替手段に注意してください。

- [1 つのデータベース](https://docs.microsoft.com/azure/sql-database/sql-database-single-database) 、 [SQL Database サーバー](https://docs.microsoft.com/azure/sql-database/sql-database-servers)によって管理される独自のリソースセットを使用します。 1つのデータベースは、オンプレミスの SQL Server デプロイに [含まれる包含データベース](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) に似ています。

- SQL データベースのコレクションが1つの SQL Database サーバーを設定価格で共有する[エラスティックプール](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)。 必要に応じて、1つのデータベースをエラスティックプールとの間で移動して、データベースグループの価格パフォーマンスを最適化することができます。

- システムデータベースとユーザーデータベースのコレクションである[Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)は、オンプレミスの SQL Server とほぼ100% の互換性を提供します。 このオプションは、35 TB までの大規模なデータベースをサポートしており、分離性を高めるために[Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)に配置されています。

Azure SQL Database は、完全に管理された[サービスとしてのプラットフォーム (PaaS) データベースエンジン](https://docs.microsoft.com/azure/sql-database/sql-database-paas)であり、ユーザーの介入なしにアップグレード、修正プログラム、バックアップ、および監視を処理します。 常に最新の安定したバージョンの SQL Server データベースエンジンと修正済みの OS を実行し、99.99% の可用性を保証します。 1つの機能である[アクティブ geo レプリケーション](https://docs.microsoft.com/azure/sql-database/sql-database-active-geo-replication)を使用すると、同じまたは別の Azure データセンターで読み取り可能なセカンダリデータベースを作成できます。 障害が発生したときに、セカンダリデータベースへのフェールオーバーを開始できます。 その時点で、他のセカンダリは自動的に新しいプライマリにリンクされます。 最大4つのセカンダリレプリカが同じまたは異なるリージョンでサポートされており、これらのセカンダリは読み取り専用アクセスクエリにも使用できます。

Azure SQL Database には、パフォーマンスを最大化し、運用コストを削減するのに役立つ、[組み込みの監視機能とインテリジェントチューニング](https://docs.microsoft.com/azure/sql-database/sql-database-monitoring-tuning-index)機能が含まれています。 たとえば、[自動チューニング](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning)機能を使用すると、AI と機械学習に基づいて継続的なパフォーマンスチューニングを行うことができます。 サービスは、実行中のワークロードから学習し、チューニングに関する推奨設定を適用できます。 自動チューニングが有効になっている Azure SQL Database の実行時間が長くなるほど、パフォーマンスが向上します。

[Azure SQL Database サーバーレス](https://docs.microsoft.com/azure/sql-database/sql-database-serverless)(本書の執筆時点でのプレビューで利用可能) は、ワークロードの需要に基づいて自動的に拡張され、1秒あたりに使用されるコンピューティングの量に応じて課金される、単一データベースのコンピューティングレベルです。 また、サーバーレスコンピューティング層は、非アクティブ期間中に自動的にデータベースを一時停止して、ストレージの料金のみが課金されるようにします。 アクティビティが戻ると自動的に再開されます。

最後に、新しい[Azure SQL Database ハイパースケール](https://azure.microsoft.com/services/sql-database/)の価格レベルがあります。 拡張性の高いストレージアーキテクチャが採用されており、必要に応じてデータベースを拡張できるため、ストレージリソースを事前にプロビジョニングする必要がなくなります。 コンピューティングリソースとストレージリソースを個別に拡張して、各ワークロードのパフォーマンスを柔軟に最適化することができます。 Azure SQL Database ハイパースケールは、100 TB までのストレージを使用した[OLTP](https://en.wikipedia.org/wiki/Online_transaction_processing)処理および高スループット分析ワークロード用に最適化されています。  読み取りを集中的に行うワークロードでは、読み取りワークロードのオフロードのために必要に応じて追加の読み取りレプリカをプロビジョニングすることによって、迅速なスケールアウトを実現します。

Azure では、従来の Microsoft SQL Server スタックに加えて、いくつかの一般的なオープンソースデータベースのマネージバージョンも機能します。

## <a name="azure-database-for-mysql"></a>Azure Database for MySQL

[MySQL](https://en.wikipedia.org/wiki/MySQL) は [オープンソースの](https://en.wikipedia.org/wiki/Open-source_software) [リレーショナルデータベース](https://en.wikipedia.org/wiki/Relational_database_management_system)です。 これは、[ランプソフトウェアスタック](https://en.wikipedia.org/wiki/LAMP_(software_bundle))のコンポーネントであり、Facebook、Twitter、YouTube を含む多くの大規模な組織で使用されています。 Community edition は無料でご利用いただけます。 enterprise edition にはライセンス購入が必要です。 1995で作成された製品は、Sun Microsystems の2008で購入されていました。この製品は、2010で Oracle によって取得されました。

[Azure Database for MySQL](https://azure.microsoft.com/services/mysql/)は、オープンソースの MySQL サーバーエンジンに基づく、完全に管理されたエンタープライズ対応のリレーショナルデータベースサービスです。 MySQL Community edition の実装には、追加コストなしで次の PaaS 機能が含まれています。

- 組み込みの[高可用性](https://docs.microsoft.com/azure/mysql/concepts-high-availability)。

- 包括的[な従量課金](https://docs.microsoft.com/azure/mysql/concepts-pricing-tiers)制の料金を使用した、予測可能なパフォーマンス。

- 必要に応じて数秒以内に[スケール](https://docs.microsoft.com/azure/mysql/concepts-high-availability)します。

- 保存中および移動中の機密データを保護するためにセキュリティで保護されています。

- [自動バックアップ](https://docs.microsoft.com/azure/mysql/concepts-backup)と[特定の時点への復元 (](https://docs.microsoft.com/azure/mysql/concepts-backup)最大35日間)。

- エンタープライズグレードのセキュリティとコンプライアンス。

これらの組み込みの PaaS 機能は、データセンターに何百もの "戦術" (非戦略的) データベースを持つ組織にとって重要ですが、パッチ適用、バックアップ、セキュリティ、およびパフォーマンスの監視を実行するためのリソースはありません。

さらに、 [Azure データ移行サービス](https://azure.microsoft.com/services/database-migration/)では、最小限のダウンタイムで、複数のデータベースソースから azure データプラットフォームにデータを移行することができます。 このサービスは、評価レポートを生成し、小規模または大規模の移行の実行に必要な変更を案内する推奨事項を提供します。

管理対象の[Azure MySQL サーバー](https://docs.microsoft.com/azure/mysql/concepts-servers)は、サービスの中央管理ポイントです。 これは、オンプレミスのデプロイに使用されるものと同じ MySQL サーバーエンジンです。 これにより、サーバーごとに1つのデータベースを作成し、すべてのリソースを使用したり、サーバーごとに複数のデータベースを作成してリソースを共有したりすることができます。 新しいスキルを習得したり、仮想マシンやインフラストラクチャを管理したりすることなく、お好きなオープンソースのツールとプラットフォームでアプリケーションを開発し続けることができます。

## <a name="azure-database-for-mariadb"></a>Azure Database for MariaDB

[MariaDB](https://mariadb.com/)サーバーは、もう1つの一般的なオープンソースのデータベースサーバーです。 Mysql のフォークとして作成されました。これは、Oracle が MySQL を所有する Sun Microsystems を購入した時点での mysql の開発者によるものです。 目的は、MariaDB がオープンソースのままになっていることを確認することでした。

MariaDB は[MySQL のフォーク](https://blog.panoply.io/a-comparative-vmariadb-vs-mysql)であるため、データとテーブルの定義には互換性があり、クライアントプロトコル、構造体、および api は knit になります。 MySQL データコネクタは、変更せずに MariaDB で動作します。

MariaDB は強力なものであり、多くの大企業で使用されています。 Oracle は MySQL を引き続き維持し、強化し、サポートしていますが、MariaDB は MariaDB Foundation によって管理されており、製品とドキュメントを公開することができます。

[Azure Database for MariaDB](https://azure.microsoft.com/services/mariadb/)は、Azure クラウドで完全に管理されたサービスとしてのデータベースです。 これは、 [MariaDB community edition](https://mariadb.org/download/)サーバーエンジンに基づいています。 予測可能なパフォーマンスと動的なスケーラビリティを備えたミッションクリティカルなワークロードを処理できます。 他の Azure データベースプラットフォームと同様に、追加コストなしで、サービスとしてのプラットフォームのさまざまな機能を備えています。

- 組み込みの[高可用性](https://docs.microsoft.com/azure/mariadb/concepts-high-availability)。

- 包括的[な従量課金](https://docs.microsoft.com/azure/mariadb/concepts-pricing-tiers)制の料金を使用した、予測可能なパフォーマンス。

- 必要に応じて数秒以内に[スケーリング](https://docs.microsoft.com/azure/mariadb/concepts-high-availability)します。

- 保存データと移動中の機密データを保護します。

- [自動バックアップ](https://docs.microsoft.com/azure/mariadb/concepts-backup)と[特定の時点への復元 (](https://docs.microsoft.com/azure/mariadb/concepts-backup)最大35日間)。

- エンタープライズグレードのセキュリティとコンプライアンス。

## <a name="azure-database-for-postgresql"></a>Azure Database for PostgreSQL

[PostgreSQL](https://www.postgresql.org/)は、30年を超えるアクティブな開発を含む、広く普及しているオープンソースのリレーショナルデータベースです。 これは、汎用的なオブジェクトリレーショナルデータベース管理システムです。 ライセンスは "自由度" と見なされ、製品は任意の形式で自由に使用、変更、および配布できます。 Apple、Red Hat、および富士通を含む多くの大企業は、PostgreSQL を使用して製品を構築しています。

[Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/)は、オープンソースの Postgres データベースエンジンに基づいた、完全に管理されたリレーショナルデータベースサービスです。 予測可能なパフォーマンス、セキュリティ、高可用性、および動的なスケーラビリティを備えたミッションクリティカルなワークロードを処理できます。 Java、Python、Node、C\#、PHP などC++、いくつかのオープンソースフレームワークと言語をサポートしています。 これにより、コマンドラインインターフェイスまたは[Azure データ移行サービス](https://azure.microsoft.com/services/database-migration/)を使用して PostgreSQL データベースを[移行](https://datamigration.microsoft.com/scenario/postgresql-to-azurepostgresql?step=1)できます。

このサービスには、独自のデータベースパターンを調査し、PostgreSQL データベースのパフォーマンスを最大化するのに役立つ、カスタマイズされた推奨事項と洞察を提供する[組み込みのインテリジェンス](https://docs.microsoft.com/azure/postgresql/concepts-monitoring)が含まれています。 [Advanced Threat Protection](https://docs.microsoft.com/azure/postgresql/concepts-data-access-and-security-threat-protection)は、データベースを時計の周りで監視し、悪意のある可能性のあるアクティビティを検出し、すぐに介入できるように検出を警告します。

Azure Database for PostgreSQL は、1台のサーバーとハイパースケール (Citus) という2つのデプロイオプションを利用できます。この書籍の執筆時点でプレビューで利用できます。

- [単一サーバー](https://docs.microsoft.com/azure/postgresql/concepts-servers)配置オプションは、複数のデータベースの中央管理ポイントです。 オンプレミスのデプロイで使用できるのと同じ PostgreSQL サーバーエンジンです。 これを使用すると、サーバーごとに1つのデータベースを作成し、すべてのリソースを使用したり、複数のデータベースを作成してリソースを共有したりすることができます。 価格は、コアとストレージに基づいてサーバーごとに構造化されています。

- [Hyperscale (Citus) オプション](https://azure.microsoft.com/blog/get-high-performance-scaling-for-your-azure-database-workloads-with-hyperscale/)は、 [Citus データ](https://www.citusdata.com/) テクノロジによって強化されています。 これにより、1つのデータベースを数百のノードで水平方向にスケーリングすることにより、パフォーマンスを向上させることができ、驚異的高速なパフォーマンスとスケールを実現できます。 このオプションを使用すると、エンジンはメモリにより多くのデータを格納し、数百のノードにわたってクエリを並列化して、データのインデックス作成を高速化できます。 ハイパースケール機能は、PostgreSQL の最新のイノベーション、バージョン、およびツールと互換性があるため、既存の PostgreSQL の専門知識を活用できます。

## <a name="cosmos-db"></a>Cosmos DB

Azure Cosmos DB は、完全に管理された、グローバルに分散された NoSQL データベースサービスであり、低待機時間、柔軟なスケーラビリティ、管理データの一貫性、および高可用性を提供するように設計されています。 つまり、アプリケーションが世界中のどこでも迅速な応答時間を保証する必要がある場合、常にオンラインにする必要があり、スループットとストレージの無制限で柔軟なスケーラビリティが必要な場合は、Cosmos DB が最適な選択肢です。 図5-13 に、Cosmos DB の概要を示します。

![Cosmos DB の概要](./media/cosmos-db-overview.png)

**図 5-13**: Cosmos DB の概要

図5-13 に、Cosmos DB は、多くの組み込みクラウドネイティブ機能を備えた堅牢で汎用性の高いデータベースサービスです。 このセクションでは、詳しく見ていきます。

### <a name="global-support"></a>グローバルサポート

世界中のすべての Azure リージョンで Cosmos データベースをグローバルに分散し、データをユーザーの近くに配置し、応答時間を短縮し、待機時間を短縮することができます。 アプリケーションを一時停止または再配置しなくても、リージョンのデータベースを追加または削除できます。 バックグラウンドでは、Cosmos DB は、構成されているすべてのリージョンにデータを透過的にレプリケートします。

Cosmos DB は、グローバルレベルで[アクティブ/アクティブ](https://kemptechnologies.com/white-papers/unfog-confusion-active-passive-activeactive-load-balancing/)クラスタリングをサポートしているので、書き込みと読み取りの両方をサポートするように、またはすべてのデータベースリージョンを構成できます。

Cosmos DB の[マルチマスター](https://docs.microsoft.com/azure/cosmos-db/how-to-multi-master)プロトコル機能を使用すると、次の機能が有効になります。

- 無制限のエラスティック書き込みと読み取りのスケーラビリティ。

- 99.999% は世界中のすべての可用性を読み取り、書き込みます。

- 99パーセンタイルでは、読み取りと書き込みが10ミリ秒未満で保証されます。

内部的には、Cosmos DB は、整合性レベルが保証され、経済的にサポートされるサービスレベルアグリーメントによって、リージョン間でのデータレプリケーションを処理します。

Cosmos DB[マルチホーム api](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally)を使用すると、アプリケーションは、最も近い Azure リージョンを自動的に認識し、要求を送信できます。 最も近いリージョンは、構成を変更せずに Cosmos DB によって識別されます。 リージョンが使用できなくなった場合、Cosmos DB は自動フェールオーバーをサポートし、マルチホーム機能は、次に最も近い利用可能なリージョンに要求を自動的にルーティングします。

### <a name="multi-model-support"></a>マルチモデルサポート

Cosmos DB は、ドキュメント、キーと値のペア、ワイド列、グラフ表現など、サポートされている多数の NoSQL モデルを使用してデータを操作できる*マルチモデルデータプラットフォーム*です。 内部的には、データは、文字列、ブール、数値などのプリミティブデータ型で構成される単純な[構造体](https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/using-structs)形式で格納されます。 データベースエンジンは、要求ごとに、選択したモデル表現にデータを変換します。 独自の Cosmos DB SQL ベースの API、または図5-14 に示されている[互換性 api](https://www.wikiwand.com/en/Cosmos_DB)から選択できます。

![Cosmos DB プロバイダー](./media/cosmos-db-providers.png)

**図 5-14**: Cosmos DB プロバイダー

図5-14 では、Cosmos DB が[Table Storage](https://azure.microsoft.com/services/storage/tables/)をサポートしている点に注意してください。 Cosmos DB と[Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)は、同じ基になるテーブルモデルを共有し、同じテーブル操作の多くを公開します。 ただし、 [Cosmos DB Table API](https://docs.microsoft.com/azure/cosmos-db/table-introduction)には、Azure Storage API では利用できない多くの premium 拡張機能が用意されています。 これらの機能は、図5-15 で比較しています。

![Azure Table API](./media/azure-table-api.png)

**図 5-15**: Azure Table API

Azure Table storage 用に作成されたアプリケーションは、コードを変更せずに Table API を使用して Azure Cosmos DB に移行できます。

既存[のデータ](https://en.wikipedia.org/wiki/Brownfield_(software_development))またはアプリケーションコードに最小限の変更を加えることで、開発チームは、既存の Mongo、Cassandra、またはのデータベースを Cosmos DB に移行することができます。 [未開発](https://en.wikipedia.org/wiki/Greenfield_project)のシナリオでは、開発チームは、MongoDB、Cassandra、およびグリーン mlin プラットフォームに対して完全にサポートされているオープンソースオプションを含む、要件と基本設定を最もよく満たすデータモデルを選択できます。

### <a name="consistency-models"></a>整合性モデル

「リレーショナルと*NoSQL* 」セクションでは *、データの*整合性について説明しました。これは、データの整合性を意味する用語です。 高可用性、低待機時間、またはその両方のレプリケーションに依存する分散データベースは、読み取り整合性、可用性、および待機時間の間に基本的なトレードオフを行う必要があります。

多くの分散データベースにより、開発者は、 [強力な整合性](https://en.wikipedia.org/wiki/Strong_consistency)と [最終的な整合性](https://en.wikipedia.org/wiki/Eventual_consistency)の2つの整合性モデルを選択できます。 *強力な一貫性*は、データプログラミングのゴールド標準です。 これにより、すべてのデータベースコピーにわたって更新がレプリケートされるのを待機する待機時間がシステムで発生しても、常に最新のデータが返されます。 一方、*最終的な整合性を確保*するように構成されたシステムは、データが最新のコピーでない場合でも、すぐにデータを返します。 このオプションを使用すると、可用性が向上し、スケールが向上し、パフォーマンスが向上します。

Azure Cosmos DB には、図5-16 に示すように、[明確に定義された5つの整合性モデル](https://docs.microsoft.com/azure/cosmos-db/consistency-levels)が用意されています。 これらのオプションを使用すると、アプリケーションのニーズに基づいて、可用性とパフォーマンスに関して正確な選択肢や詳細なトレードオフを行うことができます。 これらのモデルは、適切に定義され、直感的で、サービスレベルアグリーメント (Sla) によって支えられています。

![Cosmos DB の整合性レベル](./media/cosmos-db-consistency-levels.png)

**図 5-16**: Cosmos DB の整合性レベル

### <a name="partitioning"></a>パーティション分割

Azure Cosmos DB は自動[パーティション分割](https://docs.microsoft.com/azure/cosmos-db/partitioning-overview)を使用して、アプリケーションのパフォーマンスニーズに合わせてデータベースをスケーリングします。

図5-17 に示すように、[データベース、コンテナー、およびアイテム](https://docs.microsoft.com/azure/cosmos-db/databases-containers-items)を作成することによって、Cosmos DB データ内のデータを管理します。

![Cosmos DB エンティティ](./media/cosmos-db-entities.png)

**図 5-17**: Cosmos DB エンティティの階層

図5-17 では、データベースアカウント内で Cosmos DB データベースを作成する方法を説明します。 このデータベースは、一連のコンテナーの管理単位になります。 コンテナーは、選択した API プロバイダー (前のセクションで説明したもの) に基づいて、コレクション、テーブル、またはグラフとして表現できる項目のスキーマに依存しないグループです。 アイテムは、コンテナーに追加するデータで、ドキュメント、行、ノード、またはエッジとして表されます。 既定では、コンテナーに追加したすべてのアイテムには、明示的なインデックスまたはスキーマ管理を必要とせずに、自動的にインデックスが作成されます。

コンテナーをパーティション分割するために、項目は [論理パーティション](https://docs.microsoft.com/azure/cosmos-db/partition-data)と呼ばれる個別のサブセットに分割されます。 論理パーティションは、コンテナー内の各項目に関連付けられているパーティションキーの値に基づいて作成されます。 図5-18 は、論理パーティション内のすべての項目が同じパーティションキー値を持っていることを示しています。

![Cosmos DB パーティション分割機構](./media/cosmos-db-partitioning.png)

**図 5-18**: Cosmos DB パーティション分割機構

図5-18 では、各項目に ' city ' または ' 空港 ' のパーティションキーが含まれていることに注意してください。 このパーティションキーによって、項目の論理パーティションが決定されます。 各都市コードは、左側のコンテナー内の論理パーティションに割り当てられ、右側のコンテナーに空港コードを使用します。 パーティションキー値と項目の ID 値を組み合わせると、項目を一意に識別する項目のインデックスが作成されます。

内部的には、Cosmos DB は、コンテナーのスケーラビリティとパフォーマンスのニーズを効率的に満たすために、[物理パーティション](https://docs.microsoft.com/azure/cosmos-db/partition-data)上の[論理パーティション](https://docs.microsoft.com/azure/cosmos-db/partition-data)の配置を自動的に管理します。 アプリケーションのスループットと記憶域の要件が増加するにつれて、Azure Cosmos DB は論理パーティションを移動して、より多くのサーバーに負荷を分散させます。 これらの再配布操作は Cosmos DB によって管理され、中断やダウンタイムなしで実行されます。

## <a name="azure-redis-cache"></a>Azure Redis Cache

パフォーマンスとスケーラビリティを向上させるためのキャッシュの利点を十分に理解しておいてください。

クラウドネイティブアプリケーションの場合、キャッシュを追加する一般的な場所は API ゲートウェイ内にあります。 ゲートウェイは、すべての受信要求のフロントエンドとして機能します。 キャッシュを追加することで、キャッシュされたデータを返し、ローカルデータベースや下流サービスへのラウンドトリップを回避することで、パフォーマンスと応答性を向上させることができます。 図5-19 は、クラウドネイティブアプリケーションのキャッシュアーキテクチャを示しています。

![クラウドネイティブアプリでのキャッシュ](./media/caching-in-a-cloud-native-app.png)

**図 5-19**: クラウドネイティブアプリでのキャッシュ

一般的なキャッシュパターンは、[キャッシュアサイドパターン](https://docs.microsoft.com/azure/architecture/patterns/cache-aside)です。 受信要求の場合、最初にキャッシュのクエリを実行します。この応答は、図5-19 の手順 #1 に示されています。 見つかった場合は、すぐにデータが返されます。 データがキャッシュに存在しない場合 ([キャッシュミス](https://www.techopedia.com/definition/6308/cache-miss)とも呼ばれます)、ローカルデータベースまたは下流のサービス (ステップ #2) から取得され、将来の要求 (ステップ #3) のためにキャッシュに書き込まれ、呼び出し元に返されます。 システムの一貫性と正確性を維持するために、キャッシュされたデータを定期的に削除する必要があります。

また、図5-19 では、キャッシュがサービスの境界内でローカルに実装されておらず、その代わりに、第1章で説明したように、クラウドベースのバッキングサービスとして使用されることに注意してください。

[Azure Redis Cache](https://azure.microsoft.com/services/cache/)は、データキャッシュとメッセージングブローカーサービスです。 アプリケーションのデータへの高スループットと待機時間の短いアクセスを提供します。 Microsoft によって完全に管理され、Azure 内でホストされ、Azure の内部または外部の任意のアプリケーションからアクセスできます。

Azure cache for Redis は、内部的にはオープンソースの[redis サーバー](https://redis.io/)によって支えられており、[文字列](https://redis.io/topics/data-types#strings)、[ハッシュ](https://redis.io/topics/data-types#hashes)、[リスト](https://redis.io/topics/data-types#sets)、[セット](https://redis.io/topics/data-types#sets)、[並べ替えら](https://redis.io/topics/data-types#sorted-sets)れたセットなどのデータ構造をネイティブでサポートしています。 アプリケーションで Redis を使用する場合、Redis の Azure Cache と同様に機能します。

Redis の Azure Cache は、メモリ内のデータキャッシュ、分散型の非リレーショナルデータベース、メッセージブローカーとしても使用できます。 これは、3つの異なる価格レベルで利用できます。 Premium レベルでは、クラスタリング、データの永続性、geo レプリケーション、仮想ネットワークのセキュリティと分離など、多くのエンタープライズレベルの機能が機能します。

>[!div class="step-by-step"]
>[前へ](data-patterns.md)
>[次へ](resiliency.md)
