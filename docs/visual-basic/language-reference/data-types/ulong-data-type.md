---
title: ULong 型
ms.date: 01/31/2018
f1_keywords:
- vb.ulong
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- literal type characters [Visual Basic], UL
- ULong data type
- UL literal type characters [Visual Basic]
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
ms.openlocfilehash: ee9297ae917345d44d8e630bd09beea2245b56da
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415519"
---
# <a name="ulong-data-type-visual-basic"></a>ULong データ型 (Visual Basic)

0 から 18,446,744,073,709,551,615 (1.84 x 10 ^ 19 以上) までの値の範囲の符号なし 64 ビット (8 バイト) の整数を保持します。

## <a name="remarks"></a>Remarks

`ULong` データ型は、`UInteger` には大きすぎるバイナリ データや、可能な限り最大の符号なし整数値を格納する場合に使用します。

`ULong` の既定値は 0 です。

## <a name="literal-assignments"></a>リテラルの代入

`ULong` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `ULong` の範囲外にある場合 (つまり、<xref:System.UInt64.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.UInt64.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 7,934,076,125 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、`ULong` 値に割り当てられています。

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ULong)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As ULong = &H_F9AC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

数値リテラルには、次の例に示すように、`UL` または `ul` [型文字](../../programming-guide/language-features/data-types/type-characters.md)を含めて、`ULong` データ型を表すこともできます。

```vb
Dim number = &H_00_00_0A_96_2F_AC_14_D7ul
```

## <a name="programming-tips"></a>プログラミングのヒント

- **負の数値。** `ULong` は符号なしの型であるため、負の数を表すことはできません。 `ULong` 型に評価される式で、単項マイナス (`-`) 演算子を使用すると、Visual Basic で式が最初に `Decimal` に変換されます。

- **CLS 準拠。** `ULong` データ型は[共通言語仕様](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS) に含まれないため、CLS に準拠しているコードではそれを使用するコンポーネントを使用できません。

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトなど、.NET Framework 用に作成されていないコンポーネントとやり取りする場合、`ulong` などの型は、他の環境ではデータ幅 (32 ビット) が異なる可能性があることに注意してください。 そのようなコンポーネントに 32 ビットの引数を渡す場合は、Visual Basic のマネージド コードで、`ULong` ではなく `UInteger` として宣言します。

  さらに、オートメーションでは、Windows 95、Windows 98、Windows ME、または Windows 2000 での 64 ビットの整数はサポートされません。 これらのプラットフォームのオートメーション コンポーネントに Visual Basic の `ULong` 引数を渡すことはできません。

- **拡大変換。** `ULong` データ型は、`Decimal`、`Single`、および `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `ULong` を変換できることを意味します。

- **型文字。** あるリテラルにリテラルの型文字 `UL` を付けると、そのリテラルは `ULong` データ型に変換されます。 `ULong` には識別子の型文字がありません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.UInt64?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.UInt64>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
