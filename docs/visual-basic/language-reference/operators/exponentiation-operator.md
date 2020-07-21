---
title: ^ 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.^
helpviewer_keywords:
- raising numbers to powers
- ^ operator [Visual Basic], exponentiation
- square operator [Visual Basic]
- ^ operator [Visual Basic]
- exponentiation operator [Visual Basic]
- exponent
- numbers [Visual Basic], rasing
- powers
- arithmetic operators [Visual Basic], exponentiation
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
ms.openlocfilehash: e139becf74ae367266a23513e18d0bdbdd24cdea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371389"
---
# <a name="-operator-visual-basic"></a>^ 演算子 (Visual Basic)

一方の数値をもう一方の数値で累乗します。

## <a name="syntax"></a>構文

```vb
number ^ exponent
```

## <a name="parts"></a>指定項目

`number`\
必須です。 任意の数式。

`exponent`\
必須です。 任意の数式。

## <a name="result"></a>結果

結果は、`number` を `exponent` で累乗したもので、常に `Double` 値になります。

## <a name="supported-types"></a>サポートされている型

`Double`。 異なる型のオペランドはすべて `Double` に変換されます。

## <a name="remarks"></a>Remarks

Visual Basic では、常に [Double データ型](../data-types/double-data-type.md)で指数演算が実行されます。

`exponent` の値には、小数、負、またはその両方を指定できます。

1 つの式で複数の累乗が実行される場合、`^` 演算子は左から右の出現順に評価されます。

> [!NOTE]
> `^` 演算子は "*オーバーロード*" できます。つまり、オペランドの型がそのクラスまたは構造体であるとき、そのクラスまたは構造体でその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。

## <a name="example"></a>例

次の例では、`^` 演算子を使用して数値を指数で累乗します。 結果は、最初のオペランドを 2 番目のオペランドで累乗したものになります。

[!code-vb[VbVbalrOperators#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#20)]

前の例を実行すると、次の結果が得られます。

`exp1` は 4 (2 の 2 乗) に設定されます。

`exp2` は 19683 (3 を 3 乗してから、その値を 3 乗) に設定されます。

`exp3` は -125 (-5 の 3 乗) に設定されます。

`exp4` は 625 (-5 の 4 乗) に設定されます。

`exp5` は 2 (8 の立方根) に設定されます。

`exp6` は 0.5 (1.0 を 8 の立方根で除算) に設定されます。

上の例の式におけるかっこの重要性に注意してください。 "*演算子の優先順位*" のため、Visual Basic では、通常は `^` 演算子が、他の演算子 (単項演算子 `–` であっても) よりも前に実行されます。 `exp4` と `exp6` がかっこなしで計算された場合、次のような結果になります。

`exp4 = -5 ^ 4` は -(5 の 4 乗) として計算されるため、結果は -625 になります。

`exp6 = 8 ^ -1.0 / 3.0` は (8 の -1 乗、つまり 0.125) を 3.0 で除算として計算されるため、結果は 0.041666666666666666666666666666667 になります。

## <a name="see-also"></a>関連項目

- [^= 演算子](exponentiation-assignment-operator.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
