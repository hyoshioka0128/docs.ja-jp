---
title: Azure Container Service (Kubernetes) に Windows コンテナーをデプロイするタイミング
description: Azure Cloud と Windows コンテナーで既存の .NET アプリケーションを最新化する | Azure コンテナー サービス (Kubernetes) に Windows コンテナーをデプロイするタイミング
ms.date: 04/30/2018
ms.openlocfilehash: 3ff51a70d4e158b831155ab4992ec32f5d98cedb
ms.sourcegitcommit: e3cbf26d67f7e9286c7108a2752804050762d02d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2020
ms.locfileid: "80987765"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>Azure Container Service (Kubernetes) に Windows コンテナーをデプロイするタイミング

Azure Container Service では、一般的なオープンソース ツールとテクノロジの構成を Azure 専用に最適化します。 コンテナーとアプリケーションの構成の両方に移植性を提供するオープン ソリューションが得られます。 ユーザーはサイズ、ホストの数、オーケストレーター ツールを選択します。 インフラストラクチャはユーザーの代わりに Azure Container Service が処理します。

Kubernetes、Docker Swarm、DC/OS など、オープンソースのオーケストレーターを既に使用している場合、コンテナー ワークロードをクラウドに移行する今までの管理方法を変更する必要はありません。 既に精通している任意のアプリケーション管理ツールを使用し、選択したオーケストレーター用の標準 API エンドポイント経由で接続します。

Linux Docker コンテナーを使用している場合、このようなオーケストレーターはすべて成熟した環境になりますが、Windows コンテナーの場合、プレビュー状態に限られることがあります。

たとえば、Kubernetes の場合、コンテナーのサポートはネイティブです (第一級市民)。そのため、Kubernetes で Windows コンテナーを使用することは有効です (2018 年の早い時期から ACS でプレビュー)。

重要な注意事項:Kubernetes の ACS (Azure Container Service) の進化した "PaaS に近い" バージョンが AKS (Azure Kubernetes Service) です。ただし、Windows コンテナーは 2018 年の Q2 以降でもサポートされておりません。近日中にサポートされる予定です。

>[!div class="step-by-step"]
>[前へ](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
>[次へ](choosing-azure-compute-options-for-container-based-applications.md)
