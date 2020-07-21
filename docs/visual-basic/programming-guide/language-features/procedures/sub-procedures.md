---
title: Sub プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- Sub procedures [Visual Basic], about Sub procedures
- statement blocks
- Sub procedures [Visual Basic], calling
- procedures [Visual Basic], calling
- Sub procedures [Visual Basic], syntax
- Sub procedures
- procedures [Visual Basic], Sub
- syntax [Visual Basic], Sub procedures
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
ms.openlocfilehash: 9ca1d302a0bc8e989e0b2dddf8cce68e89211d57
ms.sourcegitcommit: 5d769956a04b6d68484dd717077fabc191c21da5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76163814"
---
# <a name="sub-procedures-visual-basic"></a>Sub プロシージャ (Visual Basic)

`Sub` プロシージャは、`Sub` ステートメントと `End Sub` ステートメントで囲まれた一連の Visual Basic ステートメントです。 `Sub` プロシージャはタスクを実行した後、呼び出し元のコードに制御を戻しますが、呼び出し元のコードに値は返しません。

プロシージャが呼び出されるたびに、そのステートメントが実行されます。`Sub` ステートメントの後の実行可能な最初のステートメントから始まり、最初に出現した `End Sub`、`Exit Sub`、または `Return` ステートメントで終了します。

`Sub` プロシージャは、モジュール、クラス、構造体で定義できます。 既定では `Public` であるため、プロシージャが定義されているモジュール、クラス、または構造体にアクセスできるアプリケーション内のどこからでも呼び出すことができます。 "*メソッド*" という用語は、プロシージャが定義されているモジュール、クラス、または構造体の外部からアクセスされる `Sub` または `Function` プロシージャを示します。 詳細については、「[プロシージャ](./index.md)」を参照してください。

`Sub` プロシージャは、呼び出し元のコードから渡される定数、変数、式などの引数を受け取ることができます。

## <a name="declaration-syntax"></a>宣言の構文

`Sub` プロシージャを宣言するための構文は次のとおりです。

```vb
[modifiers] Sub SubName[(parameterList)]
    ' Statements of the Sub procedure.
End Sub
```

`modifiers` では、アクセス レベルと、オーバーロード、オーバーライド、共有、シャドウに関する情報を指定できます。 詳細については、「[Sub Statement (Sub ステートメント)](../../../language-reference/statements/sub-statement.md)」をご覧ください。

## <a name="parameter-declaration"></a>パラメーターの宣言

変数を宣言する場合と同様に、パラメーター名とデータ型を指定して、プロシージャの各パラメーターを宣言します。 引渡し方法、パラメーターが省略可能かどうか、パラメーターがパラメーター配列かどうかを指定することもできます。

パラメーター リストの各パラメーターの構文は次のとおりです。

```vb
[Optional] [ByVal | ByRef] [ParamArray] parameterName As DataType
```

パラメーターが省略可能な場合は、宣言の一部として既定値も指定する必要があります。 既定値を指定するための構文は次のとおりです。

```vb
Optional [ByVal | ByRef]  parameterName As DataType = defaultValue
```

### <a name="parameters-as-local-variables"></a>ローカル変数としてのパラメーター

制御がプロシージャに渡されると、各パラメーターはローカル変数として扱われます。 つまり、パラメーターの有効期間はプロシージャの有効期間と同じであり、スコープはプロシージャ全体になります。

## <a name="calling-syntax"></a>呼び出しの構文

`Sub` プロシージャは、スタンドアロンの呼び出しステートメントで明示的に呼び出します。 式で名前を使用して呼び出すことはできません。 省略可能ではないすべての引数に値を指定する必要があり、引数リストをかっこで囲む必要があります。 引数を指定しない場合は、必要に応じてかっこを省略できます。 `Call` キーワードの使用は任意ですが、使用しないことをお勧めします。

`Sub` プロシージャの呼び出しの構文は次のとおりです。

```vb
[Call] SubName[(argumentlist)]
```

`Sub` メソッドは、これを定義しているクラスの外部から呼び出すことができます。 まず、`New` キーワードを使用してクラスのインスタンスを作成するか、クラスのインスタンスを返すメソッドを呼び出す必要があります。 詳細については、「[New Operator (New 演算子)](../../../language-reference/operators/new-operator.md)」をご覧ください。 次に、次の構文を使用して、インスタンス オブジェクトに対して `Sub` メソッドを呼び出すことができます。

```vb
object.MethodName[(argumentList)]
```

### <a name="illustration-of-declaration-and-call"></a>宣言と呼び出しの実例

次の `Sub` プロシージャは、アプリケーションが実行しようとしているタスクをコンピューターのオペレーターに通知し、タイム スタンプも表示します。 すべてのタスクの開始時にこのコードを複製するのではなく、アプリケーションはさまざまな場所から `tellOperator` 呼び出すだけです。 各呼び出しでは、開始されるタスクを識別する文字列を `task` 引数に渡します。

[!code-vb[VbVbcnProcedures#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#2)]

次の例は、`tellOperator` の一般的な呼び出しを示しています。

[!code-vb[VbVbcnProcedures#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#3)]

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Function プロシージャ](./function-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [方法: 値を返さないプロシージャを呼び出す](./how-to-call-a-procedure-that-does-not-return-a-value.md)
- [方法: Visual Basic でイベント ハンドラーを呼び出す](./how-to-call-an-event-handler.md)
