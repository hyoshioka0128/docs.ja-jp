---
title: 演算子の結果のデータ型
ms.date: 07/20/2015
helpviewer_keywords:
- data types [Visual Basic], operator result data types
- result data types [Visual Basic]
- operator result data types [Visual Basic]
- operators [Visual Basic], data types
- data types [Visual Basic], ranges
- operators [Visual Basic], result data types
ms.assetid: 9d524533-e1a1-4aa8-b1b8-622068173d06
ms.openlocfilehash: b80508c5619770da0c7dc78003ff9d4847dd94d8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371428"
---
# <a name="data-types-of-operator-results-visual-basic"></a>演算子の結果のデータ型 (Visual Basic)
Visual Basic では、オペランドのデータ型に基づいて、演算結果のデータ型が決定されます。 場合によっては、データ型の範囲が、どのオペランドよりも大きくなることがあります。  
  
## <a name="data-type-ranges"></a>データ型の範囲  
 関連するデータ型の範囲は、小さい方から順に、次のようになります。  
  
- [Boolean](../data-types/boolean-data-type.md) — 可能な値は 2 個  
  
- [SByte](../data-types/sbyte-data-type.md)、[Byte](../data-types/byte-data-type.md) — 可能な値は 256 個の整数  
  
- [Short](../data-types/short-data-type.md)、[UShort](../data-types/ushort-data-type.md) — 可能な値は 65,536 (6.5...E+4) 個の整数  
  
- [Integer](../data-types/integer-data-type.md)、[UInteger](../data-types/uinteger-data-type.md) — 可能な値は 4,294,967,296 (4.2...E+9) 個の整数  
  
- [Long](../data-types/long-data-type.md)、[ULong](../data-types/ulong-data-type.md) — 可能な値は 18,446,744,073,709,551,615 (1.8...E+19) 個の整数  
  
- [Decimal](../data-types/decimal-data-type.md) — 可能な値は 1.5...E+29 個の整数、最大範囲は 7.9...E+28 (絶対値)  
  
- [Single](../data-types/single-data-type.md) — 最大範囲は 3.4...E+38 (絶対値)  
  
- [Double](../data-types/double-data-type.md)最大範囲は 1.7...E+308 (絶対値)  
  
 Visual Basic のデータ型の詳細については、[データ型](../data-types/index.md)に関するページを参照してください。  
  
 オペランドは、[Nothing](../nothing.md) に評価されると、Visual Basic の算術演算子により 0 として扱われます。  
  
## <a name="decimal-arithmetic"></a>10 進数の算術演算  
 [Decimal](../data-types/decimal-data-type.md) データ型は、浮動小数点と整数のどちらでもないことに注意してください。  
  
 `+`、`–`、`*`、`/`、または `Mod` 演算のどちらか一方のオペランドが `Decimal` で、もう一方が `Single` でも `Double` でもない場合、Visual Basic により、もう一方のオペランドは `Decimal` に拡大変換されます。 `Decimal` 演算が実行され、結果のデータ型は `Decimal` になります。  
  
## <a name="floating-point-arithmetic"></a>浮動小数点数の算術演算  
 Visual Basic では、ほとんどの浮動小数点は [Double](../data-types/double-data-type.md) 算術演算が実行されます。これは、このような演算で最も効率的なデータ型です。 ただし、一方のオペランドが [Single](../data-types/single-data-type.md) であり、もう一方のオペランドが `Double` ではない場合は、Visual Basic により `Single` 演算が実行されます。 各オペランドは、演算前に必要に応じて適切なデータ型に拡大変換され、結果はそのデータ型になります。  
  
### <a name="-and--operators"></a>/ 演算子と ^ 演算子  
 `/` 演算子は、[Decimal](../data-types/decimal-data-type.md)、[Single](../data-types/single-data-type.md)、および [Double](../data-types/double-data-type.md) データ型に対してのみ定義されています。 各オペランドは、演算前に Visual Basic により必要に応じて適切なデータ型に拡大変換され、結果はそのデータ型になります。  
  
 次の表は、`/` 演算子の結果のデータ型を示しています。 この表は対称になっていることに注意してください。オペランドの順序に関係なく、オペランドのデータ型の組み合わせにより、結果のデータ型は同じになります。  
  
