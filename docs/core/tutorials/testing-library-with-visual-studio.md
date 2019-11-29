---
title: Visual Studio 2017 での .NET Core を使用した .NET Standard クラス ライブラリのテスト
description: .NET Core クラス ライブラリ用の単体テスト プロジェクトを作成します。 .NET Core クラス ライブラリが単体テストで正しく動作することを確認します。
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet, seodoc18
ms.openlocfilehash: 242234d93bc1b8f9b88749f2e3bcfb37c2bde86d
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73037970"
---
# <a name="test-a-net-standard-library-with-net-core-in-visual-studio-2017"></a>Visual Studio 2017 での .NET Core を使用した .NET Standard ライブラリのテスト

「[Visual Studio 2017 の C# と .NET Core を使用して .NET Standard クラス ライブラリを構築する](library-with-visual-studio.md)」または「[Visual Studio 2017 で Visual Basic と .NET Core SDK を使用してクラス ライブラリを構築する](vb-library-with-visual-studio.md)」では、<xref:System.String> クラスに拡張メソッドを追加する簡単なクラス ライブラリを作成しました。 ここでは、それが期待どおり動作するかを確認する単体テストを作成しましょう。 この単体テスト プロジェクトは、前の記事で作成したソリューションに追加します。

## <a name="creating-a-unit-test-project"></a>単体テスト プロジェクトの作成

単体テスト プロジェクトを作成するには、次の操作を行います。

<!-- markdownlint-disable MD025 -->

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. **ソリューション エクスプローラー**で **[ClassLibraryProjects]** ソリューション ノードのコンテキスト メニューを開き、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、 **[Visual C#]** ノードを選択します。 次に、 **[.NET Core]** ノードを選び、 **[MSTest テスト プロジェクト (.NET Core)]** プロジェクト テンプレートを選びます。 **[名前]** テキスト ボックスに、プロジェクト名として "StringLibraryTest" と入力します。 **[OK]** を選択し、単体テスト プロジェクトを作成します。

   ![単体テスト プロジェクトが表示された [新しいプロジェクトの追加] ダイアログ - C#](./media/testing-library-with-visual-studio/create-new-test-project.png)

   > [!NOTE]  
   > MSTest テスト プロジェクトに加え、Visual Studio を使用して .NET Core 用の xUnit テスト プロジェクトを作成することもできます。

1. Visual Studio でプロジェクトが作成され、コード ウィンドウ内に *UnitTest1.cs* ファイルが開かれます。

   ![単体テスト プロジェクト クラスとメソッドの Visual Studio コード ウィンドウ - C#](./media/testing-library-with-visual-studio/unit-test-editor-window.png)

   単体テストのテンプレートで作成されたソース コードにより、次の処理が行われます。

   - 単体テストで使用される型が含まれた <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 名前空間がインポートされます。

   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性が `UnitTest1` クラスに適用されます。 \[TestMethod\] 属性でタグ付けされたテスト クラス内の各テスト メソッドは、単体テスト実行時に自動実行されます。

   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性が適用され、単体テスト実行時に自動実行されるテスト メソッドとして `TestMethod1` が定義されます。

1. **ソリューション エクスプローラー**で **[StringLibraryTest]** プロジェクトの **[依存関係]** ノードを右クリックし、コンテキスト メニューの **[参照の追加]** を選択します。

   ![StringLibraryTest の依存関係のコンテキスト メニュー - C#](./media/testing-library-with-visual-studio/add-reference-context-menu.png)

1. **[参照マネージャー]** ダイアログで、 **[プロジェクト]** ノードを展開し、 **[StringLibrary]** の横のボックスをオンにします。 `StringLibrary` アセンブリへの参照を追加すると、コンパイラで **StringLibrary** メソッドを見つけることができるようになります。 **[OK]** ボタンを選択します。 これによってクラス ライブラリ プロジェクト `StringLibrary` への参照が追加されます。

   ![Visual Studio のプロジェクト参照の追加ダイアログ](./media/testing-library-with-visual-studio/project-reference-manager.png)

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. **ソリューション エクスプローラー**で **[ClassLibraryProjects]** ソリューション ノードのコンテキスト メニューを開き、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、 **[Visual Basic]** ノードを選択します。 次に、 **[.NET Core]** ノードを選び、 **[MSTest テスト プロジェクト (.NET Core)]** プロジェクト テンプレートを選びます。 **[名前]** テキスト ボックスに、プロジェクト名として "StringLibraryTest" と入力します。 **[OK]** を選択し、単体テスト プロジェクトを作成します。

   ![単体テスト プロジェクトが表示された [新しいプロジェクトの追加] ダイアログ - Visual Basic](./media/testing-library-with-visual-studio/vb-create-new-test-project.png)

   > [!NOTE]  
   > MSTest テスト プロジェクトに加え、Visual Studio を使用して .NET Core 用の xUnit テスト プロジェクトを作成することもできます。

1. Visual Studio でプロジェクトが作成され、コード ウィンドウ内に *UnitTest1.vb* ファイルが開かれます。

   ![単体テストプロジェクト クラスとメソッドの Visual Studio コード ウィンドウ - Visual Basic](./media/testing-library-with-visual-studio/vb-unit-test-editor-window.png)

   単体テストのテンプレートで作成されたソース コードにより、次の処理が行われます。

   - 単体テストで使用される型が含まれた <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 名前空間がインポートされます。

   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性が `UnitTest1` クラスに適用されます。 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性でタグ付けされたテスト クラス内の各テスト メソッドは、単体テスト実行時に自動実行されます。

   - <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性が適用され、単体テスト実行時に自動実行されるテスト メソッドとして `TestMethod1` が定義されます。

1. **ソリューション エクスプローラー**で **[StringLibraryTest]** プロジェクトの **[依存関係]** ノードを右クリックし、コンテキスト メニューの **[参照の追加]** を選択します。

   ![StringLibraryTest の依存関係のコンテキスト メニュー](./media/testing-library-with-visual-studio/add-reference-context-menu.png)

1. **[参照マネージャー]** ダイアログで、 **[プロジェクト]** ノードを展開し、 **[StringLibrary]** の横のボックスをオンにします。 `StringLibrary` アセンブリへの参照を追加すると、コンパイラで **StringLibrary** メソッドを見つけることができるようになります。 **[OK]** ボタンを選択します。 これによってクラス ライブラリ プロジェクト `StringLibrary` への参照が追加されます。

   ![Visual Studio のプロジェクト参照の追加ダイアログ - Visual Basic](./media/testing-library-with-visual-studio/project-reference-manager.png)

---

## <a name="adding-and-running-unit-test-methods"></a>単体テスト メソッドの追加と実行

Visual Studio で単体テストを実行すると、単体テスト クラス (<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性が適用されているクラス) 内の <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 属性でマークされた各メソッドが実行されます。 1 つのテスト メソッドは、最初のエラーが発生したとき、またはそのメソッドに含まれているすべてのテストが成功したときに終了します。

一般的なテストでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> クラスのメンバーが呼び出されます。 多くのアサート メソッドは最低 2 つのパラメーターを含んでいます。1 つは予期されるテスト結果、もう 1 つは実際のテスト結果です。 頻繁に呼び出されるメソッドには、次の表のようなものがあります。

Assert メソッド | 関数
--- | ---
`Assert.AreEqual` | 2 つの値または 2 つのオブジェクトが等しいことを確認します。 値またはオブジェクトが等しくない場合、アサートは失敗します。
`Assert.AreSame` | 2 つのオブジェクト変数が同じオブジェクトを参照していることを確認します。 変数が別々のオブジェクトを参照している場合、アサートは失敗します。
`Assert.IsFalse` | 条件が `false` であることを確認します。 条件が `true` の場合、アサートは失敗します。
`Assert.IsNotNull` | オブジェクトが `null` でないことを確認します。 オブジェクトが `null` である場合、アサートは失敗します。

テスト メソッドに <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> 属性を適用することもできます。 テスト メソッドがスローすることを期待されている例外の種類を示します。 指定した例外がスローされない場合、テストは失敗します。

`StringLibrary.StartsWithUpper` メソッドのテストでは、大文字で始まる文字列を多く用意します。 これらの場合ではメソッドが `true` を返すと予測されるので、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A> メソッドを呼び出すことができます。 同様に、大文字以外で始まる文字列を多く用意します。 これらの場合ではメソッドが `false` を返すと予測されるので、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A> メソッドを呼び出すことができます。

ライブラリ メソッドは文字列を処理するので、[空の文字列 (`String.Empty`) ](xref:System.String.Empty) (文字がなく <xref:System.String.Length> が 0 である、有効な文字列)、および `null` 文字列 (初期化されていない文字列) を正しく処理するか確認します。 <xref:System.String> インスタンスで `StartsWithUpper` が例外メソッドとして呼び出される場合、それに `null` 文字列を渡すことはできません。 しかし、それを静的メソッドとして直接呼び出して、単一の <xref:System.String> 引数を渡すこともできます。

メソッドを 3 つ定義します。これらのメソッドでは、文字列配列の各要素について <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> メソッドが繰り返し呼び出されます。 テスト メソッドは最初のエラーが発生するとすぐに失敗するので、メソッドのオーバー ロードを呼び出して、メソッドの呼び出しで使用される文字列値を示す文字列を渡すようにします。

テスト メソッドを作成するには

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. *UnitTest1.cs* コード ウィンドウで、コードを次のコードに置き換えます。

   [!code-csharp[Test#1](~/samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs)]

   `TestStartsWithUpper` メソッドでの大文字のテストには、ギリシャ語の大文字のアルファ (U+0391) とキリル文字の大文字 EM (U+041C) が含まれており、`TestDoesNotStartWithUpper` メソッドでの小文字のテストにはギリシャ語の小文字のアルファ (U+03B1) とキリル文字の小文字 Ghe (U+0433) が含まれています。

1. メニュー バーで、 **[ファイル]**  >  **[名前を付けて UnitTest1.cs を保存]** の順に選択します。 **[名前を付けてファイルを保存]** ダイアログで、 **[保存]** ボタンの横にある矢印を選択して、 **[エンコード付きで保存]** を選択します。

   ![Visual Studio の [名前を付けてファイルを保存] ダイアログ - C#](./media/testing-library-with-visual-studio/save-file-as-dialog.png)

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. *UnitTest1.vb* コード ウィンドウで、コードを次のコードに置き換えます。

    [!code-vb[Test#1](~/samples/snippets/core/tutorials/vb-library-with-visual-studio/testlib.vb)]

   `TestStartsWithUpper` メソッドでの大文字のテストには、ギリシャ語の大文字のアルファ (U+0391) とキリル文字の大文字 EM (U+041C) が含まれており、`TestDoesNotStartWithUpper` メソッドでの小文字のテストにはギリシャ語の小文字のアルファ (U+03B1) とキリル文字の小文字 Ghe (U+0433) が含まれています。

1. メニュー バーで、 **[ファイル]**  >  **[名前を付けて UnitTest1.vb を保存]** の順に選択します。 **[名前を付けてファイルを保存]** ダイアログで、 **[保存]** ボタンの横にある矢印を選択して、 **[エンコード付きで保存]** を選択します。

   ![Visual Studio の [名前を付けてファイルを保存] ダイアログ - Visual Basic](./media/testing-library-with-visual-studio/save-file-as-dialog.png)

---

1. **[保存の確認]** ダイアログで **[はい]** ボタンを選択してファイルを保存します。

1. **[保存オプションの詳細設定]** ダイアログの **[エンコード]** ドロップダウン リストから **[Unicode (UTF-8 シグネチャ付き) - コードページ 65001]** を選択し、 **[OK]** の順に選択します。

   ![Visual Studio の [保存オプションの詳細設定] ダイアログ](./media/testing-library-with-visual-studio/advanced-save-options.png)

   UTF8 でエンコードされたファイルにソース コードを保存できなかった場合、ASCII ファイルとして保存される場合があります。 その場合は、ランタイムで ASCII 範囲外の UTF8 文字が正確にデコードされず、テスト結果が正確でなくなります。

1. メニュー バーで **[テスト]**  >  **[実行]**  >  **[すべてのテスト]** を選択します。 **[テスト エクスプローラー]** ウィンドウが開き、テストが正常に実行されたことを示します。 3 つのテストが **[成功したテスト]** セクションに表示され、 **[概要]** セクションにはテストの実行結果が表示されています。

   ![[テスト エクスプローラー] ウィンドウと成功したテスト](./media/testing-library-with-visual-studio/test-explorer-window.png)

## <a name="handling-test-failures"></a>テスト エラーの処理

テスト実行にはエラーがなかったので、少し変更を加えてテスト メソッドが 1 つ失敗するようにしてみましょう。

1. `TestDoesNotStartWithUpper` メソッドの `words` 配列を変更し、文字列 "Error" を含めます。 ソリューションをビルドし、テストを実行するときに、Visual Studio では、自動的に開いているファイルが保存されるため、ファイルは保存する必要はありません。

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

   ```vb
   Dim words() As String = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " }

   ```

1. **[テスト]**  >  **[実行]**  >  **[すべてのテスト]** をメニュー バーから選択してテストを実行します。 **[テスト エクスプローラー]** ウィンドウに、テストが 2 つ成功し、1 つ失敗したことが示されます。

   ![[テスト エクスプローラー] ウィンドウと失敗したテスト](./media/testing-library-with-visual-studio/failed-test-window.png)

1. **[失敗したテスト]** セクションで、失敗したテスト `TestDoesNotStartWith` を選択します。 **[テスト エクスプローラー]** ウィンドウに、アサートによって生成されたメッセージ"Assert.IsFalse failed. Expected for 'Error': false; actual:True" が表示されます。 エラーのため、配列内の "Error" の後ろのすべての文字列はテストされませんでした。

   ![Is False アサーションの失敗を示す [テスト エクスプローラー] ウィンドウ](./media/testing-library-with-visual-studio/failed-test-detail.png)

1. 手順 1 で行った変更を元に戻し、文字列 "Error" を削除します。 テストを再実行すると、テストは成功します。

## <a name="testing-the-release-version-of-the-library"></a>ライブラリのリリース バージョンのテスト

ここまで、ライブラリのデバッグ バージョンをテストしてきました。 すべてのテストが成功し、ライブラリを十分にテストしたので、さらにライブラリのリリース ビルドに対してテストを行います。 コンパイラの最適化などのさまざまな要因により、デバッグ ビルドとリリース ビルドとでは動作が異なる場合があります。

リリース ビルドをテストするには、次の操作を行います。

1. Visual Studio のツールバーで、ビルド構成を **[デバッグ]** から **[リリース]** に変更します。

   ![リリース ビルドが強調表示された Visual Studio のツールバー](./media/testing-library-with-visual-studio/visual-studio-toolbar-release.png)

1. **ソリューション エクスプローラー**で **[StringLibrary]** プロジェクトを右クリックし、コンテキスト メニューの **[ビルド]** を選択し、ライブラリを再コンパイルします。

   ![StringLibrary のコンテキスト メニューとビルド コマンド](./media/testing-library-with-visual-studio/build-library-context-menu.png)

1. **[テスト]**  >  **[実行]**  >  **[すべてのテスト]** をメニュー バーから選択して単体テストを実行します。 テストが成功します。

これでライブラリのテストが完了したので、次の手順では呼び出し元が使用できるようにします。 1 つまたは複数のアプリケーションとバンドルするか、NuGet パッケージとして配布することができます。 詳細については、　[.NET Standard クラス ライブラリの使用](./consuming-library-with-visual-studio.md) に関するページを参照してください。
