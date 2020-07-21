---
title: .NET での文字エンコードの概要
description: .NET での文字エンコーディング/デコーディングについて説明します。
ms.date: 03/09/2020
no-loc:
- Rune
- char
- string
dev_langs:
- csharp
helpviewer_keywords:
- encoding, understanding
ms.openlocfilehash: 85349e1e1c4eca4dd3ef7980f48350a4145fca24
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599868"
---
# <a name="character-encoding-in-net"></a>.NET での文字エンコード

この記事では、.NET で使用される文字エンコード システムの概要について説明します。 この記事では、<xref:System.String>、<xref:System.Char>、<xref:System.Text.Rune>、および <xref:System.Globalization.StringInfo> 型が Unicode、UTF-16、および UTF-8 でどのように動作するかについて説明します。

ここでは、"*文字*" という用語が "*読者が 1 つの表示要素として認識するもの*" という全般的な意味で使用されます。 一般的な例としては、文字 "a"、記号 "@"、絵文字 "🐂" などがあります。 場合によっては、1 つの文字に見えるものが、[書記素クラスター](#grapheme-clusters)に関するセクションで説明しているように、実際には複数の独立した表示要素で構成されていることがあります。

## <a name="the-string-and-char-types"></a>string 型と char 型

[string](xref:System.String) クラスのインスタンスは、何らかのテキストを表します。 `string` は、論理的には 16 ビット値のシーケンスであり、そのそれぞれが [char](xref:System.Char) 構造体のインスタンスです。 [string.Length](xref:System.String.Length) プロパティでは、`string` インスタンスに含まれる `char` インスタンスの数が返されます。

次のサンプル関数では、`string` に含まれるすべての `char` インスタンスの 16 進表記の値が出力されます。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/PrintStringChars.cs" id="SnippetPrintChars":::

この関数に string "Hello" を渡すと、次の出力が得られます。

```csharp
PrintChars("Hello");
```

```output
"Hello".Length = 5
s[0] = 'H' ('\u0048')
s[1] = 'e' ('\u0065')
s[2] = 'l' ('\u006c')
s[3] = 'l' ('\u006c')
s[4] = 'o' ('\u006f')
```

各文字は、1 つの `char` 値で表されます。 このパターンは、世界のほとんどの言語に当てはまります。 たとえば、*nǐ hǎo* のように発音し "*こんにちは*" を意味する中国語の 2 文字に対する出力を次に示します。

```csharp
PrintChars("你好");
```

```output
"你好".Length = 2
s[0] = '你' ('\u4f60')
s[1] = '好' ('\u597d')
```

ただし、一部の言語および一部の記号と絵文字については、1 つの文字を表すために 2 つの `char` インスタンスが必要です。 たとえば、オセージ語で "*オセージ*" を表す単語に含まれる文字と `char` インスタンスを比較してください。

```csharp
PrintChars("𐓏𐓘𐓻𐓘𐓻𐓟 𐒻𐓟");
```

```output
"𐓏𐓘𐓻𐓘𐓻𐓟 𐒻𐓟".Length = 17
s[0] = '�' ('\ud801')
s[1] = '�' ('\udccf')
s[2] = '�' ('\ud801')
s[3] = '�' ('\udcd8')
s[4] = '�' ('\ud801')
s[5] = '�' ('\udcfb')
s[6] = '�' ('\ud801')
s[7] = '�' ('\udcd8')
s[8] = '�' ('\ud801')
s[9] = '�' ('\udcfb')
s[10] = '�' ('\ud801')
s[11] = '�' ('\udcdf')
s[12] = ' ' ('\u0020')
s[13] = '�' ('\ud801')
s[14] = '�' ('\udcbb')
s[15] = '�' ('\ud801')
s[16] = '�' ('\udcdf')
```

前の例では、空白を除く各文字が 2 つの `char` インスタンスによって表されています。

また、雄牛の絵文字を表す次の例で示すように、1 つの Unicode 絵文字も 2 つの `char` によって表されます。

```
"🐂".Length = 2
s[0] = '�' ('\ud83d')
s[1] = '�' ('\udc02')
```

これらの例では、`char` インスタンスの数を示す `string.Length` の値が、必ずしも表示される文字数を示していないことがわかります。 1 つの `char` インスタンスは、必ずしもそれ自体で 1 文字を表すとは限りません。

1 つの文字にマップされる `char` のペアは、"*サロゲート ペア*" と呼ばれます。 それらがどのように動作するかを理解するには、Unicode と UTF-16 のエンコードについて理解する必要があります。

## <a name="unicode-code-points"></a>Unicode コード ポイント

Unicode は、さまざまなプラットフォーム上で、さまざまな言語とスクリプトで使用するための国際エンコード標準です。

Unicode 標準では、110 万個を超える[コード ポイント](https://www.unicode.org/glossary/#code_point)が定義されています。 コード ポイントは、0 から `U+10FFFF` (10 進数の 1,114,111) までの範囲の整数値です。 一部のコード ポイントは、文字、記号、または絵文字に割り当てられています。 その他は、新しい行に進むなど、テキストや文字の表示方法を制御するアクションに割り当てられています。 多くのコード ポイントはまだ割り当てられていません。

コード ポイントの割り当てのいくつかの例と、それらが記載されている Unicode 表へのリンクを次に示します。

|Decimal (10 進数型)|Hex       |例|説明|
|------:|----------|-------|-----------|
|10     | `U+000A` |N/A| [改行](https://www.unicode.org/charts/PDF/U0000.pdf) |
|65     | `U+0061` | a | [ラテン小文字 A](https://www.unicode.org/charts/PDF/U0000.pdf) |
|562    | `U+0232` | Ȳ | [長音符号付きラテン大文字 Y](https://www.unicode.org/charts/PDF/U0180.pdf) |
|68,675 | `U+10C43`| 𐱃 | [古テュルク語文字オルホン AT](https://www.unicode.org/charts/PDF/U10C00.pdf) |
|127,801| `U+1F339`| 🌹 | [バラの絵文字](https://www.unicode.org/charts/PDF/U1F300.pdf) |

コード ポイントは、習慣的に、`U+xxxx` 構文を使用して参照されます。`xxxx` は 16 進エンコードの整数値です。

コード ポイントの全範囲内には、次の 2 つの部分範囲があります。

* `U+0000..U+FFFF` の範囲の**基本多言語面 (BMP)** 。 この 16 ビットの範囲によって 65,536 個のコード ポイントが提供され、世界の書記体系の大部分を十分にカバーできます。
* `U+10000..U+10FFFF` の範囲の**補助コード ポイント**。 この 21 ビットの範囲によって、100 万個を超える追加のコード ポイントが提供されます。これは、あまり一般的ではない言語や、絵文字などのその他の目的のために使用できます。

次の図は、BMP と補助コード ポイントの関係を示しています。

:::image type="content" source="media/character-encoding-introduction/bmp-and-supplementary.svg" alt-text="BMP と補助コード ポイント":::

## <a name="utf-16-code-units"></a>UTF-16 コード単位

16 ビット Unicode Transformation Format ([UTF-16](https://www.unicode.org/faq/utf_bom.html#UTF16)) は、16 ビットの "*コード単位*" を使用して Unicode コード ポイントを表す、文字エンコード システムです。 .NET では、`string` 内のテキストをエンコードするために UTF-16 が使用されています。 `char` インスタンスは、16 ビットのコード単位を表します。

1 つの 16 ビット コード単位は、基本多言語面の 16 ビット範囲に含まれる任意のコード ポイントを表すことができます。 ただし、補助範囲内のコード ポイントについては、2 つの `char` インスタンスが必要です。

## <a name="surrogate-pairs"></a>サロゲート ペア

2 つの 16 ビット値から 1 つの 21 ビット値への変換は、`U+D800` から `U+DFFF` (10 進数の 55,296 から 57,343) まで (境界も含める) の、"*サロゲート コード ポイント*" と呼ばれる特殊な範囲を使用して行われます。

次の図は、BMP とサロゲート コード ポイントの関係を示しています。

:::image type="content" source="media/character-encoding-introduction/bmp-and-surrogate.svg" alt-text="BMP とサロゲート コード ポイント":::

"*上位サロゲート*" コード ポイント (`U+D800..U+DBFF`) の直後に "*下位サロゲート*" コード ポイント (`U+DC00..U+DFFF`) が続く場合、そのペアは、次の数式を使用して補助コード ポイントとして解釈されます。

```
code point = 0x10000 +
  ((high surrogate code point - 0xD800) * 0x0400) +
  (low surrogate code point - 0xDC00)
```

10 進表記を使用した同じ数式を次に示します。

```
code point = 65,536 +
  ((high surrogate code point - 55,296) * 1,024) +
  (low surrogate code point - 56,320)
```

"*上位*" サロゲート コード ポイントには、"*下位*" サロゲート コード ポイントよりも大きい数値は含まれません。 上位サロゲート コード ポイントが "上位" と呼ばれる理由は、完全な 21 ビットのコード ポイント範囲の上位 11 ビットを計算するために使用されるからです。 下位サロゲート コード ポイントは、下位 10 ビットを計算するために使用されます。

たとえば、サロゲート ペア `0xD83C` と `0xDF39` に対応する実際のコード ポイントは、次のように計算されます。

```
actual = 0x10000 + ((0xD83C - 0xD800) * 0x0400) + (0xDF39 - 0xDC00)
       = 0x10000 + (          0x003C  * 0x0400) +           0x0339
       = 0x10000 +                      0xF000  +           0x0339
       = 0x1F339
```

10 進表記を使用した同じ計算を次に示します。

```
actual =  65,536 + ((55,356 - 55,296) * 1,024) + (57,145 - 56320)
       =  65,536 + (              60  * 1,024) +             825
       =  65,536 +                     61,440  +             825
       = 127,801
```

前の例では、`"\ud83c\udf39"` が、前述の `U+1F339 ROSE ('🌹')` コード ポイントの UTF-16 エンコードであることが示されています。

## <a name="unicode-scalar-values"></a>Unicode スカラー値

[Unicode スカラー値](https://www.unicode.org/glossary/#unicode_scalar_value)という用語は、サロゲート コード ポイント以外のすべてのコード ポイントを指します。 つまり、スカラー値とは、文字が割り当てられているか、将来文字が割り当てられる可能性があるコード ポイントです。 ここでの "文字" は、コード ポイントに割り当てることができるすべてのものを指します。これには、テキストや文字の表示方法を制御するアクションなどが含まれます。

次の図は、スカラー値のコード ポイントを示しています。

:::image type="content" source="media/character-encoding-introduction/scalar-values.svg" alt-text="スカラー値":::

### <a name="the-rune-type-as-a-scalar-value"></a>スカラー値としての Rune 型

.NET Core 3.0 以降では、<xref:System.Text.Rune?displayProperty=fullName> 型によって Unicode スカラー値が表されます。 **`Rune` は、.NET Core 2.x または .NET Framework 4.x では使用できません。**

`Rune` コンストラクターでは、生成されるインスタンスが有効な Unicode スカラー値であることが検証されます。そうでない場合は、例外がスローされます。 次の例は、`Rune` インスタンスのインスタンス化に成功するコードを示しています。入力が有効なスカラー値を表しているためです。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/InstantiateRunes.cs" id="SnippetValid":::

次の例では、例外がスローされます。コード ポイントがサロゲートの範囲内にあり、サロゲート ペアの一部ではないためです。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/InstantiateRunes.cs" id="SnippetInvalidSurrogate":::

次の例では、コード ポイントが補助範囲を超えているため、例外がスローされます。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/InstantiateRunes.cs" id="SnippetInvalidHigh":::

### <a name="rune-usage-example-changing-letter-case"></a>Rune の使用例: 大文字と小文字の変更

`char` を受け取り、スカラー値であるコード ポイントを操作していると仮定する API は、その `char` がサロゲート ペアのものであった場合、正しく動作しません。 たとえば、string に含まれる各 char に対して <xref:System.Char.ToUpperInvariant%2A?displayProperty=nameWithType> を呼び出す、次のようなメソッドを考えてみます。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetBadExample":::

`input` string に小文字のデザレット文字 `er` (`𐑉`) が含まれていた場合、このコードでは大文字 (`𐐡`) に変換することができません。 このコードでは、`U+D801` と `U+DC49` の各サロゲート コード ポイントに対して、個別に `char.ToUpperInvariant` が呼び出されます。 しかし、`U+D801` 自体には、それを小文字として識別するのに十分な情報が含まれていないため、`char.ToUpperInvariant` による変更は行われません。 また、`U+DC49` も同じ方法で処理されます。 その結果、`input` string に含まれる小文字の '𐑉' は、大文字の '𐐡' に変換されません。

string を適切に大文字に変換するための 2 つのオプションを次に示します。

* `char` から `char` へと反復処理するのではなく、入力 string に対して <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> を呼び出します。 `string.ToUpperInvariant` メソッドは各サロゲート ペアの両方の部分にアクセスできるため、すべての Unicode コード ポイントを正しく処理できます。
* 次の例に示すように、`char` インスタンスではなく `Rune` インスタンスとして Unicode スカラー値を反復処理します。 `Rune` インスタンスは有効な Unicode スカラー値であるため、スカラー値に対して動作することが想定されている API に渡すことができます。 たとえば、次の例に示すように <xref:System.Text.Rune.ToUpperInvariant%2A?displayProperty=nameWithType> を呼び出すと、正しい結果が得られます。

  :::code language="csharp" source="snippets/character-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetGoodExample":::

### <a name="other-rune-apis"></a>その他の Rune API

`Rune` 型では、多くの `char` API と類似した機能が公開されています。 たとえば、以下のメソッドは、`char` 型の静的 API に対応しています。

* <xref:System.Text.Rune.IsLetter%2A?displayProperty=nameWithType>
* <xref:System.Text.Rune.IsWhiteSpace%2A?displayProperty=nameWithType>
* <xref:System.Text.Rune.IsLetterOrDigit%2A?displayProperty=nameWithType>
* <xref:System.Text.Rune.GetUnicodeCategory%2A?displayProperty=nameWithType>

`Rune` インスタンスから生のスカラー値を取得するには、<xref:System.Text.Rune.Value%2A?displayProperty=nameWithType> プロパティを使用します。

`Rune` インスタンスを再び `char` のシーケンスに変換するには、<xref:System.Text.Rune.ToString%2A?displayProperty=nameWithType> または <xref:System.Text.Rune.EncodeToUtf16%2A?displayProperty=nameWithType> メソッドを使用します。

すべての Unicode スカラー値は 1 つの `char` またはサロゲート ペアによって表すことができるため、あらゆる `Rune` インスタンスは多くても 2 つの `char` インスタンスによって表すことができます。 `Rune` インスタンスを表すために必要な `char` インスタンスの数を確認するには、<xref:System.Text.Rune.Utf16SequenceLength%2A?displayProperty=nameWithType> を使用します。

.NET の `Rune` 型の詳細については、[`Rune` API リファレンス](xref:System.Text.Rune)を参照してください。

## <a name="grapheme-clusters"></a>書記素クラスター

1 つの文字に見えるものが、複数のコード ポイントの組み合わせから生成されている場合があります。このため、"文字" の代わりに使用されることが多い、[書記素クラスター](https://www.unicode.org/glossary/#grapheme_cluster)というよりわかりやすい用語があります。 .NET における同等の用語は、[テキスト要素](xref:System.Globalization.StringInfo.GetTextElementEnumerator%2A)です。

次の `string` インスタンスについて考えてみましょう: "a"、"á"。 "á"、"`👩🏽‍🚒`"。 お使いのオペレーティング システムによってこれらが Unicode 標準で指定されているとおりに処理される場合、これらの各 `string` インスタンスは、1 つのテキスト要素、または書記素クラスターとして表示されます。 ただし、最後の 2 つは、複数のスカラー値コード ポイントによって表されます。

* string "a" は 1 つのスカラー値で表され、1 つの `char` インスタンスが含まれます。

  * `U+0061 LATIN SMALL LETTER A`

* string "á" は 1 つのスカラー値で表され、1 つの `char` インスタンスが含まれます。

  * `U+00E1 LATIN SMALL LETTER A WITH ACUTE`

* string "á" は、"á" と同じように見えますが、2 つのスカラー値で表され、2 つの `char` インスタンスが含まれます。

  * `U+0061 LATIN SMALL LETTER A`
  * `U+0301 COMBINING ACUTE ACCENT`

* 最後に、string "`👩🏽‍🚒`" は 4 つのスカラー値で表され、7 つの `char` インスタンスが含まれます。

  * `U+1F469 WOMAN` (補助範囲、サロゲート ペアが必要)
  * `U+1F3FD EMOJI MODIFIER FITZPATRICK TYPE-4` (補助範囲、サロゲート ペアが必要)
  * `U+200D ZERO WIDTH JOINER`
  * `U+1F692 FIRE ENGINE` (補助範囲、サロゲート ペアが必要)

前の例の一部 (結合アクセントの修飾子や肌の色の修飾子など) では、コード ポイントが画面にスタンドアロン要素として表示されません。 代わりに、それは、その前に現れるテキスト要素の外観を変更する役割を果たしています。 これらの例は、1 つの "文字" または "書記素クラスター" と見なされるものを構成するために、複数のスカラー値が必要になる場合があることを示しています。

`string` の書記素クラスターを列挙するには、次の例に示すように <xref:System.Globalization.StringInfo> クラスを使用します。 Swift に慣れている場合、.NET の `StringInfo` 型は、概念的に [Swift の `character` 型](https://developer.apple.com/documentation/swift/character)と似ています。

### <a name="example-count-char-rune-and-text-element-instances"></a>例: char、Rune、テキスト要素のインスタンス数を数える

.NET API では、書記素クラスターは "*テキスト要素*" と呼ばれます。 次のメソッドは、`string` に含まれる `char`、`Rune`、およびテキスト要素のインスタンスの違いを示しています。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCountMethod":::

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCallCountMethod":::

.NET Framework または .NET Core 3.1 以前でこのコードを実行すると、絵文字のテキスト要素の数として `4` が表示されます。 これは、.NET 5 で修正されている `StringInfo` クラスのバグが原因です。

### <a name="example-splitting-string-instances"></a>例: string インスタンスの分割

`string` インスタンスを分割する場合は、サロゲート ペアと書記素クラスターを分割しないようにします。 不適切なコードを示す次の例について考えてみましょう。ここでは、string 内の 10 文字ごとに改行を挿入しようとしています。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetBadExample":::

このコードでは `char` インスタンスが列挙されているため、10-`char` の境界にまたがるサロゲート ペアは分割され、それらの間に改行が挿入されます。 サロゲート コード ポイントはペアとしてのみ意味があるので、この挿入によってデータの破損が発生します。

データの破損の可能性は、`char` インスタンスではなく `Rune` インスタンス (スカラー値) を列挙してもなくなりません。 `Rune` インスタンスのセットによって、10-`char` の境界にまたがる書記素クラスターが構成される可能性があります。 書記素クラスターのセットが分割された場合は、正しく解釈できません。

より適切なアプローチは、次の例のように、書記素クラスター (またはテキスト要素) をカウントすることによって string を分割することです。

:::code language="csharp" source="snippets/character-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetGoodExample":::

ただし、前述のように、.NET 5 以外の .NET の実装では、`StringInfo` クラスによって一部の書記素クラスターが不適切に処理される可能性があります。

## <a name="utf-8-and-utf-32"></a>UTF-8 と UTF-32

前のセクションでは、UTF-16 に焦点を当てました。 .NET では `string` インスタンスをエンコードするために UTF-16 が使用されるためです。 Unicode には、他のエンコード システムもあります: [UTF-8](https://www.unicode.org/faq/utf_bom.html#UTF8) と [UTF-32](https://www.unicode.org/faq/utf_bom.html#UTF32) です。 これらのエンコードでは、8 ビットのコード単位と 32 ビットのコード単位がそれぞれ使用されます。

UTF-16 と同様に、UTF-8 では、一部の Unicode スカラー値を表すために複数のコード単位が必要になります。 UTF-32 では、1 つの 32 ビット コード単位で任意のスカラー値を表すことができます。

これら 3 つの各 Unicode エンコード システムで、同じ Unicode コード ポイントがどのように表されるかを示すいくつかの例を次に示します。

```
Scalar: U+0061 LATIN SMALL LETTER A ('a')
UTF-8 : [ 61 ]           (1x  8-bit code unit  = 8 bits total)
UTF-16: [ 0061 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 00000061 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+0429 CYRILLIC CAPITAL LETTER SHCHA ('Щ')
UTF-8 : [ D0 A9 ]        (2x  8-bit code units = 16 bits total)
UTF-16: [ 0429 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 00000429 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+A992 JAVANESE LETTER GA ('ꦒ')
UTF-8 : [ EA A6 92 ]     (3x  8-bit code units = 24 bits total)
UTF-16: [ A992 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 0000A992 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+104CC OSAGE CAPITAL LETTER TSHA ('𐓌')
UTF-8 : [ F0 90 93 8C ]  (4x  8-bit code units = 32 bits total)
UTF-16: [ D801 DCCC ]    (2x 16-bit code units = 32 bits total)
UTF-32: [ 000104CC ]     (1x 32-bit code unit  = 32 bits total)
```

前述のように、[サロゲート ペア](#surrogate-pairs)に由来する 1 つの UTF-16 コード単位は、単独では意味がありません。 同様に、1 つの UTF-8 コード単位が、スカラー値の計算に使用される 2 つ、3 つ、または 4 つのシーケンスに含まれている場合、それは単独では意味がありません。

### <a name="endianness"></a>エンディアン

.NET では、string の UTF-16 コード単位は、16 ビット整数 (`char` インスタンス) のシーケンスとして連続したメモリに格納されます。 個々のコード単位のビットは、現在のアーキテクチャの[エンディアン](https://en.wikipedia.org/wiki/Endianness)に従って並べられます。

リトル エンディアンのアーキテクチャでは、UTF-16 コード ポイント `[ D801 DCCC ]` で構成される string は、バイト `[ 0x01, 0xD8, 0xCC, 0xDC ]` としてメモリ内に並べられます。 ビッグ エンディアンのアーキテクチャでは、同じ string がバイト `[ 0xD8, 0x01, 0xDC, 0xCC ]` としてメモリ内に並べられます。

相互に通信するコンピューター システムは、ネットワークを通過するデータの表現方法を一致させる必要があります。 ほとんどのネットワーク プロトコルでは、テキストの送信時に UTF-8 が標準として使用されます。その理由の一部は、ビッグ エンディアンのコンピューターがリトル エンディアンのコンピューターと通信する際に発生する可能性のある問題を回避するためです。 UTF-8 コード ポイント `[ F0 90 93 8C ]` で構成される string は、エンディアンに関係なく常にバイト `[ 0xF0, 0x90, 0x93, 0x8C ]` として表されます。

UTF-8 を使用してテキストを送信する場合、.NET アプリケーションでは、次の例のようなコードが使用されることがよくあります。

```csharp
string stringToWrite = GetString();
byte[] stringAsUtf8Bytes = Encoding.UTF8.GetBytes(stringToWrite);
await outputStream.WriteAsync(stringAsUtf8Bytes, 0, stringAsUtf8Bytes.Length);
```

前の例では、メソッド [Encoding.UTF8.GetBytes](xref:System.Text.UTF8Encoding.GetBytes%2A) によって UTF-16 の `string` が一連の Unicode スカラー値にデコードされ、そのスカラー値が UTF-8 に再エンコードされて、生成されたシーケンスが `byte` の配列に配置されます。 メソッド [Encoding.UTF8.GetString](xref:System.Text.UTF8Encoding.GetString%2A) では反対の変換が実行されます。つまり、UTF-8 の `byte` 配列が UTF-16 の `string` に変換されます。

> [!WARNING]
> インターネット上では UTF-8 が一般的であるため、ネットワークから生バイトを読み取り、そのデータを UTF-8 であるかのように扱いたくなる場合があります。 しかし、それが本当に適切な形式であることを検証する必要があります。 悪意のあるクライアントが、あなたのサービスに不適切な形式の UTF-8 を送信する可能性があります。 そのデータが適切な形式であるかのように操作された場合、アプリケーションにエラーやセキュリティ ホールが発生する可能性があります。 UTF-8 のデータを検証するには、`Encoding.UTF8.GetString` のようなメソッドを使用できます。これは、受信データを `string` に変換するときに検証を実行します。

### <a name="well-formed-encoding"></a>適切な形式のエンコード

適切な形式の Unicode エンコードとは、明確に、かつエラーなしで Unicode スカラー値のシーケンスにデコードできる、コード単位の string のことです。 適切な形式のデータは、UTF-8、UTF-16、および UTF-32 間で自由にトランスコードできます。

あるエンコード シーケンスが適切な形式であるかどうかは、コンピューターのアーキテクチャのエンディアンには関係ありません。 不適切な形式の UTF-8 シーケンスは、ビッグ エンディアンのコンピューターでもリトル エンディアンのコンピューターでも、同じように不適切な形式になります。

不適切な形式のエンコードの例を、次にいくつか示します。

* UTF-8 では、シーケンス `[ 6C C2 61 ]` は不適切な形式です。`C2` の後に `61` を配置することはできないためです。

* UTF-16 では、シーケンス `[ DC00 DD00 ]` (または、C# では、string `"\udc00\udd00"`) は不適切な形式です。下位サロゲート `DC00` の後に別の下位サロゲート `DD00` を配置することはできないためです。

* UTF-32 では、シーケンス `[ 0011ABCD ]` は不適切な形式です。`0011ABCD` が Unicode スカラー値の範囲外であるためです。

.NET では、`string` インスタンスにはほとんど常に適切な形式の UTF-16 データが含まれますが、保証されているわけではありません。 `string` インスタンス内に不適切な形式の UTF-16 データを作成する有効な C# コードを、次の例に示します。

* 不適切な形式のリテラル:

  ```csharp
  const string s = "\ud800";
  ```

* サロゲート ペアを分割する部分文字列:

  ```csharp
  string x = "\ud83e\udd70"; // "🥰"
  string y = x.Substring(1, 1); // "\udd70" standalone low surrogate
  ```

[`Encoding.UTF8.GetString`](xref:System.Text.UTF8Encoding.GetString%2A) のような API を使用する場合、不適切な形式の `string` インスタンスが返されることはありません。 `Encoding.GetString` および `Encoding.GetBytes` メソッドでは、入力に含まれる不適切な形式のシーケンスが検出され、出力を生成する際に文字の置換が実行されます。 たとえば、[`Encoding.ASCII.GetString(byte[])`](xref:System.Text.ASCIIEncoding.GetString%2A) への入力に非 ASCII バイト (U+0000..U+007F の範囲外) が含まれていた場合、返される `string` インスタンスには '?' が挿入されます。 [`Encoding.UTF8.GetString(byte[])`](xref:System.Text.UTF8Encoding.GetString%2A) によって返される `string` インスタンスでは、不適切な形式の UTF-8 シーケンスが `U+FFFD REPLACEMENT CHARACTER ('�')` に置き換えられます。 詳細については、[Unicode 標準](https://www.unicode.org/versions/latest/)の、セクション 5.22 および 3.9 を参照してください。

組み込みの `Encoding` クラスは、不適切な形式のシーケンスが検出されたときに、文字の置換を実行するのではなく、例外をスローするように構成することもできます。 この方法は、文字の置換が受け入れられない可能性がある、セキュリティに影響するアプリケーションでよく使用されます。

```csharp
byte[] utf8Bytes = ReadFromNetwork();
UTF8Encoding encoding = new UTF8Encoding(encoderShouldEmitUTF8Identifier: false, throwOnInvalidBytes: true);
string asString = encoding.GetString(utf8Bytes); // will throw if 'utf8Bytes' is ill-formed
```

組み込みの `Encoding` クラスの使用方法について詳しくは、「[.NET で文字エンコーディング クラスを使用する方法](character-encoding.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- <xref:System.String>
- <xref:System.Char>
- <xref:System.Text.Rune>
- [グローバライズとローカライズ](../globalization-localization/index.md)
