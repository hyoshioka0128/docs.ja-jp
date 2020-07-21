---
title: Sub ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Sub
helpviewer_keywords:
- Public keyword [Visual Basic], Sub statements
- procedures [Visual Basic], creating
- declaring procedures [Visual Basic], Sub statement
- arguments [Visual Basic], Sub procedures
- As keyword [Visual Basic], Sub statements
- Optional keyword [Visual Basic], Sub statements
- declarations [Visual Basic], procedures
- Sub keyword [Visual Basic]
- Handles keyword [Visual Basic], Sub statements
- Protected Friend keyword [Visual Basic]
- ParamArray keyword [Visual Basic], Sub statements
- Implements keyword [Visual Basic], Sub statements
- Sub statement [Visual Basic]
- subroutines
- ByRef keyword [Visual Basic], Sub statements
- Sub procedures [Visual Basic], Sub statement
- recursive procedures
- Private keyword [Visual Basic], Sub statements
- Friend keyword [Visual Basic], Sub statements
- Exit statement [Visual Basic], Sub statements
- procedures [Visual Basic], Sub
- End keyword [Visual Basic], Sub statements
- ByVal keyword [Visual Basic], Sub statements
- Visual Basic code, Sub procedures
ms.assetid: e347d700-d06c-405b-b302-e9b1edb57dfc
ms.openlocfilehash: e50b79c31c92ac116d6c82bcececba3340894d74
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404175"
---
# <a name="sub-statement-visual-basic"></a>Sub ステートメント (Visual Basic)

`Sub` プロシージャを定義する名前、パラメーター、およびコードを宣言します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ Partial ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async ]
Sub name [ (Of typeparamlist) ] [ (parameterlist) ] [ Implements implementslist | Handles eventlist ]
    [ statements ]
    [ Exit Sub ]
    [ statements ]
End Sub
```

## <a name="parts"></a>指定項目

- `attributelist`

  任意。 「[属性リスト](attribute-list.md)」を参照してください。

- `Partial`

  任意。 部分メソッドの定義を示します。 「[部分メソッド](../../programming-guide/language-features/procedures/partial-methods.md)」を参照してください。

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

- `name`

  必須です。 プロシージャの名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。 クラスのコンストラクター プロシージャを作成するには、`Sub` プロシージャの名前を `New` キーワードに設定します。 詳細については、以下をご覧ください: [オブジェクトの有効期間: オブジェクトの作成と破棄](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)

- `typeparamlist`

  任意。 ジェネリック プロシージャの型パラメーターの一覧。 「[型リスト](type-list.md)」を参照してください。

- `parameterlist`

  任意。 このプロシージャのパラメーターを表すローカル変数名の一覧。 「[パラメーターの一覧](parameter-list.md)」を参照してください。

- `Implements`

  任意。 それぞれこのプロシージャの含まれているクラスまたは構造体によって実装されたインターフェイスに定義されている、1 つ以上の `Sub` プロシージャを、このプロシージャが実装することを示します。 「[Implements ステートメント](implements-statement.md)」を参照してください。

- `implementslist`

  `Implements` を指定する場合は、必ず指定します。 実装される `Sub` プロシージャのリストです。

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

  任意。 このプロシージャ内で実行するステートメントのブロック。

- `End Sub`

  このプロシージャの定義を終了します。

## <a name="remarks"></a>Remarks

すべての実行可能コードは、プロシージャ内になければなりません。 呼び出し元のコードに値を返さない場合は、`Sub` プロシージャを使用します。 値を返す場合は、`Function` プロシージャを使用します。

## <a name="defining-a-sub-procedure"></a>Sub プロシージャの定義

`Sub` プロシージャは、モジュール レベルでのみ定義できます。 そのため、Sub プロシージャの宣言コンテキストはクラス、構造体、モジュール、インターフェイスにする必要があり、ソース ファイル、名前空間、プロシージャ、ブロックにすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

`Sub` プロシージャは、既定でパブリック アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。

プロシージャで `Implements` キーワードが使用されている場合、含まれているクラスまたは構造体には、その `Class` または `Structure` ステートメントの直後に `Implements` ステートメントが必要です。 `Implements` ステートメントには、`implementslist` で指定された各インターフェイスを含める必要があります。 ただし、インターフェイスで `Sub` を定義するときに使用する名前 (`definedname`) は、このプロシージャの名前 (`name`) に一致している必要はありません。

## <a name="returning-from-a-sub-procedure"></a>Sub プロシージャからの復帰

`Sub` プロシージャから呼び出し元のコードに返されると、実行は、それを呼び出したステートメントの後のステートメントから続行されます。

次の例は、`Sub` プロシージャからの戻り値を示しています。

```vb
Sub mySub(ByVal q As String)
    Return
