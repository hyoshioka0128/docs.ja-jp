---
title: UInteger 型
ms.date: 01/31/2018
f1_keywords:
- vb.uinteger
helpviewer_keywords:
- numbers [Visual Basic], whole
- UInteger data type
- literal type characters [Visual Basic], UI
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- UI literal type characters [Visual Basic]
- data types [Visual Basic], integral
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
ms.openlocfilehash: 11070f6c7f3259b8c34528eb54d99b031b68f9f9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415545"
---
# <a name="uinteger-data-type"></a>UInteger データ型

0 から 4,294,967,295 までの値の範囲の符号なし 32 ビット (4 バイト) の整数を保持します。

## <a name="remarks"></a>Remarks

`UInteger` データ型は、最も効率的なデータ幅で最も大きな符号なしの値を提供します。

`UInteger` の既定値は 0 です。

## <a name="literal-assignments"></a>リテラルの代入

`UInteger` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `UInteger` の範囲外にある場合 (つまり、<xref:System.UInt32.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.UInt32.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 3,000,000,000 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、`UInteger` 値に割り当てられています。

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UInt)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UIntS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As UInteger = &H_0F8C_0326
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

数値リテラルには、次の例に示すように、`UI` または `ui` [型文字](../../programming-guide/language-features/data-types/type-characters.md)を含めて、`UInteger` データ型を表すこともできます。

```vb
Dim number = &H_0FAC_14D7ui
```

## <a name="programming-tips"></a>プログラミングのヒント

`UInteger` データ型および `Integer` データ型は、32 ビット プロセッサで最適なパフォーマンスを発揮します。これは、より小さい整数型 (`UShort`、`Short`、`Byte`、`SByte`) では、使用するビット数が少なくても、読み込み、格納、およびフェッチにかかる時間が長くなるためです。

- **負の数値。** `UInteger` は符号なしの型であるため、負の数を表すことはできません。 `UInteger` 型に評価される式で、単項マイナス (`-`) 演算子を使用すると、Visual Basic で式が最初に `Long` に変換されます。

- **CLS 準拠。** `UInteger` データ型は[共通言語仕様](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS) に含まれないため、CLS に準拠しているコードではそれを使用するコンポーネントを使用できません。

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトなど、.NET Framework 用に作成されていないコンポーネントとやり取りする場合、`uint` などの型は、他の環境ではデータ幅 (16 ビット) が異なる可能性があることに注意してください。 そのようなコンポーネントに 16 ビットの引数を渡す場合は、Visual Basic のマネージド コードで、`UInteger` ではなく `UShort` として宣言します。

- **拡大変換。** `UInteger` データ型は、`Long`、`ULong`、`Decimal`、`Single`、および `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `UInteger` を変換できることを意味します。

- **型文字。** あるリテラルにリテラルの型文字 `UI` を付けると、そのリテラルは `UInteger` データ型に変換されます。 `UInteger` には識別子の型文字がありません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.UInt32?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.UInt32>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
