---
title: 単体テストにコードカバレッジを使用する
description: .NET の単体テストでコードカバレッジ機能を使用する方法について説明します。
author: IEvangelist
ms.author: dapine
ms.date: 07/01/2020
ms.openlocfilehash: af64116e86c3f46f37c8d5d079b9c86084095485
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853905"
---
# <a name="use-code-coverage-for-unit-testing"></a>単体テストにコードカバレッジを使用する

単体テストは、機能を保証し、リファクタリングの際の検証手段となります。 コードカバレッジとは、単体テストで実行する、行、分岐、またはメソッドのいずれかのコード量の尺度です。 たとえば、条件分岐が (_分岐 a_ と_分岐 b_ の) 2 つしかない単純なアプリケーションのコードで、条件付き_分岐 a_ を単体テストで検証する場合、分岐のコードカバレッジは 50% と報告されます。

この記事では、Coverlet での単体テストでのコードカバレッジの用途と、ReportGenerator でのレポートの生成について説明します。 この記事では、テスト フレームワークとして C# と xUnit を使用していますが、MSTest と NUnit のいずれも使用することが可能です。 Coverlet とは、C# 用のクロスプラットフォームのコードカバレッジのフレームワークである、[GitHub 上のオープン ソース プロジェクト](https://github.com/coverlet-coverage/coverlet)です。 [Coverlet](https://dotnetfoundation.org/projects/coverlet) は .NET Foundation に含まれています。 Coverlet は、レポートの生成に使用する Cobertura のカバレッジのテストの実行データを収集します。

