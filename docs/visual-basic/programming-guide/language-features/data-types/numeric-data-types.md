---
title: 数値データ型
ms.date: 07/20/2015
helpviewer_keywords:
- integral types [Visual Basic], Visual Basic
- Short data type [Visual Basic], numeric data types
- Double data type [Visual Basic], numeric data types
- Long data type [Visual Basic], Visual Basic numeric data types
- numbers [Visual Basic], whole
- fractions
- numbers
- whole numbers
- integer numbers
- numbers [Visual Basic], integer
- fractional data types [Visual Basic]
- mantissas, of fractional numbers
- mantissas
- data types [Visual Basic], numeric
- Integer data type [Visual Basic], numeric data types
- exponent, of fractional numbers
- integers [Visual Basic]
- numeric data types [Visual Basic], Visual Basic
- Single data type [Visual Basic], numeric types
- Decimal data type [Visual Basic], numeric data types
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
ms.openlocfilehash: 72cdca295e209935687f67ad290e816775d9fe13
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393677"
---
# <a name="numeric-data-types-visual-basic"></a>数値データ型 (Visual Basic)
Visual Basic には、さまざまな表現の数値を処理するためにいくつかの "*数値データ型*" が用意されています。 "*整数*" 型は整数 (正、負、ゼロ) のみを表し、"*非整数*" 型は整数部と小数部の両方がある数値を表します。  
  
 Visual Basic データ型を並べて比較している表を、[データ型](../../../language-reference/data-types/index.md)に関するページで参照してください。  
  
## <a name="integral-numeric-types"></a>整数数値型  
 "*整数データ型*" は、小数部を含まない数値のみを表す型です。  
  
 "*符号付き*" の整数データ型は、[SByte データ型](../../../language-reference/data-types/sbyte-data-type.md) (8 ビット)、[Short データ型](../../../language-reference/data-types/short-data-type.md) (16 ビット)、[Integer データ型](../../../language-reference/data-types/integer-data-type.md) (32 ビット)、および [Long データ型](../../../language-reference/data-types/long-data-type.md) (64 ビット) です。 変数に小数ではなく整数が常に格納される場合は、これらのいずれかの型として宣言します。  
  
 "*符号なし*" の整数型は、[Byte データ型](../../../language-reference/data-types/byte-data-type.md) (8 ビット)、[UShort データ型](../../../language-reference/data-types/ushort-data-type.md) (16 ビット)、[UInteger データ型](../../../language-reference/data-types/uinteger-data-type.md) (32 ビット)、および [ULong データ型](../../../language-reference/data-types/ulong-data-type.md) (64 ビット) です。 変数にバイナリ データまたは不明な性質のデータが含まれる場合は、これらのいずれかの型として宣言します。  
  
### <a name="performance"></a>パフォーマンス  
 算術演算は、整数型を使用すると他のデータ型よりも高速です。 Visual Basic では `Integer` 型と `UInteger` 型が最も高速です。  
  
### <a name="large-integers"></a>大きい整数  
 `Integer` データ型よりも大きな整数を保持する必要がある場合は、代わりに `Long` データ型を使用できます。 `Long` 変数は、-9,223,372,036,854,775,808 から 9,223,372,036,854,775,807 までの数値を保持できます。 `Long` を使用した演算は、`Integer` よりも少し遅くなります。  
  
 さらに大きな値が必要な場合は、[Decimal データ型](../../../language-reference/data-types/decimal-data-type.md)を使用できます。 小数位を使用しない場合、`Decimal` 変数には -79,228,162,514,264,337,593,543,950,335 から 79,228,162,514,264,337,593,543,950,335 までの数値を保持できます。 ただし、`Decimal` 数値を使用した演算は、他の数値データ型を使用するよりもかなり遅くなります。  
  
