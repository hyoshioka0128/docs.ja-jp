---
title: 文字型 (Char)
ms.date: 07/20/2015
f1_keywords:
- vb.Char
helpviewer_keywords:
- literal type characters [Visual Basic], C
- Char data type
- C literal type character [Visual Basic]
- data types [Visual Basic], assigning
- Char data type [Visual Basic], character literals
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
ms.openlocfilehash: 3dbbf9f6a2c4079775e05f5d2dcd8704c1ec4259
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387479"
---
# <a name="char-data-type-visual-basic"></a>文字型 (Char) (Visual Basic)

0 から 65535 までの値の範囲の符号なし 16 ビット (2 バイト) のコード ポイントを保持します。 各*コード ポイント* (文字コード) は、1 つの Unicode 文字を表します。

## <a name="remarks"></a>Remarks

1 文字だけを保持する必要があり、`String` のオーバーヘッドを必要としない場合に、`Char` データ型を使用します。 場合によっては、複数の文字を保持するために、`Char` 要素の配列である `Char()` を使用できます。

`Char` の既定値は、コード ポイントが 0 の文字です。

## <a name="unicode-characters"></a>Unicode 文字

Unicode の最初の 128 コード ポイント (0 ～ 127) は、標準の米国キーボードの文字と記号に対応しています。 これらの最初の 128 コード ポイントは、ASCII 文字セットで定義されているものと同じです。 2 番目の 128 コード ポイント (128 ～ 255) は、ラテン語に基づくアルファベット文字、アクセント、通貨記号、分数などの特殊文字を表します。 Unicode では、残りのコード ポイント (256-65535) を、世界全体のテキスト文字、分音記号、数学記号、技術記号などの多様な記号に使用しています。

`Char` 変数に対して <xref:System.Char.IsDigit%2A> や <xref:System.Char.IsPunctuation%2A> などのメソッドを使用して、その Unicode の分類を判断できます。

## <a name="type-conversions"></a>型変換

Visual Basic では、`Char` と数値型の間で直接に変換されません。 <xref:Microsoft.VisualBasic.Strings.Asc%2A> または <xref:Microsoft.VisualBasic.Strings.AscW%2A> 関数を使用して、`Char` 値をそのコード ポイントを表す `Integer` に変換できます。 <xref:Microsoft.VisualBasic.Strings.Chr%2A> または <xref:Microsoft.VisualBasic.Strings.ChrW%2A> 関数を使用して、`Integer` 値をそのコード ポイントを持つ `Char` に変換できます。

型チェック スイッチ ([Option Strict ステートメント](../statements/option-strict-statement.md)) がオンになっている場合、リテラル型の文字を 1 文字の文字列リテラルに追加して、`Char` データ型として識別する必要があります。 次に例を示します。 `charVar` 変数への最初の代入では、`Option Strict` がオンになっているため、コンパイラ エラー [BC30512](../../misc/bc30512.md) が生成されます。 2 つ目は、リテラル型の文字 `c` によって、リテラルが `Char` 値として識別されるため、正常にコンパイルされます。

```vb
Option Strict On

Module CharType
    Public Sub Main()
        Dim charVar As Char

        ' This statement generates compiler error BC30512 because Option Strict is On.  
        charVar = "Z"  

        ' The following statement succeeds because it specifies a Char literal.  
        charVar = "Z"c
    End Sub
End Module
```

## <a name="programming-tips"></a>プログラミングのヒント

- **負の数値。** `Char` は符号なしの型であるため、負の値を表すことはできません。 いかなる場合でも、`Char` を使用して数値を保持しないでください。

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトなど、.NET Framework 用に作成されていないコンポーネントとやり取りする場合、他の環境では文字型のデータ幅 (8 ビット) が異なることに注意してください。 そのようなコンポーネントに 8 ビットの引数を渡す場合は、新しい Visual Basic のコードで、`Char` ではなく `Byte` として宣言します。

- **拡大変換。** `Char` データ型は、`String` に拡大変換されます。 つまり、`Char` を `String` に変換でき、<xref:System.OverflowException?displayProperty=nameWithType> は発生しません。

- **型文字。** 1 文字の文字列リテラルにリテラルの型文字 `C` を付けると、それは `Char` データ型に変換されます。 `Char` には識別子の型文字がありません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Char?displayProperty=nameWithType> 構造体です。

## <a name="see-also"></a>関連項目

- <xref:System.Char?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [データの種類](index.md)
- [String データ型](string-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
