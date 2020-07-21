---
title: Long 型
ms.date: 01/31/2018
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
ms.openlocfilehash: 7c076cd2198c85560f7c63c69e051697966c9524
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415597"
---
# <a name="long-data-type-visual-basic"></a>Long データ型 (Visual Basic)

-9,223,372,036,854,775,808 から 9,223,372,036,854,775,807 (9.2...E+18) までの値の範囲の符号付き 64 ビット (8 バイト) の整数を保持します。

## <a name="remarks"></a>Remarks

`Long` データ型を使用して、`Integer` データ型には大きすぎて収まらない整数値を格納します。

`Long` の既定値は 0 です。

## <a name="literal-assignments"></a>リテラルの代入

`Long` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `Long` の範囲外にある場合 (つまり、<xref:System.Int64.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.Int64.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 4,294,967,296 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、`Long` 値に割り当てられています。

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

数値リテラルには、次の例に示すように、`L` [型文字](../../programming-guide/language-features/data-types/type-characters.md)を含めて、`Long` データ型を表すこともできます。

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a>プログラミングのヒント

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトなど、.NET Framework 用に作成されていないコンポーネントとやり取りする場合、他の環境では整数型 (`Long`) のデータ幅 (32 ビット) が異なることに注意してください。 そのようなコンポーネントに 32 ビットの引数を渡す場合は、新しい Visual Basic のコードで、整数型 (`Long`) ではなく短整数型 (`Integer`) として宣言します。

- **拡大変換。** `Long` データ型は、`Decimal`、`Single`、または `Double` に拡大変換されます。 これは、`Long` エラーを発生させることなく、これらの型のいずれかに <xref:System.OverflowException?displayProperty=nameWithType> を変換できることを意味します。

- **型文字。** あるリテラルにリテラルの型文字 `L` を付けると、そのリテラルは `Long` に変換されます。 ある識別子に識別子の型文字 `&` を付けると、その識別子は整数型 (`Long`) に変換されます。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Int64?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.Int64>
- [データの種類](index.md)
- [Integer データ型](integer-data-type.md)
- [Short データ型](short-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
