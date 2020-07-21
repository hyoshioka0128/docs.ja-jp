---
title: Azure でコンテナーをデプロイする
description: Azure Container Registry、Azure Kubernetes Service、Azure Dev Spaces を使用した Azure でのコンテナーのデプロイ。
ms.date: 04/13/2020
ms.openlocfilehash: ba2854323ee0f1394a3cff0dd3756cb3c7c32d5b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614150"
---
# <a name="deploying-containers-in-azure"></a>Azure でコンテナーをデプロイする

この章と第1章では、コンテナーについて説明しました。 コンテナーは、移植性など、クラウドネイティブアプリケーションに多くの利点を提供していることがわかりました。 Azure クラウドでは、ステージング環境と運用環境の間で同じコンテナー化されたサービスをデプロイできます。 Azure には、コンテナー化されたワークロードをホストするためのいくつかのオプションがあります

- Azure Kubernetes Services (AKS)
- Azure Container Instance (ACI)
- コンテナー用の Azure Web Apps

## <a name="azure-container-registry"></a>Azure Container Registry

マイクロサービスをコンテナー化するときは、まずビルドコンテナー "image" になります。 イメージは、サービスコード、依存関係、およびランタイムのバイナリ表現です。 Docker API からコマンドを使用してイメージを手動で作成することもできますが、 `Docker Build` 自動化されたビルドプロセスの一部として作成することをお勧めします。

作成されると、コンテナーイメージはコンテナーレジストリに格納されます。 コンテナーイメージを作成、保存、および管理することができます。 パブリックとプライベートの両方で、使用可能なレジストリが多数あります。 Azure Container Registry (ACR) は、Azure クラウドで完全に管理されたコンテナーレジストリサービスです。 Azure ネットワーク内にイメージが保持されるため、Azure container hosts にデプロイする時間が短縮されます。 また、他の Azure リソースに使用するのと同じセキュリティと id の手順を使用してセキュリティを保護することもできます。

Azure Container Registry を作成するには、 [Azure portal](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal)、 [Azure CLI](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli)、または[PowerShell ツール](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-powershell)を使用します。 Azure でのレジストリの作成は簡単です。 これには、Azure サブスクリプション、リソースグループ、および一意の名前が必要です。 図3-11 は、でホストされるレジストリを作成するための基本的なオプションを示して `registryname.azurecr.io` います。

![コンテナー レジストリを作成する](./media/create-container-registry.png)

**図 3-11**. コンテナー レジストリを作成する

レジストリを作成したら、それを使用する前に認証を行う必要があります。 通常は、Azure CLI コマンドを使用してレジストリにログインします。

```azurecli
az acr login --name *registryname*
```

認証が完了したら、docker コマンドを使用してコンテナーイメージをプッシュできます。 ただし、これを行う前に、ACR ログインサーバーの完全修飾名 (URL) でイメージにタグを付ける必要があります。 *Registryname*. azurecr.io の形式で指定します。

```console
docker tag mycontainer myregistry.azurecr.io/mycontainer:v1
```

イメージにタグを付けたら、コマンドを使用し `docker push` て、ACR インスタンスにイメージをプッシュします。

```console
docker push myregistry.azurecr.io/mycontainer:v1
```

イメージをレジストリにプッシュした後、次のコマンドを使用して、ローカルの Docker 環境からイメージを削除することをお勧めします。

```console
docker rmi myregistry.azurecr.io/mycontainer:v1
```

ベストプラクティスとして、開発者はイメージをコンテナーレジストリに手動でプッシュしないようにすることをお勧めします。 代わりに、GitHub や Azure DevOps などのツールで定義されたビルドパイプラインをこのプロセスに対して行う必要があります。 詳細については、「[クラウド-ネイティブ DevOps](devops.md)」を参照してください。

## <a name="acr-tasks"></a>ACR タスク