||||||  
|---|---|---|---|---|  
||`Decimal`|`Single`|`Double`|任意の整数型|  
|`Decimal`|Decimal (10 進数型)|Single|Double|Decimal (10 進数型)|  
|`Single`|Single|Single|Double|Single|  
|`Double`|Double|Double|Double|Double|  
|任意の整数型|Decimal (10 進数型)|Single|Double|Double|  
  
 `^` 演算子は、`Double` データ型に対してのみ定義されています。 各オペランドは、演算前に Visual Basic により必要に応じて `Double` に拡大変換され、結果のデータ型は常に `Double` になります。  
  
## <a name="integer-arithmetic"></a>整数の算術演算  
 整数演算の結果のデータ型は、オペランドのデータ型によって異なります。 一般に、Visual Basic では、次のポリシーを使用して結果のデータ型が決定されます。  
  
- 2 項演算子の両方のオペランドのデータ型が同じである場合、結果はそのデータ型になります。 例外は `Boolean` で、`Short` に強制変換されます。  
  
- 符号なしオペランドと符号付きオペランドを使用する場合、結果は符号付き型で、範囲は少なくともどちらかのオペランドと同じになります。  
  
- それ以外の場合、結果は通常、2 つのオペランド データ型のうち範囲が大きい方になります。  
  
 結果のデータ型が、どちらのオペランド データ型とも異なる場合があることに注意してください。  
  
> [!NOTE]
> 結果のデータ型が、演算結果として得られる可能性があるすべての値を保持するのに十分な大きさがあるとは限りません。 値が結果のデータ型に対して大きすぎる場合は、<xref:System.OverflowException> 例外が発生する可能性があります。  
  
### <a name="unary--and--operators"></a>\+ および – 単項演算子  
 次の表は、`+` と `–` の 2 つの単項演算子に対する結果のデータ型を示しています。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|単項 `+`|Short|SByte|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
|単項 `–`|Short|SByte|Short|Short|整数型|整数型|Long|Long|Decimal (10 進数型)|  
  
### <a name="-and--operators"></a><\< and >> 演算子  
 次の表は、`<<` と `>>` の 2 つのビット シフト演算子の結果のデータ型を示しています。 Visual Basic では、各ビット シフト演算子は、左オペランドの単項演算子として扱われます (ビット パターンがシフトされます)。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`<<`、`>>`|Short|SByte|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
  
 左オペランドが `Decimal`、`Single`、`Double`、または `String` の場合、演算前に Visual Basic により `Long` への変換が試行され、結果のデータ型は `Long` になります。 右オペランド (ビット位置のシフト数) は `Integer` であるか、`Integer` に拡大変換される型である必要があります。  
  
### <a name="binary----and-mod-operators"></a>+、–、\*、Mod 2 項演算子  
 次の表は、2 項演算子の `+`、`–`、`*`、`Mod` の結果のデータ型を示しています。 この表は対称になっていることに注意してください。オペランドの順序に関係なく、オペランドのデータ型の組み合わせにより、結果のデータ型は同じになります。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|整数型|整数型|Long|Long|Decimal (10 進数型)|  
|`SByte`|SByte|SByte|Short|Short|整数型|整数型|Long|Long|Decimal (10 進数型)|  
|`Byte`|Short|Short|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|整数型|整数型|Long|Long|Decimal (10 進数型)|  
|`UShort`|整数型|整数型|UShort|整数型|UShort|整数型|UInteger|Long|ULong|  
|`Integer`|整数型|整数型|整数型|整数型|整数型|整数型|Long|Long|Decimal (10 進数型)|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Decimal (10 進数型)|  
|`ULong`|Decimal (10 進数型)|Decimal (10 進数型)|ULong|Decimal (10 進数型)|ULong|Decimal (10 進数型)|ULong|Decimal (10 進数型)|ULong|  
  
