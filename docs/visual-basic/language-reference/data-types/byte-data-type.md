---
title: バイト型 (Byte)
ms.date: 01/31/2018
f1_keywords:
- vb.Byte
helpviewer_keywords:
- Byte data type
- data types [Visual Basic], assigning
ms.assetid: eed44dff-eaee-4937-a89f-444e418e74f6
ms.openlocfilehash: 97acd1bc2ff29bac6588216b9ee4a4f187078815
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374318"
---
# <a name="byte-data-type-visual-basic"></a>バイト (Byte) データ型 (Visual Basic)

0 から 255 までの値の範囲の符号なし 8 ビット (1 バイト) の整数を保持します。

## <a name="remarks"></a>Remarks

バイナリ データを格納するには、`Byte` データ型を使用します。  
  
`Byte` の既定値は 0 です。

## <a name="literal-assignments"></a>リテラルの代入

`Byte` 変数を宣言し、10 進リテラル、16 進リテラル、8 進リテラル、または (Visual Basic 2017 以降) バイナリ リテラルを代入することによって初期化できます。 整数リテラルが `Byte` の範囲外にある場合 (つまり、<xref:System.Byte.MinValue?displayProperty=nameWithType> より小さいか、<xref:System.Byte.MaxValue?displayProperty=nameWithType> より大きい場合)、コンパイル エラーが発生します。

次の例では、整数 201 を 10 進リテラル、16 進リテラル、バイナリ リテラルで表したものが、[Integer](integer-data-type.md) から `byte` 値に暗黙的に変換されています。

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Byte)]

> [!NOTE]
> 16 進リテラルを表すにはプレフィックス `&h` または `&H` を使い、バイナリ リテラルを表すにはプレフィックス `&b` または `&B` を使い、8 進リテラルを表すにはプレフィックス `&o` または `&O` を使います。 10 進リテラルには、プレフィックスはありません。

Visual Basic 2017 以降では、次の例に示すように、アンダースコア文字 `_` を桁区切り記号として使って読みやすくすることもできます。

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ByteS)]  

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As Byte = &H_6A
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

## <a name="programming-tips"></a>プログラミングのヒント

- **負の数値。** `Byte` は符号なしの型であるため、負の数を表すことはできません。 `Byte` 型に評価される式で、単項マイナス (`-`) 演算子を使用すると、Visual Basic で式が最初に `Short` に変換されます。
  
- **形式変換。** Visual Basic でファイルの読み取りまたは書き込みを行うとき、または DLL、メソッド、およびプロパティを呼び出すときに、データ形式を自動的に変換させることができます。 `Byte` 変数および配列に格納されているバイナリ データは、そのような形式の変換時に保持されます。 バイナリ データには `String` 変数を使用しないでください。ANSI 形式と Unicode 形式間の変換時に、その内容が破損する可能性があります。

- **拡大変換。** `Byte` データ型は、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、または `Double` に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、これらの型のいずれかに `Byte` を変換できることを意味します。
  
- **型文字。** `Byte` には、リテラルの型文字も識別子の型文字も含まれません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Byte?displayProperty=nameWithType> 構造体です。

## <a name="example"></a>例

 次の例では、`b` は `Byte` 変数です。 このステートメントでは、変数の範囲と、それに対するビットシフト演算子の適用を示しています。

 [!code-vb[VbVbalrDataTypes#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#16)]  

## <a name="see-also"></a>関連項目

- <xref:System.Byte?displayProperty=nameWithType>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
