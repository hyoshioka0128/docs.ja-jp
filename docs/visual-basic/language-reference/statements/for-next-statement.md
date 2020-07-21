---
title: For...Next ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Step
- vb.Next
- vb.To
- vb.for
helpviewer_keywords:
- infinite loops
- Next keyword [Visual Basic], For...Next statements
- For keyword [Visual Basic], For...Next statements
- Step keyword [Visual Basic], For...Next statements
- operator overloading, For...Next statement
- To keyword [Visual Basic], For...Next statements
- endless loops
- loops, endless
- instructions, repeating
- Next statement [Visual Basic], For...Next
- For...Next statements
- loop structures [Visual Basic], For...Next
- loops, infinite
- Exit statement [Visual Basic], For...Next statements
- For statement [Visual Basic]
ms.assetid: f5fc0d51-67ce-4c36-9f09-31c9a91c94e9
ms.openlocfilehash: 6896c6cfb4ec5d6207011e56b72639c459120e53
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404642"
---
# <a name="fornext-statement-visual-basic"></a>For...Next ステートメント (Visual Basic)

ステートメントのグループを指定した回数だけ繰り返します。

## <a name="syntax"></a>構文

```vb
For counter [ As datatype ] = start To end [ Step step ]
    [ statements ]
    [ Continue For ]
    [ statements ]
    [ Exit For ]
    [ statements ]
Next [ counter ]
```

## <a name="parts"></a>指定項目

