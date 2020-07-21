---
title: コードとしてのインフラストラクチャ
description: クラウドネイティブアプリケーションでのインフラストラクチャとしてのインフラストラクチャの導入 (IaC)
ms.date: 05/13/2020
ms.openlocfilehash: cfc9e1f0b2733048d5921de5a0400998c282b1fa
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613955"
---
# <a name="infrastructure-as-code"></a>コードとしてのインフラストラクチャ

クラウドネイティブシステムは、マイクロサービス、コンテナー、および最新のシステム設計を採用して、速度と機敏性を実現します。 一貫性のある品質のコードを確保するために、自動化されたビルドとリリースのステージを提供します。 しかし、これはストーリーの一部にすぎません。 これらのシステムを実行するクラウド環境をプロビジョニングするにはどうすればよいですか。

最新のクラウドネイティブアプリケーションは、広く受け入れられ[ているインフラストラクチャをコードとして](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code)、またはとして採用して `IaC` います。  IaC を使用すると、プラットフォームのプロビジョニングを自動化できます。 基本的に、テストやバージョン管理などのソフトウェアエンジニアリングプラクティスを DevOps プラクティスに適用します。 インフラストラクチャとデプロイは、自動化され、一貫性があり、反復可能です。 継続的デリバリーと同様に、手動デプロイの従来のモデルを自動化するのと同じように、Infrastructure as Code (IaC) は、アプリケーション環境の管理方法を進化させるものです。

Azure Resource Manager (ARM)、Terraform、Azure コマンドラインインターフェイス (CLI) などのツールを使用すると、必要なクラウドインフラストラクチャを宣言によってスクリプト化することができます。

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager のテンプレート

ARM は[Azure Resource Manager](https://azure.microsoft.com/documentation/articles/resource-group-overview/)を表します。 これは、Azure に組み込まれ、API サービスとして公開される API プロビジョニングエンジンです。 ARM では、Azure リソースグループに含まれるリソースを1回の連携した操作でデプロイ、更新、削除、管理することができます。 このエンジンには、必要なリソースとその構成を指定する JSON ベースのテンプレートが用意されています。 ARM は、依存関係を尊重する正しい順序で展開を自動的に調整します。 エンジンはべき等を保証します。 同じ構成の目的のリソースが既に存在する場合、プロビジョニングは無視されます。

Azure Resource Manager テンプレートは、Azure でさまざまなリソースを定義するための JSON ベースの言語です。 基本的なスキーマは、図10-14 のようになります。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "",
  "apiProfile": "",
  "parameters": {  },
  "variables": {  },
  "functions": [  ],
  "resources": [  ],
  "outputs": {  }
}
```

**図 10-14** -Resource Manager テンプレートのスキーマ

このテンプレート内では、次のように resources セクション内にストレージコンテナーを定義できます。

```json
"resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "location": "[parameters('location')]",
      "apiVersion": "2018-07-01",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "StorageV2",
      "properties": {}
    }
  ],
```

**図 10-15** -Resource Manager テンプレートで定義されたストレージアカウントの例

ARM テンプレートは、動的な環境と構成情報を使用してパラメーター化できます。 これにより、開発、QA、実稼働などのさまざまな環境を定義するために再利用できます。 通常、このテンプレートでは、1つの Azure リソースグループ内のすべてのリソースが作成されます。 必要に応じて、1つの Resource Manager テンプレートに複数のリソースグループを定義できます。 リソースグループ自体を削除することで、環境内のすべてのリソースを削除できます。 コスト分析は、リソースグループレベルで実行することもできます。これにより、各環境のコストをすばやく計算できます。

GitHub の[Azure クイックスタートテンプレート](https://github.com/Azure/azure-quickstart-templates)プロジェクトには、多くの例または ARM テンプレートが用意されています。 新しいテンプレートを作成したり、既存のテンプレートを変更したりするのに役立ちます。

Resource Manager テンプレートは、さまざまな方法で実行できます。 おそらく、簡単な方法は、単に Azure portal に貼り付けることです。 試験的なデプロイでは、この方法を簡単に行うことができます。 また、Azure DevOps のビルドプロセスまたはリリースプロセスの一部として実行することもできます。 Azure への接続を活用してテンプレートを実行するタスクがあります。 Resource Manager テンプレートへの変更は段階的に適用されます。つまり、新しいリソースを追加するには、テンプレートに追加するだけで済みます。 ツールは、現在のリソースと、テンプレートで定義されているリソースとの違いを調整します。 リソースは、テンプレートで定義されている内容と一致するように作成または変更されます。  

## <a name="terraform"></a>Terraform

クラウドネイティブアプリケーションは、多くの場合、として構築され `cloud agnostic` ます。 そのため、アプリケーションは特定のクラウドベンダーと緊密に結合されていないため、任意のパブリッククラウドにデプロイできます。

[Terraform](https://www.terraform.io/)は、すべての主要なクラウドプレーヤー (Azure、GOOGLE CLOUD PLATFORM、AWS、alicloud) でクラウドネイティブアプリケーションをプロビジョニングできる商用テンプレートツールです。 JSON をテンプレート定義言語として使用する代わりに、やや簡潔な YAML を使用します。

前の Resource Manager テンプレートと同様の Terraform ファイルの例 (図 10-15) を図10-16 に示します。

```terraform
provider "azurerm" {
  version = "=1.28.0"
}

