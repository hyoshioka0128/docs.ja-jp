---
title: eShopOnContainers を Azure にデプロイする
description: Azure Kubernetes Service、ヘルム、および DevSpaces を使用した eShopOnContainers アプリケーションのデプロイ。
ms.date: 05/13/2020
ms.openlocfilehash: 93a2848f095d7593e1e169f4a6c6c1818a76217d
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614098"
---
# <a name="deploying-eshoponcontainers-to-azure"></a>eShopOnContainers を Azure にデプロイする

EShopOnContainers アプリケーションは、さまざまな Azure プラットフォームにデプロイできます。 Azure Kubernetes Services (AKS) にアプリケーションをデプロイする方法をお勧めします。 Kubernetes 配置ツールであるヘルムは、デプロイの複雑さを軽減するために使用できます。 開発プロセスを効率化するために、開発者は必要に応じて Kubernetes の Azure Dev Spaces を実装することもできます。

## <a name="azure-kubernetes-service"></a>Azure Kubernetes Service

AKS で eShop をホストするには、最初の手順として、AKS クラスターを作成します。 これを行うには、Azure portal を使用します。これにより、必要な手順を実行できます。 また、Azure CLI からクラスターを作成して、ロールベースの Access Control (RBAC) とアプリケーションルーティングを有効にすることもできます。 EShopOnContainers のドキュメントでは、独自の AKS クラスターを作成する手順について詳しく説明しています。 作成したら、Kubernetes ダッシュボードからクラスターにアクセスして管理できます。

これで、ヘルムと Tiller を利用して、eShop アプリケーションをクラスターにデプロイできるようになりました。

## <a name="deploying-to-azure-kubernetes-service-using-helm"></a>ヘルムを使用した Azure Kubernetes Service へのデプロイ

ヘルムは、Kubernetes で直接動作するアプリケーションパッケージマネージャーツールです。 Kubernetes アプリケーションを定義、インストール、およびアップグレードするのに役立ちます。 単純なアプリは、カスタム CLI スクリプトまたは単純なデプロイファイルを使用して AKS にデプロイできますが、複雑なアプリには多数の Kubernetes オブジェクトを含めることができ、また、ヘルムの恩恵を受けることができます。

アプリケーションには、ヘルムを使用して、ヘルムパッケージのアプリケーションと構成を宣言的に記述する、ヘルムグラフと呼ばれるテキストベースの構成ファイルが含まれています。 グラフでは、標準の YAML 形式のファイルを使用して、関連する Kubernetes リソースのセットを記述します。 これらは、記述されているアプリケーションコードと共にバージョン管理されます。 ヘルムグラフは、記述されているインストールの要件に応じて、単純なものから複雑なものまで多岐に範囲されています。

ヘルムはコマンドラインクライアントツールで構成されています。このツールは、ヘルムグラフを使用して、という名前のサーバーコンポーネントに対してコマンドを起動します。 Tiller は、コンテナー化されたワークロードの適切なプロビジョニングを確実に行うために、Kubernetes API と通信します。 ヘルムは、クラウドネイティブコンピューティングファンデーションによって管理されています。

次の yaml ファイルは、ヘルムテンプレートを示しています。

```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.app.svc.marketing }}
  labels:
    app: {{ template "marketing-api.name" . }}
    chart: {{ template "marketing-api.chart" . }}
    release: {{ .Release.Name }}
    heritage: {{ .Release.Service }}
spec:
  type: {{ .Values.service.type }}
  ports:
    - port: {{ .Values.service.port }}
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app: {{ template "marketing-api.name" . }}
    release: {{ .Release.Name }}
```

テンプレートで、キーと値のペアの動的セットがどのように記述されているかに注意してください。 テンプレートが呼び出されると、中かっこで囲まれた値が、他の yaml ベースの構成ファイルから取り込まれます。

EShopOnContainers ヘルムグラフは、/k8s/ヘルムフォルダーにあります。 図2-6 は、アプリケーションのさまざまなコンポーネントを、ヘルムが配置を定義するために使用するフォルダー構造に編成する方法を示しています。

![eShopOnContainers アーキテクチャ ](./media/eshoponcontainers-helm-folder.png)
 **図 2-6**。 EShopOnContainers ヘルムフォルダー。

個々のコンポーネントは、コマンドを使用してインストールされ `helm install` ます。 eShop には、それぞれのヘルムグラフを使用してコンポーネントをループしてインストールする "deploy all" スクリプトが含まれています。 結果として、ソース管理のアプリケーションでバージョン管理された反復可能なプロセスが生成されます。これにより、チームのすべてのユーザーが1行のスクリプトコマンドで AKS クラスターにデプロイできるようになります。