|パーツ|説明|
|----------|-----------------|
|`counter`|`For` ステートメントには必ず指定します。 数値変数。 ループの制御変数。 詳細については、このトピックで後述する「[Counter 引数](#BKMK_Counter)」を参照してください。|
|`datatype`|任意。 `counter` のデータ型。 詳細については、このトピックで後述する「[Counter 引数](#BKMK_Counter)」を参照してください。|
|`start`|必須です。 数値式。 `counter` の初期値になります。|
|`end`|必須です。 数値式。 `counter` の最終値。|
|`step`|任意。 数値式。 ループを通るたびに `counter` が増分される量。|
|`statements`|任意。 指定した回数だけ実行される、`For` と `Next` の間の 1 つ以上のステートメント。|
|`Continue For`|任意。 ループの次の反復に制御を移します。|
|`Exit For`|任意。 `For` ループから制御を移します。|
|`Next`|必須です。 `For` ループの定義を終了します。|

> [!NOTE]
> このステートメントで `To` キーワードを使用して、カウンターの範囲を指定します。 また、このキーワードは、[Select...Case ステートメント](select-case-statement.md)と配列宣言でも使用できます。 配列宣言の詳細については、「[Dim ステートメント](dim-statement.md)」を参照してください。

## <a name="simple-examples"></a>簡単な例

一連のステートメントを設定した回数だけ繰り返す場合は、`For`...`Next` 構造を使用します。

次の例では、`index` 変数は値 1 で始まり、ループの反復ごとに増分され、`index` の値が 5 に達した後に終了します。

[!code-vb[VbVbalrStatements#111](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#111)]

次の例では、`number` 変数は 2 から始まり、ループの反復ごとに 0.25 減り、`number` の値が 0 に達した後に終了します。 `-.25` の `Step` 引数は、ループの反復ごとに値を 0.25 ずつ減らします。

[!code-vb[VbVbalrStatements#112](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#112)]

> [!TIP]
> [While...End While ステートメント](while-end-while-statement.md)または [Do...Loop ステートメント](do-loop-statement.md)は、ループ内でステートメントを実行する回数が事前にわからない場合に適しています。 ただし、ループを特定の回数だけ実行する場合は、`For`...`Next` ループを使用することをお勧めします。 ループに最初に入るときの反復の数を決定します。

## <a name="nesting-loops"></a>ループを入れ子にする

`For` ループを入れ子にするには、別のループ内にループを配置します。 次の例は、異なるステップ値を持つ入れ子になった `For`...`Next` 構造を示しています。 外側のループは、ループの反復ごとに文字列を作成します。 内側のループは、ループの反復ごとにループ カウンター変数の値を減らします。

[!code-vb[VbVbalrStatements#113](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#113)]

ループを入れ子にする場合、各ループには一意の `counter` 変数が必要です。

また、さまざまな種類の制御構造を相互に入れ子にすることもできます。 詳細については、「[入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)」を参照してください。

## <a name="exit-for-and-continue-for"></a>Exit For と Continue For

`Exit For` ステートメントは、`For`...`Next` ループを終了し、`Next` ステートメントの次のステートメントに制御を移します。

`Continue For` ステートメントは、ループの次の反復に直ちに制御を移します。 詳細については、「[Continue ステートメント](continue-statement.md)」を参照してください。

次の例では、`Continue For` および `Exit For` ステートメントの使用方法を示します。

[!code-vb[VbVbalrStatements#115](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#115)]

`For`...`Next` ループには、任意の数の `Exit For` ステートメントを 含めることができます。 入れ子になった `For`...`Next` ループ内で使用すると、 `Exit For` は、最も内側のループを終了し、次に高いレベルの入れ子に制御を移します。

`Exit For` は、何らかの条件 (たとえば、`If`...`Then`...`Else` 構造など) を評価した後によく使用されます。 `Exit For` は次の条件で使用することもできます。

- 反復処理の続行が不要または不可能である。 この条件は、正しくない値または終了要求によって生じる場合があります。

- `Try`...`Catch`...`Finally` ステートメントが例外をキャッチする。 `Exit For` ブロックの末尾で `Finally` を使用することもできます。

- 無限ループがある。無限ループは、膨大な回数または無限に実行されるループです。 このような条件を検出した場合は、`Exit For` を使用してループをエスケープできます。 詳細については、「[Do...Loop ステートメント](do-loop-statement.md)」を参照してください。

## <a name="technical-implementation"></a>技術的な実装

`For`...`Next` ループが開始されると、Visual Basic は `start`、`end`、および `step` を評価します。 Visual Basic は、現時点ではこれらの値のみを評価してから、`start` を `counter` に割り当てます。 ステートメント ブロックが実行される前に、Visual Basic は `counter` と `end` を比較します。 `counter` が既に `end` の値よりも大きい場合 (または `step` が負の場合)、`For` ループは終了し、制御は `Next` ステートメントの次のステートメントに渡されます。 それ以外の場合は、ステートメント ブロックが実行されます。

Visual Basic は、`Next` ステートメントを検出するたびに `counter` を `step` ずつ増分し、`For` ステートメントに返します。 もう一度 `counter` と `end` を比較し、その結果に応じて、もう一度ブロックを実行するかループを終了します。 このプロセスは、`counter` が `end` を渡すか、`Exit For` ステートメントが検出されるまで続行されます。

`counter` が `end` を渡すまで、ループは停止しません。 `counter` が `end` に等しい場合、ループは続行されます。 ブロックを実行するかどうかを決定する比較は、`step` が正の場合は `counter` <= `end`、`counter` が負の場合は  >= `end``step` です。

ループ内にあるときに `counter` の値を変更すると、コードの読み取りやデバッグが困難になることがあります。 `start`、`end`、または `step` の値を変更しても、ループが最初に入力されたときに決定された反復値には影響しません。

ループを入れ子にした場合、内側のレベルの `Next` ステートメントの前に外側の入れ子レベルの `Next` ステートメントが検出されると、コンパイラはエラーを通知します。 ただし、コンパイラは、すべての `Next` ステートメントで `counter` を指定した場合にのみ、この重複エラーを検出できます。

### <a name="step-argument"></a>Step 引数

`step` の値には、正または負のどちらかを指定できます。 このパラメーターは、次の表に従ってループ処理を決定します。

|**ステップ値**|**ループが実行される場合**|
|--------------------|--------------------------|
|正または 0|`counter` <= `end`|
|負|`counter` >= `end`|

`step` の既定値は 1 です。

### <a name="counter-argument"></a><a name="BKMK_Counter"></a> Counter 引数

次の表は、`counter` が `For…Next` ループ全体に範囲が設定されている新しいローカル変数を定義するかどうかを示しています。 この決定は、`datatype` が存在するかどうかと、`counter` が既に定義されているかどうかによって異なります。

|`datatype` が存在する|`counter` が既に定義されている|結果 (`counter` が `For...Next` ループ全体にスコープ設定されている新しいローカル変数を定義するかどうか)|
|----------------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------|
|いいえ|はい|いいえ。`counter` が既に定義されているため。 `counter` のスコープがプロシージャに対してローカルでない場合は、コンパイル時の警告が発生します。|
|いいえ|いいえ|はい。 データ型は、`start`、`end`、および `step` 式から推論されます。 型の推定については、「[Option Infer ステートメント](option-infer-statement.md)」と「[ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)」を参照してください。|
|はい|はい|はい。ただし、既存の `counter` 変数がプロシージャの外側で定義されている場合に限ります。 この変数は個別に保持されます。 既存の `counter` 変数のスコープがプロシージャに対してローカルである場合は、コンパイル時エラーが発生します。|
|はい|いいえ|はい。|

`counter` のデータ型によって、反復の種類が決定されます。これは、次のいずれかの型である必要があります。

- `Byte`、`SByte`、`UShort`、`Short`、`UInteger`、`Integer`、`ULong`、`Long`、`Decimal`、`Single`、または `Double`。

- [Enum ステートメント](enum-statement.md)を使用して宣言する列挙型。

- `Object`。

- 次の演算子を持つ型 `T`。ここで、`B` は `Boolean` 式で使用できる型です。

  `Public Shared Operator >= (op1 As T, op2 As T) As B`

  `Public Shared Operator <= (op1 As T, op2 As T) As B`

  `Public Shared Operator - (op1 As T, op2 As T) As T`

  `Public Shared Operator + (op1 As T, op2 As T) As T`

必要であれば、`Next` ステートメントに `counter` 変数を指定することもできます。 この構文を使用すると、特に `For` ループを入れ子にした場合に、プログラムの読みやすさが向上します。 対応する `For` ステートメントに存在する変数を指定する必要があります。

`start`、`end`、および `step` 式は、型 `counter` に拡大変換される任意のデータ型に評価できます。 `counter` にユーザー定義型を使用する場合は、型 `start`、`end`、または `step` を型 `counter` に変換するために `CType` 変換演算子を定義することが必要になる場合があります。

## <a name="example"></a>例

次の例では、ジェネリック リストからすべての要素を削除します。 [For Each...Next ステートメント](for-each-next-statement.md)の代わりに、この例では、降順で反復する `For`...`Next` ステートメントを示しています。 `removeAt` メソッドを実行すると、削除された要素の後にある各要素のインデックス値が小さくなるため、この例ではこの手法を使用しています。

[!code-vb[VbVbalrStatements#114](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#114)]

## <a name="example"></a>例

次の例では、[Enum ステートメント](enum-statement.md)を使用して宣言された列挙型を反復処理します。

[!code-vb[VbVbalrStatements#116](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#116)]

## <a name="example"></a>例

次の例では、ステートメントのパラメーターは、`+`、`-`、`>=`、および `<=` の各演算子に対して演算子のオーバーロードがあるクラスを使用しています。

[!code-vb[VbVbalrStatements#117](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class7.vb#117)]

## <a name="see-also"></a>関連項目

- <xref:System.Collections.Generic.List%601>
- [ループ構造](../../programming-guide/language-features/control-flow/loop-structures.md)
- [While...End While ステートメント](while-end-while-statement.md)
- [Do...Loop ステートメント](do-loop-statement.md)
- [入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit ステートメント](exit-statement.md)
- [コレクション](../../programming-guide/concepts/collections.md)
