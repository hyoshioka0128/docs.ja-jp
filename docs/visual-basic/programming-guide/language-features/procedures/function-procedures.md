---
title: Function プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- Function procedures
- return values [Visual Basic], function procedures
- Visual Basic code, procedures
- procedures [Visual Basic], calling
- procedures [Visual Basic], Function procedures
- syntax [Visual Basic], function procedures
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
ms.openlocfilehash: b0ba96a875fd8785e45eee565beefe4b961ffc9d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388752"
---
# <a name="function-procedures-visual-basic"></a>Function プロシージャ (Visual Basic)

`Function` プロシージャは、`Function` ステートメントと `End Function` ステートメントで囲まれた一連の Visual Basic ステートメントです。 `Function` プロシージャはタスクを実行した後、呼び出し元のコードに制御を戻します。 制御を戻すときに、呼び出し元のコードに値も返します。

プロシージャが呼び出されるたびに、そのステートメントが実行されます。`Function` ステートメントの後の実行可能な最初のステートメントから始まり、最初に出現した `End Function`、`Exit Function`、または `Return` ステートメントで終了します。

`Function` プロシージャは、モジュール、クラス、または構造体で定義できます。 既定では `Public` であるため、プロシージャが定義されているモジュール、クラス、または構造体にアクセスできるアプリケーション内のどこからでも呼び出すことができます。

`Function` プロシージャは、呼び出し元のコードから渡される定数、変数、式などの引数を受け取ることができます。

## <a name="declaration-syntax"></a>宣言の構文

`Function` プロシージャを宣言するための構文は次のとおりです。

```vb
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType
    [Statements]
End Function
```

"*修飾子*" では、アクセス レベルと、オーバーロード、オーバーライド、共有、シャドウに関する情報を指定できます。 詳細については、「[Function Statement (Function ステートメント)](../../../language-reference/statements/function-statement.md)」をご覧ください。

各パラメーターは、[Sub プロシージャ](./sub-procedures.md)の場合と同様に宣言します。

### <a name="data-type"></a>データの種類

すべての変数と同様に、すべての `Function` プロシージャにもデータ型があります。 このデータ型は、`Function` ステートメントの `As` 句で指定され、関数が呼び出し元のコードに返す値のデータ型が決定されます。 次の宣言のサンプルはこれを示しています。

```vb
Function Yesterday() As Date
End Function

Function FindSqrt(radicand As Single) As Single
End Function
```

詳細については、「[Function Statement (Function ステートメント)](../../../language-reference/statements/function-statement.md)」の「Parts (要素)」をご覧ください。

### <a name="returning-values"></a>戻り値

`Function` プロシージャが呼び出し元のコードに返す値は戻り値と呼ばれます。 プロシージャは、次の 2 つの方法のいずれかでこの値を返します。

- `Return` ステートメントを使用して戻り値を指定し、呼び出し元のプログラムに制御をすぐに戻します。 次に例を示します。

  ```vb
  Function FunctionName [(ParameterList)] As ReturnType
      ' The following statement immediately transfers control back
      ' to the calling code and returns the value of Expression.
      Return Expression
  End Function
  ```

- プロシージャの 1 つ以上のステートメントで、独自の関数名に値を割り当てます。 `Exit Function` または `End Function` ステートメントが実行されるまで、呼び出し元のプログラムに制御は戻りません。 次に例を示します。

  ```vb
  Function FunctionName [(ParameterList)] As ReturnType
      ' The following statement does not transfer control back to the calling code.
      FunctionName = Expression
      ' When control returns to the calling code, Expression is the return value.
  End Function
  ```

戻り値を関数名に割り当てる利点は、`Exit Function` または `End Function` ステートメントが出現するまで、プロシージャから制御が戻されないことです。 これにより、暫定値を割り当て、必要に応じて後で調整できます。

戻り値の詳細については、「[Function Statement (Function ステートメント)](../../../language-reference/statements/function-statement.md)」をご覧ください。 配列を返す方法については、[配列](../arrays/index.md)に関する記事をご覧ください。

## <a name="calling-syntax"></a>呼び出しの構文

`Function` プロシージャを呼び出すには、その名前と引数を代入ステートメントの右辺または式に含めます。 省略可能ではないすべての引数に値を指定する必要があり、引数リストをかっこで囲む必要があります。 引数を指定しない場合は、必要に応じてかっこを省略できます。

`Function` プロシージャの呼び出しの構文は次のとおりです。

*lvalue*  `=`  *関数名* `[(` *引数リスト* `)]`

`If ((` *関数名* `[(` *引数リスト* `)] / 3) <=`  *式* `) Then`

`Function` プロシージャを呼び出すときに、その戻り値を使用する必要はありません。 使用しない場合、関数のすべてのアクションが実行されますが、戻り値は無視されます。 多くの場合、<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> はこの方法で呼び出されます。

### <a name="illustration-of-declaration-and-call"></a>宣言と呼び出しの実例

次の `Function` プロシージャは、他の 2 つの辺の値を指定して、直角三角形の最も長い辺 (斜辺) を計算します。

[!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]

次の例は、`hypotenuse` の一般的な呼び出しを示しています。

[!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Function ステートメント](../../../language-reference/statements/function-statement.md)
- [方法: 値を返すプロシージャを作成する](./how-to-create-a-procedure-that-returns-a-value.md)
- [方法: プロシージャから値を返す](./how-to-return-a-value-from-a-procedure.md)
- [方法: 値を返すプロシージャを呼び出す](./how-to-call-a-procedure-that-returns-a-value.md)
