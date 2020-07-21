---
title: クエリの作成
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
ms.openlocfilehash: 25905d7ac3ca4bb66a22ad1df421b400eaa6b08f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413272"
---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>チュートリアル: Visual Basic でのクエリの作成

このチュートリアルでは、Visual Basic 言語の機能を使用して統合言語クエリ (LINQ) のクエリ式を記述する方法を示します。 このチュートリアルでは、Student オブジェクトのリストに対するクエリを作成する方法とそのクエリを実行する方法、さらにクエリに変更を加える方法について説明します。 クエリには、オブジェクト初期化子、ローカル型推論、匿名型などさまざまな機能が組み込まれています。

このチュートリアルを完了すれば、いつでも、興味がある特定の LINQ プロバイダーのサンプルやドキュメントに進むことができます。 LINQ プロバイダーには、[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]、LINQ to DataSet、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] が含まれます。

## <a name="create-a-project"></a>プロジェクトの作成

### <a name="to-create-a-console-application-project"></a>コンソール アプリケーション プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. **[インストールされたテンプレート]** の一覧で、 **[Visual Basic]** をクリックします。

4. プロジェクトの種類の一覧の **[コンソール アプリケーション]** をクリックします。 **[名前]** ボックスにプロジェクトの名前を入力して、 **[OK]** をクリックします。

    プロジェクトが作成されます。 System.Core.dll への参照は、既定で追加されます。 また、[プロジェクト デザイナー (Visual Basic) の [参照] ページ](/visualstudio/ide/reference/references-page-project-designer-visual-basic)にある **[インポートされた名前空間]** の一覧には <xref:System.Linq?displayProperty=nameWithType> 名前空間が含まれます。

5. [プロジェクト デザイナー (Visual Basic) の [コンパイル] ページ](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)で、 **[Option infer]** が **[On]** に設定されていることを確認します。

## <a name="add-an-in-memory-data-source"></a>インメモリ データ ソースを追加する

このチュートリアルで使用するクエリのデータ ソースは、`Student` オブジェクトのリストです。 それぞれの `Student` オブジェクトには、名、姓、学年、全学生における成績のランクが格納されます。

### <a name="to-add-the-data-source"></a>データ ソースを追加するには

- `Student` クラスを定義し、クラスのインスタンスのリストを作成します。

  > [!IMPORTANT]
  > `Student` クラスを定義し、このチュートリアルの各例で使用するリストを作成するために必要なコードは、「[方法: 項目のリストを作成する](how-to-create-a-list-of-items.md)」に掲載されています。 そこからコピーして、自分のプロジェクトに貼り付けてください。 プロジェクトの作成時にあったコードを新しいコードで置き換えます。

### <a name="to-add-a-new-student-to-the-students-list"></a>学生リストに新しい学生を追加するには

- `getStudents` メソッドのパターンに従って、`Student` クラスのインスタンスを新たにリストに追加します。 学生を追加すると、オブジェクト初期化子が挿入されます。 詳細については、「[オブジェクト初期化子: 名前付きの型と匿名型](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)」を参照してください。

## <a name="create-a-query"></a>クエリを作成する

このセクションで追加したクエリを実行すると、成績のランクがトップ 10 に入る学生のリストが生成されます。 このクエリでは都度、完全な `Student` オブジェクトが選択されるため、クエリの結果の型は `IEnumerable(Of Student)` です。 ただし通常、クエリの定義にクエリの型は指定されません。 コンパイラがローカル型推論を使用して型を特定します。 詳細については、「[ローカル型の推論](../../language-features/variables/local-type-inference.md)」を参照してください。 クエリの範囲変数 `currentStudent` は、ソース `students` に含まれる各 `Student` インスタンスへの参照として機能します。`students` 内の各オブジェクトのプロパティには、それを通じてアクセスすることができます。

### <a name="to-create-a-simple-query"></a>簡単なクエリを作成するには

