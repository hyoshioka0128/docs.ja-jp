---
title: サービスメッシュ-WCF 開発者向け gRPC
description: サービスメッシュを使用して、Kubernetes クラスター内の gRPC サービスに要求をルーティングおよび分散します。
ms.date: 09/02/2019
ms.openlocfilehash: d20275082973f30bddbb342da90454401d4f019b
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73966970"
---
# <a name="service-meshes"></a>サービスメッシュ

サービスメッシュは、ネットワーク内のルーティングサービス要求を制御するインフラストラクチャコンポーネントです。 サービスメッシュは、Kubernetes クラスター内のあらゆる種類のネットワークレベルの問題を処理できます。これには次のものが含まれる。

- サービスの検出
- 負荷分散
- フォールト トレランス
- 暗号化
- 監視

Kubernetes サービスメッシュは、メッシュに含まれる各ポッドにサイドカー*プロキシ*と呼ばれる追加のコンテナーを追加することによって機能します。 プロキシは、すべての受信および送信ネットワーク要求を処理します。これにより、ネットワークの構成と管理がアプリケーションコンテナーとは別に維持され、多くの場合、アプリケーションコードを変更する必要がなくなります。

[前の章の例](kubernetes.md#testing-the-application)を参照してください。 web アプリケーションからの grpc 要求はすべて、grpc サービスの1つのインスタンスにルーティングされていました。 これは、サービスのホスト名が IP アドレスに解決され、その IP アドレスが `HttpClientHandler` インスタンスの有効期間にわたってキャッシュされているために発生します。 DNS 参照を手動で処理するか、複数のクライアントを作成することにより、この問題を回避できる場合がありますが、ビジネスや顧客の価値を追加しなくても、アプリケーションコードが大幅に複雑になります。

サービスメッシュを使用して、アプリケーションコンテナーからの要求がサイドカープロキシに送信されます。このプロキシは、他のサービスのすべてのインスタンスに対してインテリジェントに配布できます。 メッシュは次のようにすることもできます。

- サービスの個々のインスタンスの障害にシームレスに対応できます。
- 失敗した呼び出しまたはタイムアウトの再試行セマンティクスを処理する
- クライアントアプリケーションに戻らずに、別のインスタンスに失敗した要求を再ルーティングします。

次のスクリーンショットは、Linkerd サービスメッシュで実行される StockWeb アプリケーションを示しています。アプリケーションコードや、使用されている Docker イメージは変更されていません。 必要な変更は、`stockdata` および `stockweb` サービスの YAML ファイルの配置に注釈を追加することだけでした。

![サービスメッシュを使用した StockWeb](media/service-mesh/stockweb-servicemesh-screenshot.png)

アプリケーションコードの1つの `HttpClient` インスタンスから発生した場合でも、StockWeb アプリケーションからの要求が Stockweb service の両方のレプリカにルーティングされていることを、[サーバー] 列から確認できます。 実際には、コードを確認すると、同じ `HttpClient` インスタンスを使用して StockData サービスに対する100要求がすべて同時に行われることがわかります。ただし、サービスメッシュでは、これらの要求は多くのサービスインスタンスに分散されますが、複数のサービスインスタンスを使用できます。

サービスメッシュは、クラスター内のトラフィックにのみ適用されます。 外部クライアントの場合は、[次の章「負荷分散](load-balancing.md)」を参照してください。

## <a name="service-mesh-options"></a>サービスメッシュオプション

現在、Kubernetes: ILinkerd o、、Consul Connect で使用できる汎用サービスメッシュ実装は3つあります。 3つすべては、要求のルーティング/プロキシ、トラフィックの暗号化、回復性、ホストからホストへの認証、およびトラフィック制御を提供します。

サービスメッシュの選択は、次の複数の要因によって異なります。

- コスト、コンプライアンス、有償サポートプランなどに関する組織固有の要件。
- クラスターの特性、サイズ、デプロイされたサービスの数、およびクラスターネットワーク内のトラフィックの量。
- メッシュのデプロイと管理を容易にし、サービスで使用できます。

各サービスメッシュの詳細については、それぞれの web サイトを参照してください。

- [**Iistio.io**](https://istio.io)
- [**Linkerd** -linkerd.io](https://linkerd.io)
- [**Consul** -consul.io/mesh.html](https://consul.io/mesh.html)

## <a name="example-add-linkerd-to-a-deployment"></a>例: デプロイへの Linkerd の追加

この例では、[前のセクション](kubernetes.md)の*StockKube*アプリケーションで Linkerd service メッシュを使用する方法について説明します。
この例を実行するには、 [LINKERD CLI をインストール](https://linkerd.io/2/getting-started/#step-1-install-the-cli)する必要があります。 Windows バイナリは、GitHub リリースセクションからダウンロードできます。エッジリリースの1つではなく、最新の**安定**したリリースを使用するようにしてください。

Linkerd CLI がインストールされている状態で、Linkerd web サイトの [*はじめに*の指示に従って、Kubernetes クラスターに Linkerd コンポーネントをインストールします。 手順は簡単であり、インストールにはローカル Kubernetes インスタンスで数分かかることがあります。

### <a name="add-linkerd-to-kubernetes-deployments"></a>Linkerd を Kubernetes デプロイに追加する

Linkerd CLI には、必要なセクションとプロパティを Kubernetes ファイルに追加するための `inject` コマンドが用意されています。 コマンドを実行し、出力を新しいファイルに書き込むことができます。

```console
linkerd inject stockdata.yml > stockdata-with-mesh.yml
linkerd inject stockweb.yml > stockweb-with-mesh.yml
```

新しいファイルを調べて、どのような変更が加えられたかを確認できます。 配置オブジェクトの場合、メタデータ注釈が追加され、Linkerd が作成時にサイドカープロキシコンテナーをポッドに挿入するように指示します。

パイプを使用して `linkerd inject` コマンドの出力を直接 `kubectl` にすることもできます。 次のコマンドは、PowerShell または任意の Linux シェルで動作します。

```console
linkerd inject stockdata.yml | kubectl apply -f -
linkerd inject stockweb.yml | kubectl apply -f -
```

### <a name="inspect-services-in-the-linkerd-dashboard"></a>Linkerd ダッシュボードでサービスを検査する

`linkerd` CLI を使用して Linkerd ダッシュボードを起動します。

```console
linkerd dashboard
```

ダッシュボードには、メッシュに接続されているすべてのサービスに関する詳細情報が表示されます。

![StockKube アプリケーションを示す Linkerd ダッシュボード](media/service-mesh/linkerd-screenshot.png)

次の例に示すように StockData gRPC サービスのレプリカの数を増やし、ブラウザーで Stockdata ページを更新すると、サーバー列に Id が混在していることが示されます。これは、使用可能なすべてのインスタンスによって要求が処理されていることを示します.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockdata
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockdata
  replicas: 2 # Increase the target number of instances
  template:
    metadata:
      annotations:
        linkerd.io/inject: enabled
      creationTimestamp: null
      labels:
        run: stockdata
    spec:
      containers:
      - name: stockdata
        image: stockdata:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
```

>[!div class="step-by-step"]
>[前へ](kubernetes.md)
>[次へ](load-balancing.md)