> バージョン3のヘルムは、Tiller サーバーコンポーネントの必要性を正式に排除することに注意してください。 この拡張機能の詳細については、[こちら](https://medium.com/better-programming/why-is-tiller-missing-in-helm-3-2347c446714)を参照してください。

## <a name="azure-dev-spaces"></a>Azure Dev Spaces

クラウドネイティブアプリケーションは、大規模で複雑な拡張が可能で、大量のコンピューティングリソースを実行する必要があります。 このようなシナリオでは、アプリケーション全体を開発用コンピューター (特にラップトップ) でホストすることはできません。 Azure Dev Spaces は、AKS を使用してこの問題に対処するように設計されています。 開発者は、AKS 開発クラスターでアプリケーションの残りの部分をホストしながら、ローカルバージョンのサービスを操作できます。

開発者は、コンテナー化されたアプリケーション全体を含む AKS クラスターで実行中の (開発) インスタンスを共有します。 ただし、ユーザーは自分のコンピューターに設定されている個人用のスペースを使用して、サービスをローカルに開発します。 準備ができたら、依存関係をレプリケートせずに、AKS クラスターでエンドツーエンドのテストを行います。 Azure Dev Spaces は、ローカルコンピューターから AKS のサービスとコードをマージします。 チームメンバーは、実際の AKS 環境で変更がどのように動作するかを確認できます。 開発者は、Visual Studio 2017 または Visual Studio Code を使用して、Kubernetes 内で直接コードをすばやく反復処理し、デバッグすることができます。

図2-7 では、Developer Susie が開発スペースに自転車マイクロサービスの更新バージョンをデプロイしたことがわかります。 次に、自分のスペースの名前 (susie.s.dev.myapp.eus.azds.io) で始まるカスタム URL を使用して、自分の変更をテストできます。

![eShopOnContainers アーキテクチャ ](./media/azure-devspaces-one.png)
 **図 2-7**。 Developer Susie は独自のバージョンの Bikes マイクロサービスをデプロイしてテストします。

同時に、開発者 John は予約マイクロサービスをカスタマイズし、変更をテストする必要があります。 図2-8 に示すように、Susie の変更と競合することなく、自分の開発スペースに自分の変更をデプロイします。 John は、スペースの名前 (john.s.dev.myapp.eus.azds.io) をプレフィックスとした独自の URL を使用して、自分の変更をテストします。

![eShopOnContainers アーキテクチャ ](./media/azure-devspaces-two.png)
 **図 2-8**。 開発者 John は独自のバージョンの予約マイクロサービスをデプロイし、他の開発者と競合することなくテストします。

Azure Dev Spaces を使用すると、チームは AKS を直接操作しながら、変更の変更、配置、およびテストを行うことができます。 この方法では、すべての開発者が独自の AKS 環境を使用するため、個別の専用ホスト環境が必要になります。 開発者は CLI を使用して Azure Dev Spaces を操作したり、アプリケーションを起動して Visual Studio から直接 Azure Dev Spaces したりできます。 [Azure Dev Spaces のしくみと構成方法の詳細については、こちらを参照してください。](https://docs.microsoft.com/azure/dev-spaces/how-dev-spaces-works)

## <a name="azure-functions-and-logic-apps-serverless"></a>Azure Functions と Logic Apps (サーバーレス)

EShopOnContainers サンプルには、オンラインマーケティングキャンペーンの追跡のサポートが含まれています。 特定のキャンペーン ID のマーケティングキャンペーンの詳細を追跡するには、Azure 関数を使用します。 完全なマイクロサービスを作成するのではなく、1つの Azure 関数がシンプルで十分です。 Kubernetes で実行するように構成されている場合は特に、単純なビルドおよびデプロイモデルが Azure Functions ます。 関数の配置は、Azure Resource Manager (ARM) テンプレートと Azure CLI を使用してスクリプト化されます。 このキャンペーンサービスは顧客向けではなく、1つの操作を呼び出して、Azure Functions に最適な候補となります。 関数には、データベース接続文字列データやイメージベース URI 設定など、最小限の構成が必要です。 Azure portal で Azure Functions を構成します。

>[!div class="step-by-step"]
>[前へ](map-eshoponcontainers-azure-services.md)
>[次へ](centralized-configuration.md)