End Sub
```

`Exit Sub` および `Return` ステートメントでは、`Sub` プロシージャがすぐに終了します。 任意の数の `Exit Sub` および `Return` ステートメントをプロシージャ内の任意の場所に記述でき、`Exit Sub` ステートメントと `Return` ステートメントを混在させることができます。

## <a name="calling-a-sub-procedure"></a>Sub プロシージャの呼び出し

`Sub` プロシージャを呼び出すには、ステートメントでプロシージャ名を使用し、その名前の後にかっこで囲んだ引数リストを指定します。 引数を指定しない場合のみ、かっこを省略できます。 ただし、常にかっこを含めると、コードが読みやすくなります。

`Sub` プロシージャと `Function` プロシージャは、パラメーターを持つことができ、一連のステートメントを実行できます。 ただし、`Function` プロシージャは値を返し、`Sub` プロシージャは返しません。 そのため、式の中で `Sub` プロシージャを使用することはできません。

`Sub` プロシージャを呼び出すときに `Call` キーワードを使用できますが、ほとんどの用途で、そのキーワードは推奨されません。 詳細については、「[Call ステートメント](call-statement.md)」を参照してください。

Visual Basic では、内部効率を高めるために算術式が再配置されることがあります。 そのため、引数リストに他のプロシージャを呼び出す式が含まれている場合は、それらの式が特定の順序で呼び出されることを前提としないでください。

## <a name="async-sub-procedures"></a>Async Sub プロシージャ

Async 機能を使用することによって、明示的なコールバックを使用せずに、または複数のメソッドやラムダ式にわたって手動でコードを分割することなく、非同期関数を呼び出すことができます。

プロシージャに [Async](../modifiers/async.md) 修飾子を付けると、そのプロシージャで [Await](../operators/await-operator.md) 演算子を使用できます。 制御が `Async` プロシージャの `Await` 式に到達すると、制御が呼び出し元に戻り、待機中のタスクが完了するまでプロシージャの進行が中断されます。 タスクが完了すると、プロシージャで実行を再開できます。

> [!NOTE]
> `Async` プロシージャは、まだ完了していない待機中の最初のオブジェクトが検出されるか、または `Async` プロシージャの最後に達するか、どちらか先に発生したときに、呼び出し元に戻ります。

また、`Async` 修飾子で、[Function ステートメント](function-statement.md)をマークすることもできます。 `Async` 関数の戻り値の型には、<xref:System.Threading.Tasks.Task%601> または <xref:System.Threading.Tasks.Task> を指定できます。 このトピックの後述の例では、<xref:System.Threading.Tasks.Task%601> の戻り値の型を持つ `Async` 関数を示します。

`Async` `Sub` プロシージャは、主にイベント ハンドラーで使用し、その場合、値を返すことはできません。 `Async` `Sub` プロシージャは待機できず、`Async` `Sub` プロシージャの呼び出し元では、`Sub` プロシージャがスローする例外をキャッチできません。

`Async` プロシージャでは、[ByRef](../modifiers/byref.md) パラメーターを宣言することはできません。

`Async` プロシージャの詳細については、「[Async および Await を使用した非同期プログラミング](../../programming-guide/concepts/async/index.md)」、「[非同期プログラムにおける制御フロー](../../programming-guide/concepts/async/control-flow-in-async-programs.md)」、「[非同期の戻り値の型](../../programming-guide/concepts/async/async-return-types.md)」を参照してください。

## <a name="example"></a>例

次の例では、`Sub` ステートメントを使用して、`Sub` プロシージャの本体を形成する名前、パラメーター、およびコードを定義しています。

[!code-vb[VbVbalrStatements#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#58)]

## <a name="example"></a>例

次の例で、`DelayAsync` は、戻り値の型が <xref:System.Threading.Tasks.Task%601> である `Async` `Function` です。 `DelayAsync` には、整数を返す `Return` ステートメントがあります。 そのため、`DelayAsync` の関数宣言では、戻り値の型を `Task(Of Integer)` とする必要があります。 戻り値の型が `Task(Of Integer)` であるため、ステートメント `Dim result As Integer = Await delayTask` に示すように、`DoSomethingAsync` 内の `Await` 式を評価すると、整数が生成されます。

`startButton_Click` プロシージャは、`Async Sub` プロシージャの一例です。 `DoSomethingAsync` が `Async` 関数であるため、ステートメント `Await DoSomethingAsync()` に示すように、`DoSomethingAsync` を呼び出すタスクは、待機させる必要があります。 `startButton_Click` `Sub` プロシージャは、`Await` 式を使用しているため、`Async` 修飾子を使用して定義する必要があります。

[!code-vb[csAsyncMethod#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncmethod/vb/mainwindow.xaml.vb#1)]

## <a name="see-also"></a>関連項目

- [Implements ステートメント](implements-statement.md)
- [Function ステートメント](function-statement.md)
- [パラメーター リスト](parameter-list.md)
- [Dim ステートメント](dim-statement.md)
- [Call ステートメント](call-statement.md)
- [Of](of-clause.md)
- [パラメーター配列](../../programming-guide/language-features/procedures/parameter-arrays.md)
- [方法: ジェネリック クラスを使用する](../../programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [プロシージャのトラブルシューティング](../../programming-guide/language-features/procedures/troubleshooting-procedures.md)
- [部分メソッド](../../programming-guide/language-features/procedures/partial-methods.md)
