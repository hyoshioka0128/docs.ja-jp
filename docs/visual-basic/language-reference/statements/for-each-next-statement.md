---
title: For Each...Next ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.ForEach
- vb.ForEachNext
- vb.Each
- ForEachNext
helpviewer_keywords:
- infinite loops
- Next statement [Visual Basic], For Each...Next
- endless loops
- loop structures [Visual Basic], For Each...Next
- loops, endless
- Each keyword [Visual Basic]
- instructions, repeating
- For Each statement [Visual Basic]
- collections, instruction repetition
- loops, infinite
- For Each...Next statements
- For keyword [Visual Basic], For Each...Next statements
- Exit statement [Visual Basic], For Each...Next statements
- iteration
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
ms.openlocfilehash: 0feb938121a97b06509b472652e6a753841ab2b8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404655"
---
# <a name="for-eachnext-statement-visual-basic"></a>For Each...Next ステートメント (Visual Basic)

コレクション内の要素ごとにステートメントのグループを繰り返します。

## <a name="syntax"></a>構文

```vb
For Each element [ As datatype ] In group
    [ statements ]
    [ Continue For ]
    [ statements ]
    [ Exit For ]
    [ statements ]
Next [ element ]
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`element`|`For Each` ステートメントには必ず指定します。 `Next` ステートメントでは省略可能です。 変数。 コレクションの要素の反復処理に使用されます。|
|`datatype`|[`Option Infer`](option-infer-statement.md) がオン (既定値) または `element` が既に宣言されている場合は省略可能です。`Option Infer` がオフで `element` がまだ宣言されていない場合は必須です。 `element`のデータ型。|
|`group`|必須です。 コレクション型または Object である型を持つ変数。 `statements` が繰り返されるコレクションを参照します。|
|`statements`|任意。 `group` の各項目に対して実行される、`For Each` と `Next` の間の 1 つ以上のステートメント。|
|`Continue For`|任意。 `For Each` ループの先頭に制御を移します。|
|`Exit For`|任意。 `For Each` ループから制御を移します。|
|`Next`|必須です。 `For Each` ループの定義を終了します。|

## <a name="simple-example"></a>簡単な例

コレクションまたは配列の要素ごとに一連のステートメントを繰り返す場合は、`For Each`...`Next` ループを使用します。

> [!TIP]
> [For...Next ステートメント](for-next-statement.md) は、ループの各反復を制御変数に関連付けて、その変数の初期値と最終値を決定できる場合に適しています。 ただし、コレクションを処理する場合、初期値と最終値の概念は意味がなく、コレクションに含まれる要素の数がわかるとは限りません。 このような場合は、`For Each`...`Next` ループの方が適していることがよくあります。

次の例では、`For Each`...`Next` ステートメントは、リスト コレクションのすべての要素を反復処理します。

[!code-vb[VbVbalrStatements#121](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#121)]

その他の例については、[コレクション](../../../standard/collections/index.md)および[配列](../../programming-guide/language-features/arrays/index.md)に関するページを参照してください。

## <a name="nested-loops"></a>Nested Loops

`For Each` ループを入れ子にするには、別のループ内にループを配置します。

次の例は、入れ子になった `For Each`...`Next` 構造を示しています。

[!code-vb[VbVbalrStatements#122](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#122)]

ループを入れ子にする場合、各ループには一意の `element` 変数が必要です。

また、さまざまな種類の制御構造を相互に入れ子にすることもできます。 詳細については、「[入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)」を参照してください。

## <a name="exit-for-and-continue-for"></a>Exit For と Continue For

[Exit For](exit-statement.md) ステートメントは、実行により `For`...`Next` ループを終了し、`Next` ステートメントの次のステートメントに制御を移します。

`Continue For` ステートメントは、ループの次の反復に直ちに制御を移します。 詳細については、「[Continue ステートメント](continue-statement.md)」を参照してください。

`Continue For` および `Exit For` ステートメントを使用する方法の例を次に示します。

[!code-vb[VbVbalrStatements#123](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#123)]

`For Each` ループには、任意の数の `Exit For` ステートメントを配置できます。 入れ子になった `For Each` ループ内で使用すると、`Exit For` は、実行により最も内側のループを終了し、次に高いレベルの入れ子に制御を移します。

`Exit For` は、何らかの条件 (たとえば、`If`...`Then`...`Else` 構造の場合など) を評価した後によく使用されます。 `Exit For` は次の条件で使用することもできます。

- 反復処理の続行が不要または不可能である。 これは、正しくない値または終了要求によって生じる場合があります。

- `Try`...`Catch`...`Finally` で例外がキャッチされる。`Finally` ブロックの末尾で `Exit For` を使用することもできます。

- 無限ループがある。無限ループは、膨大な回数または無限に実行されるループです。 このような条件を検出した場合は、`Exit For` を使用してループをエスケープできます。 詳細については、「[Do...Loop ステートメント](do-loop-statement.md)」を参照してください。

## <a name="iterators"></a>Iterators

*反復子*は、コレクションに対するカスタムの反復処理を実行するために使用します。 反復子は、関数または `Get` アクセサーのいずれかです。 これは、`Yield` ステートメントを使用して、コレクションの各要素を 1 回に 1 つ返します。

`For Each...Next` ステートメントを使用して、反復子を呼び出します。 `For Each` ループの各イテレーションは、反復子を呼び出します。 `Yield` ステートメントが反復子に到達すると、`Yield` ステートメント内の式が返され、コードの現在の位置が保持されます。 次回、反復子が呼び出されると、この位置から実行が再開されます。

次の例は、iterator 関数を使用します。 iterator 関数には、[For…Next](for-next-statement.md) ループ内に `Yield` ステートメントがあります。 `ListEvenNumbers` メソッドでは、`For Each` ステートメント本文の各反復で iterator 関数が呼び出され、これが次の `Yield` ステートメントに続行されます。

[!code-vb[VbVbalrStatements#127](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#127)]

詳細については、「[反復子](../../programming-guide/concepts/iterators.md)」、「[Yield ステートメント](yield-statement.md)」、および「[Iterator](../modifiers/iterator.md)」を参照してください。

## <a name="technical-implementation"></a>技術的な実装

`For Each`…`Next` ステートメントを実行すると、ループが開始される前に、Visual Basic によってコレクションが 1 回だけ評価されます。 ステートメント ブロックで `element` または `group` が変更された場合、これらの変更はループの繰り返しに影響しません。

コレクション内のすべての要素が連続して `element` に割り当てられている場合、`For Each` ループは停止し、制御は `Next` ステートメントの次のステートメントに移ります。

[Option Infer](option-infer-statement.md) がオン (既定の設定) の場合、Visual Basic コンパイラはデータ型 `element` を推測できます。 オフで、`element` がループの外側で宣言されていない場合は、`For Each` ステートメントで宣言する必要があります。 データ型 `element` を明示的に宣言するには、`As` 句を使用します。 要素のデータ型が `For Each`...`Next` コンストラクトの外側で定義されている場合を除き、そのスコープはループの本体です。 `element` をループの内側と外側の両方で宣言することはできないことに注意してください。

必要であれば、`Next` ステートメントに `element` を指定することもできます。 これを使用すると、特に `For Each` ループを入れ子にした場合に、プログラムの読みやすさが向上します。 対応する `For Each` ステートメントに存在するものと同じ変数を指定する必要があります。

ループ内の `element` の値を変更しないようにすることもできます。 これにより、コードの読み取りとデバッグが困難になる可能性があります。 `group` の値を変更しても、ループが最初に入力されたときに決定されたコレクションまたはその要素には影響しません。

ループを入れ子にするときに、外側の入れ子レベルの `Next` ステートメントが内側のレベルの `Next` より前に検出された場合、コンパイラはエラーを通知します。 ただし、コンパイラは、すべての `Next` ステートメントで `element` を指定した場合にのみ、この重複エラーを検出できます。

コードが特定の順序でのコレクションの走査に依存している場合は、コレクションが公開する列挙子オブジェクトの特性がわかっていない限り、`For Each`...`Next` ループは最適な選択ではありません。 走査の順序は Visual Basic によって決定されるのではなく、列挙子オブジェクトの <xref:System.Collections.IEnumerator.MoveNext%2A> メソッドによって決定されます。 したがって、コレクションのどの要素が `element` で最初に返されるか、またはどれが指定された要素の後に返される次の要素であるかを、予測できない場合があります。 `For`...`Next` や `Do`...`Loop` などの別のループ構造を使用すると、より信頼性の高い結果を得られる場合があります。

ランタイムは、`group` 内の要素を `element` に変換できる必要があります。 [`Option Strict`] ステートメントは、拡大変換と縮小変換の両方を許可するかどうか (`Option Strict` がオフ、既定値)、または拡大変換のみを許可するかどうか (`Option Strict` がオン) を制御します。 詳細については、「[縮小変換](#narrowing-conversions)」を参照してください。

データ型 `group` は、列挙可能なコレクションまたは配列を参照する参照型である必要があります。 ほとんどの場合、これは、`group` が `System.Collections` 名前空間の <xref:System.Collections.IEnumerable> インターフェイスまたは `System.Collections.Generic` 名前空間の <xref:System.Collections.Generic.IEnumerable%601> インターフェイスを実装するオブジェクトを参照することを意味します。 `System.Collections.IEnumerable` は、コレクションの列挙子オブジェクトを返す <xref:System.Collections.IEnumerable.GetEnumerator%2A> メソッドを定義します。 列挙子オブジェクトは、`System.Collections` 名前空間の `System.Collections.IEnumerator` インターフェイスを実装し、<xref:System.Collections.IEnumerator.Current%2A> プロパティと <xref:System.Collections.IEnumerator.Reset%2A> および <xref:System.Collections.IEnumerator.MoveNext%2A> メソッドを公開します。 Visual Basic では、これらを使用してコレクションを走査します。

### <a name="narrowing-conversions"></a>縮小変換

`Option Strict` が `On` に設定されている場合、縮小変換では、通常はコンパイラ エラーが発生します。 ただし、`For Each` ステートメントでは、`group` 内の要素から `element` への変換は実行時に評価されて実行され、縮小変換によって発生するコンパイラ エラーは抑制されます。

次の例では、`n` の初期値としての `m` の割り当ては、`Option Strict` がオンのときにはコンパイルされません。これは、`Long` から `Integer` への変換が縮小変換であるためです。 ただし、`For Each` ステートメントでは、`number` への割り当てに `Long` から `Integer` への変換が必要な場合でも、コンパイラ エラーは報告されません。 多数の数値が含まれている `For Each` ステートメントでは、<xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A> が大きい数値に適用されると実行時エラーが発生します。

[!code-vb[VbVbalrStatements#89](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class3.vb#89)]

### <a name="ienumerator-calls"></a>IEnumerator 呼び出し

`For Each`...`Next` ループの実行が開始されると、Visual Basic で、`group` が有効なコレクション オブジェクトを参照していることが検証されます。 そうでない場合は、例外がスローされます。 それ以外の場合は、列挙子オブジェクトの <xref:System.Collections.IEnumerator.MoveNext%2A> メソッドと <xref:System.Collections.IEnumerator.Current%2A> プロパティが呼び出されて、最初の要素が返されます。 `MoveNext` が次の要素がないことを示している場合 (つまり、コレクションが空の場合)、`For Each` ループは停止し、制御は `Next` ステートメントの次のステートメントに移ります。 それ以外の場合は、Visual Basic で、最初の要素に `element` が設定され、ステートメント ブロックが実行されます。

Visual Basic は、`Next` ステートメントを検出するたびに、`For Each` ステートメントに返します。 もう一度 `MoveNext` と `Current` を呼び出して次の要素を返し、その結果に応じて、もう一度ブロックを実行するかループを停止します。 このプロセスは、`MoveNext` で次の要素が存在しないことを示すか、`Exit For` ステートメントが検出されるまで続行されます。

**コレクションの変更。** <xref:System.Collections.IEnumerable.GetEnumerator%2A> によって返される列挙子オブジェクトでは、通常、要素の追加、削除、置換、または並べ替えによってコレクションを変更することはできません。 `For Each`...`Next` ループを開始した後にコレクションを変更した場合、列挙子オブジェクトは無効になり、次に要素にアクセスしようとすると <xref:System.InvalidOperationException> 例外が発生します。

ただし、この変更のブロックは、Visual Basic によってではなく、<xref:System.Collections.IEnumerable> インターフェイスの実装によって決まります。 反復中の変更を許可する方法で `IEnumerable` を実装することができます。 このような動的な変更を検討している場合は、使用しているコレクションでの `IEnumerable` 実装の特性を理解しておいてください。

**コレクションの要素の変更。** 列挙子オブジェクトの <xref:System.Collections.IEnumerator.Current%2A> プロパティは [ReadOnly](../modifiers/readonly.md) であり、各コレクション要素のローカル コピーを返します。 つまり、`For Each`...`Next` ループで要素自体を変更することはできません。 行った変更は、`Current` からのローカル コピーにのみ適用され、基になるコレクションには反映されません。 ただし、要素が参照型の場合は、その要素が指すインスタンスのメンバーを変更できます。 次の例では、各 `thisControl` 要素の `BackColor` メンバーを変更します。 ただし、`thisControl` 自体を変更することはできません。

```vb
Sub LightBlueBackground(thisForm As System.Windows.Forms.Form)
    For Each thisControl In thisForm.Controls
        thisControl.BackColor = System.Drawing.Color.LightBlue
    Next thisControl
