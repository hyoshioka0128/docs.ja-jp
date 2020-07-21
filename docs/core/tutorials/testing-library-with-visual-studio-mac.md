---
title: Visual Studio for Mac を使用して .NET Core で .NET Standard クラス ライブラリをテストする
description: .NET Core クラス ライブラリ用の単体テスト プロジェクトを作成します。 .NET Core クラス ライブラリが単体テストで正しく動作することを確認します。
ms.date: 06/08/2020
ms.openlocfilehash: a183049623df44cbb8c4abd47ce6e78d91adae12
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84713305"
---
# <a name="test-a-net-standard-class-library-with-net-core-using-visual-studio"></a>Visual Studio を使用して .NET Core で .NET Standard クラス ライブラリをテストする

このチュートリアルでは、テスト プロジェクトをソリューションに追加して、単体テストを自動化する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio for Mac での .NET Standard ライブラリの作成](library-with-visual-studio-mac.md)に関する記事で作成したソリューションを使用します。

## <a name="create-a-unit-test-project"></a>単体テスト プロジェクトを作成する

単体テストでは、開発および公開時に自動化されたソフトウェア テストが提供されます。 [MSTest](https://github.com/Microsoft/testfx-docs) は、選択できる 3 つのテスト フレームワークのうちの 1 つです。 これ以外は、[xUnit](https://xunit.net/) と [nUnit](https://nunit.org/) です。

1. Visual Studio for Mac を起動します。

1. [Visual Studio for Mac での .NET Standard ライブラリの作成](library-with-visual-studio-mac.md)に関する記事で作成した `ClassLibraryProjects` ソリューションを開きます。

1. **[ソリューション]** パッドで、<kbd>ctrl</kbd> キーを押しながら `ClassLibraryProjects` ソリューションをクリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログで、 **[Web and Console]\(Web とコンソール\)** ノードから **[テスト]** を選択します。 **[MSTest プロジェクト]** を選択してから **[次へ]** を選択します。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-project.png" alt-text="テスト プロジェクトを作成する Visual Studio Mac の [新しいプロジェクト] ダイアログ":::

1. **.NET Core 3.1** を選択します。 新しいプロジェクトに "StringLibraryTest" という名前を付けて、 **[作成]** を選択します。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-new-project-name.png" alt-text="プロジェクト名を指定する Visual Studio Mac の [新しいプロジェクト] ダイアログ":::

   Visual Studio によって、次のコードを含むクラス ファイルが作成されます。

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

   単体テストのテンプレートで作成されたソース コードにより、次の処理が行われます。

   - 単体テストで使用される型が含まれた <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 名前空間がインポートされます。
   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性が `UnitTest1` クラスに適用されます。
   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性が `TestMethod1` に適用されます。

   [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute)でタグ付けされたテスト クラスの [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) でタグ付けされた各テスト メソッドが、単体テスト実行時に自動実行されます。

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

テスト プロジェクトが `StringLibrary` クラスと連動するように、`StringLibrary` プロジェクトへの参照を追加します。

1. **[ソリューション]** パッドで、**StringLibraryTest** の下にある **[依存関係]** を <kbd>ctrl</kbd> キーを押しながらクリックします。 コンテキスト メニューから **[参照の追加]** を選択します。

1. **[参照]** ダイアログで、 **[StringLibrary]** プロジェクトを選択します。 **[OK]** を選択します。

      :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-edit-references.png" alt-text="Visual Studio Mac の [参照の編集] ダイアログ":::

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

1. *UnitTest1.cs* ファイルを開き、コードを次のコードに置き換えます。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibraryTest/UnitTest1.cs":::

   `TestStartsWithUpper` メソッドの大文字のテストには、ギリシャ語の大文字のアルファ (U+0391) とキリル文字の大文字 EM (U+041C) が含まれています。 `TestDoesNotStartWithUpper` メソッドの小文字のテストには、ギリシャ語の小文字のアルファ (U+03B1) とキリル文字の小文字 Ghe (U+0433) が含まれています。

1. メニュー バーから、 **[ファイル]**  >  **[名前を付けて保存]** の順に選択します。 ダイアログで、 **[エンコード]** が **[Unicode (UTF-8)]** に設定されていることを確認します。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/save-file-as-dialog.png" alt-text="Visual Studio の [名前を付けてファイルを保存] ダイアログ":::

1. 既存のファイルを置き換えるかどうかを確認するメッセージが表示されたら、 **[置換]** を選択します。

   UTF8 でエンコードされたファイルにソース コードを保存できなかった場合、ASCII ファイルとして保存される場合があります。 その場合は、ランタイムで ASCII 範囲外の UTF8 文字が正確にデコードされず、テスト結果が正確でなくなります。

1. 画面の右側の **[単体テスト]** パネルを開きます。 メニューから **[表示]**  >  **[テスト]** を選択します。

1. **[ドッキング]** アイコンをクリックして、パネルを開いたままにします。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-dock-icon.png" alt-text="Visual Studio for Mac の [単体テスト] パネルの [ドッキング] アイコン":::

1. **[すべて実行]** ボタンをクリックします。

   すべてのテストに成功します。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-pass.png" alt-text="Visual Studio for Mac の予測されるテスト成功":::

## <a name="handle-test-failures"></a>テストの失敗の処理

テスト駆動開発 (TDD) を行っている場合、最初にテストを作成すると、1 回目のテスト実行は失敗します。 その後、テストを成功させるコードをアプリに追加します。 このチュートリアルでは、検証するアプリ コードを記述した後にテストを作成したため、テストが失敗することはありませんでした。 テストの失敗が予想されるときにテストが失敗することを検証するには、テスト入力に無効な値を追加します。

1. `TestDoesNotStartWithUpper` メソッドの `words` 配列を変更し、文字列 "Error" を含めます。 ソリューションをビルドし、テストを実行するときに、Visual Studio では、自動的に開いているファイルが保存されるため、ファイルは保存する必要はありません。

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. テストをもう一度実行します。

   今回は、 **[テスト エクスプローラー]** ウィンドウに、2 つのテストが成功し、1 つが失敗したことが示されます。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/failed-test-window.png" alt-text="[テスト エクスプローラー] ウィンドウと失敗したテスト":::

1. <kbd>ctrl</kbd> キーを押しながら、失敗したテスト、`TestDoesNotStartWithUpper` の順にクリックして、コンテキスト メニューから **[結果パッドを表示する]** を選択します。

   **[結果]** パッドに、アサートによって生成されたメッセージが表示されます。"Assert.IsFalse failed. Expected for 'Error': false; actual:True" が表示されます。 エラーのため、配列内の "Error" の後ろの文字列はテストされませんでした。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-failure.png" alt-text="IsFalse アサーションの失敗を示す [テスト エクスプローラー] ウィンドウ":::

1. 手順 1 で追加した文字列 "Error" を削除します。 テストを再実行すると、テストは成功します。

## <a name="test-the-release-version-of-the-library"></a>ライブラリのリリース バージョンのテスト

これで、ライブラリのデバッグ ビルドを実行したときにすべてのテストが成功したので、さらにライブラリのリリース ビルドに対してテストを行います。 コンパイラの最適化などのさまざまな要因により、デバッグ ビルドとリリース ビルドとでは動作が異なる場合があります。

リリース ビルドをテストするには、次の操作を行います。

1. Visual Studio のツールバーで、ビルド構成を **[デバッグ]** から **[リリース]** に変更します。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="リリース ビルドが強調表示された Visual Studio のツールバー":::

1. **[ソリューション]** パッドで、<kbd>ctrl</kbd> キーを押しながら **StringLibrary** プロジェクトをクリックし、コンテキスト メニューから **[ビルド]** を選択してライブラリを再コンパイルします。

   :::image type="content" source="media/testing-library-with-visual-studio-mac/build-library-context-menu.png" alt-text="StringLibrary のコンテキスト メニューとビルド コマンド":::

1. 単体テストをもう一度実行します。

   テストが成功します。

## <a name="debug-tests"></a>テストのデバッグ

「[チュートリアル:Visual Studio for Mac を使用して .NET Core コンソール アプリケーションをデバッグする](debugging-with-visual-studio-mac.md)」に記載されているのと同じプロセスに従って、単体テスト プロジェクトを使用してコードをデバッグできます。 ShowCase アプリ プロジェクトを開始する代わりに、<kbd>ctrl</kbd> キーを押しながら **[StringLibraryTests]** プロジェクトをクリックし、コンテキスト メニューから **[プロジェクトのデバッグを開始]** を選択します。 Visual Studio により、デバッガーがアタッチされた状態でテスト プロジェクトが開始されます。 実行は、テスト プロジェクトまたは基になるライブラリ コードに追加したブレークポイントで停止します。

## <a name="additional-resources"></a>その他の技術情報

* [.NET Core と .NET Standard の単体テスト](../testing/index.md)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、クラス ライブラリの単体テストを行いました。 ライブラリをパッケージとして [NuGet](https://nuget.org) に発行した場合、他のユーザーもそれを使用できます。 方法については、次の NuGet のチュートリアルに従ってください。

> [!div class="nextstepaction"]
> [パッケージの作成と公開 (dotnet CLI)](/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)

ライブラリを NuGet パッケージとして発行した場合、他のユーザーもそれをインストールして使用できます。 方法については、次の NuGet のチュートリアルに従ってください。

> [!div class="nextstepaction"]
> [Visual Studio for Mac にパッケージをインストールして使用する](/nuget/quickstart/install-and-use-a-package-in-visual-studio-mac)

ライブラリはパッケージとして配布する必要はありません。 それが使用されるコンソール アプリにバンドルすることができます。 コンソール アプリを発行する方法については、このシリーズの前のチュートリアルを参照してください。

> [!div class="nextstepaction"]
> [Visual Studio for Mac を使用して .NET Core コンソール アプリケーションを発行する](publishing-with-visual-studio-mac.md)
