---
title: 集中管理構成
description: Azure アプリ構成と AzureKey Vault を使用して、クラウドネイティブアプリケーションの構成を一元化します。
ms.date: 05/13/2020
ms.openlocfilehash: d389d29dcdb1db5162d95370d181ab5a85d72dc8
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614228"
---
# <a name="centralized-configuration"></a>集中管理構成

すべてが1つのインスタンス内で実行されるモノリシックアプリとは異なり、クラウドネイティブアプリケーションは、仮想マシン、コンテナー、および地理的領域に分散された独立したサービスで構成されます。 多数の相互に依存するサービスの構成設定を管理することは困難な場合があります。 異なる場所にある構成設定の重複コピーは、エラーが発生しやすく、管理が困難です。 一元化された構成は、分散型クラウドネイティブアプリケーションにとって重要な要件です。

[第1章](introduction.md)で説明したように、12要素アプリの推奨事項では、コードと構成を厳密に分離する必要があります。 構成は、アプリケーションから外部に保存し、必要に応じて読み込む必要があります。 構成値を定数またはリテラル値としてコードに格納することは違反です。 同じアプリケーション内の多くのサービスで、多くの場合、同じ構成値が使用されます。 さらに、開発、テスト、運用など、複数の環境で同じ値をサポートする必要があります。 ベストプラクティスとして、一元化された構成ストアに格納することをお勧めします。

Azure クラウドには、いくつかの優れたオプションが用意されています。

## <a name="azure-app-configuration"></a>Azure App Configuration

[Azure アプリ構成](https://docs.microsoft.com/azure/azure-app-configuration/overview)は、セキュリティで保護された一元化された場所に機密以外の構成設定を格納する、完全に管理された Azure サービスです。 格納されている値は、複数のサービスとアプリケーションの間で共有できます。

このサービスは簡単に使用でき、いくつかの利点があります。

- 柔軟なキー/値表現とマッピング
- Azure ラベルを使用したタグ付け
- 管理用の専用 UI
- 機密情報の暗号化
- クエリとバッチ取得

Azure アプリ構成では、キー値の設定に対して行われた変更を7日間保持します。 特定の時点のスナップショット機能を使用すると、設定の履歴を再構築したり、失敗したデプロイのロールバックを実行したりすることができます。

アプリの構成では、構成ストアの過剰な呼び出しを避けるために、各設定が自動的にキャッシュされます。 キャッシュされた設定の値は、構成ストアで変更されたとしても、その有効期限が切れるまで、設定の更新操作は先延ばしされます。 キャッシュの既定の有効期間は 30 秒です。 有効期限を無効にすることができます。

アプリの構成では、転送中および保存中のすべての構成値が暗号化されます。 キー名とラベルは、構成データを取得するためのインデックスとして使用され、暗号化されません。

アプリ構成ではセキュリティが強化されていますが、アプリケーションシークレットを格納するための最適な場所は Azure Key Vault です。 Key Vault には、ハードウェアレベルの暗号化、きめ細かいアクセスポリシー、および証明書のローテーションなどの管理操作が用意されています。 Key Vault に格納されているシークレットを参照するアプリ構成値を作成できます。

## <a name="azure-key-vault"></a>Azure Key Vault

Key Vault は、機密情報を安全に格納してアクセスするための管理されたサービスです。 シークレットは、API キー、パスワード、証明書など、アクセスを厳密に制御する必要がある任意のものです。 コンテナーはシークレットの論理グループです。

Key Vault によって、シークレットが誤って漏洩する可能性が大幅に小さくなります。 Key Vault を使用すると、アプリケーション開発者は、アプリケーションにセキュリティ情報を格納する必要がなくなります。 この方法では、この情報をコード内に格納する必要がなくなります。 たとえば、必要に応じてデータベースに接続するアプリケーションがあるとします。 この場合、接続文字列をアプリのコードに格納する代わりに、Key Vault に安全に格納できます。

アプリケーションでは、URI を使用して、必要な情報に安全にアクセスできます。 アプリケーションでは、これらの URI を使用して特定のバージョンのシークレットを取得できます。 Key Vault に格納されている機密情報を保護するために、カスタムコードを記述する必要はありません。

Key Vault にアクセスするには、適切な呼び出し元の認証と承認が必要です。 通常、各クラウドネイティブマイクロサービスでは、ClientId/ClientSecret の組み合わせを使用します。 これらの資格情報は、ソース管理の外部で保持することが重要です。 アプリケーションの環境で設定することをお勧めします。 AKS から Key Vault への直接アクセスは、 [FlexVolume Key Vault](https://github.com/Azure/kubernetes-keyvault-flexvol)使用して実現できます。

## <a name="configuration-in-eshop"></a>EShop での構成

EShopOnContainers アプリケーションには、各マイクロサービスにローカルアプリケーション設定ファイルが含まれています。 これらのファイルはソース管理にチェックインされますが、接続文字列や API キーなどの運用シークレットは含まれません。 運用環境では、個々の設定がサービスごとの環境変数で上書きされる可能性があります。 環境変数にシークレットを挿入することは、ホストされるアプリケーションの一般的な方法ですが、中央の構成ストアは提供しません。 構成設定の一元管理をサポートするために、各マイクロサービスには、ローカル設定または Azure Key Vault 設定の使用を切り替えるための設定が含まれています。

## <a name="references"></a>References

- [EShopOnContainers アーキテクチャ](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Architecture)
- [高いスケーラビリティと可用性のためにマイクロサービスと複数のコンテナー アプリケーションを調整する](https://docs.microsoft.com/dotnet/architecture/microservices/architect-microservice-container-applications/scalable-available-multi-container-microservice-applications)
- [Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-key-concepts)
- [Azure SQL Database の概要](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
- [Azure Cache for Redis](https://azure.microsoft.com/services/cache/)
- [Azure Cosmos DB の MongoDB 用 API](https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction)
- [Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)
- [Azure Monitor の概要](https://docs.microsoft.com/azure/azure-monitor/overview)
- [eShopOnContainers: AKS で Kubernetes クラスターを作成する](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Azure-Kubernetes-Service-(AKS)#create-kubernetes-cluster-in-aks)
- [eShopOnContainers: Azure Dev Spaces](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Azure-Dev-Spaces)
- [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/about)

>[!div class="step-by-step"]
>[前へ](deploy-eshoponcontainers-azure.md)
>[次へ](scale-applications.md)
