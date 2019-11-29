---
title: コンテナー ベース アプリケーション用の Azure コンピューティング プラットフォームの選択
description: Azure Cloud および Windows コンテナーで既存の .NET アプリケーションを最新化する |コンテナー ベース アプリケーション用の Azure コンピューティング プラットフォームの選択
ms.date: 05/04/2018
ms.openlocfilehash: 079c9c5ca02b6dc75214d63cb59afdead03d3190
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73737001"
---
# <a name="choosing-azure-compute-platforms-for-container-based-applications"></a>コンテナー ベース アプリケーション用の Azure コンピューティング プラットフォームの選択

前のセクションを読まれたらお気づきのように、Azure は複数の選択肢を提供するオープン クラウドです。 ニーズに最適なものを使用できますが、ここにはコンテナー化されたアプリケーションに使用する製品やテクノロジに関する質問も表示されます。

*既定の*推奨事項として、このガイダンスで推奨される主な条件を次に示します。

- **単一モノリシック アプリ:** Azure App Service を選ぶ
- **n 層アプリ:** バックエンド サービスが 1 つまたは少数の場合は、Azure Kubernetes Service (AKS) や App Service などのオーケストレーターを選択する
- **マイクロサービス:** AKS または Azure Web Apps for Containers を選ぶ
- **サーバーレス関数とイベント ハンドラー:** Azure Functions を選ぶ
- **大規模なバッチ:** Azure Batch を選ぶ

しかし、この推奨事項は、特定のアプリケーションのニーズと特性によって製品の選択が異なるため、完全には信じないことをお勧めします。 すべてのアプリケーションが同様の種類のように見えても、すべてが同じというわけではありません。

アプリケーションのニーズをより詳しく分析した後、選択した製品が違っている場合があります。 しかし、出発点として、特定の優先順位に基づいて評価とテストを開始できる最初のガイダンスを用意することをお勧めします。

図 1 では、さまざまな種類のアプリの内訳と Azure ホスティングの理想的なシナリオを確認できます。

![さまざまなアプリに最適な Azure ホスティング シナリオの表。](./media/choosing-azure-compute-options-for-container-based-applications/azure-hosting-scenarios-for-apps.png)

> [!div class="step-by-step"]
> [前へ](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
> [次へ](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