1. プロジェクトの `Main` メソッドから、次のように記述されている箇所を見つけます。

    [!code-vb[VbLINQWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#1)]

    次のコードをコピーして、そこに貼り付けます。

    [!code-vb[VbLINQWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#2)]

2. コード内の `studentQuery` にマウス ポインターを合わせて、コンパイラによって割り当てられた型が `IEnumerable(Of Student)` であることを確認します。

## <a name="run-the-query"></a>クエリを実行する

変数 `studentQuery` には、クエリの実行結果ではなくクエリの定義が格納されます。 クエリを実行するための通常のメカニズムは `For Each` ループです。 返されたシーケンス内の各要素には、ループの反復変数を介してアクセスします。 クエリの実行の詳細については、「[初めての LINQ クエリの作成](writing-your-first-linq-query.md)」を参照してください。

### <a name="to-run-the-query"></a>クエリを実行するには

1. 対象のプロジェクトで、クエリの下に次の `For Each` ループを追加します。

    [!code-vb[VbLINQWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#3)]

2. ループの制御変数 `studentRecord` にマウス ポインターを合わせて、そのデータ型を確認します。 `studentQuery` から返されるのは `Student` インスタンスのコレクションであるため、`studentRecord` の型も `Student` であると推定されます。

3. Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、実行します。 コンソール ウィンドウで結果を確認してください。

## <a name="modify-the-query"></a>クエリの変更

クエリの結果は、特定の順序で並んでいた方が見やすくなります。 返されたシーケンスは、使用できるあらゆるフィールドを基準にして並べ替えることができます。

### <a name="to-order-the-results"></a>結果を並べ替えるには

1. クエリの `Where` ステートメントと `Select` ステートメントの間に、次の `Order By` 句を追加します。 `Order By` 句は、各学生の姓を基準にして、A から Z のアルファベット順に結果を並べ替えます。

    ```vb
    Order By currentStudent.Last Ascending
    ```

2. まず姓で並べ替えたうえで、名で並べ替えるために、その両方のフィールドをクエリに追加します。

    ```vb
    Order By currentStudent.Last Ascending, currentStudent.First Ascending
    ```

    `Descending` を指定して、Z から A の順に並べ替えることもできます。

3. Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、実行します。 コンソール ウィンドウで結果を確認してください。

### <a name="to-introduce-a-local-identifier"></a>ローカルの識別子を挿入するには

1. ローカルの識別子をクエリ式に挿入するには、このセクションのコードを追加します。 ローカルの識別子には中間結果が保持されます。 次の例の `name` は、学生の名と姓を連結した値を保持する識別子です。 ローカルの識別子は利便性を目的に使用できるほか、式の結果を格納しておくことで、計算を何度も行う必要がなくなるのでパフォーマンスの向上にもつながります。

    [!code-vb[VbLINQWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#4)]

2. Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、実行します。 コンソール ウィンドウで結果を確認してください。

### <a name="to-project-one-field-in-the-select-clause"></a>Select 句で 1 つのフィールドを投影するには

1. ソース内の要素とは異なる要素のシーケンスを生成するクエリを作成するには、このセクションのクエリと `For Each` ループを追加します。 次の例のソースは `Student` オブジェクトのコレクションですが、返されるのは各オブジェクトの 1 つのメンバー (姓が Garcia である学生の名) だけです。 `currentStudent.First` は文字列であるため、`studentQuery3` から返されるシーケンスのデータ型は `IEnumerable(Of String)`、つまり一連の文字列です。 これまでの例と同様、`studentQuery3` に対するデータ型の割り当ては、コンパイラに委ねられ、ローカル型推論を使用して特定されます。

    [!code-vb[VbLINQWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#5)]

2. コード内の `studentQuery3` にマウス ポインターを合わせて、割り当てられた型が `IEnumerable(Of String)` であることを確認します。

3. Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、実行します。 コンソール ウィンドウで結果を確認してください。

### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>Select 句で匿名型を作成するには

1. クエリにおける匿名型の使用法を確認するために、このセクションのコードを追加します。 これらをクエリで使用するのは、レコード全体 (前の例では `currentStudent` レコード) や単一のフィールド (前セクションの `First`) ではなく複数のフィールドがデータ ソースから返されるようにしたい場合です。 結果に含めたいフィールドを格納する名前付きの型を新たに定義するのではなく、`Select` 句でフィールドを指定すると、それらのフィールドをプロパティとして持つ匿名型がコンパイラによって作成されます。 詳細については、「[匿名型](../../language-features/objects-and-classes/anonymous-types.md)」を参照してください。

    次の例では、成績のランクが 1 から 10 である最上級生 (Senior) の名前とランクを、成績のランク順に返すクエリを作成しています。 この例では、`studentQuery4` の型を推定する必要があります。`Select` 句で返されるのは匿名型のインスタンスであり、使用できる名前が匿名型にはないためです。

    [!code-vb[VbLINQWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#6)]

2. Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、実行します。 コンソール ウィンドウで結果を確認してください。

## <a name="additional-examples"></a>その他の例

これで基本的な事柄を理解できたので、別の一連の例で、LINQ クエリの柔軟性と機能を見てみましょう。 それぞれの例には、その処理の内容について最初に簡潔な説明が記述されています。 それぞれのクエリの結果変数にマウス ポインターを合わせると、推定された型が表示されます。 結果の生成には、`For Each` ループを使用します。

[!code-vb[VbLINQWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#7)]

## <a name="additional-information"></a>追加情報

クエリ操作の基本的な概念が理解できたら、興味がある種類の LINQ プロバイダーについて、ドキュメントやサンプルを読んでみましょう。

- [LINQ to Objects](linq-to-objects.md)

- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)

- [LINQ to XML](linq-to-xml.md)

- [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)

## <a name="see-also"></a>関連項目

- [統合言語クエリ (LINQ) (Visual Basic)](index.md)
- [Visual Basic の LINQ の概要](getting-started-with-linq.md)
- [ローカル型の推論](../../language-features/variables/local-type-inference.md)
- [オブジェクト初期化子: 名前付きの型と匿名型](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [匿名型](../../language-features/objects-and-classes/anonymous-types.md)
- [Visual Basic における LINQ の概要](../../language-features/linq/introduction-to-linq.md)
- [LINQ](../../language-features/linq/index.md)
- [クエリ](../../../language-reference/queries/index.md)
