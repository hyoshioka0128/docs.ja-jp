---
title: 倍精度浮動小数点数型 (Double)
ms.date: 07/20/2015
f1_keywords:
- vb.Double
helpviewer_keywords:
- 'identifier type characters [Visual Basic], #'
- trailing zeros
- real numbers
- trailing 0 characters [Visual Basic]
- 0 characters [Visual Basic], trailing
- literal type characters [Visual Basic], R
- data types [Visual Basic], assigning
- Double data type [Visual Basic]
- '# identifier type character'
- double-precision numbers
- floating-point numbers [Visual Basic], Double data type
- R literal type character [Visual Basic]
- zeros, trailing
- Double data type
ms.assetid: 0c5670f7-fcb1-453a-bef1-374730cd38fd
ms.openlocfilehash: 899554f427ac77ead465752c35e51ca88d045763
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415635"
---
# <a name="double-data-type-visual-basic"></a>倍精度浮動小数点数型 (Double) (Visual Basic)

-1.79769313486231570 E + 308 から -4.94065645841246544 E-324 (負の値の場合) および 4.94065645841246544 E-324 から 1.79769313486231570 E + 308 (正の値の場合) までの値の範囲の、符号付き IEEE 64 ビット (8 バイト) の倍精度浮動小数点数を保持します。 倍精度の数値は、実数の概数を格納します。

## <a name="remarks"></a>Remarks

`Double` データ型は、数値に対して可能な最大と最小の絶対値を提供します。

`Double` の既定値は 0 です。

## <a name="programming-tips"></a>プログラミングのヒント

- **精度。** 浮動小数点数を操作する場合、それらがメモリ内で常に正確な表現が使用されているとは限らないことに注意してください。 これにより、値の比較や `Mod` 演算子など、特定の操作によって、予期しない結果につながる可能性があります。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」を参照してください。

- **末尾のゼロ。** 浮動小数点データ型には、末尾がゼロの文字の内部表現はありません。 たとえば、4.2000 と 4.2 は区別されません。 そのため、浮動小数点値を表示または出力すると、末尾がゼロの文字は表示されません。

- **型文字。** あるリテラルにリテラルの型文字 `R` を付けると、そのリテラルは `Double` に変換されます。 たとえば、整数値の後に `R` が続く場合、値は `Double` に変更されます。

  ```vb
  ' Visual Basic expands the 4 in the statement Dim dub As Double = 4R to 4.0:
  Dim dub As Double = 4.0R
  ```

  ある識別子に識別子の型文字 `#` を付けると、その識別子は整数型 (`Double`) に変換されます。 次の例では、変数 `num` は `Double` として型指定されます。

  ```vb
  Dim num# = 3
  ```

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Double?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.Double?displayProperty=nameWithType>
- [データの種類](index.md)
- [Decimal データ型](decimal-data-type.md)
- [Single データ型](single-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [トラブルシューティング (データ型)](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [型文字](../../programming-guide/language-features/data-types/type-characters.md)
