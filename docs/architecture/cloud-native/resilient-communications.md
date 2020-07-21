---
title: 回復性のある通信
description: Azure 向けのクラウドネイティブ .NET アプリの設計 |回復力のある通信
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 33e4c03c1f3d8c01f72c588326fbb0bdfa512cdd
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613747"
---
# <a name="resilient-communications"></a>回復力のある通信

この書籍全体で、マイクロサービスベースのアーキテクチャアプローチを採用しています。 このアーキテクチャには重要な利点がありますが、多くの課題があります。

- *プロセス外のネットワーク通信。* 各マイクロサービスはネットワークプロトコルを介して通信し、ネットワークの輻輳、待機時間、および一時的な障害を発生させることができます。

- *サービス検出。* 異なる IP アドレスとポートを持つマシンのクラスターで実行している場合、マイクロサービスはどのようにして互いを検出し、相互に通信しますか。

- *柔軟性.* 短時間の障害を管理し、システムの安定性を維持するにはどうすればよいですか。

- *負荷分散。* 受信トラフィックは、マイクロサービスの複数のインスタンスにどのように分散されるのですか。

- *セキュリティ。* トランスポートレベルの暗号化と証明書の管理などのセキュリティの問題はどのように適用されますか。

- *分散型監視。* -複数のマイクロサービスにまたがる1つの要求について、追跡可能性と監視を相互に関連付けてキャプチャする方法を教えてください。

さまざまなライブラリやフレームワークでこれらの問題に対処できますが、実装はコストが高く、複雑で、時間がかかることがあります。 また、インフラストラクチャに関する懸念事項をビジネスロジックと組み合わせることもできます。

## <a name="service-mesh"></a>サービスメッシュ

より優れたアプローチは、*サービスメッシュ*を利用する進化テクノロジです。 [サービスメッシュ](https://www.nginx.com/blog/what-is-a-service-mesh/)は、構成可能なインフラストラクチャレイヤーであり、サービスの通信と上記の他の課題に対処するための組み込みの機能を備えています。 これらの問題は、サービスプロキシに移動することで分離されます。 プロキシは、ビジネスコードから分離するために、別のプロセス (サイド[カーと呼ばれます) に](https://docs.microsoft.com/azure/architecture/patterns/sidecar)展開されます。 ただし、サイドカーはサービスにリンクされており、それを使用して作成され、ライフサイクルを共有します。 図6-7 はこのシナリオを示しています。

![サイドカーを使用したサービスメッシュ](./media/service-mesh-with-side-car.png)

**図 6-7**。 サイドカーを使用したサービスメッシュ

前の図では、プロキシがマイクロサービスとクラスター間の通信を傍受して管理する方法に注意してください。

サービスメッシュは、[データプレーン](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc)と[コントロールプレーン](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc)の2つの異なるコンポーネントに論理的に分割されます。 図6-8 は、これらのコンポーネントとその役割を示しています。

![サービスメッシュ制御とデータプレーン](./media/istio-control-and-data-plane.png)

**図 6-8.** サービスメッシュ制御とデータプレーン

構成が完了すると、サービスメッシュが非常に機能します。 サービス探索エンドポイントから、対応するインスタンスのプールを取得できます。 その後、メッシュは特定のインスタンスに要求を送信し、結果の待機時間と応答の種類を記録できます。 メッシュでは、最近の要求の待機時間など、多くの要因に基づいて高速な応答を返す可能性の高いインスタンスを選択できます。

インスタンスが応答しない場合、または失敗した場合、メッシュは別のインスタンスで要求を再試行します。 エラーが返された場合、メッシュは負荷分散プールからインスタンスを削除し、復旧後にそのインスタンスを再度実行します。 要求がタイムアウトになると、メッシュが失敗し、要求を再試行することができます。 メッシュは、メトリックをキャプチャし、集中型のメトリックシステムに分散トレースを出力します。

## <a name="istio-and-envoy"></a>Iとエンボイ

現在、いくつかのサービスメッシュオプションが存在しますが、このドキュメントの執筆時点では、 [iws-at o](https://istio.io/docs/concepts/what-is-istio/)が最も人気です。 Iフェロー o は、IBM、Google、およびその他の顧客との共同事業です。 これは、新規または既存の分散アプリケーションに統合できるオープンソースのオファリングです。 このテクノロジは、マイクロサービスのセキュリティ保護、接続、監視を行うための一貫した完全なソリューションを提供します。 その特徴は次のとおりです。

- 強力な id ベースの認証と承認を使用して、クラスター内のサービス間通信をセキュリティで保護します。
- HTTP、 [Grpc](https://grpc.io/)、WEBSOCKET、TCP トラフィックの自動負荷分散。
- 豊富なルーティング規則、再試行、フェールオーバー、およびフォールトインジェクションにより、トラフィックの動作をきめ細かく制御できます。
- アクセス制御、レート制限、クォータをサポートするプラグ可能なポリシーレイヤーと構成 API。
- クラスター内のすべてのトラフィック (クラスターの受信と送信を含む) の自動メトリック、ログ、およびトレース。

Iの実装の主要なコンポーネントは、[エンボイプロキシ](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy)を持つプロキシサービスです。 各サービスと共に実行され、次の機能のためのプラットフォームに依存しない基盤を提供します。

- 動的サービスの検出。
- 負荷分散。
- TLS の終了。
- HTTP および gRPC プロキシ。
- サーキットブレーカーの回復性。
- 正常性チェック。
- [カナリア](https://martinfowler.com/bliki/CanaryRelease.html)デプロイによる更新のローリング。

既に説明したように、エンボイはクラスター内の各マイクロサービスにサイドカーとしてデプロイされます。

## <a name="integration-with-azure-kubernetes-services"></a>Azure Kubernetes Services との統合

Azure クラウドは、azure Kubernetes Services 内での直接サポートを提供します。 次のリンクを使用して作業を開始できます。

- [AKS での Ip のインストール](https://docs.microsoft.com/azure/aks/istio-install)
- [AKS と Iを使用する](https://docs.microsoft.com/azure/aks/istio-scenario-routing)

### <a name="references"></a>References

- [Polly](http://www.thepollyproject.org/)

- [再試行パターン](https://docs.microsoft.com/azure/architecture/patterns/retry)

- [サーキット ブレーカー パターン](https://docs.microsoft.com/azure/architecture/patterns/circuit-breaker)

- [Azure での復元に関するホワイトペーパー](https://azure.microsoft.com/mediahandler/files/resourcefiles/resilience-in-azure-whitepaper/Resilience%20in%20Azure.pdf)

- [ネットワーク待機時間](https://www.techopedia.com/definition/8553/network-latency)

- [冗長性](https://docs.microsoft.com/azure/architecture/guide/design-principles/redundancy)

- [geo レプリケーション](https://docs.microsoft.com/azure/sql-database/sql-database-active-geo-replication)

- [Azure の Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)

- [自動スケール ガイダンス](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling)

- [Istio](https://istio.io/docs/concepts/what-is-istio/)

- [エンボイプロキシ](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy)

>[!div class="step-by-step"]
>[前へ](infrastructure-resiliency-azure.md)
>[次へ](monitoring-health.md)