この記事では、Coverlet のテストの実行から収集したコードカバレッジ情報を使用して、レポートを生成する方法についても詳しく説明します。 レポートは、別の [GitHub 上のオープンソース プロジェクトである ReportGenerator](https://github.com/danielpalme/ReportGenerator) を使用して生成できます。 ReportGenerator では、Cobertura などから生成されたカバレッジレポートを、人間が判読できるさまざまな形式のレポートに変換します。

この記事は、サンプル ブラウザーで使用できる、[サンプル ソース コード プロジェクト](https://docs.microsoft.com/samples/dotnet/samples/unit-testing-code-coverage-cs)に基づいています。

## <a name="system-under-test"></a>テスト対象のシステム

"テスト対象のシステム" とは、単体テストを記述している対象のコードを指します。これは、オブジェクト、サービス、またはその他のテスト可能な機能を公開しているものです。 この記事では、テスト対象のシステムとなるクラス ライブラリと、それに対応する 2 つの単体テスト プロジェクトを作成します。

### <a name="create-a-class-library"></a>クラス ライブラリを作成する

コマンド プロンプトで、次のように [`dotnet new classlib`](../tools/dotnet-new.md#classlib) コマンドを使用して、`UnitTestingCodeCoverage` という名前の新しいディレクトリに、新しい .NET Standard クラス ライブラリを作成します。

```dotnetcli
dotnet new classlib -n Numbers
```

以下のスニペットでは、数値が素数であるかどうかを確認する単純な `PrimeService` クラスを定義しています。 以下のスニペットをコピーし、*Numbers* ディレクトリに自動作成された *Class1.cs* の内容と置き換えます。 *Class1.cs* ファイルを *PrimeService.cs* に名前変更します。

```csharp
namespace System.Numbers
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            if (candidate < 2)
            {
                return false;
            }

            for (int divisor = 2; divisor <= Math.Sqrt(candidate); ++divisor)
            {
                if (candidate % divisor == 0)
                {
                    return false;
                }
            }
            return true;
        }
    }
}
```

> [!TIP]
> `Numbers` クラス ライブラリが意図的に `System` 名前空間に追加されていることに着目してください。 これにより、`using System;` 名前空間を宣言せずに <xref:System.Math?displayProperty=fullName> にアクセスできます。 詳細については、「[namespace (C# リファレンス)](../../csharp/language-reference/keywords/namespace.md)」を参照してください。

### <a name="create-test-projects"></a>テスト プロジェクトを作成する

次のように、[`dotnet new xunit`](../tools/dotnet-new.md#test) コマンドを使用して、同じコマンド プロンプトから 2 つの新しい **xUnit テスト プロジェクト (.NET Core)** テンプレートを作成します。

```dotnetcli
dotnet new xunit -n XUnit.Coverlet.Collector
```

```dotnetcli
dotnet new xunit -n XUnit.Coverlet.MSBuild
```

新しく作成した 2 つの xUnit テスト プロジェクトには、*Numbers* クラス ライブラリのプロジェクト参照が追加される必要があります。 これにより、テストのためにテスト プロジェクトが *PrimeService* にアクセスできるようになります。 コマンド プロンプトで、次のように [`dotnet add`](../tools/dotnet-add-reference.md) コマンドを使用します。

```dotnetcli
dotnet add XUnit.Coverlet.Collector\XUnit.Coverlet.Collector.csproj reference Numbers\Numbers.csproj
```

```dotnetcli
dotnet add XUnit.Coverlet.MSBuild\XUnit.Coverlet.MSBuild.csproj reference Numbers\Numbers.csproj
```

[coverlet.msbuild](https://www.nuget.org/packages/coverlet.msbuild) NuGet パッケージに依存して、*MSBuild* プロジェクトに適切な名前が付けられます。 次のように [`dotnet add package`](../tools/dotnet-add-package.md) コマンドを実行し、このパッケージの依存関係を追加します。

```dotnetcli
cd XUnit.Coverlet.MSBuild && dotnet add package coverlet.msbuild && cd ..
```

前のコマンドでは、ディレクトリを効果的に *MSBuild* テスト プロジェクトに変更し、NuGet パッケージを追加しました。 これが完了すると、1 レベル上がり、ディレクトリが変更されます。

両方の *UnitTest1.cs* ファイルを開き、その内容を次のスニペットと置き換えます。 *UnitTest1.cs* ファイルを *PrimeServiceTests.cs* に名前変更します。

```csharp
using System.Numbers;
using Xunit;

namespace XUnit.Coverlet
{
    public class PrimeServiceTests
    {
        readonly PrimeService _primeService;

        public PrimeServiceTests() => _primeService = new PrimeService();

        [
            Theory,
            InlineData(-1), InlineData(0), InlineData(1)
        ]
        public void IsPrime_ValuesLessThan2_ReturnFalse(int value) =>
            Assert.False(_primeService.IsPrime(value), $"{value} should not be prime");

        [
            Theory,
            InlineData(2), InlineData(3), InlineData(5), InlineData(7)
        ]
        public void IsPrime_PrimesLessThan10_ReturnTrue(int value) =>
            Assert.True(_primeService.IsPrime(value), $"{value} should be prime");

        [
            Theory,
            InlineData(4), InlineData(6), InlineData(8), InlineData(9)
        ]
        public void IsPrime_NonPrimesLessThan10_ReturnFalse(int value) =>
            Assert.False(_primeService.IsPrime(value), $"{value} should not be prime");
    }
}
```

### <a name="create-a-solution"></a>ソリューションを作成する

コマンド プロンプトから、クラス ライブラリと 2 つのテスト プロジェクトをカプセル化する新しいソリューションを作成します。 [`dotnet sln`](../tools/dotnet-sln.md) コマンドの使用する場合、次のようになります。

```dotnetcli
dotnet new sln -n XUnit.Coverage
```

これにより、*UnitTestingCodeCoverage* ディレクトリに `XUnit.Coverage` という新しいソリューション ファイル名が作成されます。 ソリューションのルートにプロジェクトを追加します。

## <a name="linux"></a>[Linux](#tab/linux)

```dotnetcli
dotnet sln XUnit.Coverage.sln add **/*.csproj --in-root
```

## <a name="windows"></a>[Windows](#tab/windows)

```dotnetcli
dotnet sln XUnit.Coverage.sln add (ls **/*.csproj) --in-root
```

---

次のように [`dotnet build`](../tools/dotnet-build.md) コマンドを使用してソリューションを作成します。

```dotnetcli
dotnet build
```

ビルドが成功した場合は、3 つのプロジェクトが作成され、プロジェクトとパッケージが正しく参照され、ソース コードが正しく更新されます。 お疲れさまでした。

## <a name="tooling"></a>ツール

コード カバレッジには、次の 2 種類のツールがあります。

- **DataCollectors:** DataCollector は、テストの実行を監視し、テストの実行に関する情報を収集します。 これらでは、XML や JSON などのさまざまな出力形式で、収集された情報を報告します。 詳細については、[初めての DataCollector の使用](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/datacollector.md)に関する記事を参照してください。
- **レポート ジェネレーター:** テストの実行から収集したデータを使用して、多くの場合にスタイル付きの HTML でレポートを生成します。

このセクションでは、データ コレクター ツールに重点を置いて説明します。 コードカバレッジに Coverlet を使用する場合、既存の単体テスト プロジェクトにパッケージに対する正しい依存関係が存在している必要があります。または [.NET グローバル ツール](../tools/global-tools.md)と、それに対応する [coverlet.console](https://www.nuget.org/packages/coverlet.console) NuGet パッケージに依存している必要があります。

## <a name="integrate-with-net-test"></a>.NET のテストと統合する

XUnit テスト プロジェクト テンプレートは、既定で [coverlet.collector](https://www.nuget.org/packages/coverlet.collector) と統合されています。
コマンド プロンプトから、ディレクトリを *XUnit.Coverlet.Collector* プロジェクトに変更し、次のように [`dotnet test`](../tools/dotnet-test.md) コマンドを実行します。

```dotnetcli
cd XUnit.Coverlet.Collector && dotnet test --collect:"XPlat Code Coverage"
```

> [!NOTE]
> `"XPlat Code Coverage"` 引数は、Coverlet のデータ コレクターに対応するフレンドリ名です。 この名前は必須です。大文字と小文字は区別されません。

`dotnet test` の実行の一環で、*coverage.cobertura.xml* ファイルが結果として *TestResults* ディレクトリに出力されます。 この XML ファイルにその結果が格納されます。 これは、.NET Core CLI に依存するクロスプラットフォーム オプションであり、MSBuild を使用できないビルド システムに適しています。

*coverage.cobertura.xml* ファイルの例は、次のとおりです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<coverage line-rate="1" branch-rate="1" version="1.9" timestamp="1592248008"
          lines-covered="12" lines-valid="12" branches-covered="6" branches-valid="6">
  <sources>
    <source>C:\</source>
  </sources>
  <packages>
    <package name="Numbers" line-rate="1" branch-rate="1" complexity="6">
      <classes>
        <class name="Numbers.PrimeService" line-rate="1" branch-rate="1" complexity="6"
               filename="Numbers\PrimeService.cs">
          <methods>
            <method name="IsPrime" signature="(System.Int32)" line-rate="1"
                    branch-rate="1" complexity="6">
              <lines>
                <line number="8" hits="11" branch="False" />
                <line number="9" hits="11" branch="True" condition-coverage="100% (2/2)">
                  <conditions>
                    <condition number="7" type="jump" coverage="100%" />
                  </conditions>
                </line>
                <line number="10" hits="3" branch="False" />
                <line number="11" hits="3" branch="False" />
                <line number="14" hits="22" branch="True" condition-coverage="100% (2/2)">
                  <conditions>
                    <condition number="57" type="jump" coverage="100%" />
                  </conditions>
                </line>
                <line number="15" hits="7" branch="False" />
                <line number="16" hits="7" branch="True" condition-coverage="100% (2/2)">
                  <conditions>
                    <condition number="27" type="jump" coverage="100%" />
                  </conditions>
                </line>
                <line number="17" hits="4" branch="False" />
                <line number="18" hits="4" branch="False" />
                <line number="20" hits="3" branch="False" />
                <line number="21" hits="4" branch="False" />
                <line number="23" hits="11" branch="False" />
              </lines>
            </method>
          </methods>
          <lines>
            <line number="8" hits="11" branch="False" />
            <line number="9" hits="11" branch="True" condition-coverage="100% (2/2)">
              <conditions>
                <condition number="7" type="jump" coverage="100%" />
              </conditions>
            </line>
            <line number="10" hits="3" branch="False" />
            <line number="11" hits="3" branch="False" />
            <line number="14" hits="22" branch="True" condition-coverage="100% (2/2)">
              <conditions>
                <condition number="57" type="jump" coverage="100%" />
              </conditions>
            </line>
            <line number="15" hits="7" branch="False" />
            <line number="16" hits="7" branch="True" condition-coverage="100% (2/2)">
              <conditions>
                <condition number="27" type="jump" coverage="100%" />
              </conditions>
            </line>
            <line number="17" hits="4" branch="False" />
            <line number="18" hits="4" branch="False" />
            <line number="20" hits="3" branch="False" />
            <line number="21" hits="4" branch="False" />
            <line number="23" hits="11" branch="False" />
          </lines>
        </class>
      </classes>
    </package>
  </packages>
</coverage>
```

> [!TIP]
> ビルド システムで既に MSBuild を使用している場合は、代わりに MSBuild パッケージを使用することもできます。 コマンド プロンプトで、ディレクトリを *XUnit.Coverlet.MSBuild* プロジェクトに変更し、次のように `dotnet test` コマンドを実行します。
>
> ```dotnetcli
> dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=cobertura
> ```
>
> *coverage.cobertura.xml* ファイルが結果として出力されます。  
> [こちらの](https://github.com/coverlet-coverage/coverlet/blob/master/Documentation/MSBuildIntegration.md) msbuild 統合ガイドに従ってください

## <a name="generate-reports"></a>レポートの生成

これで、単体テストの実行からデータを収集できるようになったので、[ReportGenerator](https://github.com/danielpalme/ReportGenerator) を使用してレポートを生成できます。 次のように [`dotnet tool install`](../tools/dotnet-tool-install.md) コマンドを使用し、[.NET グローバル ツール](../tools/global-tools.md)として [ReportGenerator](https://www.nuget.org/packages/dotnet-reportgenerator-globaltool) NuGet パッケージをインストールします。

```dotnetcli
dotnet tool install -g dotnet-reportgenerator-globaltool
```

ツールを実行し、前のテストの実行の出力である *coverage.cobertura.xml* ファイルを指定して必要なオプションを指定します。

```console
reportgenerator
"-reports:Path\To\TestProject\TestResults\{guid}\coverage.cobertura.xml"
"-targetdir:coveragereport"
-reporttypes:Html
```

このコマンドを実行すると、HTML ファイルにレポートが生成されます。

:::image type="content" source="media/test-report.png" lightbox="media/test-report.png" alt-text="単体テストで生成されたレポート":::

## <a name="see-also"></a>関連項目

- [Visual Studio 単体テストのカバー カバレッジ](/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested)
- [GitHub - Coverlet リポジトリ](https://github.com/coverlet-coverage/coverlet)
- [GitHub - ReportGenerator リポジトリ](https://github.com/danielpalme/ReportGenerator)
- [ReportGenerator プロジェクト サイト](https://danielpalme.github.io/ReportGenerator)
- [.NET Core CLI テスト コマンド](../tools/dotnet-test.md)
- [サンプル ソース コード](https://docs.microsoft.com/samples/dotnet/samples/unit-testing-code-coverage-cs)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [ベスト プラクティスの単体テスト](unit-testing-best-practices.md)
