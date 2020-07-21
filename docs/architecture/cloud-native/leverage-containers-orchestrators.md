---
title: コンテナーとコンテナー オーケストレーターの活用
description: Azure での Docker コンテナーと Kubernetes Orchestrators 活用
ms.date: 05/31/2020
ms.openlocfilehash: 25e981e0fb7957e7180be09a19a406eddfe4e51b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84446868"
---
# <a name="leveraging-containers-and-orchestrators"></a>コンテナーとコンテナー オーケストレーターの活用

コンテナーとオーケストレーター、モノリシックデプロイアプローチに共通する問題を解決するように設計されています。

## <a name="challenges-with-monolithic-deployments"></a>モノリシックデプロイに関する課題

従来、ほとんどのアプリケーションは1つのユニットとして展開されていました。 このようなアプリケーションは、モノリスと呼ばれます。 図3-1 に示すように、複数のモジュールまたはアセンブリで構成されている場合でも、アプリケーションを1つの単位としてデプロイする一般的な方法を次に示します。

![モノリシックアーキテクチャ。](./media/monolithic-design.png)

**図 3-1**. モノリシックアーキテクチャ。

単純化の利点はありますが、モノリシックアーキテクチャはいくつかの課題に直面します。

### <a name="deployment"></a>デプロイ

モノリシックアプリケーションでは、わずかな変更しか加えられていない場合でも、アプリケーション全体を完全に展開する必要があります。 完全な展開はコストが高く、エラーが発生しやすい場合があります。 また、アプリケーションを再起動する必要があり、一時的に使用不可に影響します。

### <a name="scaling"></a>Scaling

モノリシックアプリケーションは、1台のコンピューターインスタンスで完全にホストされ、多くの場合、高い機能を備えたハードウェアを必要とします。 モノリスのいずれかの部分にスケーリングが必要な場合は、アプリケーション全体の別のコピーを別のコンピューターに配置する必要があります。 モノリスを使用すると、アプリケーションコンポーネントを個別に拡張することはできません。 スケーリングを必要としないコンポーネントをスケーリングすると、効率が高く、コストがかかるリソースが使用されます。

### <a name="environment"></a>環境

モノリシックアプリケーションは、通常、インストール済みのオペレーティングシステム、ランタイム、およびライブラリの依存関係を備えたホスト環境に配置されます。 この環境は、アプリケーションを開発またはテストしたときと一致しない場合があります。 アプリケーション環境間での不整合は、モノリシック配置における一般的な問題の原因となります。

### <a name="coupling"></a>結合

モノリシックアプリケーションでは、その機能コンポーネント間で高い結合が発生する可能性が高くなります。 ハードな境界がないと、システムの変更によって意図しないコストの高い副作用が生じることがよくあります。 新機能と修正プログラムは、複雑になり、時間がかかり、実装にコストがかかります。 更新には広範なテストが必要です。 また、結合を使用すると、別の実装でのコンポーネントのリファクタリングやスワップが困難になります。 問題の厳密な分離によって構築された場合でも、アーキテクチャ erosion はをモノリシックコードベース悪化として設定します。

### <a name="platform-lock-in"></a>プラットフォームのロックイン

モノリシックアプリケーションは、1つのテクノロジスタックを使用して構築されます。 統一性を提供する一方で、このコミットメントはイノベーションの妨げになる可能性があります。 新しい機能とコンポーネントは、アプリケーションの現在のスタックを使用して構築されます。最新のテクノロジがより適している場合もあります。 長期的なリスクとしては、テクノロジスタックが古くなったり時代遅れになったりすることがあります。 アプリケーション全体を新しい最新のプラットフォームに再設計することは、最高のコストとリスクを伴います。

## <a name="what-are-the-benefits-of-containers-and-orchestrators"></a>コンテナーと orchestrators はどのような利点がありますか。

