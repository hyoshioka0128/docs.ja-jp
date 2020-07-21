---
title: Function ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Function
helpviewer_keywords:
- procedures [Visual Basic], creating
- Function procedures [Visual Basic], Function statement syntax
- functions [Visual Basic], function procedures
- ParamArray keyword [Visual Basic], Function statements
- Private keyword [Visual Basic], Function statements
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- Public keyword [Visual Basic], in Function statement
- ByVal keyword [Visual Basic], Function statements
- procedures [Visual Basic], recursive
- Implements keyword [Visual Basic], Function statements
- procedures [Visual Basic], returning values
- Exit statement [Visual Basic], in Function procedures
- recursive procedures
- As keyword [Visual Basic], in Function statement
- Optional keyword [Visual Basic], Function statements
- Function statement [Visual Basic]
- Visual Basic code, Function procedures
- procedures [Visual Basic], function
- ByRef keyword [Visual Basic], Function statements
- Friend keyword [Visual Basic], Function statements
- End keyword [Visual Basic], Function statements
- Handles keyword [Visual Basic], Function statements
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
ms.openlocfilehash: 49cf4fead2c5594b7ac6815f82fea0dc995ea436
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404629"
---
# <a name="function-statement-visual-basic"></a>Function ステートメント (Visual Basic)

`Function` プロシージャを定義する名前、パラメーター、およびコードを宣言します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]
    [ statements ]
    [ Exit Function ]
    [ statements ]
