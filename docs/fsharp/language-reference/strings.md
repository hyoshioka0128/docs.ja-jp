---
title: 文字列
description: F# 'string' 型が、不変のテキストを Unicode 文字のシーケンスとして表す方法について説明します。
ms.date: 07/05/2019
ms.openlocfilehash: 242a2cefa1cce8995090dddd1d1fd7181e0f5e0c
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739571"
---
# <a name="strings"></a>文字列

> [!NOTE]
> この記事の API リファレンスのリンクをクリックすると MSDN に移動します。  docs.microsoft.com API リファレンスは完全ではありません。

この`string`型は、変更できないテキストを Unicode 文字のシーケンスとして表します。 `string` は、.NET Framework の `System.String` のエイリアスです。

## <a name="remarks"></a>解説

文字列リテラルは、引用符 (") 文字で区切られます。 円記号 ( \\ ) は、特定の特殊文字をエンコードするために使用されます。 バックスラッシュと次の文字はエスケープシーケンスと呼*ばれます*。 F# 文字列リテラルでサポートされているエスケープ シーケンスを次の表に示します。

|文字|エスケープ シーケンス|
|---------|---------------|
|アラート:|`\a`|
|バックスペース|`\b`|
|改ページ|`\f`|
|改行|`\n`|
|キャリッジ リターン|`\r`|
|タブ|`\t`|
|垂直タブ|`\v`|
|円記号|`\\`|
|引用符|`\"`|
|アポストロフィ|`\'`|
|Unicode 文字|`\DDD`(ここで`D`、10 進数、000 から 255 の範囲`\231`、たとえば、="ç")|
|Unicode 文字|`\xHH`(ここで`H`、16 進数を示し、範囲は 00 から`\xE7`FF、例えば、"ç")|
|Unicode 文字|`\uHHHH`(UTF-16)(ここで`H`、16 進数を示し、0000 から FFFF の範囲を示します。 たとえば、="ç") `\u00E7`|
|Unicode 文字|`\U00HHHHHH`(UTF-32)(ここで`H`、16 進数を示し、000000 から 10FFFF の範囲を示します。 たとえば、= `\U0001F47D` "👽" "|

> [!IMPORTANT]
> `\DDD`エスケープ シーケンスは 10 進数表記であり、他のほとんどの言語のように 8 進数表記ではありません。 したがって、数字`8`と`9`は有効であり、シーケンスは`\032`スペース(U+0020)を表しますが、8 進数表記の同じコードポイントは`\040`.

> [!NOTE]
> 0 ~ 255 (0xFF) の範囲に`\DDD`制約`\x`されているエスケープ シーケンスとエスケープ シーケンスは、最初の 256 個の Unicode コード ポイントと一致するため、実質的には[ISO-8859-1](https://en.wikipedia.org/wiki/ISO/IEC_8859-1#Code_page_layout)文字セットになります。

## <a name="verbatim-strings"></a>逐語的な文字列

@ 記号が前に付いている場合、リテラルは逐語的な文字列です。 これは、2 つの引用符文字が 1 つの引用符文字として解釈されることを除いて、エスケープ・シーケンスはすべて無視されることを意味します。

## <a name="triple-quoted-strings"></a>三重引用符文字列

また、文字列は三重引用符で囲む場合があります。 この場合、二重引用符文字を含め、すべてのエスケープ・シーケンスは無視されます。 埋め込み引用符付き文字列を含む文字列を指定するには、逐語的文字列または三重引用符で囲まれた文字列を使用できます。 逐語的文字列を使用する場合は、単一引用符文字を示す 2 つの引用符文字を指定する必要があります。 三重引用符で囲まれた文字列を使用する場合は、文字列の末尾として解析されずに単一引用符文字を使用できます。 この方法は、XML や、引用符が埋め込まれた他の構造を操作する場合に役立ちます。

```fsharp
// Using a verbatim string
let xmlFragment1 = @"<book author=""Milton, John"" title=""Paradise Lost"">"

// Using a triple-quoted string
let xmlFragment2 = """<book author="Milton, John" title="Paradise Lost">"""
```

コードでは、改行のある文字列は受け入れられ、改行文字は改行前の最後の文字でない限り、改行文字は改行として解釈されます。 円記号文字を使用する場合、次の行の先頭の空白は無視されます。 次のコードは、値`str1`を持つ`"abc\ndef"`文字列と値`str2`を持つ`"abcdef"`文字列を生成します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1001.fs)]

## <a name="string-indexing-and-slicing"></a>文字列のインデックス作成とスライス

次のように、配列のような構文を使用して、文字列内の個々の文字にアクセスできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1002.fs)]

出力は `b`になります。

または、次のコードに示すように、配列スライス構文を使用して部分文字列を抽出できます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1003.fs)]

出力は次のとおりです。

```console
abc
def
```

ASCII 文字列は、符号なしバイトの配列で表すことができます`byte[]`。 文字列リテラルにサフィックス`B`を追加して、それが ASCII 文字列であることを示します。 バイト配列で使用される ASCII 文字列リテラルは、Unicode エスケープ シーケンスを除き、Unicode 文字列と同じエスケープ シーケンスをサポートします。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1004.fs)]

## <a name="string-operators"></a>文字列演算子

この`+`演算子を使用して文字列を連結し、.NET Framework の文字列処理機能との互換性を維持できます。 次の例は、文字列の連結を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1006.fs)]

## <a name="string-class"></a>文字列クラス

F# の文字列型は実際には .NET `System.String` Framework 型であるため`System.String`、すべてのメンバーが使用できます。 これには、文字列`+`を連結するために使用される演算子、`Length`プロパティ、および Unicode 文字の`Chars`配列として文字列を返すプロパティが含まれます。 文字列の詳細については、を参照`System.String`してください。

のプロパティを`Chars`使用すると`System.String`、次のコードに示すように、インデックスを指定して文字列内の個々の文字にアクセスできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1005.fs)]

## <a name="string-module"></a>文字列モジュール

文字列処理の追加機能は、名前空間の`String`モジュールに`FSharp.Core`含まれています。 詳細については、「 [Core.String モジュール](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.string-module-%5bfsharp%5d)」を参照してください。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
