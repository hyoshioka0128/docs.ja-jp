---
title: クラウドネイティブサービスでのコンテナーとサーバーレスアプローチの組み合わせ
description: コンテナーと Kubernetes をサーバーレスアプローチと組み合わせる
ms.date: 05/13/2020
ms.openlocfilehash: 67eee89659026db06eb16ef6f1154ab6935725a4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614202"
---
# <a name="combining-containers-and-serverless-approaches"></a>コンテナーとサーバーレスの手法の組み合わせ

クラウドネイティブアプリケーションは、通常、コンテナーとオーケストレーションを活用するサービスを実装します。 多くの場合、アプリケーションのサービスの一部を Azure Functions として公開する機会があります。 ただし、Kubernetes にデプロイされたクラウドネイティブアプリでは、この同じツールセット内で Azure Functions を活用すると便利です。 幸いにも、Docker コンテナー内で Azure Functions をラップして、Kubernetes ベースのアプリの他の部分と同じプロセスとツールを使用してデプロイすることができます。

## <a name="when-does-it-make-sense-to-use-containers-with-serverless"></a>サーバーレスでコンテナーを使用することは、どのような場合に適していますか。

Azure 関数は、デプロイされているプラットフォームについての情報を持っていません。 シナリオによっては、特定の要件があり、関数コードを実行する環境をカスタマイズする必要がある場合があります。 依存関係をサポートするカスタムイメージ、または既定のイメージでサポートされていない構成が必要です。 このような場合は、カスタム Docker コンテナーに関数をデプロイするのが理にかなっています。

## <a name="when-should-you-avoid-using-containers-with-azure-functions"></a>Azure Functions でコンテナーを使用しない場合はどうすればよいでしょうか。

従量課金制を使用する場合は、コンテナーで関数を実行することはできません。 さらに、関数を Kubernetes クラスターにデプロイした場合は、Azure Functions によって提供される組み込みのスケーリングを利用できなくなります。 この章の前半で説明した Kubernetes のスケーリング機能を使用する必要があります。

## <a name="how-to-combine-serverless-and-docker-containers"></a>サーバーレスコンテナーと Docker コンテナーを結合する方法

Docker コンテナーで Azure 関数をラップするには、 [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools)をインストールしてから、次のコマンドを実行します。

```console
func init ProjectName --worker-runtime dotnet --docker
```

プロジェクトが作成されると、Dockerfile とワーカーランタイムがに構成され `dotnet` ます。 ここで、関数をローカルで作成してテストできます。 コマンドとコマンドを使用してビルドし、実行し `docker build` `docker run` ます。 Docker サポートを使用して Azure Functions の構築を開始する詳細な手順については、「[カスタムイメージを使用した Linux での関数の作成](https://docs.microsoft.com/azure/azure-functions/functions-create-function-linux-custom-image)」チュートリアルを参照してください。

## <a name="how-to-combine-serverless-and-kubernetes-with-keda"></a>サーバーレスと Kubernetes を KEDA と組み合わせる方法

この章では、Azure Functions のプラットフォームが需要に応じて自動的にスケールアウトされることを確認しました。 ただし、コンテナー化された関数を AKS に配置する場合、組み込みのスケーリング機能は失われます。 これには、 [Kubernetes ベースのイベントドリブン (KEDA)](https://docs.microsoft.com/azure/azure-functions/functions-kubernetes-keda)が用意されています。 これにより、コンテナー化された関数を含めるための高度な自動スケールが可能になり `event-driven Kubernetes workloads,` ます。

KEDA は、Docker コンテナー内の関数のランタイムにイベントドリブンスケーリング機能を提供します。 KEDA は `n instances` 、負荷に基づいて、ゼロのインスタンス (イベントが発生していない場合) からまで拡張できます。 Kubernetes オートスケーラー (水平ポッドオートスケーラー) にカスタムメトリックを公開することによって、自動スケールを有効にします。 KEDA で Functions のコンテナーを使用すると、任意の Kubernetes クラスターにおいてサーバーレス関数の機能をレプリケートできるようになります。

KEDA プロジェクトは、Cloud Native Computing Foundation (CNCF) によって管理されていることに注意してください。

>[!div class="step-by-step"]
>[前へ](leverage-serverless-functions.md)
>[次へ](deploy-containers-azure.md)
