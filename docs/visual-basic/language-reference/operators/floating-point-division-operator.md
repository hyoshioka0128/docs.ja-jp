---
title: / 演算子
ms.date: 07/20/2015
f1_keywords:
- vb./
helpviewer_keywords:
- division operator [Visual Basic], floating point
- floating-point numbers [Visual Basic], division operator
- slash (/) operator
- zero, division by zero
- operators [Visual Basic], arithmetic
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- operators [Visual Basic], division
- division operator [Visual Basic], syntax
- / operator [Visual Basic]
- math operators [Visual Basic]
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
ms.openlocfilehash: e9400b50a84522f87a9a2ea4cd05b479d7a4538e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371169"
---
# <a name="-operator-visual-basic"></a>/ 演算子 (Visual Basic)
2 つの数値の商を計算し、結果を浮動小数点で返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
expression1 / expression2  
```  
  
## <a name="parts"></a>指定項目  
 `expression1`  
 必須です。 任意の数式。  
  
 `expression2`  
 必須です。 任意の数式。  
  
## <a name="supported-types"></a>サポートされている型  
 符号なし型、浮動小数点型、`Decimal` を含む、すべての数値型。  
  
## <a name="result"></a>結果  
 結果は、`expression1` を `expression2` で除算した完全な商で、剰余も含まれます。  
  
 [\ 演算子 (Visual Basic)](integer-division-operator.md) では整数の商が返され、剰余は捨てられます。  
  
## <a name="remarks"></a>Remarks  
 結果のデータ型は、オペランドの型によって異なります。 次の表は、結果のデータ型がどのように決定されるかを示しています。  
  
|オペランドのデータ型|結果のデータ型|  
|------------------------|----------------------|  
|両方の式が整数データ型 ([SByte](../data-types/sbyte-data-type.md)、[Byte](../data-types/byte-data-type.md)、[Short](../data-types/short-data-type.md)、[UShort](../data-types/ushort-data-type.md)、[Integer](../data-types/integer-data-type.md)、[UInteger](../data-types/uinteger-data-type.md)、[Long](../data-types/long-data-type.md)、[ULong](../data-types/ulong-data-type.md)) である|`Double`|  
|一方の式が [Single](../data-types/single-data-type.md) データ型であり、もう一方が [Double](../data-types/double-data-type.md) でない|`Single`|  
|一方の式が [Decimal](../data-types/decimal-data-type.md) データ型であり、もう一方が [Single](../data-types/single-data-type.md) でも [Double](../data-types/double-data-type.md) でもない|`Decimal`|  
|どちらか一方の式が [Double](../data-types/double-data-type.md) データ型である|`Double`|  
  
 除算を実行する前に、整数の数値式はすべて `Double` に拡大変換されます。 結果を整数データ型に代入すると、結果は、Visual Basic により `Double` からその型への変換が試行されます。 結果がその型に合わない場合、例外がスローされる可能性があります。 特に、このヘルプ ページの「0 除算が試行された場合」を参照してください。  
  
 `expression1` または `expression2` が [Nothing](../nothing.md) に評価される場合、0 として扱われます。  
  
## <a name="attempted-division-by-zero"></a>0 除算が試行された場合  
 `expression2` が 0 に評価される場合、`/` 演算子の動作は、オペランドのデータ型によって異なります。 次の表に、起こりうる動作を示します。  
  
|オペランドのデータ型|`expression2` が 0 の場合の動作|  
|------------------------|---------------------------------------|  
|浮動小数点 (`Single` または `Double`)|無限大 (<xref:System.Double.PositiveInfinity> または <xref:System.Double.NegativeInfinity>) を返し、`expression1` も 0 の場合は <xref:System.Double.NaN> (数値ではない) を返す|  
|`Decimal`|<xref:System.DivideByZeroException> をスローする|  
|整数 (符号付きまたは符号なし)|整数型への変換を試行すると、整数型は <xref:System.Double.PositiveInfinity>、<xref:System.Double.NegativeInfinity>、または <xref:System.Double.NaN> を受け入れることができないため、<xref:System.OverflowException> をスローする|  
  
> [!NOTE]
> `/` 演算子は "*オーバーロード*" できます。つまり、オペランドの型がクラスまたは構造体であるとき、そのクラスまたは構造体で、演算子の動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`/` 演算子を使用して、浮動小数点除算を実行します。 結果は 2 つのオペランドの商になります。  
  
 [!code-vb[VbVbalrOperators#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#16)]  
  
 この例の式では、2.5 と 3.333333 の値が返されます。 両方のオペランドが整数定数でも、結果は常に浮動小数点 (`Double`) になることに注意してください。  
  
## <a name="see-also"></a>関連項目

- [/= 演算子 (Visual Basic)](floating-point-division-assignment-operator.md)
- [\ 演算子 (Visual Basic)](integer-division-operator.md)
- [演算子の結果のデータ型](data-types-of-operator-results.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
