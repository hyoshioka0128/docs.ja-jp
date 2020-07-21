---
title: 機能フラグ
description: Azure アプリ構成を利用するクラウドネイティブアプリケーションで機能フラグを実装する
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 607bd14a415a25b382f550e697542cf749a21772
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614072"
---
# <a name="feature-flags"></a>機能フラグ

第1章では、クラウドネイティブの速度と機敏性が非常に高くなっています。 ユーザーは、迅速な応答性と革新的な機能を期待し、ダウンタイムをゼロにする必要があります。 `Feature flags`は、クラウドネイティブアプリケーションの俊敏性を向上させるための最新の展開手法です。 新しい機能を運用環境に展開することはできますが、その可用性は制限されます。 スイッチのフリックを使用すると、アプリを再起動したり新しいコードを展開したりせずに、特定のユーザーに対して新しい機能をアクティブ化できます。 これらは、新機能のリリースをコード配置から分離します。

機能フラグは、実行時にユーザーの機能の可視性を制御する条件付きロジックに基づいて構築されます。 最新のクラウドネイティブシステムでは、新しい機能を早い段階で運用環境にデプロイすることは一般的ですが、限定された対象ユーザーを使用してテストします。 信頼度が高くなるにつれて、機能をより広範な対象ユーザーに段階的にロールアウトできます。

機能フラグのその他のユースケースは次のとおりです。

- Premium 機能を特定の顧客グループに限定して、より高いサブスクリプション料金を支払うことができます。
- 問題のある機能を迅速に非アクティブ化してシステムを安定化し、ロールバックや即時修正プログラムのリスクを回避します。
- ピーク時の使用期間中にリソース使用率が高いオプション機能を無効にします。
- `experimental feature releases`小規模のユーザーセグメントに対して、実現可能性と人気度を検証します。

機能フラグも `trunk-based` 開発を促進します。 これは、開発者が1つの分岐の機能に対して共同作業を行うソース管理の分岐モデルです。 この方法では、多数の実行時間の長い機能ブランチをマージするリスクと複雑さが最小限に抑えられます。 機能は、アクティブ化されるまで使用できません。

## <a name="implementing-feature-flags"></a>機能フラグの実装

主要な特徴フラグは、単純なへの参照です `decision object` 。 またはのブール値の状態を返し `on` `off` ます。 通常、このフラグは、機能機能をカプセル化するコードブロックをラップします。 フラグの状態によって、そのコードブロックが特定のユーザーに対して実行されるかどうかが決まります。 図10-11 に実装を示します。

```c#
if (featureFlag) {
    // Run this code block if the featureFlag value is true
} else {
    // Run this code block if the featureFlag value is false
}
```

**図 10-11** -単純な機能フラグの実装。

この方法では、機能コードから意思決定ロジックを分離する方法に注意してください。

第1章では、「」について説明しました `Twelve-Factor App` 。 構成設定をアプリケーションの実行可能コードから外部に保持することを推奨するガイダンスです。 必要に応じて、外部ソースから設定を読み取ることができます。 機能フラグの構成値は、コードベースから独立している必要もあります。 別のリポジトリに外部化するフラグを設定することにより、アプリケーションを変更して再デプロイしなくてもフラグの状態を変更できます。

[Azure アプリ構成](https://docs.microsoft.com/azure/azure-app-configuration/overview)では、機能フラグの一元的なリポジトリが提供されます。 この機能を使用すると、さまざまな種類の特徴フラグを定義し、その状態を迅速かつ自信を持って操作できます。 アプリ構成クライアントライブラリをアプリケーションに追加して、機能フラグの機能を有効にします。 さまざまなプログラミング言語フレームワークがサポートされています。

機能フラグは、 [ASP.NET Core サービス](https://docs.microsoft.com/azure/azure-app-configuration/use-feature-flags-dotnet-core)に簡単に実装できます。 .NET 機能管理ライブラリとアプリ構成プロバイダーをインストールすると、宣言によって機能フラグをコードに追加できます。 属性を有効にすると、 `FeatureGate` コードベースで if ステートメントを手動で作成する必要がなくなります。

Startup クラスで構成すると、コントローラー、アクション、またはミドルウェアレベルで機能フラグ機能を追加できます。 図10-12 は、コントローラーとアクションの実装を示しています。

```c#
[FeatureGate(MyFeatureFlags.FeatureA)]
public class ProductController : Controller
{
    ...
}
```

```c#
[FeatureGate(MyFeatureFlags.FeatureA)]
public IActionResult UpdateProductStatus()
{
    return ObjectResult(ProductDto);
}
```

**図 10-12** -コントローラーとアクションでの機能フラグの実装

機能フラグが無効になっている場合、ユーザーには応答本文のない 404 (見つかりません) 状態コードが表示されます。

機能フラグは、C# クラスに直接挿入することもできます。 図10-13 は、機能フラグの挿入を示しています。

```c#
public class ProductController : Controller
{
    private readonly IFeatureManager _featureManager;

    public ProductController(IFeatureManager featureManager)
    {
        _featureManager = featureManager;
    }
}
```

**図 10-13** -クラスへの機能フラグの挿入

機能管理ライブラリは、バックグラウンドで機能フラグのライフサイクルを管理します。 たとえば、構成ストアへの呼び出しの数を最小限に抑えるために、ライブラリは指定された期間のフラグの状態をキャッシュします。 要求の呼び出し中にフラグの状態の不変性を保証できます。 また、も提供 `Point-in-time snapshot` します。 任意のキー値の履歴を再構築し、過去7日以内の任意の時点でその過去の値を提供できます。

>[!div class="step-by-step"]
>[前へ](devops.md)
>[次へ](infrastructure-as-code.md)
