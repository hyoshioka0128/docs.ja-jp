---
title: dotnet テストと xUnit を使用した .NET Core での単体テスト Visual Basic
description: dotnet テストおよび xUnit を使用した Visual Basic ソリューションのサンプルを段階的に構築していく対話型エクスペリエンスを通じて、.NET Core の単体テストの概念について説明します。
author: billwagner
ms.author: wiwagn
ms.date: 05/18/2020
ms.openlocfilehash: d87550d692e0b7f3bfee1633bd00cbf501cc2e67
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502757"
---
# <a name="unit-testing-visual-basic-net-core-libraries-using-dotnet-test-and-xunit"></a>dotnet テストと xUnit を使用した Visual Basic .NET Core ライブラリでの単体テスト

このチュートリアルでは、単体テスト プロジェクトとライブラリ プロジェクトが含まれるソリューションを構築する方法を示します。 構築済みのソリューションを使用してチュートリアルに従う場合は、[サンプル コードを表示またはダウンロードしてください](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-using-dotnet-test/)。 ダウンロード方法については、「[サンプルおよびチュートリアル](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)」を参照してください。

## <a name="create-the-solution"></a>ソリューションを作成する

このセクションでは、ソース プロジェクトとテスト プロジェクトを含むソリューションが作成されます。 完成したソリューションのディレクトリ構造は次のようになります。

```
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
        PrimeService.vb
        PrimeService.vbproj
    /PrimeService.Tests
        PrimeService_IsPrimeShould.vb
        PrimeServiceTests.vbproj
```

