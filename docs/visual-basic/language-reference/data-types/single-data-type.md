---
title: 単精度浮動小数点型 (Single)
ms.date: 07/20/2015
f1_keywords:
- vb.Single
helpviewer_keywords:
- Single data type
- F literal type character [Visual Basic]
- trailing zeros
- real numbers
- literal type characters [Visual Basic], F
- trailing 0 characters [Visual Basic]
- identifier type characters [Visual Basic], !
- single-precision numbers
- '! identifier type character'
- 0 characters [Visual Basic], trailing
- data types [Visual Basic], assigning
- floating-point numbers [Visual Basic], Single data type
- numbers [Visual Basic], real
- zeros, trailing
- numbers [Visual Basic], floating point
ms.assetid: 224a2795-4cd5-496c-8f7a-a4f05a06d45d
ms.openlocfilehash: ecb0f5f6416a2dd4ddd6888cb80ed3ac11ee58df
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415532"
---
# <a name="single-data-type-visual-basic"></a>単精度浮動小数点型 (Single) (Visual Basic)

負の値の場合は -3.4028235E+38 から -1.401298E-45 まで、正の値の場合は 1.401298E-45 から 3.4028235E+38 までの値の範囲の符号付き IEEE 32 ビット (4 バイト) の単精度浮動小数点数を保持します。 単精度の数値は、実数の概数を格納します。  
  
## <a name="remarks"></a>Remarks  

 `Double` の完全なデータ幅を必要としない浮動小数点値を格納するには、`Single` データ型を使用します。 場合によっては、共通言語ランタイムで `Single` 変数を緊密にパックし、メモリ消費を節約できる可能性があります。  
  
 `Single` の既定値は 0 です。  
  
## <a name="programming-tips"></a>プログラミングのヒント  
  
- **精度。** 浮動小数点数を操作する場合、それらがメモリ内で常に正確な表現が使用されているとは限らないことに注意してください。 これにより、値の比較や `Mod` 演算子など、特定の操作によって、予期しない結果につながる可能性があります。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」を参照してください。  
  
- **拡大変換。** `Single` データ型は、`Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、`Single` を `Double` に変換できることを意味します。  
  
- **末尾のゼロ。** 浮動小数点データ型には、末尾がゼロの文字の内部表現はありません。 たとえば、4.2000 と 4.2 は区別されません。 そのため、浮動小数点値を表示または出力すると、末尾がゼロの文字は表示されません。  
  
- **型文字。** あるリテラルにリテラルの型文字 `F` を付けると、そのリテラルは `Single` に変換されます。 ある識別子に識別子の型文字 `!` を付けると、その識別子は整数型 (`Single`) に変換されます。  
  
- **Framework の型。** .NET Framework において対応する型は、<xref:System.Single?displayProperty=nameWithType> 構造体です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Single?displayProperty=nameWithType>
- [データの種類](index.md)
- [Decimal データ型](decimal-data-type.md)
- [Double 型](double-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [トラブルシューティング (データ型)](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