End Sub
```

前の例では、各 `thisControl` 要素の `BackColor` メンバーを変更できますが、`thisControl` 自体を変更することはできません。

**配列の走査。** <xref:System.Array> クラスは <xref:System.Collections.IEnumerable> インターフェイスを実装するため、すべての配列は <xref:System.Array.GetEnumerator%2A> メソッドを公開します。 これは、`For Each`...`Next` ループを含む配列を反復処理できることを意味します。 ただし、読み取ることができるのは配列要素だけです。 これらを変更することはできません。

## <a name="example"></a>例

次の例では、<xref:System.IO.DirectoryInfo> クラスを使用して、C:\ ディレクトリにあるすべてのフォルダーを一覧表示します。

[!code-vb[VbVbalrStatements#124](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#124)]

## <a name="example"></a>例

次の例では、コレクションを並べ替えるための手順を示しています。 この例は、<xref:System.Collections.Generic.List%601> に格納されている `Car` クラスのインスタンスの並べ替えを実行します。 `Car` クラスは、<xref:System.IComparable%601> のメソッドの実装を必要とする <xref:System.IComparable%601.CompareTo%2A> インターフェイスを実装します。

<xref:System.IComparable%601.CompareTo%2A> メソッドに対する各呼び出しは、並べ替えに使用される単一の比較を実行します。 `CompareTo` メソッドのユーザーが作成したコードは、現在のオブジェクトと別のオブジェクトとの各比較の値を戻します。 現在のオブジェクトが別のオブジェクトよりも小さい場合はゼロ未満の値を、大きい場合はゼロ以上の値を、等しい場合はゼロを戻します。 これによって、より大きい、より小さい、等しい、の条件をコードに定義することができます。

`ListCars` のメソッドでは、`cars.Sort()` ステートメントがリストを並べ替えます。 <xref:System.Collections.Generic.List%601.Sort%2A> の <xref:System.Collections.Generic.List%601> メソッドへの呼び出しによって、`CompareTo` メソッドは `Car` 内の `List` オブジェクトに自動的に呼び出されます。

[!code-vb[VbVbalrStatements#125](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#125)]

## <a name="see-also"></a>関連項目

- [コレクション](../../../standard/collections/index.md)
- [For...Next ステートメント](for-next-statement.md)
- [ループ構造](../../programming-guide/language-features/control-flow/loop-structures.md)
- [While...End While ステートメント](while-end-while-statement.md)
- [Do...Loop ステートメント](do-loop-statement.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [オブジェクト初期化子: 名前付きの型と匿名型](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [コレクション初期化子](../../programming-guide/language-features/collection-initializers/index.md)
- [配列](../../programming-guide/language-features/arrays/index.md)
