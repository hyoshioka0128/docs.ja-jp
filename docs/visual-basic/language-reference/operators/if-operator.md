---
title: If 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.IfOperator
- IfOperator
helpviewer_keywords:
- ternary operators [Visual Basic]
- conditional execution
- If expressions [Visual Basic]
- conditional operator [Visual Basic]
- If Operator [Visual Basic]
ms.assetid: dd56c9df-7cd4-442c-9ba6-20c70ee44c8f
ms.openlocfilehash: 28fb2afb2c4cf78ffbbb028145de647a8dc512ed
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371104"
---
# <a name="if-operator-visual-basic"></a>If 演算子 (Visual Basic)

ショートサーキット評価を使用して、条件に応じて 2 つの値のいずれかを返します。 `If` 演算子は、3 つの引数または 2 つの引数を指定して呼び出すことができます。

## <a name="syntax"></a>構文

```vb
If( [argument1,] argument2, argument3 )
```

## <a name="if-operator-called-with-three-arguments"></a>3 つの引数を指定して If 演算子を呼び出す場合

3 つの引数を使用して `If` を呼び出す場合、最初の引数は `Boolean` としてキャストできる値に評価される必要があります。 この `Boolean` 値によって、他の 2 つの引数のうち、どちらが評価されて返されるかが決まります。 次の一覧は、3 つの引数を使用して `If` 演算子を呼び出す場合にのみ適用されます。

### <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`argument1`|必須です。 `Boolean`。 他のどの引数を評価して返すかを決定します。|
|`argument2`|必須です。 `Object`。 `argument1` が `True` に評価された場合に、評価されて返されます。|
|`argument3`|必須です。 `Object`。 `argument1` が `False` に評価された場合、または `argument1` が [Nothing](../nothing.md) に評価された [null 許容](../../programming-guide/language-features/data-types/nullable-value-types.md)`Boolean` 変数である場合に、評価されて返されます。|

3 つの引数を指定して呼び出される `If` 演算子は、ショートサーキット評価を使用する点を除き、`IIf` 関数と同様に機能します。 `IIf` 関数では常に、その 3 つの引数がすべて評価されます。それに対し、3 つの引数を持つ `If` 演算子では、そのうちの 2 つだけが評価されます。 最初の `If` 引数が評価され、結果が `Boolean` 値 (`True` または `False`) としてキャストされます。 値が `True` の場合、`argument2` が評価され、その値が返されますが、`argument3` は評価されません。 `Boolean` 式の値が `False` の場合、`argument3` が評価され、その値が返されますが、`argument2` は評価されません。 次の例では、3 つの引数が使用されている場合の `If` の使用法を示しています。

[!code-vb[VbVbalrOperators#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#100)]

次の例は、ショートサーキット評価の値を示しています。 この例では、変数 `divisor` による変数 `number` の除算が 2 回試行されていることを示しています。これは `divisor` がゼロの場合以外に行われます。 該当する場合は 0 が返されます。また、実行時エラーが発生するため、除算を実行しようとしないでください。 `If` 式ではショートサーキット評価が使用されるため、最初の引数の値に応じて、2 番目または 3 番目の引数のいずれかが評価されます。 最初の引数が true の場合、除数はゼロではなく、2 番目の引数を評価して除算を実行しても問題はありません。 最初の引数が false の場合、3 番目の引数のみが評価され、0 が返されます。 したがって、除数が 0 の場合、除算の実行は試みられず、エラーも発生しません。 ただし、`IIf` ではショートサーキット評価が使用されないため、最初の引数が false の場合でも 2 番目の引数が評価されます。 これにより、実行時の 0 除算エラーが発生します。

[!code-vb[VbVbalrOperators#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#101)]

## <a name="if-operator-called-with-two-arguments"></a>2 つの引数を指定して If 演算子を呼び出す場合

`If` の最初の引数は省略できます。 これにより、2 つの引数のみを使用してこの演算子を呼び出すことができます。 次の一覧は、2 つの引数を使用して `If` 演算子を呼び出す場合にのみ適用されます。

### <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`argument2`|必須です。 `Object`。 参照または null 許容値型でなければなりません。 `Nothing` 以外に評価される場合、評価され、返されます。|
|`argument3`|必須です。 `Object`。 `argument2` が `Nothing` に評価された場合に、評価されて返されます。|

`Boolean` 引数が省略された場合、最初の引数は参照または null 許容値型でなければなりません。 最初の引数が `Nothing` に評価された場合は、2 番目の引数の値が返されます。 その他すべての場合、最初の引数の値が返されます。 次の例は、この評価のしくみを示しています。

[!code-vb[VbVbalrOperators#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#102)]

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.IIf%2A>
- [null 許容値型](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [Nothing](../nothing.md)