### <a name="small-integers"></a>小さい整数  
 `Integer` データ型のすべての範囲が必要ない場合は、-32,768 から 32,767 までの整数を保持できる `Short` データ型を使用できます。 最も小さい整数の範囲のためには、`SByte` データ型に -128 から 127 までの整数が保持されます。 小さい整数を保持する変数の数が非常に多い場合、共通言語ランタイムによって `Short` と `SByte` 変数がより効率的に格納され、メモリ消費が節約されることがあります。 ただし、`Short` と `SByte` を使用した演算は、`Integer` よりも多少遅くなります。  
  
### <a name="unsigned-integers"></a>符号なし整数  
 変数が負の数を保持する必要がないことがわかっている場合は、"*符号なしの型*" である `Byte`、`UShort`、`UInteger`、および `ULong` を使用できます。 これらのデータ型はそれぞれ、対応する符号付きの型 (`SByte`、`Short`、`Integer`、および `Long`) の 2 倍の正の整数を保持できます。 パフォーマンス面では、符号なしの各型の効率は、対応する符号付きの型とまったく同じです。 特に、`UInteger` が `Integer` と共通するのは、すべての基本数値データ型の中で最も効率的であるという特徴です。  
  
## <a name="nonintegral-numeric-types"></a>非整数数値型  
 "*非整数データ型*" は、整数部と小数部の両方を含む数値を表す型です。  
  
 非整数データ型は、`Decimal` (128 ビット固定小数点)、[Single データ型](../../../language-reference/data-types/single-data-type.md) (32 ビット浮動小数点)、および [Double データ型](../../../language-reference/data-types/double-data-type.md) (64 ビット浮動小数点) です。 これらはすべて符号付きの型です。 変数が小数を含む可能性がある場合は、これらのいずれかの型として宣言します。  
  
 `Decimal` は浮動小数点データ型ではありません。 `Decimal` 数は、2 進数の整数値と、値のどの部分が小数であるかを指定する整数のスケーリング ファクターを保持します。  
  
 金額には `Decimal` 変数を使用できます。 利点は値の精度です。 `Double` データ型の方が高速で、必要なメモリが少なくなりますが、丸めエラーが発生する可能性があります。 `Decimal` データ型では、小数点以下 28 桁まで完全な精度が保持されます。  
  
 浮動小数点 (`Single` および `Double`) 数は、`Decimal` 数よりも広い範囲に対応しますが、丸めエラーが発生する可能性があります。 浮動小数点型は、`Decimal` よりも有効桁数は少ないものの、より大きい値を表すことができます。  
  
 非整数の数値は mmmEeee として表すことができます。mmm は "*仮数*" (有効桁数)、eee は "*指数*" (10 の累乗) です。 非整数型の最大の正の値は、7.9228162514264337593543950335E+28 (`Decimal`)、3.4028235E+38 (`Single`)、および 1.79769313486231570E+308 (`Double`) です。  
  
### <a name="performance"></a>パフォーマンス  
 `Double` は小数データ型の中で最も効率的です。現在のプラットフォームのプロセッサが、倍精度で浮動小数点演算を実行するためです。 ただし、`Double` を使用した演算は、`Integer` などの整数型ほど高速ではありません。  
  
### <a name="small-magnitudes"></a>大きさが小さい  
 大きさが最も小さくなる (0 に最も近くなる) 可能性がある数の場合、`Double` 変数は、負の値として -4.94065645841246544E-324、正の値として 4.94065645841246544E-324 を保持できます。  
  
### <a name="small-fractional-numbers"></a>小さい小数  
 `Double` データ型のすべての範囲が必要ない場合は、-3.4028235E+38 から 3.4028235E+38 までの浮動小数点数を保持できる `Single` データ型を使用できます。 `Single` 変数の最小の大きさは、負の値が -1.401298E-45、正の値が 1.401298E-45 です。 小さい浮動小数点数を保持する変数の数が非常に多い場合、共通言語ランタイムによって `Single` 変数がより効率的に格納され、メモリ消費が節約されることがあります。  
  
## <a name="see-also"></a>関連項目

- [基本データ型](elementary-data-types.md)
- [文字データ型](character-data-types.md)
- [その他のデータ型](miscellaneous-data-types.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
