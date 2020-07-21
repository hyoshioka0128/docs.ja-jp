---
title: SByte 型
ms.date: 04/20/2017
f1_keywords:
- vb.sbyte
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- SByte data type
ms.assetid: 5c38374a-18a1-4cc2-b493-299e3dcaa60f
ms.openlocfilehash: e7d45c74056ce5b6aa66674c99e48b5ab60015f0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415571"
---
# <a name="sbyte-data-type-visual-basic"></a>SByte データ型 (Visual Basic)

-128 から 127 までの符号付き 8 ビット (1 バイト) の整数を保持します。

## <a name="remarks"></a>Remarks

完全なデータ幅の `Integer` や半分のデータ幅の `Short` も必要としない整数値を格納するには、`SByte` データ型を使用します。 場合によっては、共通言語ランタイムで `SByte` 変数を緊密にパックし、メモリ消費を節約できる可能性があります。

`SByte` の既定値は 0 です。

## <a name="literal-assignments"></a>リテラルの代入

`SByte` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。

次の例では、整数 -102 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、`SByte` 値に代入されています。 この例では、`/removeintchecks` コンパイラ スイッチを使用してコンパイルする必要があります。

[!code-vb[SByte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByte)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[SByteSeparator](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByteS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As SByte = &H_F9
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

整数リテラルが `SByte` の範囲外にある場合 (つまり、<xref:System.SByte.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.SByte.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。 整数リテラルにサフィックスがない場合は、[Integer](integer-data-type.md) が推定されます。 整数リテラルが `Integer` 型の範囲外の場合は、[Long](long-data-type.md) が推定されます。 つまり、前の例では、数値リテラル `0x9A` と `0b10011010` は値が 156 の 32 ビット符号付き整数として解釈され、これは <xref:System.SByte.MaxValue?displayProperty=nameWithType> を超えています。 `SByte` に 10 進数以外の整数を代入する次のようなコードを正常にコンパイルするには、次のいずれかの操作を行います。

- `/removeintchecks` コンパイラ スイッチを使用してコンパイルすることにより、整数境界のチェックを無効にします。

- `SByte` に代入するリテラル値を明示的に定義するには、[型文字](../../programming-guide/language-features/data-types/type-characters.md)を使用します。 次の例では、負のリテラル `Short` 値を `SByte` に代入します。 負の数値の場合は、数値リテラルの上位ワードの上位ビットを設定する必要があることに注意してください。 この例の場合、これはリテラル `Short` 値のビット 15 です。

   [!code-vb[SByteTypeChars](../../../../samples/snippets/visualbasic/language-reference/data-types/sbyte-assignment.vb#1)]

## <a name="programming-tips"></a>プログラミングのヒント

- **CLS 準拠。** `SByte` データ型は[共通言語仕様](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS) に含まれないため、CLS に準拠しているコードではそれを使用するコンポーネントを使用できません。

- **拡大変換。** `SByte` データ型は、`Short`、`Integer`、`Long`、`Decimal`、`Single`、および `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `SByte` を変換できることを意味します。

- **型文字。** `SByte` には、リテラルの型文字も識別子の型文字も含まれません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.SByte?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.SByte?displayProperty=nameWithType>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [Short データ型](short-data-type.md)
- [Integer データ型](integer-data-type.md)
- [Long データ型](long-data-type.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
