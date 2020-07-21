---
title: 10 進型 (Decimal)
ms.date: 07/20/2015
f1_keywords:
- vb.Decimal
helpviewer_keywords:
- literal type characters [Visual Basic], D
- trailing zeros
- real numbers
- trailing 0 characters [Visual Basic]
- Decimal data type
- D literal type character [Visual Basic]
- decimals, Decimal data type
- 0 characters [Visual Basic], trailing
- data types [Visual Basic], assigning
- decimal keyword [Visual Basic]
- numbers [Visual Basic], real
- variable-precision numbers
- zeros, trailing
- '@ identifier type character'
- identifier type characters [Visual Basic], @
ms.assetid: 1d855b45-afe2-45b0-a623-96b6f63a43d5
ms.openlocfilehash: 690c8061b6df1115aa24668520170b44edfa8287
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415648"
---
# <a name="decimal-data-type-visual-basic"></a>10 進型 (Decimal) (Visual Basic)

可変の 10 の累乗によってスケーリングされた 96 ビット (12 バイト) 整数値を表す符号付き 128 ビット (16 バイト) 値を保持します。 スケール ファクターは小数点以下の桁数を指定し、0 から 28 の範囲になります。 0 のスケール (小数点以下の桁数なし) では、有効な最大値は +/-79,228,162,514,264,337,593,543,950,335 (+/-7.9228162514264337593543950335E+28) です。 28 桁の小数点以下の桁数では、最大値は +/-7.9228162514264337593543950335 で、0 以外の最小値は +/-0.0000000000000000000000000001 (+/-1E-28) になります。

## <a name="remarks"></a>Remarks

`Decimal` データ型は、数値の最大有効桁数を提供します。 最大 29 桁の有効桁数をサポートし、7.9228 x 10^28 を超える値を表すことができます。 これは、多くの桁数を必要とするが丸め誤差を許容できない財務などの計算に特に適しています。

`Decimal` の既定値は 0 です。

## <a name="programming-tips"></a>プログラミングのヒント

- **精度。** `Decimal` は浮動小数点データ型ではありません。 `Decimal` 構造体は、2 進数の整数値を保持します。符号ビットと、値のどの部分が小数であるかを指定する整数のスケーリング ファクターです。 このため、`Decimal` の数値は、浮動小数点型 (`Single` と `Double`) よりもメモリ内でより正確に表現されます。

- **パフォーマンス。** `Decimal` データ型は、すべての数値型の中で最も低速です。 データ型を選択する前に、精度の重要性をパフォーマンスに照らして検討する必要があります。

- **拡大変換。** `Decimal` データ型は、`Single` または `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `Decimal` を変換できることを意味します。

- **末尾のゼロ。** Visual Basic では、末尾のゼロが `Decimal` リテラルに格納されません。 ただし、`Decimal` 変数では、計算によって取得されたすべての末尾のゼロが保持されます。 次に例を示します。

  ```vb
  Dim d1, d2, d3, d4 As Decimal
  d1 = 2.375D
  d2 = 1.625D
  d3 = d1 + d2
  d4 = 4.000D
  MsgBox("d1 = " & CStr(d1) & ", d2 = " & CStr(d2) &
        ", d3 = " & CStr(d3) & ", d4 = " & CStr(d4))
  ```

  前の例の `MsgBox` の出力は次のようになります。

  ```console
  d1 = 2.375, d2 = 1.625, d3 = 4.000, d4 = 4
  ```

- **型文字。** あるリテラルにリテラルの型文字 `D` を付けると、そのリテラルは `Decimal` に変換されます。 ある識別子に識別子の型文字 `@` を付けると、その識別子は整数型 (`Decimal`) に変換されます。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Decimal?displayProperty=nameWithType> 構造体です。

## <a name="range"></a>範囲

 `Decimal` 変数または定数に大きな値を代入するために、`D` 型文字を使用する必要がある場合があります。 この要件は、次の例に示すように、リテラルの型文字がリテラルの後に続く場合を除いて、コンパイラではリテラルが `Long` として解釈されるためです。

```vb
Dim bigDec1 As Decimal = 9223372036854775807   ' No overflow.
Dim bigDec2 As Decimal = 9223372036854775808   ' Overflow.
Dim bigDec3 As Decimal = 9223372036854775808D  ' No overflow.
```

それに代入される値は `Long` の範囲に収まるため、`bigDec1` の宣言でオーバーフローが発生しません。 `Long` 値は `Decimal` 変数に代入することができます。

`bigDec2` の宣言で、オーバーフロー エラーが発生するのは、それに代入された値が `Long` に対して大きすぎるためです。 数値リテラルは最初に `Long` として解釈できないため、`Decimal` 変数に代入できません。

`bigDec3` の場合、リテラルの型文字 `D` で、コンパイラにリテラルを `Long` ではなく `Decimal` として強制的に解釈させることによって、問題を解決します。

## <a name="see-also"></a>関連項目

- <xref:System.Decimal?displayProperty=nameWithType>
- <xref:System.Decimal.%23ctor%2A>
- <xref:System.Math.Round%2A?displayProperty=nameWithType>
- [データの種類](index.md)
- [Single データ型](single-data-type.md)
- [Double 型](double-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
