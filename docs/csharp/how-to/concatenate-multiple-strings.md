---
title: 複数の文字列を連結する方法 (C# ガイド)
description: C# で文字列を連結する方法は複数あります。 各選択のオプションと、それを選ぶ理由も示します。
ms.date: 02/20/2018
helpviewer_keywords:
- joining strings [C#]
- concatenating strings [C#]
- strings [C#], concatenation
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
ms.openlocfilehash: ef3d79c5b40d08cb76e58eba1c8831c468fd1fc0
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663019"
---
# <a name="how-to-concatenate-multiple-strings-c-guide"></a>複数の文字列を連結する方法 (C# ガイド)

*連結*とは、ある文字列を別の文字列の末尾に追加するプロセスです。 文字列を連結するには、`+` 演算子を使用します。 文字列リテラルと文字列定数の場合、連結はコンパイル時に行われ、実行時には行われません。 文字列変数の連結は実行時にのみ行われます。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

次の例では、ソース コードを読みやすくするために、連結を使用して長い文字列リテラルを短い文字列に分割しています。 これらの部分は、コンパイル時に単一の文字列に連結されます。 関係する文字列の数に関係なく、実行時にパフォーマンス コストは発生しません。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet1":::

文字列変数を連結する場合は、`+` または `+=` 演算子、[文字列補間](../language-reference/tokens/interpolated.md)または <xref:System.String.Format%2A?displayProperty=nameWithType>、<xref:System.String.Concat%2A?displayProperty=nameWithType>、<xref:System.String.Join%2A?displayProperty=nameWithType>、<xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> メソッドを使用できます。 `+` 演算子は使い方が簡単で、直感的なコードにすることができます。 1 つのステートメントで複数の `+` 演算子を使用している場合でも、文字列の内容がコピーされるのは 1 回のみです。 次のコードは、`+` および `+=` 演算子を使用して文字列を連結する例を示しています。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet2":::

式によっては、次のコードに示すように、文字列補間を使用して文字列を連結する方が簡単な場合があります。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet3":::

> [!NOTE]
> 文字列連結操作において、C# コンパイラでは null 文字列は空の文字列と同様に扱われます。

文字列を連結する他のメソッドとして、<xref:System.String.Format%2A?displayProperty=nameWithType> があります。 このメソッドは、少数のコンポーネント文字列から文字列を作成する場合に有効です。

他にも、結合するソース文字列の数がわからないループ内の文字列を結合する場合、ソース文字列の実際の数は大きくなる可能性があります。 <xref:System.Text.StringBuilder> クラスは、このようなシナリオのために設計されています。 次のコードでは、<xref:System.Text.StringBuilder> クラスの <xref:System.Text.StringBuilder.Append%2A> メソッドを使用して文字列を連結しています。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet4":::

[文字列の連結または `StringBuilder` クラスを選択する理由](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder#the-string-and-stringbuilder-types)に関するページで詳細をご確認ください。

コレクションからの文字列を結合する別のオプションとして、<xref:System.String.Concat%2A?displayProperty=nameWithType> メソッドを使用する方法があります。 ソース文字列を区切り記号で区切る必要がある場合は、<xref:System.String.Join%2A?displayProperty=nameWithType> メソッドを使用します。 次のコードでは、両方のメソッドを使用して単語の配列を結合します。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet5":::

最後に、[LINQ](../programming-guide/concepts/linq/index.md) および <xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=nameWithType> メソッドを使用して、コレクションからの文字列を結合できます。 このメソッドは、ラムダ式を使用してソース文字列を結合します。 ラムダ式は、各文字列を既存の蓄積に追加する処理を行います。 次の例では、配列内の各単語の間にスペースを追加することによって単語の配列を結合します。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/Concatenate.cs" id="Snippet6":::

## <a name="see-also"></a>関連項目

- <xref:System.String>
- <xref:System.Text.StringBuilder>
- [C# プログラミング ガイド](../programming-guide/index.md)
- [文字列](../programming-guide/strings/index.md)