テスト ソリューションを作成する手順を次に示します。 テスト ソリューションをワンステップで作成する手順については、[テスト ソリューションを作成するためのコマンド](#create-test-cmd)に関する記事を参照してください。

* シェル ウィンドウを開きます。
* 次のコマンドを実行します。

  ```dotnetcli
  dotnet new sln -o unit-testing-using-dotnet-test
  ```

  [`dotnet new sln`](../tools/dotnet-new.md) コマンドによって、新しいソリューションが *unit-testing-using-dotnet-test* ディレクトリに作成されます。
* ディレクトリを *unit-testing-using-dotnet-test* フォルダーに変更します。
* 次のコマンドを実行します。

  ```dotnetcli
  dotnet new classlib -o PrimeService --lang VB
  ```

   [`dotnet new classlib`](../tools/dotnet-new.md) コマンドによって、*PrimeService* フォルダーに新しいクラス ライブラリ プロジェクトが作成されます。 この新しいクラス ライブラリに、テスト対象のコードが含まれることになります。
* *Class1.vb* の名前を *PrimeService.vb* に変更します。
* *PrimeService.vb* のコードを、次のコードに置き換えます。
  
  ```vb
  Imports System
  
  Namespace Prime.Services
      Public Class PrimeService
          Public Function IsPrime(candidate As Integer) As Boolean
              Throw New NotImplementedException("Not implemented.")
          End Function
      End Class
  End Namespace
  ```

* 上記のコードでは次の操作が行われます。
  * 実装されていないことを示すメッセージを含む <xref:System.NotImplementedException> がスローされます。
  * このチュートリアルの中で、後で更新します。

<!-- preceding code shows an english bias. Message makes no sense outside english -->

* *unit-testing-using-dotnet-test* ディレクトリで、次のコマンドを実行して、クラス ライブラリ プロジェクトをソリューションに追加します。

  ```dotnetcli
  dotnet sln add ./PrimeService/PrimeService.vbproj
  ```

* 次のコマンドを実行して、*PrimeService.Tests* プロジェクトを作成します。

  ```dotnetcli
  dotnet new xunit -o PrimeService.Tests
  ```

* 上記のコマンドにより、次のことが行われます。
  * *PrimeService.Tests* ディレクトリに *PrimeService.Tests* プロジェクトが作成されます。 このテスト プロジェクトでは、テスト ライブラリとして [xUnit](https://xunit.net/) が使用されます。
  * プロジェクト ファイルに次の `<PackageReference />` 要素を追加することで、テスト ランナーを構成します。
    * "Microsoft.NET.Test.Sdk"
    * "xunit"
    * "xunit.runner.visualstudio"

* 次のコマンドを実行して、ソリューション ファイルにテスト プロジェクトを追加します。

  ```dotnetcli
  dotnet sln add ./PrimeService.Tests/PrimeService.Tests.vbproj
  ```

* *PrimeService.Tests* プロジェクトへの依存関係として `PrimeService` クラス ライブラリを追加します。

  ```dotnetcli
  dotnet add ./PrimeService.Tests/PrimeService.Tests.vbproj reference ./PrimeService/PrimeService.vbproj  
  ```

<a name="create-test-cmd"></a>

### <a name="commands-to-create-the-solution"></a>ソリューションを作成するためのコマンド

このセクションでは、前のセクション内のすべてのコマンドの概要を示します。 前のセクションの手順を完了している場合は、このセクションをスキップしてください。

次のコマンドによって、Windows コンピューター上にテスト ソリューションが作成されます。 macOS と Unix の場合は、`ren` コマンドを `ren` の OS バージョンに更新してファイルの名前を変更します。

```dotnetcli
dotnet new sln -o unit-testing-using-dotnet-test
cd unit-testing-using-dotnet-test
dotnet new classlib -o PrimeService
ren .\PrimeService\Class1.vb PrimeService.vb
dotnet sln add ./PrimeService/PrimeService.vbproj
dotnet new xunit -o PrimeService.Tests
dotnet add ./PrimeService.Tests/PrimeService.Tests.vbproj reference ./PrimeService/PrimeService.vbproj
dotnet sln add ./PrimeService.Tests/PrimeService.Tests.vbproj
```

前のセクションの「*PrimeService.vb* 内のコードを次のコードに置き換える」の指示に従います。

## <a name="create-a-test"></a>テストの作成

テスト駆動開発 (TDD) の一般的なアプローチは、ターゲット コードを実装する前にテストを記述することです。 このチュートリアルでは、この TDD アプローチを使用します。 `IsPrime` メソッドは呼び出し可能ですが、実装されていません。 `IsPrime` のテスト呼び出しは失敗します。 TDD では、失敗することがわかっているテストを記述します。 テストに合格するように、ターゲット コードを更新します。 このアプローチを繰り返して、失敗するテストを記述した後、テストに合格するようにターゲット コードを更新します。

*PrimeService.Tests* プロジェクトを更新します。

* *PrimeService.Tests/UnitTest1.vb* を削除します。
* *PrimeService.Tests/PrimeService_IsPrimeShould.vb* ファイルを作成します。
* *PrimeService_IsPrimeShould.vb* のコードを、次のコードに置き換えます。

```vb
Imports Xunit

Namespace PrimeService.Tests
    Public Class PrimeService_IsPrimeShould
        Private ReadOnly _primeService As Prime.Services.PrimeService

        Public Sub New()
            _primeService = New Prime.Services.PrimeService()
        End Sub


        <Fact>
        Sub IsPrime_InputIs1_ReturnFalse()
            Dim result As Boolean = _primeService.IsPrime(1)

            Assert.False(result, "1 should not be prime")
        End Sub

    End Class
End Namespace
```

`[Fact]` 属性で、テスト ランナーによって実行されるテスト メソッドを宣言します。 *PrimeService.Tests* フォルダーから、`dotnet test` を実行します。 [dotnet test](../tools/dotnet-test.md) コマンドで、両方のプロジェクトをビルドし、テストを実行します。 xUnit テスト ランナーには、テストを実行するためのプログラムのエントリ ポイントが含まれています。 `dotnet test` で、単体テスト プロジェクトを使用するテスト ランナーが開始されます。

`IsPrime` が実装されていないため、テストは失敗します。 TDD アプローチでは、このテストに合格するのに十分なコードだけを記述します。 次のコードを使用して `IsPrime` を更新します。

```vb
Public Function IsPrime(candidate As Integer) As Boolean
    If candidate = 1 Then
        Return False
    End If
    Throw New NotImplementedException("Not implemented.")
End Function
```

`dotnet test` を実行します。 テストに合格します。

### <a name="add-more-tests"></a>さらにテストを追加する

0 と -1 のための素数テストを追加します。 前のテストをコピーし、次のコードを 0 と -1 を使用するように変更できます。

```vb
Dim result As Boolean = _primeService.IsPrime(1)

Assert.False(result, "1 should not be prime")
```

パラメーターだけを変更するときにテスト コードをコピーすると、コードの重複が発生してテストが膨張します。 次の xUnit 属性を使用して、類似する一連のテストを記述できます。

- `[Theory]` は同じコードを実行するものの、異なる入力引数が含まれる一連のテストを表します。
- `[InlineData]` 属性は、これらの入力の値を指定します。

新しいテストを作成するのではなく、上記の xUnit 属性を適用することで、単一の理論を作成できます。 以下のコードを

```vb
<Fact>
Sub IsPrime_InputIs1_ReturnFalse()
    Dim result As Boolean = _primeService.IsPrime(1)

    Assert.False(result, "1 should not be prime")
End Sub
```

次のコードに置き換えます。

```vb
<Theory>
<InlineData(-1)>
<InlineData(0)>
<InlineData(1)>
Sub IsPrime_ValuesLessThan2_ReturnFalse(ByVal value As Integer)
    Dim result As Boolean = _primeService.IsPrime(value)

    Assert.False(result, $"{value} should not be prime")
End Sub
```

上記のコードでは、`[Theory]` と `[InlineData]` によって、2 未満のいくつかの値をテストできます。 2 は最小の素数です。

`dotnet test` を実行すると、2 のテストは失敗します。 すべてのテストに合格するようにするには、次のコードで `IsPrime` メソッドを更新します。

```vb
Public Function IsPrime(candidate As Integer) As Boolean
    If candidate < 2 Then
        Return False
    End If
    Throw New NotImplementedException("Not fully implemented.")
End Function
```

TDD アプローチに従って、失敗するテストをさらに追加した後、ターゲット コードを更新します。 [テストの最終版](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-vb-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.vb)と、[ライブラリの完全な実装](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-vb-dotnet-test/PrimeService/PrimeService.vb)を参照してください。

完成した `IsPrime` メソッドは、素数性をテストするための効率的なアルゴリズムではありません。

### <a name="additional-resources"></a>その他の技術情報

- [xUnit.net の公式サイト](https://xunit.net/)
- [ASP.NET Core のコントローラー ロジックをテストする](/aspnet/core/mvc/controllers/testing)
- [`dotnet add reference`](../tools/dotnet-add-reference.md)
