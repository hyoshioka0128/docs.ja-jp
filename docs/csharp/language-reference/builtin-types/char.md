---
title: char 型 - C# リファレンス
ms.date: 11/22/2019
f1_keywords:
- char
- char_CSharpKeyword
helpviewer_keywords:
- char data type [C#]
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
ms.openlocfilehash: ab49b8cbddac2569d6063a5f312105bef3033e84
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74552299"
---
# <a name="char-c-reference"></a>char (C# リファレンス)

`char` 型のキーワードは、Unicode UTF-16 文字を表す .NET <xref:System.Char?displayProperty=nameWithType> 構造体型のエイリアスです。

|型|範囲|サイズ|.NET 型|
|----------|-----------|----------|-------------------------|
|`char`|U+0000 ～ U+FFFF|16 ビット|<xref:System.Char?displayProperty=nameWithType>|

`char` 型の既定値は `\0` (つまり U+0000) です。

[string](reference-types.md#the-string-type) 型では、`char` 値のシーケンスとしてテキストを表わします。

## <a name="literals"></a>リテラル

`char` 値は以下で指定できます。

- 文字リテラル。
- Unicode エスケープシーケンス。これは `\u` の後に文字コードの 16 進数表現 (4 つの記号) を続けたものになります。
- 16 進数エスケープシーケンス。これは `\x` の後に文字コードの 16 進数表現を続けたものになります。

[!code-csharp-interactive[char literals](~/samples/csharp/language-reference/builtin-types/CharType.cs#Literals)]

前の例のように、文字コードの値をそれに対応する `char` 値に型変換することもできます。

> [!NOTE]
> Unicode エスケープ シーケンスの場合、4 つの 16 進数をすべて指定する必要があります。 つまり、`\u006A` は有効なエスケープ シーケンスであり、`\u06A` と `\u6A` は有効ではありません。
>
> 16 進数エスケープ シーケンスの場合、先頭のゼロを省略できます。 つまり、エスケープ シーケンスの `\x006A`、`\x06A`、`\x6A` は有効であり、同じ文字に対応します。

## <a name="conversions"></a>変換

`char` 型は、[整数](integral-numeric-types.md)型 (`ushort`、`int`、`uint`、`long`、`ulong`) に暗黙的に変換できます。 また、組み込みの[浮動小数点](floating-point-numeric-types.md)数値型 (`float`、`double`、`decimal`) に暗黙的に変換することもできます。 `sbyte`、`byte`、`short` 整数型に明示的に変換できます。

他の型から `char` 型へと暗黙的に変換することはできません。 しかし、[整数](integral-numeric-types.md)または[浮動小数点](floating-point-numeric-types.md)の数値型は、`char` に明示的に変換できます。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の[整数型](~/_csharplang/spec/types.md#integral-types)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [組み込み型の一覧表](../keywords/built-in-types-table.md)
- [文字列](../../programming-guide/strings/index.md)
