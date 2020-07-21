---
title: UShort 型
ms.date: 01/31/2018
f1_keywords:
- vb.ushort
helpviewer_keywords:
- numbers [Visual Basic], whole
- literal type characters [Visual Basic], US
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- UShort data type
- US literal type characters [Visual Basic]
ms.assetid: 138db892-665d-4ba8-9cae-d8d91c4a8f39
ms.openlocfilehash: ee31156e00059699125fd72a7f091afbb21beab0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415480"
---
# <a name="ushort-data-type-visual-basic"></a>UShort データ型 (Visual Basic)

0 から 65,535 までの値の範囲の符号なし 16 ビット (2 バイト) の整数を保持します。  
  
## <a name="remarks"></a>Remarks

 `Byte` には大きすぎるバイナリ データを格納する場合に、`UShort` データ型を使用します。  
  
 `UShort` の既定値は 0 です。  

## <a name="literal-assignments"></a>リテラルの代入

`UShort` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `UShort` の範囲外にある場合 (つまり、<xref:System.UInt16.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.UInt16.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 65,034 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、`UShort` 値に代入されています。
  
[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShort)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShortS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As UShort = &H_FF8C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

数値リテラルには、次の例に示すように、`US` または `us` [型文字](../../programming-guide/language-features/data-types/type-characters.md)を含めて、`UShort` データ型を表すこともできます。

```vb
Dim number = &H_5826us
```

## <a name="programming-tips"></a>プログラミングのヒント
  
- **負の数値。** `UShort` は符号なしの型であるため、負の数を表すことはできません。 `UShort` 型に評価される式で、単項マイナス (`-`) 演算子を使用すると、Visual Basic で式が最初に `Integer` に変換されます。  
  
- **CLS 準拠。** `UShort` データ型は[共通言語仕様](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS) に含まれないため、CLS に準拠しているコードではそれを使用するコンポーネントを使用できません。
  
- **拡大変換。** `UShort` データ型は、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、および `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `UShort` を変換できることを意味します。  
  
- **型文字。** あるリテラルにリテラルの型文字 `US` を付けると、そのリテラルは `UShort` データ型に変換されます。 `UShort` には識別子の型文字がありません。  
  
- **Framework の型。** .NET Framework において対応する型は、<xref:System.UInt16?displayProperty=nameWithType> 構造体です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.UInt16>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
