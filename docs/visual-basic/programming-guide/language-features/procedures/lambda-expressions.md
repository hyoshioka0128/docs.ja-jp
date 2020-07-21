---
title: ラムダ式
ms.date: 07/20/2015
f1_keywords:
- vb.LambdaFunction
helpviewer_keywords:
- functions [Visual Basic], lambda expressions
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
- inline functions [Visual Basic]
ms.assetid: 137064b0-3928-4bfa-ba71-c3f9cbd951e2
ms.openlocfilehash: 54a9c0cf275a67c77748c32771c3c5dcbdb916d7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406704"
---
# <a name="lambda-expressions-visual-basic"></a>ラムダ式 (Visual Basic)

"*ラムダ式*" は、デリゲートが有効な場所であればどこでも使用できる、名前のない関数またはサブルーチンです。 ラムダ式は関数またはサブルーチンにすることができ、単一行または複数行にすることができます。 値を現在のスコープからラムダ式に渡すことができます。

> [!NOTE]
> `RemoveHandler` ステートメントは例外です。 `RemoveHandler` のデリゲート パラメーターにラムダ式を渡すことはできません。

標準の関数またはサブルーチンを作成する場合と同様に、`Function` または `Sub` キーワードを使用してラムダ式を作成します。 ただし、ラムダ式はステートメントに含まれます。

次の例は、引数をインクリメントして値を返すラムダ式です。 この例は、関数の単一行および複数行のラムダ式の構文を示しています。

