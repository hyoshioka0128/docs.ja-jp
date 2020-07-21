---
title: ステートメント
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- colons (:) [Visual Basic]
- constants [Visual Basic], defining
- underlines
- constants [Visual Basic], statements
- blue underline [Visual Basic]
- procedures [Visual Basic], statements
- variables [Visual Basic], assigning
- line breaks [Visual Basic], in code
- executable statements [Visual Basic]
- variables [Visual Basic], defining
- statements [Visual Basic], about statements
ms.assetid: fcfdee1a-82b7-4846-98f7-9ca3f5160089
ms.openlocfilehash: 09fe53f4bc2b6d025b762c6595c5337263456bae
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401980"
---
# <a name="statements-in-visual-basic"></a>Visual Basic におけるステートメント

Visual Basic におけるステートメントは完全な命令です。 キーワード、演算子、変数、定数、および式を含めることができます。 各ステートメントは、次のいずれかのカテゴリに属します。

- **宣言ステートメント**。変数、定数、またはプロシージャの名前を指定します。データ型を指定することもできます。

- **実行可能なステートメント**。アクションを開始します。 これらのステートメントでは、メソッドまたは関数を呼び出すことができ、コードのブロックをループまたは分岐できます。 実行可能なステートメントには、変数または定数に値または式を代入する、**代入ステートメント**が含まれます。

このトピックでは、各カテゴリについて説明します。 また、このトピックでは、複数のステートメントを 1 行に結合する方法と、複数の行にわたってステートメントを続ける方法について説明します。

## <a name="declaration-statements"></a>宣言ステートメント

宣言ステートメントを使用して、プロシージャ、変数、プロパティ、配列、および定数の名前を指定して定義します。 プログラミング要素を宣言するときに、そのデータ型、アクセス レベル、およびスコープを定義することもできます。 詳細については、「[宣言された要素の特性](./declared-elements/declared-element-characteristics.md)」を参照してください。

次の例には 3 つの宣言が含まれています。

