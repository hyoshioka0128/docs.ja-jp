---
title: Azure Kubernetes Services での監視
description: Azure Kubernetes Services での監視
ms.date: 05/13/2020
ms.openlocfilehash: 138acf9d27fb4a676ec422c848097a6bea98fa42
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613825"
---
# <a name="monitoring-in-azure-kubernetes-services"></a>Azure Kubernetes Services での監視

Kubernetes の組み込みログはプリミティブです。 ただし、Kubernetes からログを取得し、適切に分析できる場所にするための優れたオプションがいくつかあります。 AKS クラスターを監視する必要がある場合は、Kubernetes のエラスティックスタックの構成が優れたソリューションです。

## <a name="azure-monitor-for-containers"></a>Azure Monitor for Containers

[コンテナーの Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)は、Kubernetes だけでなく、DC/OS、Docker の群れ、Red Hat openshift などの他のオーケストレーションエンジンからのログの使用もサポートしています。

![さまざまなコンテナーからのログの消費 ](./media/containers-diagram.png)
 **図 7-10**。 さまざまなコンテナーからのログの使用

[Prometheus](https://prometheus.io/)は、広く普及しているオープンソースのメトリック監視ソリューションです。 クラウドネイティブコンピューティングファンデーションの一部です。 通常、Prometheus を使用するには、独自のストアで Prometheus サーバーを管理する必要があります。 ただし、[コンテナーの Azure Monitor は、Prometheus メトリックエンドポイントと直接統合](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-prometheus-integration)できるため、個別のサーバーは必要ありません。

ログとメトリックの情報は、クラスターで実行されているコンテナーだけでなく、クラスターからも収集されます。 これにより、2つのログ情報を相互に関連付けることができるため、エラーをより簡単に追跡できます。

ログコレクターのインストールは、 [Windows](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-windows-agent-for-kubernetes)クラスターと[Linux](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-linux-agent-for-kubernetes)クラスターで異なります。 ただし、どちらの場合も、ログの収集は Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)として実装されます。つまり、ログコレクターは各ノード上のコンテナーとして実行されます。

Azure Monitor デーモンを実行している orchestrator またはオペレーティングシステムにかかわらず、ログ情報は、ユーザーが使い慣れているのと同じ Azure Monitor ツールに転送されます。 これにより、ハイブリッド Kubernetes/Azure Functions 環境などのさまざまなログソースが混在する環境での並行操作が可能になります。

![多数の実行中のコンテナーからのログ記録とメトリック情報を示すサンプルダッシュボードです。 ](./media/containers-dashboard.png)
**図 7-11**. 多数の実行中のコンテナーからのログ記録とメトリック情報を示すサンプルダッシュボードです。

## <a name="logfinalize"></a>Log. Finalize ()

ログ記録は、大規模なアプリケーションのデプロイにおいて、見過ごされていて最も重要な部分の1つです。 アプリケーションのサイズと複雑さが増加するにつれて、アプリケーションのデバッグが困難になります。 高品質のログを使用すると、デバッグがはるかに簡単になり、"ほぼ不可能な" 領域から "快適なエクスペリエンス" に移行することができます。

>[!div class="step-by-step"]
>[前へ](logging-with-elastic-stack.md)
>[次へ](azure-monitor.md)
