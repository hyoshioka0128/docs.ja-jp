---
title: Short 型
ms.date: 01/31/2018
f1_keywords:
- vb.Short
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- S literal type character [Visual Basic]
- Short data type
- literal type characters [Visual Basic], S
ms.assetid: 65fcbcf3-a841-400e-885e-301497729a8b
ms.openlocfilehash: 176d27c86127dac1d9c9c0231790f7a5c2a2fefc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415558"
---
# <a name="short-data-type-visual-basic"></a>Short データ型 (Visual Basic)

-32,768 から 32,767 までの符号付き 16 ビット (2 バイト) の整数を保持します。  
  
## <a name="remarks"></a>Remarks  

 `Integer` の完全なデータ幅を必要としない整数値を格納するには、`Short` データ型を使用します。 場合によっては、共通言語ランタイムで `Short` 変数を緊密にパックし、メモリ消費を節約できます。  
  
 `Short` の既定値は 0 です。  
  
## <a name="literal-assignments"></a>リテラルの代入

`Short` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `Short` の範囲外にある場合 (つまり、<xref:System.Int16.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.Int16.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 1,034 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、[Integer](integer-data-type.md) から `Short` 値に暗黙的に変換されています。

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Short)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ShortS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As Short = &H_3264
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

数値リテラルには、次の例に示すように、`S` [型文字](../../programming-guide/language-features/data-types/type-characters.md)を含めて、`Short` データ型を表すこともできます。

```vb
Dim number = &H_3264S
```

## <a name="programming-tips"></a>プログラミングのヒント

- **拡大変換。** `Short` データ型は、`Integer`、`Long`、`Decimal`、`Single`、または `Double` に拡大変換されます。 これは、`Short` エラーを発生させることなく、これらの型のいずれかに <xref:System.OverflowException?displayProperty=nameWithType> を変換できることを意味します。  
  
- **型文字。** あるリテラルにリテラルの型文字 `S` を付けると、そのリテラルは `Short` に変換されます。 `Short` には識別子の型文字がありません。  
  
- **Framework の型。** .NET Framework において対応する型は、<xref:System.Int16?displayProperty=nameWithType> 構造体です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Int16?displayProperty=nameWithType>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [Integer データ型](integer-data-type.md)
- [Long データ型](long-data-type.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