[!code-vb[VbVbalrLambdas#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#14)]

次の例は、コンソールに値を書き込むラムダ式です。 この例は、サブルーチンの単一行および複数行のラムダ式の構文を示しています。

[!code-vb[VbVbalrLambdas#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#15)]

上記の例では、ラムダ式が変数名に割り当てられていることに注意してください。 変数を参照するときは常にラムダ式を呼び出します。 次の例に示すように、ラムダ式の宣言と呼び出しを同時に行うこともできます。

[!code-vb[VbVbalrLambdas#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#3)]

ラムダ式は関数呼び出しの値として返すことも (このトピックで後述する「[コンテキスト](#context)」の例を参照)、次の例に示すように、デリゲート型を受け取るパラメーターに引数として渡すこともできます。

[!code-vb[VbVbalrLambdas#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class2.vb#8)]

## <a name="lambda-expression-syntax"></a>ラムダ式の構文

ラムダ式の構文は、標準の関数またはサブルーチンの構文に似ています。 相違点は、次のとおりです。

- ラムダ式には名前はありません。

- ラムダ式には、`Overloads` や `Overrides` などの修飾子を含めることはできません。

- 単一行のラムダ関数では、`As` 句を戻り値の型を指定しません。 代わりに、ラムダ式の本体が評価される値から型が推論されます。 たとえば、ラムダ式の本体が `cust.City = "London"` の場合、戻り値の型は `Boolean` になります。

- 複数行のラムダ関数では、`As` 句を使用して戻り値の型を指定することも、戻り値の型が推論されるように `As` 句を省略することもできます。 複数行のラムダ関数で `As` 句を省略すると、戻り値の型として、複数行のラムダ関数のすべての `Return` ステートメントから最も優先度の高い型が推論されます。 "*最も優先度の高い型*" は、他のすべての型から拡大変換できる一意の型です。 この一意の型を特定できない場合、最も優先度の高い型は、配列内の他のすべての型から縮小変換できる一意の型になります。 これらの一意の型をどちらも特定できない場合は、 `Object`が最も優先度の高い型になります。 この場合、`Option Strict` が `On` に設定されていると、コンパイラ エラーが発生します。

     たとえば、`Return` ステートメントに指定された式に、`Integer`、`Long`、`Double` の各型の値が含まれている場合、結果の配列は `Double` 型になります。 `Integer` と `Long` はどちらも `Double` に拡大変換され、`Double` のみになります。 そのため、 `Double` が最も優先度の高い型になります。 詳細については、「 [Widening and Narrowing Conversions](../data-types/widening-and-narrowing-conversions.md)」を参照してください。

- 単一行の関数の本体は、ステートメントではなく、値を返す式である必要があります。 単一行の関数の `Return` ステートメントはありません。 単一行の関数によって返される値は、関数の本体に含まれる式の値です。

- 単一行のサブルーチンの本体は、単一行のステートメントである必要があります。

- 単一行の関数とサブルーチンには、`End Function` または `End Sub` ステートメントは含まれません。

- `As` キーワードを使用して、ラムダ式のパラメーターのデータ型を指定できます。また、パラメーターのデータ型を推論することもできます。 すべてのパラメーターにデータ型が指定されているか、すべて推論される必要があります。

- `Optional` および `Paramarray` パラメーターは使用できません。

- ジェネリック パラメーターは使用できません。

## <a name="async-lambdas"></a>非同期ラムダ

[Async](../../../language-reference/modifiers/async.md) キーワードと [Await Operator](../../../language-reference/operators/await-operator.md) キーワードを使用すると、非同期処理を組み込んだラムダ式およびステートメントを簡単に作成できます。 たとえば、次に示す Windows フォーム例には、非同期メソッド `ExampleMethodAsync`を呼び出して待機するイベント ハンドラーが含まれています。

```vb
Public Class Form1

    Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        ' ExampleMethodAsync returns a Task.
        Await ExampleMethodAsync()
        TextBox1.Text = vbCrLf & "Control returned to button1_Click."
    End Sub

    Async Function ExampleMethodAsync() As Task
        ' The following line simulates a task-returning asynchronous process.
        Await Task.Delay(1000)
    End Function

End Class
```

[AddHandler ステートメント](../../../language-reference/statements/addhandler-statement.md)で非同期ラムダを使用して、同じイベント ハンドラーを追加できます。 次の例に示すように、このハンドラーを追加するには、ラムダ パラメーター リストの前に `Async` 修飾子を追加します。

```vb
Public Class Form1

    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        AddHandler Button1.Click,
            Async Sub(sender1, e1)
                ' ExampleMethodAsync returns a Task.
                Await ExampleMethodAsync()
                TextBox1.Text = vbCrLf & "Control returned to Button1_ Click."
            End Sub
    End Sub

    Async Function ExampleMethodAsync() As Task
        ' The following line simulates a task-returning asynchronous process.
        Await Task.Delay(1000)
    End Function

End Class
```

非同期メソッドの作成および使用方法の詳細については、「[Asynchronous programming with Async and Await (Async および Await を使用した非同期プログラミング)](../../concepts/async/index.md)」をご覧ください。

## <a name="context"></a>コンテキスト

ラムダ式は、その式が定義されているスコープとコンテキストを共有します。 包含スコープで記述されたコードと同じアクセス権を持ちます。 これには、包含スコープ内のメンバー変数、関数とサブルーチン、`Me`、パラメーターとローカル変数へのアクセスが含まれます。

包含スコープ内のローカル変数とパラメーターへのアクセスは、そのスコープの有効期間を超えて拡張できます。 ラムダ式を参照するデリゲートがガベージ コレクションで使用できない間は、元の環境の変数へのアクセスが保持されます。 次の例では、変数 `target` は、`makeTheGame` に対してローカルです。これは、ラムダ式 `playTheGame` が定義されているメソッドです。 `Main` で `takeAGuess` に割り当てられた、返されたラムダ式は、引き続きローカル変数 `target` にアクセスできます。

[!code-vb[VbVbalrLambdas#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class6.vb#12)]

次の例は、入れ子になったラムダ式の幅広いアクセス権を示しています。 返されたラムダ式は、`Main` から `aDel` として実行されると、次の要素にアクセスします。

- それが定義されているクラスのフィールド: `aField`

- それが定義されているクラスのプロパティ: `aProp`

- それが定義されている `functionWithNestedLambda` メソッドのパラメーター: `level1`

- `functionWithNestedLambda` のローカル変数: `localVar`

- それが入れ子になっているラムダ式のパラメーター: `level2`

 [!code-vb[VbVbalrLambdas#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class3.vb#9)]

## <a name="converting-to-a-delegate-type"></a>デリゲート型への変換

ラムダ式は、互換性のあるデリゲート型に暗黙的に変換できます。 互換性に関する一般的な要件については、「[厳密でないデリゲート変換](../delegates/relaxed-delegate-conversion.md)」をご覧ください。 たとえば、次のコード例は、`Func(Of Integer, Boolean)` または一致するデリゲート シグネチャに暗黙的に変換するラムダ式を示しています。

[!code-vb[VbVbalrLambdas#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#16)]

次のコード例は、`Sub(Of Double, String, Double)` または一致するデリゲート シグネチャに暗黙的に変換するラムダ式を示しています。

[!code-vb[VbVbalrLambdas#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/class7.vb#23)]

ラムダ式をデリゲートに割り当てるか、引数としてプロシージャに渡す場合、パラメーター名を指定できますが、データ型を省略することで、デリゲートから型を取得できます。

## <a name="examples"></a>使用例

- 次の例では、null 許容値型引数に値が割り当てられている場合は `True` を返し、値が `Nothing` の場合は `False` を返すラムダ式を定義します。

     [!code-vb[VbVbalrLambdas#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#4)]

- 次の例では、配列の最後の要素のインデックスを返すラムダ式を定義します。

     [!code-vb[VbVbalrLambdas#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#5)]

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
- [デリゲート](../delegates/index.md)
- [Function ステートメント](../../../language-reference/statements/function-statement.md)
- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [null 許容値型](../data-types/nullable-value-types.md)
- [方法: Visual Basic でプロシージャを別のプロシージャに渡す](../delegates/how-to-pass-procedures-to-another-procedure.md)
- [方法: ラムダ式を作成する](./how-to-create-a-lambda-expression.md)
- [厳密でないデリゲート変換](../delegates/relaxed-delegate-conversion.md)