End Function
```

## <a name="parts"></a>指定項目

- `attributelist`

  任意。 「[属性リスト](attribute-list.md)」を参照してください。

- `accessmodifier`

  任意。 次のいずれかの値を指定します。

  - [Public](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Private](../modifiers/private.md)

  - [Protected Friend](../modifiers/protected-friend.md)

  - [Private Protected](../modifiers/private-protected.md)

  「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

- `proceduremodifiers`

  任意。 次のいずれかの値を指定します。

  - [Overloads](../modifiers/overloads.md)

  - [Overrides](../modifiers/overrides.md)

  - [Overridable](../modifiers/overridable.md)

  - [NotOverridable](../modifiers/notoverridable.md)

  - [MustOverride](../modifiers/mustoverride.md)

  - `MustOverride Overrides`

  - `NotOverridable Overrides`

- `Shared`

  任意。 「[Shared](../modifiers/shared.md)」を参照してください。

- `Shadows`

  任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。

- `Async`

  任意。 「[Async](../modifiers/async.md)」を参照してください。

- `Iterator`

  任意。 「[Iterator](../modifiers/iterator.md)」を参照してください。

- `name`

  必須です。 プロシージャの名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

- `typeparamlist`

  任意。 ジェネリック プロシージャの型パラメーターの一覧。 「[型リスト](type-list.md)」を参照してください。

- `parameterlist`

  任意。 このプロシージャのパラメーターを表すローカル変数名の一覧。 「[パラメーターの一覧](parameter-list.md)」を参照してください。

- `returntype`

  `Option Strict` が `On` の場合は必ず指定します。 このプロシージャによって返される値のデータ型。

- `Implements`

  任意。 それぞれこのプロシージャの含まれているクラスまたは構造体によって実装されたインターフェイスに定義されている、1 つ以上の `Function` プロシージャを、このプロシージャが実装することを示します。 「[Implements ステートメント](implements-statement.md)」を参照してください。

- `implementslist`

  `Implements` を指定する場合は、必ず指定します。 実装される `Function` プロシージャのリストです。

  `implementedprocedure [ , implementedprocedure ... ]`

  `implementedprocedure` の構文と指定項目は次のとおりです。

  `interface.definedname`

  |パーツ|説明|
  |---|---|
  |`interface`|必須です。 このプロシージャの含まれているクラスまたは構造体によって実装されたインターフェイスの名前。|
  |`definedname`|必須です。 `interface` の中でプロシージャを定義するために使用する名前。|

- `Handles`

  任意。 このプロシージャで 1 つ以上の特定のイベントを処理できることを示します。 「[Handles](handles-clause.md)」を参照してください。

- `eventlist`

  `Handles` を指定する場合は、必ず指定します。 このプロシージャで処理するイベントの一覧。

  `eventspecifier [ , eventspecifier ... ]`

  `eventspecifier` の構文と指定項目は次のとおりです。

  `eventvariable.event`

  |パーツ|説明|
  |---|---|
  |`eventvariable`|必須です。 イベントを発生させるクラスまたは構造体のデータ型で宣言されたオブジェクト変数。|
  |`event`|必須です。 このプロシージャで処理するイベントの名前。|

- `statements`

  任意。 このプロシージャ内で実行されるステートメントのブロック。

- `End Function`

  このプロシージャの定義を終了します。

## <a name="remarks"></a>Remarks

すべての実行可能コードは、プロシージャ内になければなりません。 さらに各プロシージャは、含んでいるクラス、構造体、またはモジュールと呼ばれるクラス、構造体、またはモジュール内で宣言します。

呼び出し元のコードに値を返すには、`Function` プロシージャを使用します。それ以外の場合は、`Sub` プロシージャを使用します。

## <a name="defining-a-function"></a>関数の定義

`Function` プロシージャは、モジュール レベルでのみ定義できます。 そのため、関数の宣言コンテキストは、クラス、構造体、モジュール、インターフェイスにする必要があり、ソース ファイル、名前空間、プロシージャ、ブロックにすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

`Function` プロシージャは、既定でパブリック アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。

`Function` プロシージャでは、プロシージャが返す値のデータ型を宣言できます。 任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。 `returntype` パラメーターを指定しない場合、プロシージャから `Object` が返されます。

このプロシージャで `Implements` キーワードを使用している場合、含まれているクラスまたは構造体にも、その `Class` または `Structure` ステートメントの直後に `Implements` ステートメントが必要です。 `Implements` ステートメントには、`implementslist` で指定された各インターフェイスを含める必要があります。 ただし、インターフェイスで `Function` を定義するときに使用する名前 (`definedname`) は、このプロシージャの名前 (`name`) に一致している必要はありません。

> [!NOTE]
> ラムダ式を使用して、関数式をインラインで定義できます。 詳細については、「[関数式](../operators/function-expression.md)」と「[ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)」を参照してください。

## <a name="returning-from-a-function"></a>関数からの復帰

`Function` プロシージャが呼び出し元のコードに戻ると、実行は、プロシージャを呼び出したステートメントの後のステートメントから続行されます。

関数から値を返すには、関数名に値を代入するか、`Return` ステートメントに値を含めることができます。

`Return` ステートメントでは、次の例に示すように、戻り値を代入して、同時に関数を終了します。

[!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]

次の例では、関数名 `myFunction` に戻り値を代入してから、`Exit Function` ステートメントを使用して戻ります。

[!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]

`Exit Function` および `Return` ステートメントでは、`Function` プロシージャがすぐに終了します。 任意の数の `Exit Function` および `Return` ステートメントをプロシージャ内の任意の場所に記述でき、`Exit Function` ステートメントと `Return` ステートメントを混在させることができます。

`name` に値を代入せずに `Exit Function` を使用すると、プロシージャから、`returntype` に指定したデータ型の既定値が返されます。 `returntype` を指定していない場合、プロシージャから `Nothing` が返されます。これは `Object` の既定値です。

## <a name="calling-a-function"></a>関数の呼び出し

`Function` プロシージャを呼び出すには、式の中でプロシージャ名の後にかっこで囲んだ引数リストを使用します。 引数を指定しない場合に限り、かっこを省略できます。 ただし、常にかっこを含めると、コードが読みやすくなります。

`Function` プロシージャは、`Sqrt`、`Cos`、`ChrW` などの任意のライブラリ関数を呼び出すのと同じ方法で呼び出します。

`Call` キーワードを使用して関数を呼び出すこともできます。 その場合、戻り値は無視されます。 ほとんどの場合に `Call` キーワードを使用しないことをお勧めします。 詳細については、「[Call ステートメント](call-statement.md)」を参照してください。

Visual Basic では、内部効率を高めるために算術式が再配置されることがあります。 そのため、関数で同じ式内の変数の値を変更する場合は、算術式で `Function` プロシージャを使用しないでください。

## <a name="async-functions"></a>Async 関数

*Async* 機能を使用することによって、明示的なコールバックを使用せずに、または複数の関数やラムダ式にわたって手動でコードを分割することなく、非同期メソッドを呼び出すことができます。

関数を [Async](../modifiers/async.md) 修飾子でマークすると、その関数で [Await](../operators/await-operator.md) 演算子を使用できます。 制御が `Async` 関数の `Await` 式に到達すると、制御が呼び出し元に戻り、待機中のタスクが完了するまで関数の進行が中断されます。 タスクが完了すると、関数で実行を再開できます。

> [!NOTE]
> `Async` プロシージャは、まだ完了していない待機中の最初のオブジェクトが検出されるか、または `Async` プロシージャの最後に達するか、どちらか先に発生したときに、呼び出し元に戻ります。

`Async` 関数の戻り値の型には、<xref:System.Threading.Tasks.Task%601> または <xref:System.Threading.Tasks.Task> を指定できます。 戻り値の型が <xref:System.Threading.Tasks.Task%601> の `Async` 関数の例を次に示します。

`Async` 関数で、[ByRef](../modifiers/byref.md) パラメーターを宣言することはできません。

[Sub ステートメント](sub-statement.md) を、`Async` 修飾子でマークすることもできます。 これは主に、値を返すことができないイベント ハンドラーに使用します。 `Async` `Sub` プロシージャは待機できず、`Async` `Sub` プロシージャの呼び出し元は、`Sub` プロシージャによってスローされた例外をキャッチできません。

`Async` 関数の詳細については、「[Async および Await を使用した非同期プログラミング](../../programming-guide/concepts/async/index.md)」、「[非同期プログラムにおける制御フロー](../../programming-guide/concepts/async/control-flow-in-async-programs.md)」、「[非同期の戻り値の型](../../programming-guide/concepts/async/async-return-types.md)」を参照してください。

## <a name="iterator-functions"></a>iterator 関数

*iterator* 関数は、リストや配列など、コレクションに対するカスタムの反復を実行します。 iterator 関数は、[Yield](yield-statement.md) ステートメントを使用して、各要素を 1 回に 1 つ返します。 [Yield](yield-statement.md) ステートメントに達すると、コードの現在の場所が記憶されます。 次回、iterator 関数が呼び出されると、この位置から実行が再開されます。

[For Each...Next](for-each-next-statement.md) ステートメントを使用して、クライアント コードから反復子を呼び出します。

iterator 関数の戻り値の型には、<xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator>、または <xref:System.Collections.Generic.IEnumerator%601> を指定できます。

詳細については、「 [反復子](../../programming-guide/concepts/iterators.md)」を参照してください。

## <a name="example"></a>例

次の例では、`Function` ステートメントを使用して、`Function` プロシージャの本体を形成する名前、パラメーター、およびコードを宣言しています。 `ParamArray` 修飾子を使用すると、関数では可変数の引数を受け取ることができます。

[!code-vb[VbVbalrStatements#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#25)]

## <a name="example"></a>例

次の例では、前の例で宣言した関数を呼び出しています。

[!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]

## <a name="example"></a>例

次の例で、`DelayAsync` は、戻り値の型が <xref:System.Threading.Tasks.Task%601> である `Async` `Function` です。 `DelayAsync` には、整数を返す `Return` ステートメントがあります。 そのため、`DelayAsync` の関数宣言では、戻り値の型を `Task(Of Integer)` にする必要があります。 戻り値の型が `Task(Of Integer)` であるため、`DoSomethingAsync` 内の `Await` 式を評価すると整数が生成されます。 これは、ステートメント `Dim result As Integer = Await delayTask` に示しています。

`startButton_Click` プロシージャは、`Async Sub` プロシージャの一例です。 `DoSomethingAsync` が `Async` 関数であるため、`DoSomethingAsync` を呼び出すタスクは、`Await DoSomethingAsync()` ステートメントに示すように、待機させる必要があります。 `startButton_Click` `Sub` プロシージャは、`Await` 式を使用しているため、`Async` 修飾子を使用して定義する必要があります。

[!code-vb[csAsyncMethod#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncmethod/vb/mainwindow.xaml.vb#1)]

## <a name="see-also"></a>関連項目

- [Sub ステートメント](sub-statement.md)
- [Function プロシージャ](../../programming-guide/language-features/procedures/function-procedures.md)
- [パラメーター リスト](parameter-list.md)
- [Dim ステートメント](dim-statement.md)
- [Call ステートメント](call-statement.md)
- [Of](of-clause.md)
- [パラメーター配列](../../programming-guide/language-features/procedures/parameter-arrays.md)
- [方法: ジェネリック クラスを使用する](../../programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [プロシージャのトラブルシューティング](../../programming-guide/language-features/procedures/troubleshooting-procedures.md)
- [ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [Function 式](../operators/function-expression.md)