[!code-vb[VbVbalrStatements#80](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#80)]

最初の宣言は、`Sub` ステートメントです。 それに対応する `End Sub` ステートメントと共に、`applyFormat` という名前のプロシージャを宣言します。 また、`applyFormat` が `Public` であることを示します。これは、それを参照できるすべてのコードでそれを呼び出せることを意味します。

2 番目の宣言は `Const` ステートメントであり、`Integer` データ型と 33 の値を指定して、定数 `limit` を宣言します。

3 番目の宣言は、変数 `thisWidget` を宣言する、`Dim` ステートメントです。 データ型は特定のオブジェクト、つまり、`Widget` クラスから作成されるオブジェクトです。 任意の基本データ型、または使用しているアプリケーションで公開される任意のオブジェクト型の変数を宣言できます。

### <a name="initial-values"></a>初期値

宣言ステートメントを含むコードが実行されると、Visual Basic で、宣言された要素に必要なメモリが予約されます。 要素に値が保持されている場合、Visual Basic によって、そのデータ型の既定値に初期化されます。 詳細については、「[Dim ステートメント](../../language-reference/statements/dim-statement.md)」の "動作" に関する記述を参照してください。

次の例に示すように、変数には、その宣言の一部として初期値を代入することができます。

[!code-vb[VbVbalrStatements#81](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#81)]

変数がオブジェクト変数である場合は、次の例に示すように、[New 演算子](../../language-reference/operators/new-operator.md)キーワードを使用して宣言するときに、そのクラスのインスタンスを明示的に作成できます。

[!code-vb[VbVbalrStatements#82](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#82)]

宣言ステートメントで指定する初期値は、実行がその宣言ステートメントに到達するまで変数に代入されないことに注意してください。 それまでは、変数にそのデータ型の既定値が含まれます。

## <a name="executable-statements"></a>実行可能なステートメント

実行可能なステートメントでアクションが実行されます。 プロシージャを呼び出したり、コード内の別の場所に分岐したり、複数のステートメントをループしたり、式を評価したりすることができます。 代入ステートメントは、実行可能なステートメントの特殊なケースです。

次の例では、`If...Then...Else` 制御構造を使用して、変数の値に基づいてさまざまなコード ブロックを実行します。 各コード ブロック内では、`For...Next` ループが指定された回数だけ実行されます。

[!code-vb[VbVbalrStatements#83](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#83)]

前の例の `If` ステートメントでは、パラメーター `clockwise` の値を確認します。 値が `True` である場合は、`aWidget` の `spinClockwise` メソッドを呼び出します。 値が `False` である場合は、`aWidget` の `spinCounterClockwise` メソッドを呼び出します。 `If...Then...Else` 制御構造は、`End If` で終わります。

各ブロック内の `For...Next` ループでは、`revolutions` パラメーターの値と等しい回数だけ、適切なメソッドを呼び出します。

## <a name="assignment-statements"></a>代入ステートメント

代入ステートメントでは、次の例のように、代入演算子 (`=`) の右辺の値を取り、左側の要素に格納することで構成される代入演算を実行します。

[!code-vb[VbVbalrStatements#73](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#73)]

前の例の代入ステートメントでは、リテラル値 42 が変数 `v` に格納されます。

### <a name="eligible-programming-elements"></a>対象となるプログラミング要素

代入演算子の左辺のプログラミング要素では、値を受け入れて格納できる必要があります。 これは、[ReadOnly](../../language-reference/modifiers/readonly.md) ではない変数またはプロパティである必要があるか、あるいは配列要素である必要があることを意味します。 代入ステートメントのコンテキストでは、このような要素は、"左辺値" の場合、*lvalue* と呼ばれることもあります。

代入演算子の右辺の値は、式によって生成されます。これは、リテラル、定数、変数、プロパティ、配列要素、その他の式、または関数呼び出しの任意の組み合わせで構成できます。 次に例を示します。

[!code-vb[VbVbalrStatements#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#74)]

前の例では、変数 `y` に保持されている値を、変数 `z` に保持されている値に追加してから、関数 `findResult` への呼び出しによって返される値を追加します。 その後、この式の合計値は、変数 `x` に格納されます。

### <a name="data-types-in-assignment-statements"></a>代入ステートメントのデータ型

次の例に示すように、代入演算子では、数値に加え、`String` 値も代入することができます。

[!code-vb[VbVbalrStatements#75](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#75)]

次の例に示すように、`Boolean` リテラルまたは `Boolean` 式を使用して、`Boolean` 値を代入することもできます。

[!code-vb[VbVbalrStatements#76](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#76)]

同様に、`Char`、`Date`、または `Object` データ型のプログラミング要素に適切な値を代入することができます。 また、インスタンスの作成元のクラスとして宣言された要素に、オブジェクト インスタンスを代入することができます。

### <a name="compound-assignment-statements"></a>複合代入ステートメント

"*複合代入ステートメント*" では、最初に式で演算を行ってから、プログラミング要素に代入します。 次の例では、演算子の左辺の変数値を、右側の式の値でインクリメントする、これらの `+=` の演算子を示します。

[!code-vb[VbVbalrStatements#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#77)]

前の例では、`n` の値に 1 を加算してから、その新しい値を `n` に格納します。 これは、次のステートメントに相当する短縮形です。

[!code-vb[VbVbalrStatements#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#78)]

この型の演算子を使用することで、さまざまな複合代入演算を実行できます。 これらの演算子の一覧と詳細については、「[代入演算子](../../language-reference/operators/assignment-operators.md)」を参照してください。

連結代入演算子 (`&=`) は、次の例に示すように、既存の文字列の末尾に文字列を追加する場合に便利です。

[!code-vb[VbVbalrStatements#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#79)]

### <a name="type-conversions-in-assignment-statements"></a>代入ステートメントでの型変換

変数、プロパティ、または配列要素に代入する値は、そのターゲット要素に適したデータ型である必要があります。 一般には、ターゲット要素と同じデータ型の値の生成を試みることをお勧めします。 しかし、代入時に他の型に変換できる型もあります。

データ型間の変換については、「[Visual Basic における型変換](./data-types/type-conversions.md)」を参照してください。 簡単に言えば、Visual Basic では、指定された型の値を、拡大変換される他の型に自動的に変換します。 "*拡大変換*" は、実行時に常に成功し、データが失われないものです。 たとえば、Visual Basic では、必要に応じて、`Integer` 値を `Double` に変換します。これは、`Integer` が `Double` に拡大変換されるためです。 詳細については、「 [Widening and Narrowing Conversions](./data-types/widening-and-narrowing-conversions.md)」を参照してください。

*縮小変換* (拡大しないもの) は、実行時の失敗、あるいはデータ損失のリスクを伴います。 型変換関数を使用して、縮小変換を明示的に実行することも、`Option Strict Off` を設定して、暗黙的にすべての変換を実行するようにコンパイラに指示することもできます。 詳細については、「[暗黙の型変換と明示的な型変換](./data-types/implicit-and-explicit-conversions.md)」を参照してください。

## <a name="putting-multiple-statements-on-one-line"></a>1 行に複数のステートメントを配置する

1 行に複数のステートメントを配置し、コロン (`:`) 文字で区切ることができます。 次に例を示します。

[!code-vb[VbVbalrStatements#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#70)]

この形式の構文は、便利な場合もありますが、コードを読んだり、保持することが難しくなります。 したがって、1 つのステートメントを 1 行に収めることをお勧めします。

## <a name="continuing-a-statement-over-multiple-lines"></a>複数行にわたってステートメントを続ける

ステートメントは通常、1 行に収まりますが、長すぎる場合は、行連結シーケンスを使用して、次の行に続けることができます。これは、スペース、その後に続くアンダースコア文字 (`_`)、さらにその後に続く復帰で構成されます。 次の例では、`MsgBox` の実行可能なステートメントは 2 行にわたって続きます。

[!code-vb[VbVbalrStatements#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#71)]

### <a name="implicit-line-continuation"></a>暗黙的な行連結

多くの場合、アンダースコア文字 (`_`) を使用せずに、次の連続する行にステートメントを続けることができます。 以下の構文要素では、暗黙的にステートメントを次のコード行に続けます。

- コンマ (`,`) の後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#1)]

- 開きかっこ (`(`) の後、または閉じかっこ (`)`) の前。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#2)]

- 左中かっこ (`{`) の後、または右中かっこ (`}`) の前。 次に例を示します。

    [!code-vb[VbVbalrLineContinuation#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#3)]

    詳細については、「[オブジェクト初期化子: 名前付きの型と匿名型](./objects-and-classes/object-initializers-named-and-anonymous-types.md)」または「[コレクション初期化子](./collection-initializers/index.md)」を参照してください。

- XML リテラル内の開始埋め込み式 (`<%=`) の後、または埋め込み式の終了 (`%>`) の前。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#4)]

   詳細については、「[XML での埋め込み式](./xml/embedded-expressions-in-xml.md)」を参照してください。

- 連結演算子 (`&`) の後。 次に例を示します。

   [!code-vb[VbVbcnConventions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/vb/Class1.vb#9)]

   詳細については、「[機能別の演算子一覧](../../language-reference/operators/operators-listed-by-functionality.md)」を参照してください。

- 代入演算子 (`=`、`&=`、`:=`、`+=`、`-=`、`*=`、`/=`、`\=`、`^=`、`<<=`、`>>=`) の後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#5)]

   詳細については、「[機能別の演算子一覧](../../language-reference/operators/operators-listed-by-functionality.md)」を参照してください。

- 式内の 2 項演算子 (`+`、`-`、`/`、`*`、`Mod`、`<>`、`<`、`>`、`<=`、`>=`、`^`、`>>`、`<<`、`And`、`AndAlso`、`Or`、`OrElse`、`Like`、`Xor`) の後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#7)]

   詳細については、「[機能別の演算子一覧](../../language-reference/operators/operators-listed-by-functionality.md)」を参照してください。

- `Is` および `IsNot` 演算子の後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#8)]

   詳細については、「[機能別の演算子一覧](../../language-reference/operators/operators-listed-by-functionality.md)」を参照してください。

- メンバー修飾子文字 (`.`) の後、およびメンバー名の前。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#5)]

   しかし、`With` ステートメントを使用する場合、または型の初期化一覧に値を指定する場合は、メンバー修飾子文字の後に行連結文字 (`_`) を含める必要があります。 `With` ステートメントまたはオブジェクト初期化一覧を使用する場合は、代入演算子 (`=` など) の後で改行することを検討してください。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#14)]

   詳細については、「[With...End With ステートメント](../../language-reference/statements/with-end-with-statement.md)」または「[オブジェクト初期化子: 名前付きの型と匿名型](./objects-and-classes/object-initializers-named-and-anonymous-types.md)」を参照してください。

- XML 軸プロパティの修飾子 (`.`、`.@` または `...`) の後。 しかし、`With` キーワードを使用する場合は、メンバー修飾子を指定するときに行連結文字 (`_`) を含める必要があります。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#9)]

   詳細については、「[XML 軸プロパティ](../../language-reference/xml-axis/index.md)」を参照してください。

- 属性を指定する場合は、小なり記号 (<) の後、または大なり記号 (`>`) の前。 また、属性を指定する場合は、大なり記号 (`>`) の後。 しかし、アセンブリ レベルまたはモジュール レベルの属性を指定する場合は、行連結文字 (`_`) を含める必要があります。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#10)]

   詳細については、「[属性の概要](../concepts/attributes/index.md)」を参照してください。

- クエリ演算子 (`Aggregate`、`Distinct`、`From`、`Group By`、`Group Join`、`Join`、`Let`、`Order By`、`Select`、`Skip`、`Skip While`、`Take`、`Take While`、`Where`、`In`、`Into`、`On`、`Ascending`、および `Descending`) の前か後。 複数のキーワードで構成されているクエリ演算子 (`Order By`、`Group Join`、`Take While`、および `Skip While`) のキーワードの間で改行することはできません。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#11)]

   詳細については、「[クエリ](../../language-reference/queries/index.md)」を参照してください。

- `For Each` ステートメント内の `In` キーワードの後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#12)]

   詳細については、[For Each...Next ステートメント](../../language-reference/statements/for-each-next-statement.md) を参照してください。

- コレクション初期化子内の `From` キーワードの後。 次に例を示します。

   [!code-vb[VbVbalrLineContinuation#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrlinecontinuation/vb/module1.vb#13)]

   詳細については、「[コレクション初期化子](collection-initializers/index.md)」を参照してください。

## <a name="adding-comments"></a>コメントの追加

ソース コードは、それを記述したプログラマであっても、見ればすぐわかるとは限りません。 そのため、コードの文書化に役立つように、ほとんどのプログラマは埋め込みコメントを十分に利用します。 コード内のコメントでは、後でそれを読んだり、操作を行うすべてのユーザーに対して、プロシージャまたは特定の命令について説明することができます。 Visual Basic では、コンパイル時にコメントが無視され、コンパイルされたコードには影響しません。

コメント行はアポストロフィ (`'`) または `REM` で始まり、その後にスペースが続きます。 文字列内の場合を除き、コード内の任意の場所に追加することができます。 ステートメントにコメントを追加するには、ステートメントの後にアポストロフィまたは `REM` を挿入し、その後にコメントを続けます。 コメントを独自の行に続けることもできます。 これらの考えられる例を以下に示します。

[!code-vb[VbVbalrStatements#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#72)]

## <a name="checking-compilation-errors"></a>コンパイル エラーの確認

コード行を入力した後、その行の下に青い破線が表示されている場合 (エラー メッセージも表示される場合があります)、ステートメントに構文エラーがあります。 ステートメントの問題を確認し (タスク一覧を調べるか、マウス ポインターでエラーをポイントしてエラー メッセージを読んで)、修正する必要があります。 コード内の構文エラーをすべて修正するまで、プログラムでは正しくコンパイルできません。

## <a name="related-sections"></a>関連項目

|用語|定義|
|---|---|
|[代入演算子](../../language-reference/operators/assignment-operators.md)|`=`、`*=`、`&=` などの代入演算子に関する言語リファレンス ページへのリンクを提供します。|
|[演算子および式](./operators-and-expressions/index.md)|要素を演算子と組み合わせて新しい値を生成する方法を示します。|
|[方法: コード内でステートメントを分割および連結する](../program-structure/how-to-break-and-combine-statements-in-code.md)|1 つのステートメントを複数の行に分割する方法と、複数のステートメントを同じ行に配置する方法を示します。|
|[方法: ステートメントへのラベル付け](../program-structure/how-to-label-statements.md)|コード行にラベルを付ける方法を示します。|
