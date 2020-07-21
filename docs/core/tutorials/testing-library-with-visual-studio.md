---
title: Visual Studio を使用して .NET Core で .NET Standard クラス ライブラリをテストする
description: .NET Core クラス ライブラリ用の単体テスト プロジェクトを作成します。 .NET Core クラス ライブラリが単体テストで正しく動作することを確認します。
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: f20b089fd22794d5aaeff34502e960fe41a565e1
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84700970"
---
# <a name="tutorial-test-a-net-standard-class-library-with-net-core-using-visual-studio"></a>チュートリアル: Visual Studio を使用して .NET Core で .NET Standard クラス ライブラリをテストする

このチュートリアルでは、テスト プロジェクトをソリューションに追加して、単体テストを自動化する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、「[Visual Studio で .NET Standard ライブラリを構築する](library-with-visual-studio.md)」で作成したソリューションを使用します。

## <a name="create-a-unit-test-project"></a>単体テスト プロジェクトを作成する

単体テストでは、開発および公開時に自動化されたソフトウェア テストが提供されます。 [MSTest](https://github.com/Microsoft/testfx-docs) は、選択できる 3 つのテスト フレームワークのうちの 1 つです。 これ以外は、[xUnit](https://xunit.net/) と [nUnit](https://nunit.org/) です。

1. Visual Studio を起動します。

1. 「[Visual Studio で .NET Standard ライブラリを構築する](library-with-visual-studio.md)」で作成した `ClassLibraryProjects` ソリューションを開きます。

1. 「StringLibraryTest」 という名前の新しい単体テスト プロジェクトをソリューションに追加します。

   1. **ソリューション エクスプローラー**で、ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

   1. **[新しいプロジェクトの追加]** ページで、検索ボックスに「**mstest**」と入力します。 言語の一覧から **[C#]** または **[Visual Basic]** を選択し、次に、プラットフォームの一覧から **[すべてのプラットフォーム]** を選択します。

   1. **[MsTest テスト プロジェクト (.NET Core)]** テンプレートを選択し、 **[次へ]** を選択します。

   1. **[新しいプロジェクトの構成]** ページで、 **[プロジェクト名]** ボックスに「**StringLibraryTest**」と入力します。 次に、 **[作成]** を選択します。

1. Visual Studio によってプロジェクトが作成され、クラス ファイルが次のコードでコード ウィンドウに開かれます。 使用する言語で表示されていない場合は、ページの上部にある言語セレクターを変更します。

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;

   namespace StringLibraryTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestMethod1()
           {
           }
       }
   }
   ```

   ```vb
   Imports Microsoft.VisualStudio.TestTools.UnitTesting

   Namespace StringLibraryTest
       <TestClass>
       Public Class UnitTest1
           <TestMethod>
           Sub TestSub()

           End Sub
       End Class
   End Namespace
   ```

   単体テストのテンプレートで作成されたソース コードにより、次の処理が行われます。

   - 単体テストで使用される型が含まれた <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 名前空間がインポートされます。
   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性が `UnitTest1` クラスに適用されます。
   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性を適用して、C# では `TestMethod1` を、また Visual Basic では `TestSub` が定義されます。

   [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute)でタグ付けされたテスト クラスの [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) でタグ付けされた各テスト メソッドが、単体テスト実行時に自動実行されます。

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

テスト プロジェクトが `StringLibrary` クラスと連動するように、**StringLibraryTest** プロジェクトに `StringLibrary` プロジェクトへの参照を追加します。

1. **ソリューション エクスプローラー**で **[StringLibraryTest]** プロジェクトの **[依存関係]** ノードを右クリックし、コンテキスト メニューの **[プロジェクト参照の追加]** を選択します。

1. **[参照マネージャー]** ダイアログで、 **[プロジェクト]** ノードを展開し、 **[StringLibrary]** の横のボックスをオンにします。 `StringLibrary` アセンブリに参照を追加すると、コンパイラが **StringLibraryTest** プロジェクトをコンパイル中に、**StringLibrary** メソッドを見つけることができるようになります。

1. **[OK]** を選択します。

## <a name="add-and-run-unit-test-methods"></a>単体テスト メソッドの追加と実行

Visual Studio で単体テストを実行すると、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性でマークされたクラス内で、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性でマークされた各メソッドが実行されます。 テスト メソッドは、最初の失敗が検出されたとき、またはそのメソッドに含まれているすべてのテストが成功したときに終了します。

一般的なテストでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> クラスのメンバーが呼び出されます。 多くのアサート メソッドは最低 2 つのパラメーターを含んでいます。1 つは予期されるテスト結果、もう 1 つは実際のテスト結果です。 次の表に、`Assert` クラスの頻繁に呼び出されるメソッドをいくつか示します。

| Assert メソッド     | 関数 |
| ------------------ | -------- |
| `Assert.AreEqual`  | 2 つの値または 2 つのオブジェクトが等しいことを確認します。 値またはオブジェクトが等しくない場合、アサートは失敗します。 |
| `Assert.AreSame`   | 2 つのオブジェクト変数が同じオブジェクトを参照していることを確認します。 変数が別々のオブジェクトを参照している場合、アサートは失敗します。 |
| `Assert.IsFalse`   | 条件が `false` であることを確認します。 条件が `true` の場合、アサートは失敗します。 |
| `Assert.IsNotNull` | オブジェクトが `null` でないことを確認します。 オブジェクトが `null` である場合、アサートは失敗します。 |

また、テスト メソッドで <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> メソッドを使用して、スローすることが期待される例外の種類を示すこともできます。 指定した例外がスローされない場合、テストは失敗します。

`StringLibrary.StartsWithUpper` メソッドのテストでは、大文字で始まる文字列を多く用意します。 これらの場合ではメソッドが `true` を返すと予測されるので、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A?displayProperty=nameWithType> メソッドを呼び出すことができます。 同様に、大文字以外で始まる文字列を多く用意します。 これらの場合ではメソッドが `false` を返すと予測されるので、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A?displayProperty=nameWithType> メソッドを呼び出すことができます。

ライブラリ メソッドは文字列を処理するため、[空の文字列 (`String.Empty`) ](xref:System.String.Empty) (文字がなく <xref:System.String.Length> が 0 である有効な文字列)、および初期化されていない `null` 文字列を正しく処理することも確認します。 しかし、`StartsWithUpper` を静的メソッドとして直接呼び出して、単一の <xref:System.String> 引数を渡すこともできます。 または、`null` に割り当てられた `string` 変数の拡張メソッドとして `StartsWithUpper` を呼び出すこともできます。

メソッドを 3 つ定義します。これらのメソッドでは、文字列配列の各要素に対して <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> メソッドが呼び出されます。 メソッドのオーバーロードを呼び出します。これにより、テストが失敗した場合に表示されるエラー メッセージを指定できます。 このメッセージによって、エラーの原因となった文字列が識別されます。

テスト メソッドを作成するには

1. *UnitTest1.cs* または *UnitTest1.vb* コード ウィンドウで、コードを次のコードに置き換えます。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibraryTest/UnitTest1.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/StringLibraryTest/UnitTest1.vb":::

   `TestStartsWithUpper` メソッドの大文字のテストには、ギリシャ語の大文字のアルファ (U+0391) とキリル文字の大文字 EM (U+041C) が含まれています。 `TestDoesNotStartWithUpper` メソッドの小文字のテストには、ギリシャ語の小文字のアルファ (U+03B1) とキリル文字の小文字 Ghe (U+0433) が含まれています。

1. メニュー バーで、 **[ファイル]**  >  **[名前を付けて UnitTest1.cs を保存]** または **[ファイル]**  >  **[名前を付けて UnitTest1.vb を保存]** の順に選択します。 **[名前を付けてファイルを保存]** ダイアログで、 **[保存]** ボタンの横にある矢印を選択して、 **[エンコード付きで保存]** を選択します。

   > [!div class="mx-imgBorder"]
   > ![Visual Studio の [名前を付けてファイルを保存] ダイアログ](./media/testing-library-with-visual-studio/save-file-as-dialog.png)

1. **[保存の確認]** ダイアログで **[はい]** ボタンを選択してファイルを保存します。

1. **[保存オプションの詳細設定]** ダイアログの **[エンコード]** ドロップダウン リストから **[Unicode (UTF-8 シグネチャ付き) - コードページ 65001]** を選択し、 **[OK]** の順に選択します。

   > [!div class="mx-imgBorder"]
   > ![Visual Studio の [保存オプションの詳細設定] ダイアログ](./media/testing-library-with-visual-studio/advanced-save-options.png)

   UTF8 でエンコードされたファイルにソース コードを保存できなかった場合、ASCII ファイルとして保存される場合があります。 その場合は、ランタイムで ASCII 範囲外の UTF8 文字が正確にデコードされず、テスト結果が正確でなくなります。

1. メニュー バーで **[テスト]**  >  **[すべてのテストを実行する]** を選択します。 **テスト エクスプローラー** ウィンドウが開かない場合は、 **[テスト]**  >  **[テスト エクスプローラー]** を選択して開きます。 3 つのテストが **[成功したテスト]** セクションに表示され、 **[概要]** セクションにはテストの実行結果が表示されています。

   > [!div class="mx-imgBorder"]
   > ![[テスト エクスプローラー] ウィンドウと成功したテスト](./media/testing-library-with-visual-studio/test-explorer-window.png)

## <a name="handle-test-failures"></a>テストの失敗の処理

テスト駆動開発 (TDD) を行っている場合、最初にテストを作成すると、1 回目のテスト実行は失敗します。 その後、テストを成功させるコードをアプリに追加します。 このチュートリアルでは、検証するアプリ コードを記述した後にテストを作成したため、テストが失敗することはありませんでした。 テストの失敗が予想されるときにテストが失敗することを検証するには、テスト入力に無効な値を追加します。

1. `TestDoesNotStartWithUpper` メソッドの `words` 配列を変更し、文字列 "Error" を含めます。 ソリューションをビルドし、テストを実行するときに、Visual Studio では、自動的に開いているファイルが保存されるため、ファイルは保存する必要はありません。

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

   ```vb
   Dim words() As String = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " }

   ```

1. メニュー バーから **[テスト]**  >  **[すべてのテストを実行]** を選択してテストを実行します。 **[テスト エクスプローラー]** ウィンドウに、テストが 2 つ成功し、1 つ失敗したことが示されます。

   > [!div class="mx-imgBorder"]
   > ![[テスト エクスプローラー] ウィンドウと失敗したテスト](./media/testing-library-with-visual-studio/failed-test-window.png)

1. 失敗したテスト `TestDoesNotStartWith` を選択します。

   **[テスト エクスプローラー]** ウィンドウに、アサートによって生成されたメッセージ"Assert.IsFalse failed. Expected for 'Error': false; actual:True" が表示されます。 エラーのため、配列内の "Error" の後ろの文字列はテストされませんでした。

   > [!div class="mx-imgBorder"]
   > ![IsFalse アサーションの失敗を示す [テスト エクスプローラー] ウィンドウ](./media/testing-library-with-visual-studio/failed-test-detail.png)

1. 手順 1 で追加した文字列 "Error" を削除します。 テストを再実行すると、テストは成功します。

## <a name="test-the-release-version-of-the-library"></a>ライブラリのリリース バージョンのテスト

これで、ライブラリのデバッグ ビルドを実行したときにすべてのテストが成功したので、さらにライブラリのリリース ビルドに対してテストを行います。 コンパイラの最適化などのさまざまな要因により、デバッグ ビルドとリリース ビルドとでは動作が異なる場合があります。

リリース ビルドをテストするには、次の操作を行います。

1. Visual Studio のツールバーで、ビルド構成を **[デバッグ]** から **[リリース]** に変更します。

   > [!div class="mx-imgBorder"]
   > ![リリース ビルドが強調表示された Visual Studio のツールバー](./media/testing-library-with-visual-studio/visual-studio-toolbar-release.png)

1. **ソリューション エクスプローラー**で **[StringLibrary]** プロジェクトを右クリックし、コンテキスト メニューの **[ビルド]** を選択し、ライブラリを再コンパイルします。

   > [!div class="mx-imgBorder"]
   > ![StringLibrary のコンテキスト メニューとビルド コマンド](./media/testing-library-with-visual-studio/build-library-context-menu.png)

1. **[テストの実行]**  >  **[すべてのテスト]** をメニュー バーから選択して単体テストを実行します。 テストが成功します。

## <a name="additional-resources"></a>その他の技術情報

* [Visual Studio - 単体テストの基本](/visualstudio/test/unit-test-basics)
* [.NET Core と .NET Standard の単体テスト](../testing/index.md)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、クラス ライブラリの単体テストを行いました。 ライブラリをパッケージとして [NuGet](https://nuget.org) に発行した場合、他のユーザーもそれを使用できます。 方法については、次の NuGet のチュートリアルに従ってください。

> [!div class="nextstepaction"]
> [Visual Studio を使用した NuGet パッケージの作成と公開](/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)

ライブラリを NuGet パッケージとして発行した場合、他のユーザーもそれをインストールして使用できます。 方法については、次の NuGet のチュートリアルに従ってください。

> [!div class="nextstepaction"]
> [Visual Studio でパッケージをインストールして使用する](/nuget/quickstart/install-and-use-a-package-in-visual-studio)

ライブラリはパッケージとして配布する必要はありません。 それが使用されるコンソール アプリにバンドルすることができます。 コンソール アプリを発行する方法については、このシリーズの前のチュートリアルを参照してください。

> [!div class="nextstepaction"]
> [Visual Studio での .NET Core コンソール アプリケーションの発行](publishing-with-visual-studio.md)
