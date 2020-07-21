---
title: その他のコンテナー配置オプション
description: Azure を使用したその他のコンテナーデプロイオプション
ms.date: 05/13/2020
ms.openlocfilehash: acb022e3d4fd4862c592fa571894e1b8ce17f465
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613760"
---
# <a name="other-container-deployment-options"></a>その他のコンテナー配置オプション

Azure Kubernetes Service (AKS) とは別に、コンテナーと Azure Container Instances の Azure App Service にコンテナーをデプロイすることもできます。

## <a name="when-does-it-make-sense-to-deploy-to-app-service-for-containers"></a>コンテナーの App Service に展開するのはどのような場合に適していますか。

オーケストレーションを必要としない単純な実稼働アプリケーションは、コンテナーの Azure App Service に適しています。

## <a name="how-to-deploy-to-app-service-for-containers"></a>コンテナーの App Service にデプロイする方法

[コンテナーの Azure App Service](https://azure.microsoft.com/services/app-service/containers/)にデプロイするには、AZURE CONTAINER REGISTRY (ACR) インスタンスと、それにアクセスするための資格情報が必要です。 コンテナーイメージを ACR リポジトリにプッシュして、Azure App Service に取り込むことができるようにします。 完了すると、アプリを継続的にデプロイするように構成できます。 これにより、ACR でイメージが変更されるたびに更新が自動的に展開されます。

## <a name="when-does-it-make-sense-to-deploy-to-azure-container-instances"></a>Azure Container Instances に展開するにはどのような意味がありますか。

[Azure Container Instances (ACI)](https://azure.microsoft.com/services/container-instances/)を使用すると、仮想マシンまたはクラスターを設定しなくても、管理されたサーバーレスクラウド環境で Docker コンテナーを実行できます。 分離されたコンテナーで実行できる短時間のワークロードに適したソリューションです。 単純なサービス、テストシナリオ、タスクオートメーション、およびビルドジョブについては、ACI を検討してください。 ACI は、コンテナーインスタンスをスピンアップし、タスクを実行してから、スピンダウンします。

## <a name="how-to-deploy-an-app-to-azure-container-instances"></a>Azure Container Instances にアプリを展開する方法

[Azure Container Instances (ACI)](https://docs.microsoft.com/azure/container-instances/)にデプロイするには、AZURE CONTAINER REGISTRY (ACR) と、それにアクセスするための資格情報が必要です。 コンテナーイメージをリポジトリにプッシュすると、ACI にプルできるようになります。 Azure portal またはコマンドラインインターフェイスを使用して ACI を操作できます。 ACR は、ACI との緊密な統合を提供します。 図3-14 は、個々のコンテナーイメージを ACR にプッシュする方法を示しています。

![実行インスタンスの Azure Container Registry](./media/acr-runinstance-contextmenu.png)

**図 3-14**. 実行インスタンスの Azure Container Registry

ACI にインスタンスを作成することは、迅速に行うことができます。 イメージレジストリ、Azure リソースグループの情報、割り当てるメモリの量、およびリッスンするポートを指定します。 この[クイックスタートでは、Azure portal を使用して、コンテナーインスタンスを ACI にデプロイする方法を示し](https://docs.microsoft.com/azure/container-instances/container-instances-quickstart-portal)ます。

デプロイが完了したら、新しくデプロイされたコンテナーの IP アドレスを見つけて、指定したポートを介して通信します。

Azure Container Instances は、Azure でシンプルなコンテナーワークロードを実行する最速の方法を提供します。 App service、orchestrator、または仮想マシンを構成する必要はありません。 完全なコンテナーオーケストレーション、サービス検出、自動スケール、または調整アップグレードが必要なシナリオでは、Azure Kubernetes Service (AKS) をお勧めします。

## <a name="references"></a>References

- [Kubernetes とは](https://blog.newrelic.com/engineering/what-is-kubernetes/)
- [Minikube を使用した Kubernetes のインストール](https://kubernetes.io/docs/setup/learning-environment/minikube/)
- [MiniKube vs Docker デスクトップ](https://medium.com/containers-101/local-kubernetes-for-windows-minikube-vs-docker-desktop-25a1c6d3b766)
- [Visual Studio Tools for Docker](https://docs.microsoft.com/dotnet/standard/containerized-lifecycle-architecture/design-develop-containerized-apps/visual-studio-tools-for-docker)
- [サーバーレスコールドスタートについて](https://azure.microsoft.com/blog/understanding-serverless-cold-start/)
- [事前に準備した med-v Azure Functions インスタンス](https://docs.microsoft.com/azure/azure-functions/functions-premium-plan#pre-warmed-instances)
- [カスタム イメージを使用して Linux で関数を作成する](https://docs.microsoft.com/azure/azure-functions/functions-create-function-linux-custom-image)
- [Docker コンテナーで Azure Functions を実行する](https://markheath.net/post/azure-functions-docker)
- [カスタム イメージを使用して Linux で関数を作成する](https://docs.microsoft.com/azure/azure-functions/functions-create-function-linux-custom-image)
- [Kubernetes イベントドリブン自動スケールを使用した Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-kubernetes-keda)
- [カナリアリリース](https://martinfowler.com/bliki/CanaryRelease.html)
- [VS Code での Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/quickstart-netcore)
- [Visual Studio での Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/quickstart-netcore-visualstudio)
- [複数のノードプールの AKS](https://docs.microsoft.com/azure/aks/use-multiple-node-pools)
- [AKS クラスターオートスケーラー](https://docs.microsoft.com/azure/aks/cluster-autoscaler)
- [チュートリアル: AKS でのアプリケーションのスケーリング](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale)
- [Azure Functions のスケールとホスティング](https://docs.microsoft.com/azure/azure-functions/functions-scale)
- [Azure Container Instances Docs](https://docs.microsoft.com/azure/container-instances/)
- [ACR からコンテナーインスタンスをデプロイする](https://docs.microsoft.com/azure/container-instances/container-instances-using-azure-container-registry#deploy-with-azure-portal)

>[!div class="step-by-step"]
>[前へ](scale-containers-serverless.md)
>[次へ](communication-patterns.md)