### <a name="-operator"></a>\\ 演算子  
 次の表は、`\` 演算子の結果のデータ型を示しています。 この表は対称になっていることに注意してください。オペランドの順序に関係なく、オペランドのデータ型の組み合わせにより、結果のデータ型は同じになります。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|整数型|整数型|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|整数型|整数型|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|整数型|整数型|Long|Long|Long|  
|`UShort`|整数型|整数型|UShort|整数型|UShort|整数型|UInteger|Long|ULong|  
|`Integer`|整数型|整数型|整数型|整数型|整数型|整数型|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 `\` 演算子のどちらかのオペランドが [Decimal](../data-types/decimal-data-type.md)、[Single](../data-types/single-data-type.md)、または [Double](../data-types/double-data-type.md) の場合、演算前に Visual Basic により [Long](../data-types/long-data-type.md) への変換が試行され、結果のデータ型は `Long` になります。  
  
## <a name="relational-and-bitwise-comparisons"></a>リレーショナルおよびビット単位の比較  
 リレーショナル演算 (`=`、`<>`、`<`、`>`、`<=`、`>=`) の結果のデータ型は、常に `Boolean`[ ブール データ型](../data-types/boolean-data-type.md)です。 これは、`Boolean` オペランドの論理演算 (`And`、`AndAlso`、`Not`、`Or`、`OrElse`、`Xor`) でも同じです。  
  
 ビット論理演算の結果のデータ型は、オペランドのデータ型によって異なります。 `AndAlso` と `OrElse` は `Boolean` に対してのみ定義され、各オペランドは、演算実行前に Visual Basic により必要に応じて `Boolean` に変換されます。  
  
### <a name="-----and--operators"></a>=、<>、\<, >、\<=, and >= 演算子  
 両方のオペランドが `Boolean` である場合、Visual Basic では、`True` は `False` 未満と見なされます。 数値型を `String` と比較する場合、演算前に Visual Basic により、`String` から `Double` への変換が試行されます。 `Char` または `Date` のオペランドは、同じデータ型の別のオペランドとのみ比較できます。 結果のデータ型は常に `Boolean` になります。  
  
### <a name="bitwise-not-operator"></a>Not ビット演算子  
 次の表は、`Not` ビット演算子の結果のデータ型を示しています。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Not`|ブール型|SByte|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
  
 オペランドが `Decimal`、`Single`、`Double`、または `String` の場合、演算前に Visual Basic により `Long` への変換が試行され、結果のデータ型は `Long` になります。  
  
### <a name="bitwise-and-or-and-xor-operators"></a>And、Or、Xor ビット演算子  
 次の表は、`And`、`Or`、`Xor` ビット演算子の結果のデータ型を示しています。 この表は対称になっていることに注意してください。オペランドの順序に関係なく、オペランドのデータ型の組み合わせにより、結果のデータ型は同じになります。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|ブール型|SByte|Short|Short|整数型|整数型|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|整数型|整数型|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|整数型|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|整数型|整数型|Long|Long|Long|  
|`UShort`|整数型|整数型|UShort|整数型|UShort|整数型|UInteger|Long|ULong|  
|`Integer`|整数型|整数型|整数型|整数型|整数型|整数型|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 オペランドが `Decimal`、`Single`、`Double`、または `String` の場合、演算前に Visual Basic により `Long` への変換が試行され、結果のデータ型は、そのオペランドが既に `Long` である場合と同じになります。  
  
## <a name="miscellaneous-operators"></a>その他の演算子  
 `&` 演算子は、`String` オペランドを連結する場合に対してのみ定義されています。 各オペランドは、演算前に Visual Basic により必要に応じて `String` に変換され、結果のデータ型は常に `String` になります。 `&` 演算子においては、`Option Strict` が `On` の場合でも、`String` への変換はすべて拡大変換と見なされます。  
  
 `Is` 演算子と `IsNot` 演算子では、両方のオペランドが参照型である必要があります。 `TypeOf`...`Is` 式では、最初のオペランドが参照型で、2 番目のオペランドがデータ型の名前である必要があります。 これらはすべて、結果のデータ型は `Boolean` になります。  
  
 `Like` 演算子は、`String` オペランドのパターン マッチングに対してのみ定義されています。 各オペランドは、演算前に Visual Basic により必要に応じて`String` への変換が試行されます。 結果のデータ型は常に `Boolean` になります。  
  
## <a name="see-also"></a>関連項目

- [データの種類](../data-types/index.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Visual Basic における比較演算子](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [演算子](index.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [算術演算子](arithmetic-operators.md)
- [比較演算子](comparison-operators.md)
- [Option Strict ステートメント](../statements/option-strict-statement.md)