第1章ではコンテナーを紹介しました。 Cloud native Computing Foundation (CNCF) の順位付けは、クラウドネイティブのコンテナー化[マップ](https://raw.githubusercontent.com/cncf/trailmap/master/CNCF_TrailMap_latest.png)の最初の手順として、クラウドネイティブの旅を開始する企業向けのガイダンスとして強調されています。 このセクションでは、コンテナーの利点について説明します。

Docker は、最も一般的なコンテナー管理プラットフォームです。 Linux と Windows の両方でコンテナーと連携して動作します。 コンテナーは、任意のシステムで同じように動作する、再現可能な別のアプリケーション環境を提供します。 この側面により、クラウドネイティブサービスの開発とホスティングに最適なものになります。 コンテナーは相互に分離されています。 同じホストハードウェア上の2つのコンテナーは、競合を発生させることなく、異なるバージョンのソフトウェアを持つことができます。

コンテナーは、プロジェクトの成果物になる単純なテキストベースのファイルによって定義され、ソース管理にチェックインされます。 完全なサーバーと仮想マシンは手動で更新する必要がありますが、コンテナーは簡単にバージョン管理できます。 コンテナーで実行するようにビルドされたアプリは、ビルドパイプラインの一部として自動化ツールを使用して開発、テスト、および配置できます。

コンテナーは変更できません。 コンテナーを定義したら、それをまったく同じ方法で再作成し、実行することができます。 この不変性は、コンポーネントベースの設計に役立ちます。 アプリケーションの一部が他の部分とは異なる方法で進化する場合、最も頻繁に変更される部分を展開するだけで、アプリ全体を再展開するのはなぜですか。 アプリのさまざまな機能と横断的な問題を別々の単位に分割できます。 図3-2 は、モノリシックアプリが特定の機能を委任することによってコンテナーとマイクロサービスを利用する方法を示しています。 アプリ自体のその他の機能もコンテナー化されています。

![バックエンドでマイクロサービスを使用するようにモノリシックアプリを分割します。](./media/cloud-native-design.png)

**図 3-2**. モノリシックアプリを分解してマイクロサービスを利用する。

各クラウドネイティブサービスは、個別のコンテナーにビルドおよび展開されます。 各は必要に応じて更新できます。 個々のサービスは、各サービスに適切なリソースを持つノードでホストできます。 各サービスが実行されている環境は、開発環境、テスト環境、運用環境間で共有することも、簡単にバージョン管理することもできます。 アプリケーションのさまざまな領域間の結合は、モノリス内のコンパイル時の依存関係ではなく、サービス間の呼び出しまたはメッセージとして明示的に行われます。 また、アプリの他の部分に変更を加えることなく、特定の機能に最適なテクノロジを選択することもできます。

コンテナー化されたサービスには、自動管理が必要です。 個別にデプロイされた多数のコンテナーを手動で管理することはできません。 たとえば、次のタスクについて考えてみます。

- 多くのコンピューターのクラスターに対してコンテナーインスタンスをプロビジョニングするにはどうすればよいですか。
- デプロイ後、コンテナーはどのようにして相互に検出され、相互に通信しますか。
- コンテナーをオンデマンドでスケールインまたはスケールアウトするにはどうすればよいですか。
- 各コンテナーの正常性を監視するにはどうすればよいですか。
- コンテナーをハードウェアおよびソフトウェアの障害から保護するにはどうすればよいですか。
- ダウンタイムなしでライブアプリケーションのコンテナーをアップグレードするにはどうすればよいですか?

コンテナーオーケストレーター、これらの問題に対処して自動化します。

クラウドネイティブエコシステムでは、Kubernetes は事実上コンテナー orchestrator になりました。 これは、クラウドネイティブコンピューティングファンデーション (CNCF) によって管理されるオープンソースのプラットフォームです。 Kubernetes は、マシンクラスター全体のコンテナー化されたワークロードのデプロイ、スケーリング、および運用上の懸念事項を自動化します。 ただし、Kubernetes のインストールと管理は非常に複雑です。

クラウドベンダーの管理されたサービスとして Kubernetes を利用する方が、はるかに優れたアプローチです。 Azure クラウドは、完全に管理された[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/)の Kubernetes プラットフォームを特徴としています。 AKS は、Kubernetes を管理する際の複雑さと運用上のオーバーヘッドを抽象化します。 クラウドサービスとして Kubernetes を使用します。Microsoft は、it を管理およびサポートする責任を担います。 また、AKS は、他の Azure サービスや開発ツールと緊密に統合されています。

AKS は、クラスターベースのテクノロジです。 フェデレーション仮想マシン (ノード) のプールが Azure クラウドにデプロイされます。 これらの組み合わせにより、高可用性環境 (クラスター) が形成されます。 クラスターは、クラウドネイティブアプリケーションに対してシームレスな単一のエンティティとして表示されます。 内部的には、AKS は、負荷を均等に分散する定義済みの方法に従って、これらのノード間でコンテナー化されたサービスをデプロイします。

## <a name="what-are-the-scaling-benefits"></a>スケーリングにはどのような利点がありますか。

コンテナー上に構築されたサービスは、Kubernetes などのオーケストレーションツールによって提供されるスケーリングの利点を活用できます。 設計コンテナーによって認識されるのは、それ自体だけです。 複数のコンテナーを連携させる必要がある場合は、より高いレベルでそれらを整理する必要があります。 多数のコンテナーとその共有依存関係 (ネットワーク構成など) を整理すると、その日を節約するためにオーケストレーションツールが提供されます。 Kubernetes は、コンテナーのグループに対して抽象化レイヤーを作成し、*ポッド*に整理します。 ポッドは、*ノード*と呼ばれるワーカーマシン上で実行されます。 この体系化された構造は*クラスター*と呼ばれます。 図3-3 は、Kubernetes クラスターのさまざまなコンポーネントを示しています。

![クラスターコンポーネントを Kubernetes します。 ](./media/kubernetes-cluster-components.png)
**図 3-3**. クラスターコンポーネントを Kubernetes します。

コンテナー化されたワークロードのスケーリングは、コンテナー orchestrators 主要な機能です。 AKS は、コンテナーインスタンスとコンピューティングノードの2つのディメンション間の自動スケーリングをサポートしています。 AKS を利用することで、需要の急増に迅速かつ効率的に応答し、リソースを追加することができます。 AKS でのスケーリングについては、この章で後ほど説明します。

### <a name="declarative-versus-imperative"></a>宣言型と命令型

Kubernetes は、宣言型と命令型の両方の構成をサポートしています。 命令型のアプローチには、各手順の実行方法を Kubernetes に指示するさまざまなコマンドを実行する必要があります。 このイメージを実行します。 このポッドを削除します。 このポートを公開します。 宣言型の方法では、マニフェストと呼ばれる構成ファイルを作成して、何を行うかではなく、目的の内容を記述します。 Kubernetes はマニフェストを読み取り、目的の終了状態を実際の終了状態に変換します。

命令型コマンドは、学習や対話型の実験に適しています。 ただし、信頼性が高く反復可能なデプロイを実現するために、コードのアプローチとしてインフラストラクチャを採用するために、Kubernetes マニフェストファイルを宣言によって作成することをお勧めします。 マニフェストファイルはプロジェクトアーティファクトになり、Kubernetes デプロイを自動化するために CI/CD パイプラインで使用されます。

命令型コマンドを使用して既にクラスターを構成している場合は、を使用して宣言型マニフェストをエクスポートでき `kubectl get svc SERVICENAME -o yaml > service.yaml` ます。 このコマンドを実行すると、次のようなマニフェストが生成されます。

```yaml
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2019-09-13T13:58:47Z"
  labels:
    component: apiserver
    provider: kubernetes
  name: kubernetes
  namespace: default
  resourceVersion: "153"
  selfLink: /api/v1/namespaces/default/services/kubernetes
  uid: 9b1fac62-d62e-11e9-8968-00155d38010d
spec:
  clusterIP: 10.96.0.1
  ports:
  - name: https
    port: 443
    protocol: TCP
    targetPort: 6443
  sessionAffinity: None
  type: ClusterIP
status:
  loadBalancer: {}
```

宣言型の構成を使用する場合は、構成ファイルが配置されているフォルダーに対してを使用してコミットする前に、変更をプレビューでき `kubectl diff -f FOLDERNAME` ます。 変更を適用することを確認したら、を実行 `kubectl apply -f FOLDERNAME` します。 `-R`フォルダー階層を再帰的に処理するには、を追加します。

宣言型の構成を他の Kubernetes 機能と共に使用することもできます。そのうちの1つは配置です。 宣言型の配置は、リリース、更新、およびスケーリングを管理するのに役立ちます。 新しい変更をデプロイする方法、負荷をスケールアウトする方法、または以前のリビジョンにロールバックする方法について、Kubernetes deployment controller に指示します。 クラスターが不安定な場合、宣言型のデプロイはクラスターを自動的に適切な状態に戻します。 たとえば、ノードがクラッシュした場合、デプロイメカニズムによって、目的の状態を実現するために置き換えが再デプロイされます。

宣言型の構成を使用すると、アプリケーションコードと共にチェックインおよびバージョン管理できるコードとして、インフラストラクチャを表すことができます。 改良された変更管理と、ビルドおよびデプロイパイプラインを使用した継続的なデプロイのサポートが向上します。

## <a name="what-scenarios-are-ideal-for-containers-and-orchestrators"></a>コンテナーと orchestrators 最適なシナリオ

次のシナリオは、コンテナーと orchestrators 使用する場合に最適です。

### <a name="applications-requiring-high-uptime-and-scalability"></a>高いアップタイムとスケーラビリティを必要とするアプリケーション

アップタイムとスケーラビリティの要件が高い個々のアプリケーションは、マイクロサービス、コンテナー、および orchestrators 使用したクラウドネイティブアーキテクチャに最適です。 これらは、コンテナーで開発し、バージョン管理された環境でテストし、ダウンタイムなしで運用環境にデプロイすることができます。 Kubernetes クラスターを使用することにより、このようなアプリはオンデマンドでスケールしたり、ノードの障害から自動的に回復したりすることができます。

### <a name="large-numbers-of-applications"></a>多数のアプリケーション

多数のアプリケーションを展開して管理する組織は、コンテナーと orchestrators 利用できます。 コンテナー化された環境と Kubernetes クラスターを設定する前の作業は、主に固定コストです。 個々のアプリケーションの配置、保守、および更新には、アプリケーションの数に応じてコストがかかります。 アプリケーションの数が少ない場合、カスタムアプリケーションを手動で管理することの複雑さは、コンテナーと orchestrators 使用したソリューションの実装コストを上回ることになります。

## <a name="when-should-you-avoid-using-containers-and-orchestrators"></a>コンテナーと orchestrators 使用する必要があるのはどのような場合ですか。

12要素アプリの原則に従ってアプリケーションをビルドできない場合は、コンテナーと orchestrators 避けることを検討してください。 このような場合は、VM ベースのホスティングプラットフォームや、場合によっては一部のハイブリッドシステムを検討してください。 この機能を使用すると、特定の機能をいつでも個別のコンテナーやサーバーレス機能に分解できます。

## <a name="development-resources"></a>開発リソース

このセクションでは、次のアプリケーションでコンテナーとオーケストレーター使用を開始する際に役立つ、開発リソースの簡単な一覧を示します。 クラウドネイティブマイクロサービスアーキテクチャアプリを設計する方法に関するガイダンスについては、「 [.Net マイクロサービス: コンテナー化された .Net アプリケーションのアーキテクチャ](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)」を参照してください。

### <a name="local-kubernetes-development"></a>ローカル Kubernetes の開発

Kubernetes のデプロイは、運用環境での優れた価値を提供しますが、開発用コンピューターでローカルに実行することもできます。 個々のマイクロサービスを独立して作業することもありますが、運用環境にデプロイしたときに実行するのと同じように、ローカルでシステム全体を実行することが必要になる場合があります。 Minikube と Docker Desktop に役立つツールがいくつかあります。 Visual Studio には、Docker 開発用のツールも用意されています。

### <a name="minikube"></a>Minikube

Minikube とは Minikube プロジェクトでは、"Minikube は macOS、Linux、および Windows でローカルの Kubernetes クラスターを実装しています" と表示されます。 主な目的は、"ローカル Kubernetes アプリケーションの開発に最適なツールであり、Kubernetes のすべての機能をサポートすることです。" ということです。 Minikube のインストールは Docker とは分離されていますが、Minikube は Docker デスクトップでサポートされるのとは異なるハイパーバイザーをサポートします。 現在、Minikube では次の Kubernetes 機能がサポートされています。

- DNS
- NodePorts
- ConfigMaps とシークレット
- ダッシュボード
- コンテナーランタイム: Docker、rkt、CRI、および格納されている
- コンテナーネットワークインターフェイスを有効にする (CNI)
- イングレス

Minikube をインストールしたら、 `minikube start` イメージをダウンロードしてローカルの Kubernetes クラスターを起動するコマンドを実行して、すぐに使用を開始できます。 クラスターを起動したら、標準の Kubernetes コマンドを使用して操作し `kubectl` ます。

### <a name="docker-desktop"></a>Docker Desktop

Windows の Docker デスクトップから直接 Kubernetes を使用することもできます。 Windows コンテナーを使用している場合の唯一のオプションであり、Windows 以外のコンテナーにも適しています。 図3-4 は、Docker Desktop の実行時にローカル Kubernetes のサポートを有効にする方法を示しています。

![Docker Desktop での Kubernetes の構成](./media/docker-desktop-kubernetes.png)

**図 3-4**. Docker Desktop で Kubernetes を構成しています。

Docker Desktop は、コンテナー化されたアプリをローカルで構成して実行するための最も一般的なツールです。 Docker Desktop を使用する場合は、実稼働環境にデプロイする Docker コンテナーイメージのまったく同じセットに対してローカルで開発できます。 Docker Desktop は、コンテナー化されたアプリをローカルで "ビルド、テスト、および出荷" するように設計されています。 Linux と Windows の両方のコンテナーをサポートしています。 Azure Container Registry や Docker Hub などのイメージレジストリにイメージをプッシュすると、AKS はそれらをプルして運用環境にデプロイできます。

### <a name="visual-studio-docker-tooling"></a>Visual Studio Docker ツール

Visual Studio では、web ベースアプリケーションの Docker 開発をサポートしています。 新しい ASP.NET Core アプリケーションを作成するときに、図3-5 に示すように、Docker サポートを使用して構成することもできます。

![Visual Studio による Docker サポートの有効化](./media/visual-studio-enable-docker-support.png)

**図 3-5**. Visual Studio による Docker サポートの有効化

このオプションを選択すると、プロジェクトはというルートに作成され、 `Dockerfile` Docker コンテナーでアプリをビルドしてホストするために使用できます。 図 3-6 に Dockerfile の例を示します。

```docker
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["eShopWeb/eShopWeb.csproj", "eShopWeb/"]
RUN dotnet restore "eShopWeb/eShopWeb.csproj"
COPY . .
WORKDIR "/src/eShopWeb"
RUN dotnet build "eShopWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "eShopWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "eShopWeb.dll"]
```

**図 3-6**. Visual Studio によって生成された Dockerfile

アプリを実行するときの既定の動作は、Docker も使用するように構成されます。 図3-7 は、Docker サポートを追加して作成された新しい ASP.NET Core プロジェクトで使用できるさまざまな実行オプションを示しています。

![Visual Studio Docker の実行オプション](./media/visual-studio-docker-run-options.png)

**図 3-7**. Visual Studio Docker の実行オプション

[Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/)には、ローカル開発に加えて、複数の開発者が Azure 内で独自の Kubernetes 構成を操作するための便利な方法が用意されています。 図3-7 に示すように、Azure Dev Spaces でアプリケーションを実行することもできます。

また、いつでも既存の ASP.NET Core アプリケーションに Docker サポートを追加できます。 図3-8 に示すように、Visual Studio ソリューションエクスプローラーからプロジェクト**Add**を右クリックし、  >  **Docker サポート**を追加します。

![Visual Studio による Docker サポートの追加](./media/visual-studio-add-docker-support.png)

**図 3-8**. Visual Studio への Docker サポートの追加

また、図3-8 に示すように、コンテナーオーケストレーションのサポートを追加することもできます。 既定では、orchestrator は Kubernetes とヘルムを使用します。 Orchestrator を選択する `azds.yaml` と、ファイルがプロジェクトのルートに追加され、 `charts` アプリケーションを構成して Kubernetes に配置するために使用されるヘルムグラフを含むフォルダーが追加されます。 図3-9 に、新しいプロジェクトで生成されるファイルを示します。

![Visual Studio の Orchestrator サポートの追加](./media/visual-studio-add-orchestrator-support.png)

**図 3-9**. Visual Studio へのオーケストレーションサポートの追加

### <a name="visual-studio-code-docker-tooling"></a>Docker ツールの Visual Studio Code

Docker 開発をサポートする Visual Studio Code には、いくつかの拡張機能が用意されています。

Microsoft では、 [Docker for Visual Studio Code 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)を提供しています。 この拡張機能により、アプリケーションにコンテナーサポートを追加するプロセスが簡略化されます。 スキャフォールディングは、必要なファイルを作成し、Docker イメージをビルドして、コンテナー内でアプリをデバッグできるようにします。 拡張機能は、開始、停止、検査、削除などのコンテナーとイメージに対して簡単にアクションを実行できるようにする visual explorer を特徴としています。 また、この拡張機能では、複数の実行中のコンテナーを1つの単位として管理できる Docker Compose もサポートされています。

>[!div class="step-by-step"]
>[前へ](scale-applications.md)
>[次へ](leverage-serverless-functions.md)
