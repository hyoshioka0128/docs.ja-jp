---
title: Mod 演算子
ms.date: 04/24/2018
f1_keywords:
- vb.Mod
helpviewer_keywords:
- remainder (Mod operator)
- division operator [Visual Basic], Mod operator
- modulus operator [Visual Basic], Visual Basic
- Mod operator [Visual Basic]
- operators [Visual Basic], division
- arithmetic operators [Visual Basic], Mod
- math operators [Visual Basic]
ms.assetid: 6ff7e40e-cec8-4c77-bff6-8ddd2791c25b
ms.openlocfilehash: 32065567799b023556a018ae2f5ba338796e0b49
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401512"
---
# <a name="mod-operator-visual-basic"></a>Mod 演算子 (Visual Basic)

2 つの数値を除算して剰余のみを返します。

## <a name="syntax"></a>構文

```vb
result = number1 Mod number2
```

## <a name="parts"></a>指定項目

`result` \
必須です。 任意の数値変数またはプロパティ。

`number1` \
必須です。 任意の数式。

`number2` \
必須です。 任意の数式。

## <a name="supported-types"></a>サポートされている型

すべての数値型。 これには、符号なしおよび浮動小数点の型と `Decimal` が含まれます。

## <a name="result"></a>結果

結果は、`number1` が `number2` で除算された後の剰余になります。 たとえば、式 `14 Mod 4` は 2 に評価されます。

> [!NOTE]
> 数学的には "*剰余 (remainder)* " と "*法 (modulus)* " には違いがあり、負数の場合の結果が異なります。 Visual Basic の `Mod` 演算子、.NET Framework の `op_Modulus` 演算子、基礎になる [rem](<xref:System.Reflection.Emit.OpCodes.Rem>) IL 命令ではすべて、剰余演算が実行されます。

`Mod` 演算の結果には被除数の符号 (`number1`) が保持されるため、結果は正または負になります。 結果は常に (-`number2`, `number2`) の範囲 (境界値は除外) になります。 次に例を示します。

```vb
Public Module Example
   Public Sub Main()
      Console.WriteLine($" 8 Mod  3 = {8 Mod 3}")
      Console.WriteLine($"-8 Mod  3 = {-8 Mod 3}")
      Console.WriteLine($" 8 Mod -3 = {8 Mod -3}")
      Console.WriteLine($"-8 Mod -3 = {-8 Mod -3}")
   End Sub
End Module
' The example displays the following output:
'       8 Mod  3 = 2
'      -8 Mod  3 = -2
'       8 Mod -3 = 2
'      -8 Mod -3 = -2
```

## <a name="remarks"></a>Remarks

`number1` または `number2` のいずれかが浮動小数点値の場合、除算の浮動小数点の剰余が返されます。 結果のデータ型は、`number1` と `number2` のデータ型による除算によって得られる可能性のあるすべての値を保持できる最小のデータ型です。

`number1` または `number2` が [Nothing](../nothing.md) に評価された場合は、0 として扱われます。

関連する演算子には、次のものがあります。

- [\ 演算子 (Visual Basic)](integer-division-operator.md) では、除算の整数の商が返されます。 たとえば、式 `14 \ 4` は 3 に評価されます。

- [/ 演算子 (Visual Basic)](floating-point-division-operator.md) では、剰余を含めた完全な商が浮動小数点数として返されます。 たとえば、式 `14 / 4` は 3.5 に評価されます。

## <a name="attempted-division-by-zero"></a>0 除算を試行した場合

`number2` がゼロに評価された場合、`Mod` 演算子の動作は、オペランドのデータ型によって異なります。

- 整数除算では、コンパイル時に `number2` を特定できない場合は <xref:System.DivideByZeroException> 例外がスローされ、コンパイル時に `number2` がゼロに評価された場合、コンパイル時エラー `BC30542 Division by zero occurred while evaluating this expression` が生成されます。
- 浮動小数点の除算では <xref:System.Double.NaN?displayProperty=nameWithType> が返されます。

## <a name="equivalent-formula"></a>同等の式

式 `a Mod b` は、次のいずれかの式と同等です。

`a - (b * (a \ b))`

`a - (b * Fix(a / b))`

## <a name="floating-point-imprecision"></a>浮動小数点の誤差

浮動小数点数を操作する場合、メモリ内で常に正確な 10 進数表現が使用されるとは限らないことに注意してください。 これにより、値の比較や `Mod` 演算子など、特定の演算によって、予期しない結果につながる可能性があります。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」を参照してください。

## <a name="overloading"></a>オーバーロード

`Mod` 演算子は "*オーバーロード*" できます。つまり、クラスまたは構造体がその動作を再定義できます。 コードによって、そのようなオーバーロードを含むクラスまたは構造体のインスタンスに `Mod` を適用する場合は、その再定義された動作を確実に理解しておいてください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。

## <a name="example"></a>例

次の例では、`Mod` 演算子を使用して 2 つの数値を除算し、剰余だけを返します。 どちらかの数値が浮動小数点数の場合、結果は剰余を表す浮動小数点数になります。

[!code-vb[VbVbalrOperators#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#31)]

## <a name="example"></a>例

次の例は、浮動小数点オペランドにおける誤差の可能性を示しています。 最初のステートメントでは、オペランドは `Double` であり、0.2 は、格納された値 0.20000000000000001 での無限に繰り返される 2 進小数です。 2 番目のステートメントでは、リテラル型の文字 `D` によって両方のオペランドが強制的に `Decimal` になり、0.2 には正確な表現が含まれます。

[!code-vb[VbVbalrOperators#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#32)]

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Conversion.Int%2A>
- <xref:Microsoft.VisualBasic.Conversion.Fix%2A>
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [トラブルシューティング (データ型)](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [\ 演算子 (Visual Basic)](integer-division-operator.md)
