---
title: データ型のトラブルシューティング
ms.date: 07/20/2015
helpviewer_keywords:
- Char data type [Visual Basic], converting
- Decimal data type [Visual Basic], conversions
- data types [Visual Basic], troubleshooting
- literals [Visual Basic], default types
- type characters [Visual Basic], literal
- Mod operator [Visual Basic], in floating-point operations
- troubleshooting Visual Basic, data types
- troubleshooting data types [Visual Basic]
- floating-point numbers [Visual Basic], precision
- Boolean data type [Visual Basic], converting
- literal types [Visual Basic]
- literal type characters [Visual Basic]
- floating-point numbers [Visual Basic], imprecision
- String data type [Visual Basic], converting
- floating-point numbers [Visual Basic], comparison
- floating-point numbers
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
ms.openlocfilehash: 239e1c2f908a9023aeca6e92aff4633b60f27b69
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393404"
---
# <a name="troubleshooting-data-types-visual-basic"></a>データ型のトラブルシューティング (Visual Basic)

このページでは、組み込みデータ型に対して操作を実行するときに発生する可能性がある一般的な問題をいくつか示します。

## <a name="floating-point-expressions-do-not-compare-as-equal"></a>浮動小数点式を比較したときに等しくならない

浮動小数点数 ([Single データ型](../../../language-reference/data-types/single-data-type.md)および [Double データ型](../../../language-reference/data-types/double-data-type.md)) を扱うときは、それらがバイナリの分数として格納されることに注意してください。 つまり、これらは、バイナリの分数 (形式は k / (2 ^ n)、k と n は整数) ではない数量表現を保持できません。 たとえば、0.5 (= 1/2) と 0.3125 (= 5/16) は正確な値を保持できますが、0.2 (= 1/5) と 0.3 (= 3/10) は概算値しか保持できません。

この誤差のため、浮動小数点値の演算では、正確な結果かどうか信頼できません。 特に、理論的には等しい 2 つの値の表現が多少異なる場合があります。

| 浮動小数点数の数量を比較するには |
|---|
|1.<xref:System> 名前空間の <xref:System.Math> クラスの <xref:System.Math.Abs%2A> メソッドを使用して、差の絶対値を計算します。<br />2.最大の許容差を決めて、差がそれよりも小さい場合には、実際に 2 つの数量を等価と見なすようにします。<br />3.差の絶対値と許容差を比較します。|

次の例は、2 つの `Double` 値の誤った比較と正しい比較を示しています。

