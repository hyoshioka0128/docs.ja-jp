---
title: クラウドネイティブアプリケーションの Elasticsearch
description: クラウドネイティブアプリケーションにエラスティック検索機能を追加する方法について説明します。
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: e956f28877d88ce5279944964a877efc324918b6
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614085"
---
# <a name="elasticsearch-in-a-cloud-native-app"></a>クラウドネイティブアプリでの Elasticsearch

Elasticsearch は、さまざまな種類のデータに対して複雑な検索機能を有効にする分散検索および分析システムです。 オープンソースで広く普及しています。 次の企業が Elasticsearch をアプリケーションに統合する方法を検討します。

- フルテキストとインクリメンタル (入力時の検索) の[Wikipedia](https://blog.wikimedia.org/2014/01/06/wikimedia-moving-to-elasticsearch/) 。
- 800万コードリポジトリにインデックスを作成して公開する[GitHub](https://www.elastic.co/customers/github) 。  
- コンテナーライブラリを検出できるようにするための[Docker](https://www.elastic.co/customers/docker) 。

Elasticsearch は、 [Apache Lucene](https://lucene.apache.org/core/)フルテキスト検索エンジンの上に構築されています。 Lucene は、高パフォーマンスのドキュメントのインデックス作成とクエリを実行します。 逆インデックススキームを使用してデータのインデックスを作成します。ページをキーワードにマップするのではなく、ブックの最後にある用語集と同じように、キーワードをページにマップします。 Lucene には強力なクエリ構文機能があり、次の方法でデータを照会できます。

- 用語 (完全な単語)
- プレフィックス (先頭は word)
- ワイルドカード (" \* " フィルターまたは "?" フィルターを使用)
- フレーズ (ドキュメント内のテキストのシーケンス)
- ブール値 (複合検索クエリの結合)

Lucene では検索のための低レベルのプラミングが提供されますが、Elasticsearch は Lucene の上にあるサーバーを提供します。 Elasticsearch は、Lucene のインデックス作成と検索機能にアクセスする RESTful API など、操作を簡略化するために、より高度な機能を追加します。 また、大規模なスケーラビリティ、フォールトトレランス、高可用性を備えた分散インフラストラクチャも提供します。

複雑な検索要件を持つ大規模なクラウドネイティブアプリケーションの場合、Elasticsearch は Azure の管理されたサービスとして利用できます。 Microsoft Azure Marketplace には、Azure で Elasticsearch クラスターをデプロイするために開発者が使用できる事前構成済みのテンプレートが用意されています。

Microsoft Azure Marketplace から、開発者は、Azure で Elasticsearch クラスターをすばやくデプロイするために構築された構成済みテンプレートを使用できます。 Azure で管理されたサービスを使用すると、最大50のデータノード、20個の調整ノード、3つの専用マスターノードをデプロイできます。

## <a name="summary"></a>要約

この章では、クラウドネイティブシステムのデータについて詳しく説明します。 クラウドネイティブシステムのデータストレージパターンを使用してモノリシックアプリケーションのデータストレージを比較することから始めました。 クラウドネイティブシステムに実装されているデータパターンを見てきました。これには、クロスサービスクエリ、分散トランザクション、および大量システムを扱うためのパターンが含まれます。 NoSQL データを使用して SQL を比較しています。 Microsoft の中心とオープンソースの両方のオプションを含む、Azure で利用可能なデータストレージオプションについて説明しました。 最後に、クラウドネイティブアプリケーションでのキャッシュと Elasticsearch について説明しました。

### <a name="references"></a>References

- [コマンド クエリ責務分離 (CQRS) パターン](https://docs.microsoft.com/azure/architecture/patterns/cqrs)

- [イベントソーシングパターン](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)

- [定理で RDBMS パーティショントレラントが使用できないのはなぜですか。](https://stackoverflow.com/questions/36404765/why-isnt-rdbms-partition-tolerant-in-cap-theorem-and-why-is-it-available)

- [具体化されたビュー](https://docs.microsoft.com/azure/architecture/patterns/materialized-view)

- [オープンソースデータベースについて理解しておく必要があること](https://www.ibm.com/blogs/systems/all-you-really-need-to-know-about-open-source-databases/)

- [補正トランザクション パターン](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction)

- [Saga パターン](https://microservices.io/patterns/data/saga.html)

- [Saga Patterns |マイクロサービスを使用してビジネストランザクションを実装する方法](https://blog.couchbase.com/saga-pattern-implement-business-transactions-using-microservices-part/)

- [補正トランザクション パターン](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction)

- [9 ~ ボールの背後: Cosmos DB の一貫性レベルについて説明します。](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/)

- [さまざまな種類の NoSQL データベースの調査パート II](https://www.3pillarglobal.com/insights/exploring-the-different-types-of-nosql-databases)

- [RDBMS、NoSQL、NewSQL データベースの場合。John ライアンとのインタビュー](http://www.odbms.org/blog/2018/03/on-rdbms-nosql-and-newsql-databases-interview-with-john-ryan/)
  
- [SQL vs NoSQL vs NewSQL: 完全な比較](https://www.xenonstack.com/blog/sql-vs-nosql-vs-newsql/)

- [ダッシュ: Kubernetes ネイティブデータベースの4つのプロパティ](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/)

- [CockroachDB](https://www.cockroachlabs.com/)

- [TiDB](https://pingcap.com/en/)

- [YugabyteDB](https://www.yugabyte.com/)

- [Vitess](https://vitess.io/)

- [Elasticsearch: 決定版ガイド](http://shop.oreilly.com/product/0636920028505.do)
  
- [Apache Lucene の概要](https://www.baeldung.com/lucene)

>[!div class="step-by-step"]
>[前へ](azure-caching.md)
>[次へ](resiliency.md) <!-- Next Chapter -->
