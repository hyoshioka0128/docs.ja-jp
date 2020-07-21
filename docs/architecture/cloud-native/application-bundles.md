---
title: クラウド ネイティブ アプリケーション バンドル
description: Azure 向けのクラウドネイティブ .NET アプリの設計 |クラウドネイティブアプリケーションバンドル
ms.date: 05/13/2020
ms.openlocfilehash: fc6ee96078650dccd2ebeb3e65a0a00c4e05ecdb
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614345"
---
# <a name="cloud-native-application-bundles"></a>クラウド ネイティブ アプリケーション バンドル

クラウドネイティブアプリケーションの重要な特性は、クラウドの機能を活用して開発を高速化できることです。 この設計は、多くの場合、アプリケーション全体がさまざまな種類のテクノロジを使用することを意味します。 アプリケーションは、Docker コンテナーに配布される場合があります。一部のサービスでは Azure Functions が使用される場合がありますが、ハードウェア GPU アクセラレーションを使用する大金属サーバー上に割り当てられた仮想マシン上で直接実行することもできます。 2つのクラウドネイティブアプリケーションは同じではありません。そのため、1つのメカニズムを配布することは困難でした。

Docker コンテナーは、配置のためのヘルムグラフを使用して、Kubernetes 上で実行できます。 Azure Functions は、Terraform テンプレートを使用して割り当てることができます。 最後に、仮想マシンは Terraform を使用して割り当てられますが、を使用して構築される可能性があります。 これは非常に厄介なテクノロジであり、すべてを適切なパッケージにパッケージ化する方法はありませんでした。 これまでは。

クラウドネイティブアプリケーションバンドル (CNABs) は、分散アプリケーションをパッケージ化するための仕様を開発するために、Microsoft、Docker、HashiCorp などの多数のコミュニティ志向企業による共同作業です。

この作業は2018年12月に発表されました。そのため、より大きなコミュニティに労力を公開するために、かなりの作業が必要になります。 ただし、既に開いている[仕様](https://github.com/deislabs/cnab-spec)と、[ダッフル](https://duffle.sh/)と呼ばれる参照実装があります。 このツールは、外出先で作成されたもので、Docker と Microsoft の間の共同作業です。

CNABs には、さまざまな種類のインストールテクノロジを含めることができます。 これにより、ヘルムグラフ、Terraform テンプレート、およびその他のプレイブックのようなものを同じパッケージに共存させることができます。 ビルドされると、パッケージは自己完結型でポータブルになります。USB スティックからインストールできます。  パッケージは、要求されたパーティからのものであることを確認するために、暗号署名が行われます。

CNAB の中核となるのは、という名前のファイルです `bundle.json` 。 このファイルでは、バンドルの内容を定義します。このファイルは、Terraform や images などです。 図11-9 では、Terraform を呼び出す CNAB を定義しています。 ただし、Terraform を呼び出すために使用される呼び出しイメージを実際に定義することに注意してください。 パッケージ化されると、 *cnab*ディレクトリに配置されている docker ファイルは、バンドルに含まれる docker イメージに組み込まれます。 バンドル内の Docker コンテナー内に Terraform をインストールすると、バンドルを実行するためにユーザーのコンピューターに Terraform をインストールする必要がなくなります。

```json
{
    "name": "terraform",
    "version": "0.1.0",
    "schemaVersion": "v1.0.0-WD",
    "parameters": {
        "backend": {
            "type": "boolean",
            "defaultValue": false,
            "destination": {
                "env": "TF_VAR_backend"
            }
        }
    },
    "invocationImages": [
        {
        "imageType": "docker",
        "image": "cnab/terraform:latest"
        }
    ],
    "credentials": {
        "tenant_id": {
            "env": "TF_VAR_tenant_id"
        },
        "client_id": {
            "env": "TF_VAR_client_id"
        },
        "client_secret": {
            "env": "TF_VAR_client_secret"
        },
        "subscription_id": {
            "env": "TF_VAR_subscription_id"
        },
        "ssh_authorized_key": {
            "env": "TF_VAR_ssh_authorized_key"
        }
    },
    "actions": {
        "status": {
            "modifies": true
        }
    }
}
```

**図 10-18** -Terraform ファイルの例

また、は、 `bundle.json` Terraform に渡されるパラメーターのセットも定義します。 バンドルのパラメーター化により、さまざまな環境でのインストールが可能になります。

また、CNAB 形式は柔軟であり、任意のクラウドに対して使用することができます。 [Openstack](https://www.openstack.org/)などのオンプレミスソリューションに対しても使用できます。

## <a name="devops-decisions"></a>DevOps の意思決定

これらの日の DevOps 領域には多くの優れたツールがあり、これを成功させる方法についてはもっとすばらしい書籍や論文もあります。 DevOps の旅を始めるためのお気に入りの書籍は、架空の企業を NoOps から DevOps に変換する、[フェニックスのプロジェクト](https://www.oreilly.com/library/view/the-phoenix-project/9781457191350/)です。 1つは、複雑なクラウドネイティブアプリケーションをデプロイするときに、DevOps が "優れた" ということです。 これは要件であり、プロジェクトの開始時に、およびに対して計画を行う必要があります。

## <a name="references"></a>References

- [Azure DevOps](https://azure.microsoft.com/services/devops/)
- [Azure Resource Manager](https://azure.microsoft.com/documentation/articles/resource-group-overview/)
- [Terraform](https://www.terraform.io/)
- [Azure CLI](https://docs.microsoft.com/cli/azure/)

>[!div class="step-by-step"]
>[前へ](infrastructure-as-code.md)
>[次へ](summary.md)