[!code-vb[VbVbalrDataTypes#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#10)]

前の例では、<xref:System.Double> 構造体の <xref:System.Double.ToString%2A> メソッドを使用して、`CStr` キーワードで使用されるよりも高い精度を指定できるようにしています。 既定値は 15 桁ですが、"G17" 形式によって 17 桁に拡張されます。

## <a name="mod-operator-does-not-return-accurate-result"></a>Mod 演算子が正確な結果を返さない

浮動小数点数の格納が正確でないため、少なくとも 1 つのオペランドが浮動小数点数である場合、[Mod 演算子](../../../language-reference/operators/mod-operator.md)は予期しない結果を返す可能性があります。

[Decimal データ型](../../../language-reference/data-types/decimal-data-type.md)では、浮動小数点表現は使用されません。 `Single` と `Double` で正確ではない多くの数値は、`Decimal` では正確です (0.2 や 0.3 など)。 浮動小数点型より `Decimal` では算術が遅くなりますが、パフォーマンスが低下しても精度が高まる値打ちがあります。

|浮動小数点数の整数の剰余を求めるには|
|---|
|1.変数を `Decimal` として宣言します。<br />2.リテラルの型文字 `D` を使用して、リテラルを強制的に `Decimal` にします (値が `Long` データ型に対して大きすぎる場合)。|

次の例は、浮動小数点オペランドにおける誤差の可能性を示しています。

[!code-vb[VbVbalrDataTypes#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#11)]

前の例では、<xref:System.Double> 構造体の <xref:System.Double.ToString%2A> メソッドを使用して、`CStr` キーワードで使用されるよりも高い精度を指定できるようにしています。 既定値は 15 桁ですが、"G17" 形式によって 17 桁に拡張されます。

`zeroPointTwo` は `Double` であるため、0.2 に対する値は、無限に連続するバイナリ分数値で、値 0.20000000000000001 が格納されます。 2\.0 をこの数で割ると 9.9999999999999995 になり、剰余が 0.19999999999999991 になります。

`decimalRemainder` の式では、リテラルの型文字 `D` によって両方のオペランドが強制的に `Decimal` になり、0.2 の表現は正確です。 したがって、`Mod` 演算子では、0.0 という予期される剰余が得られます。

`decimalRemainder` を `Decimal` として宣言するだけでは十分ではないことに注意してください。 また、リテラルを強制的に `Decimal` にする必要があります。そうしないと、`Double` が既定で使用され、`decimalRemainder` は `doubleRemainder` と同じ不正確な値を受け取ります。

## <a name="boolean-type-does-not-convert-to-numeric-type-accurately"></a>Boolean 型が数値型に正確に変換されない

[Boolean データ型](../../../language-reference/data-types/boolean-data-type.md)の値は数値として格納されず、格納された値は数値と等価であると見なされません。 以前のバージョンとの互換性のために、Visual Basic は変換キーワード ([CType 関数](../../../language-reference/functions/ctype-function.md)、`CBool`、`CInt` など) を使用して、`Boolean` と数値型の間で変換を行います。 ただし、その他の言語では、.NET Framework メソッドと同様に、これらの変換が異なる方法で実行されることがあります。

`True` と `False` に対して等価の数値に依存するコードを記述することは避けてください。 可能な限り、`Boolean` 変数には、仕様で定められている論理値以外の値を使用しないようにしてください。 `Boolean` 値と数値を混在させる必要がある場合は、選択する変換方法をよく理解してください。

### <a name="conversion-in-visual-basic"></a>Visual Basic での変換

`CType` または `CBool` の変換キーワードを使用して数値データ型を `Boolean` に変換するとき、0 が `False` になり、その他のすべての値が `True` になります。 変換キーワードを使用して `Boolean` 値を数値型に変換するとき、`False` は 0 になり、`True` は -1 になります。

### <a name="conversion-in-the-framework"></a>フレームワークでの変換

<xref:System> 名前空間の <xref:System.Convert> クラスの <xref:System.Convert.ToInt32%2A> メソッドによって、`True` が +1 に変換されます。

`Boolean` 値を数値データ型に変換する必要がある場合は、使用する変換方法に注意してください。

## <a name="character-literal-generates-compiler-error"></a>文字リテラルによってコンパイラ エラーが生成される

型文字が存在しない場合、Visual Basic によってリテラルの既定データ型と見なされます。 二重引用符 (`" "`) で囲まれた文字リテラルの既定型は `String` です。

`String` データ型は [Char データ型](../../../language-reference/data-types/char-data-type.md)に拡大変換されません。 つまり、`Char` 変数にリテラルを代入する場合は、縮小変換を行うか、リテラルを強制的に `Char` 型にする必要があります。

|変数または定数に代入する Char リテラルを作成するには|
|---|
|1.変数または定数を `Char` として宣言します。<br />2.文字値を二重引用符 `" "` で囲みます。<br />3.終わりの二重引用符の後にリテラルの型文字 `C` を指定して、リテラルを強制的に `Char` にします。 これは型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) が `On` の場合に必須ですが、どのような場合でもお勧めします。|

次の例では、`Char` 変数へのリテラルの代入の失敗と成功の両方を示します。

[!code-vb[VbVbalrDataTypes#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#12)]

縮小変換は実行時に失敗する可能性があるため、使用には常にリスクがあります。 たとえば、`String` から `Char` への変換が失敗する可能性があるのは、`String` 値に複数の文字が含まれている場合です。 そのため、`C` 型文字を使用する方が適切なプログラミングです。

## <a name="string-conversion-fails-at-run-time"></a>実行時に文字列変換が失敗する

[String データ型](../../../language-reference/data-types/string-data-type.md)は、非常に多くの拡大変換に関連します。 `String` はそれ自体と `Object` に拡大変換され、`Char` と `Char()` (`Char` 配列) のみが `String` に拡大変換されます。 これは、`String` の変数と定数には、他のデータ型に含めることができない値が含まれている可能性があるためです。

型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) が `On` のとき、コンパイラによって暗黙の縮小変換がすべて禁止されます。 これには、`String` に関係するものも含まれます。 .NET Framework が変換を試行するように指示する変換キーワード (`CStr` や [CType 関数](../../../language-reference/functions/ctype-function.md)など) をコードで引き続き使用できます。

> [!NOTE]
> `For Each…Next` コレクション内の要素からループ制御変数への変換では、縮小変換エラーが抑制されます。 詳細と例については、「[For Each...Next ステートメント](../../../language-reference/statements/for-each-next-statement.md)」の縮小変換に関するセクションを参照してください。

### <a name="narrowing-conversion-protection"></a>縮小変換の保護

縮小変換の欠点は、実行時にエラーが発生する可能性があることです。 たとえば、`String` 変数に "True" または "False" 以外が含まれる場合は、`Boolean` に変換できません。 区切り文字が含まれている場合は、どの数値型への変換も失敗します。 `String` 変数が、変換先の型で受け入れ可能な値を常に保持していることがわかっている場合を除き、変換を試行しないでください。

`String` から別のデータ型に変換する必要がある場合、最も安全な手順は、[Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)に変換の試行を含めることです。 これにより、実行時エラーに対処できます。

### <a name="character-arrays"></a>文字配列

1 つの `Char` および `Char` 要素の配列 1 つは、どちらも `String` に拡大変換されます。 ただし、`String` は `Char()` に拡大変換されません。 `String` 値を `Char` 配列に変換するには、<xref:System.String?displayProperty=nameWithType> クラスの <xref:System.String.ToCharArray%2A> メソッドを使用できます。

### <a name="meaningless-values"></a>意味のない値

一般に、`String` の値は他のデータ型では意味がなく、変換は非常に人為的で危険です。 可能な限り、`String` 変数には、仕様で定められている文字シーケンス以外の値を使用しないようにしてください。 他の型の等価の値に依存するコードを記述することは避けてください。

## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [型文字](type-characters.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
- [データ型の有効な使用方法](efficient-use-of-data-types.md)