resource "azurerm_resource_group" "test" {
  name     = "production"
  location = "West US"
}

resource "azurerm_storage_account" "testsa" {
  name                     = "${var.storageAccountName}"
  resource_group_name      = "${azurerm_resource_group.testrg.name}"
  location                 = "${var.region}"
  account_tier             = "${var.tier}"
  account_replication_type = "${var.replicationType}"

}
```

**図 10-16** -Resource Manager テンプレートの例

Terraform は、問題のあるテンプレートに対して直感的なエラーメッセージも提供します。 また、テンプレートエラーを早期にキャッチするためにビルドフェーズで使用できる、便利な検証タスクもあります。

Resource Manager テンプレートと同様に、コマンドラインツールを使用して Terraform テンプレートをデプロイできます。 また、Azure Pipelines には、Terraform テンプレートを検証して適用できるコミュニティによって作成されたタスクもあります。

Terraform と ARM テンプレートは、新しく作成されたデータベースへの接続文字列など、意味のある値を出力する場合があります。 この情報は、ビルドパイプラインでキャプチャし、後続のタスクで使用できます。

## <a name="azure-cli-scripts-and-tasks"></a>Azure CLI のスクリプトとタスク

最後に、 [Azure CLI](https://docs.microsoft.com/cli/azure/)を利用して、クラウドインフラストラクチャの宣言によるスクリプト作成を行うことができます。 Azure CLI スクリプトを作成、検出、および共有して、ほぼすべての Azure リソースをプロビジョニングして構成することができます。 CLI は、非常に簡単な学習曲線で簡単に使用できます。 スクリプトは、PowerShell または Bash 内で実行されます。 また、特に ARM テンプレートと比較してデバッグするのも簡単です。

Azure CLI スクリプトは、インフラストラクチャを破棄して再展開する必要がある場合に適しています。 既存の環境を更新することは、難しい場合があります。 多くの CLI コマンドはべき等ではありません。 つまり、リソースが既に存在する場合でも、実行されるたびにリソースが再作成されます。 各リソースが作成される前に存在するかどうかをチェックするコードを追加することは常に可能です。 しかし、そうすると、スクリプトが肥大化し、管理が困難になる可能性があります。

これらのスクリプトは、Azure DevOps パイプラインにとして埋め込むこともでき `Azure CLI tasks` ます。 パイプラインを実行すると、スクリプトが呼び出されます。

図10-17 は、Azure CLI のバージョンとサブスクリプションの詳細を一覧表示する YAML スニペットを示しています。 インラインスクリプトに Azure CLI コマンドが含まれていることに注意してください。

```yaml
- task: AzureCLI@2
  displayName: Azure CLI
  inputs:
    azureSubscription: <Name of the Azure Resource Manager service connection>
    scriptType: ps
    scriptLocation: inlineScript
    inlineScript: |
      az --version
      az account show
```

**図 10-17** -Azure CLI スクリプト

「[コードとしてのインフラストラクチャとは](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code)」の記事では、作成者 Sam Guckenheimer は、"IaC を実装するチームは、安定した環境を迅速かつ大規模に提供する方法を説明しています。 チームは環境の手動構成を回避し、コードを使用して環境の望ましい状態を表すことによって一貫性を適用します。 IaC を使用したインフラストラクチャのデプロイは反復可能であり、構成のずれや依存関係の不足によって発生するランタイムの問題を回避できます。 DevOps チームは、統合された一連のプラクティスとツールを一緒に使用して、アプリケーションとそのサポートインフラストラクチャを迅速かつ確実に、かつ大規模に配信できます。 "

>[!div class="step-by-step"]
>[前へ](feature-flags.md)
>[次へ](application-bundles.md)
