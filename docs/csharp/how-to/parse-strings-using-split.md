---
title: String.Split を使用して文字列を解析する (C# ガイド)
description: Split メソッドは、一連の区切り記号で分割された文字列の配列を返します。 文字列を解析する簡単な方法です。
ms.date: 01/03/2018
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
ms.custom: mvc
ms.openlocfilehash: 7c5d8fa462775c6f3a9981693129997dda6c2286
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324140"
---
# <a name="how-to-parse-strings-using-stringsplit-in-c"></a>C\# で String.Split を使用して文字列を解析する方法

<xref:System.String.Split%2A?displayProperty=nameWithType> メソッドは、1 つまたは複数の区切り記号に基づいて入力文字列を分割することで部分文字列の配列を作成します。 このメソッドは、英語のように単語の間にスペースがある文章の場合に、単語の境界で文字列を分割する最も簡単な方法になります。 他の特定の文字や文字列で文字列を分割する際にも利用されます。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

次のコードは一般的なフレーズを単語ごとの文字列の配列に分割します。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet1":::

区切り文字のインスタンスごとに、返される配列で値が生成されます。 連続する区切り文字により、返される配列の値として空の文字列が生成されます。 空白文字を区切り記号として使用する次の例では、空の文字列がどのように作成されるかを確認できます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet2":::

この動作により、コンマ区切り値 (CSV) ファイルなどの形式で表形式データを簡単に表すことができます。 連続するコンマは空の列を表します。

任意の <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> パラメーターを渡し、返される配列で空の文字列を除外できます。 返されるコレクションの処理が複雑な場合、[LINQ](../programming-guide/concepts/linq/index.md) を使用し、結果のシーケンスを操作できます。

<xref:System.String.Split%2A?displayProperty=nameWithType> では、複数の区切り文字を使用できます。
次の例ではスペース、コンマ、ピリオド、コロン、タブを区切り文字として使用しています。これらは配列で <xref:System.String.Split%2A> に渡されます。
コードの一番下にあるループは、返される配列の各単語を表示します。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet3":::

区切りの連続するインスタンスにより、出力配列で空の文字列が生成されます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet4":::

<xref:System.String.Split%2A?displayProperty=nameWithType> は、文字列の配列 (1 つの文字ではなく、対象の文字列を解析するための区切り記号として機能する文字シーケンス) を受け取ることができます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet5":::

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../programming-guide/index.md)
- [文字列](../programming-guide/strings/index.md)
- [.NET 正規表現](../../standard/base-types/regular-expressions.md)
