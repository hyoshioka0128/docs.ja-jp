---
title: コンテナーとサーバーレスのアプリケーションのスケーリング
description: ユーザーの要求を満たすために、Azure Kubernetes サービスを使用してクラウドネイティブアプリケーションをスケーリングします。
ms.date: 05/13/2020
ms.openlocfilehash: a5e1e8df785fd08901d9be41c0a06db35e09296b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613721"
---
# <a name="scaling-containers-and-serverless-applications"></a>コンテナーとサーバーレスのアプリケーションのスケーリング

アプリケーションの規模を設定するには、次の2つの方法があります。前者は容量を1つのリソースに追加することを示していますが、後者は容量を増やすためにリソースを追加することを意味しています。

## <a name="the-simple-solution-scaling-up"></a>単純な解決策: スケールアップ

CPU、メモリ、ディスク i/o 速度、およびネットワーク i/o 速度が向上している既存のホストサーバーをアップグレードすることを、*スケールアップ*と呼びます。 クラウドネイティブアプリケーションをスケールアップするには、クラウドベンダーから、より多くの対応リソースを選択する必要があります。 たとえば、Kubernetes クラスター内のより大きな Vm を含む新しいノードプールを作成できます。 次に、コンテナー化されたサービスを新しいプールに移行します。

サーバーレスアプリをスケールアップするには、専用の app service プランから[Premium Functions プラン](https://docs.microsoft.com/azure/azure-functions/functions-scale)または premium インスタンスのサイズを選択します。

## <a name="scaling-out-cloud-native-apps"></a>クラウドネイティブアプリのスケールアウト

クラウドネイティブアプリケーションでは、多くの場合、必要に応じて大規模な変動が発生し、その時点の通知にスケールが必要です。 スケールアウトを優先します。スケールアウトは、既存のクラスターにコンピューター (ノードと呼ばれます) またはアプリケーションインスタンスを追加することによって、水平方向に実行されます。 Kubernetes では、アプリの構成設定 ([ノードプールのスケーリング](https://docs.microsoft.com/azure/aks/use-multiple-node-pools#scale-a-node-pool-manually)など) を調整するか、自動スケールを使用して手動でスケールすることができます。

AKS クラスターは、次の2つの方法のいずれかで自動スケールできます。

まず、[水平ポッドオートスケーラー](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale#autoscale-pods)はリソースの需要を監視し、ポッドレプリカに合わせて自動的にサイズを調整します。 トラフィックが増加すると、サービスをスケールアウトするために、追加のレプリカが自動的にプロビジョニングされます。 同様に、要求が減少すると、サービスをスケールインするために削除されます。 スケールするメトリック (CPU 使用率など) を定義します。 また、実行するレプリカの最小数と最大数を指定することもできます。 AKS はそのメトリックを監視し、それに応じてスケールします。

次に、 [AKS Cluster オートスケーラー](https://docs.microsoft.com/azure/aks/cluster-autoscaler)機能を使用すると、需要に合わせて自動的に Kubernetes クラスター全体にコンピューティングノードをスケーリングできます。 この機能を使用すると、のコンピューティング容量が必要になるたびに、基になる Azure 仮想マシンスケールセットに新しい Vm を自動的に追加できます。 また、不要になったときにノードが削除されます。

図3-13 に、これら2つのスケーリングサービスの関係を示します。

![App Service プランをスケールアウトします。](./media/aks-cluster-autoscaler.png)

**図 3-13**. App Service プランをスケールアウトします。

同時に作業することで、必要に応じた需要をサポートするために、コンテナーインスタンスとコンピューティングノードの数が最適になります。 水平ポッドオートスケーラーは、必要なポッドの数を最適化します。 クラスターオートスケーラーは、必要なノードの数を最適化します。

### <a name="scaling-azure-functions"></a>Azure Functions のスケーリング

Azure Functions、必要に応じて自動的にスケールアウトされます。 サーバーリソースは、トリガーされたイベントの数に基づいて動的に割り当てられ、削除されます。 関数の実行時に消費されるコンピューティングリソースに対してのみ課金されます。 課金は、実行回数、実行時間、および使用されたメモリに基づいて行われます。

既定の従量課金プランでは、ほとんどのアプリに対して経済的でスケーラブルなソリューションが提供されますが、premium オプションを使用すると、開発者はカスタム Azure Functions 要件を柔軟に設定できます。 Premium プランにアップグレードすると、インスタンスサイズ、事前に準備された med-v インスタンス (コールドスタートの遅延を回避するため)、および専用 Vm を制御できるようになります。

>[!div class="step-by-step"]
>[前へ](deploy-containers-azure.md)
>[次へ](other-deployment-options.md)
