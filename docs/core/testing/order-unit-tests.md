---
title: 単体テストの順序を設定する
description: .NET Core で単体テストの順序を設定する方法について説明します。
author: IEvangelist
ms.author: dapine
ms.date: 05/18/2020
zone_pivot_groups: unit-testing-framework-set-one
ms.openlocfilehash: eb426b790e0623b0cf233a763e93d2bd501b8034
ms.sourcegitcommit: 4ad2f8920251f3744240c3b42a443ffbe0a46577
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86100822"
---
# <a name="order-unit-tests"></a>単体テストの順序を設定する

場合によっては、単体テストを特定の順序で実行する必要があります。 理想的には、単体テストの実行順序が問題になるようなことがあっては "_ならず_"、単体テストの順序を設定しなくて済むようにするのが[ベスト プラクティス](unit-testing-best-practices.md)です。 そうはいっても、それを行うことが必要になる場合があります。 この記事では、そのような場合にテストの実行順序を設定する方法について説明します。

ソース コードを見た方がよい場合は、「[.NET Core の単体テストの順序を設定する](/samples/dotnet/samples/order-unit-tests-cs)」サンプル リポジトリを参照してください。

> [!TIP]
> この記事で説明する順序設定機能に加え、代わりの方法として、[Visual Studio でカスタム プレイリストを作成する](/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2019#create-custom-playlists)ことを検討してください。

:::zone pivot="mstest"

## <a name="order-alphabetically"></a>アルファベット順に設定する

MSTest では、テストはテスト名の順序に自動的に設定されます。

> [!NOTE]
> 番号 `2` の方が `14` より小さくても、`Test14` という名前のテストが `Test2` より前に実行されます。 これは、テスト名の順序の設定ではテストのテキスト名が使用されるためです。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/MSTest.Project/ByAlphabeticalOrder.cs":::

:::zone-end
:::zone pivot="xunit"

xUnit テスト フレームワークでは、テストの実行順序をさらに細かく制御できます。 クラスのテスト ケースまたはテスト コレクションの順序を制御するには、`ITestCaseOrderer` インターフェイスと `ITestCollectionOrderer` インターフェイスを実装します。

## <a name="order-by-test-case-alphabetically"></a>テスト ケースのアルファベット順に順序を設定する

メソッド名でテスト ケースの順序を設定するには、`ITestCaseOrderer` を実装し、順序設定のメカニズムを提供します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/Orderers/AlphabeticalOrderer.cs":::

その後、テスト クラスで、`TestCaseOrdererAttribute` を使用してテスト ケースの順序を設定します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/ByAlphabeticalOrder.cs":::

## <a name="order-by-collection-alphabetically"></a>コレクションのアルファベット順に順序を設定する

表示名でテスト コレクションの順序を設定するには、`ITestCollectionOrderer` を実装し、順序設定のメカニズムを提供します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/Orderers/DisplayNameOrderer.cs":::

テスト コレクションは並列に実行される可能性があるため、`CollectionBehaviorAttribute` を使用して、コレクションのテスト並列化を明示的に無効にする必要があります。 その後、`TestCollectionOrdererAttribute` の実装を指定します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/ByDisplayName.cs":::

## <a name="order-by-custom-attribute"></a>カスタム属性で順序を設定する

カスタム属性で xUnit テストの順序を設定するには、その前に、利用する属性が存在している必要があります。 次のように `TestPriorityAttribute` を定義します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/Attributes/TestPriorityAttribute.cs":::

次に、`ITestCaseOrderer` インターフェイスの `PriorityOrderer` の実装を次のようにします。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/Orderers/PriorityOrderer.cs":::

その後、テスト クラスで、`TestCaseOrdererAttribute` を `PriorityOrderer` にしてテスト ケースの順序を設定します。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/XUnit.TestProject/ByPriorityOrder.cs":::

:::zone-end
:::zone pivot="nunit"

## <a name="order-by-priority"></a>優先順位で順序を設定する

テストの順序を明示的に設定できるように、NUnit には [`OrderAttribute`](https://github.com/nunit/docs/wiki/Order-Attribute) が用意されています。 この属性が指定されているテストは、指定されていないテストより前に開始されます。 順序の値を使用して、単体テストを実行する順序が決定されます。

:::code language="csharp" source="~/dotnet-samples/csharp/unit-testing/NUnit.TestProject/ByOrder.cs":::

:::zone-end

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [単体テストのコード カバレッジ](unit-testing-code-coverage.md)