[ACR タスク](https://docs.microsoft.com/azure/container-registry/container-registry-tasks-overview)は、Azure Container Registry から使用できる一連の機能です。 Azure クラウドでコンテナーイメージを構築および管理することによって、[内部ループの開発サイクル](https://docs.microsoft.com/dotnet/architecture/containerized-lifecycle/design-develop-containerized-apps/docker-apps-inner-loop-workflow)を拡張します。 開発用コンピューター上でを呼び出すのではなく、 `docker build` `docker push` クラウド内の ACR タスクによって自動的に処理されます。

次の AZ CLI コマンドは、両方ともコンテナーイメージを構築し、ACR にプッシュします。

```azurecli
# create a container registry
az acr create --resource-group myResourceGroup --name myContainerRegistry008 --sku Basic

# build container image in ACR and push it into your container regsitry
az acr build --image sample/hello-world:v1  --registry myContainerRegistry008 --file Dockerfile .
```

前のコマンドブロックからわかるように、開発用コンピューターに Docker Desktop をインストールする必要はありません。 また、ACR タスクトリガーを構成して、ソースコードと基本イメージの更新の両方でコンテナーイメージを再構築することもできます。

## <a name="azure-kubernetes-service"></a>Azure Kubernetes Service

この章では、Azure Kubernetes Service (AKS) について説明しました。 コンテナー化されたクラウドネイティブアプリケーションを管理する事実上のコンテナー orchestrator であることがわかりました。

ACR などのレジストリにイメージをデプロイしたら、自動的にプルおよびデプロイされるように AKS を構成できます。 CI/CD パイプラインが配置されている場合は、更新プログラムを迅速に展開するときのリスクを最小限に抑えるために、[カナリアリリース](https://martinfowler.com/bliki/CanaryRelease.html)戦略を構成することができます。 アプリの新しいバージョンは、最初に運用環境で構成され、トラフィックはルーティングされません。 その後、システムは、新しく展開されたバージョンにユーザーの小さな割合をルーティングします。 新しいバージョンではチームが自信を持っているため、より多くのインスタンスをロールアウトし、古いものを削除することができます。 AKS は、このスタイルのデプロイを簡単にサポートします。

Azure のほとんどのリソースと同様に、ポータル、コマンドライン、または、ヘルムや Terraform などの自動化ツールを使用して、Azure Kubernetes サービスクラスターを作成できます。 新しいクラスターの使用を開始するには、次の情報を提供する必要があります。

- Azure サブスクリプション
- Resource group
- Kubernetes クラスター名
- リージョン
- Kubernetes バージョン
- DNS 名プレフィックス
- ノード サイズ
- ノード数

作業を開始するには、この情報で十分です。 Azure portal の作成プロセスの一環として、クラスターの次の機能のオプションを構成することもできます。

- スケール
- 認証
- ネットワーク
- 監視
- タグ

この[クイックスタートでは、Azure portal を使用して AKS クラスターをデプロイ](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal)する手順について説明します。

## <a name="azure-dev-spaces"></a>Azure Dev Spaces

クラウドネイティブアプリケーションは、大規模で複雑な拡張が可能で、大量のコンピューティングリソースを実行する必要があります。 このようなシナリオでは、アプリケーション全体を開発用コンピューター (特にラップトップ) でホストすることはできません。 Azure Dev Spaces は、AKS を使用してこの問題に対処するように設計されています。 開発者は、AKS 開発クラスターでアプリケーションの残りの部分をホストしながら、ローカルバージョンのサービスを操作できます。

開発者は、コンテナー化されたアプリケーション全体を含む AKS クラスターで実行中の (開発) インスタンスを共有します。 ただし、ユーザーは自分のコンピューターに設定されている個人用のスペースを使用して、サービスをローカルに開発します。 準備ができたら、依存関係をレプリケートせずに、AKS クラスターでエンドツーエンドのテストを行います。 Azure Dev Spaces は、ローカルコンピューターから AKS のサービスとコードをマージします。 開発者は、Visual Studio または Visual Studio Code を使用して、Kubernetes 内で直接コードをすばやく反復処理し、デバッグすることができます。

Azure Dev Spaces の価値を理解するために、Microsoft Azure でコンテナーの Gabe Monroy PM の潜在顧客からこの引用を共有しましょう。

> 「新しい従業員が、多数のコンポーネントで構成される複雑なマイクロサービスアプリケーションでバグを修正しようとしていて、それぞれ独自の構成サービスとバックアップサービスを備えているとします。 使用を開始するには、ローカル開発環境を構成して、IDE のセットアップ、ツールチェーンの構築、コンテナー化されたサービスの依存関係、ローカルの Kubernetes 環境、バッキングサービスのモックなどの運用を模倣できるようにする必要があります。 開発環境の設定に関連する時間があれば、最初のバグを修正するには数日かかる可能性があります。
> または、Dev Spaces と AKS を使用することもできます。

Azure Dev Spaces を操作するプロセスには、次の手順が含まれます。

1. 開発領域を作成します。
2. ルートの dev space を構成します。
3. (独自のバージョンのシステムの) 子の開発領域を構成します。
4. Dev 空間に接続します。

これらの手順はすべて、Azure CLI と新しいコマンドラインツールを使用して実行でき `azds` ます。 たとえば、特定の Kubernetes クラスター用に新しい Azure Dev Space を作成するには、次のようなコマンドを使用します。

```azurecli
az aks use-dev-spaces -g my-aks-resource-group -n MyAKSCluster
```

次に、コマンドを使用して、 `azds prep` アプリケーションを実行するために必要な Docker およびヘルムグラフ資産を生成できます。 次に、を使用して AKS でコードを実行し `azds up` ます。 このコマンドを初めて実行すると、ヘルムグラフがインストールされます。 コンテナーは、指示に従ってビルドおよびデプロイされます。 このタスクが初めて実行されたときに、数分かかることがあります。 ただし、変更を行った後は、を使用して独自の子開発領域に接続して `azds space select` から、分離された子開発領域に更新プログラムをデプロイしてデバッグすることができます。 開発領域が稼働状態になったら、コマンドを再発行して更新プログラムを送信する `azds up` か、Visual Studio または Visual Studio Code の組み込みツールを使用することができます。 VS Code では、コマンドパレットを使用して、開発領域に接続します。 図3-12 は、Visual Studio で Azure Dev Spaces を使用して web アプリケーションを起動する方法を示しています。

![Visual Studio の Azure Dev Spaces に接続 ](./media/azure-dev-spaces-visual-studio-launchsettings.png)
 **図 3-12**。 Visual Studio での Azure Dev Spaces への接続

>[!div class="step-by-step"]
>[前へ](combine-containers-serverless-approaches.md)
>[次へ](scale-containers-serverless.md)
