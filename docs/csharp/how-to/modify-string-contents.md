---
title: 文字列の内容を変更する方法 - C# ガイド
ms.date: 02/26/2018
helpviewer_keywords:
- strings [C#], modifying
ms.openlocfilehash: e607a8a2e96a73f64463d75a75a2bfe3f518d118
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324169"
---
# <a name="how-to-modify-string-contents-in-c"></a>C\# で文字列の内容を変更する方法

この記事では、既存の `string` を変更して `string` を生成するためのいくつかの手法を示します。 紹介するすべての手法で、変更の結果が `string` オブジェクトとして返されます。 元と変更後の文字列が異なるインスタンスであることを示すために、例では、新しい変数に結果が格納されています。 各例を実行するとき、元の `string` と変更後の新しい `string` を調べることができます。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

この記事ではいくつかの手法を示します。 既存のテキストは置き換えることができます。 パターンを検索して、一致するテキストを他のテキストに置き換えることができます。 文字列は、一連の文字として扱うことができます。 空白を削除する便利なメソッドも使用できます。 シナリオに最も近い手法を選択してください。

## <a name="replace-text"></a>テキストの置換

次のコードでは、既存のテキストを代替のテキストと置き換えることで新しい文字列が作成されます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet1":::

先のコードは、文字列のこの*不変*プロパティを示しています。 先の例では、元の文字列 `source` が変更されていないことがわかります。 <xref:System.String.Replace%2A?displayProperty=nameWithType> メソッドによって、変更を含む新しい `string` が生成されます。

<xref:System.String.Replace%2A> メソッドは、文字列または単一の文字のどちらかを置き換えることができます。 どちらの場合も、検索で見つかったすべてのテキストが置き換えられます。  次の例では、すべての ' ' の文字が '\_' に置き換えられます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet2":::

ソース文字列は変更されず、置き換えられた新しい文字列が返されます。

## <a name="trim-white-space"></a>空白のトリミング

<xref:System.String.Trim%2A?displayProperty=nameWithType>、<xref:System.String.TrimStart%2A?displayProperty=nameWithType>、および <xref:System.String.TrimEnd%2A?displayProperty=nameWithType> メソッドを使用して、先頭または末尾の空白を削除することができます。  次のコードは、それぞれの例を示しています。 ソース文字列は変更されません。これらのメソッドは、変更した内容を含む新しい文字列を返します。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet3":::

## <a name="remove-text"></a>テキストの削除

<xref:System.String.Remove%2A?displayProperty=nameWithType> メソッドを使用して文字列からテキストを削除することができます。 このメソッドによって、特定のインデックスから始まる文字が削除されます。 次の例は、<xref:System.String.IndexOf%2A?displayProperty=nameWithType> とそれに続く <xref:System.String.Remove%2A> を使用して文字列からテキストを削除する方法を示しています。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet4":::

## <a name="replace-matching-patterns"></a>一致パターンの置換

[正規表現](../../standard/base-types/regular-expressions.md)を使用すると、テキスト一致パターンを新しいテキストに置き換えることができます (パターンで定義されている場合もあります)。 次の例では、<xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> クラスを使用してソース文字列でパターンを検索し、適切な大文字と小文字に置き換えています。 <xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.Text.RegularExpressions.MatchEvaluator,System.Text.RegularExpressions.RegexOptions)?displayProperty=nameWithType> メソッドは、置換のロジックをその引数の 1 つとして提供する機能を受け取ります。 この例で、関数 `LocalReplaceMatchCase` は、サンプル メソッド内で宣言された**ローカル関数**です。 `LocalReplaceMatchCase` は、<xref:System.Text.StringBuilder?displayProperty=nameWithType> クラスを使用して大文字と小文字が適切な置換文字列を作成します。

正規表現は、既知のテキストよりもパターンに従ったテキストを検索して置き換える場合に特に役立ちます。 詳細については、「[文字列を検索する方法](search-strings.md)」を参照してください。 検索パターン "the\s" は、単語 "the" とその後の空白文字を検索します。 パターンのこの部分により、ソース文字列の "there" は一致しなくなります。 正規表現言語要素の詳細については、「[正規表現言語 - クイック リファレンス](../../standard/base-types/regular-expression-language-quick-reference.md)」をご覧ください。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet5":::

<xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> メソッドによって、<xref:System.Text.StringBuilder> オブジェクトの内容と不変の文字列が返されます。

## <a name="modifying-individual-characters"></a>各文字の変更

文字列から文字配列を生成し、配列の内容を変更して、変更された配列の内容から新しい文字列を作成できます。

次の例は、文字列の文字のセットを置き換える方法を示しています。 最初に、<xref:System.String.ToCharArray?displayProperty=nameWithType> メソッドを使用して文字の配列が作成されます。 <xref:System.String.IndexOf%2A> メソッドを使用して "fox" という単語の開始インデックスを検索します。 次の 3 つの文字が、別の単語に置き換えられます。 最後に、新しい文字列が更新された文字配列から構築されます。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet6":::

## <a name="programmatically-build-up-string-content"></a>プログラムによって文字列の内容を作成する

文字列は不変なので、これまでの例ではすべて、一時的な文字列または文字の配列を作成しています。 ハイパフォーマンスのシナリオでは、これらのヒープの割り当てを回避することが望ましい場合があります。 .NET Core では <xref:System.String.Create%2A?displayProperty=nameWithType> メソッドを提供しており、中間の一時的な文字列の割り当てを回避しながら、コールバックを介してプログラムによって文字列の文字の内容を入力できます。

:::code language="csharp" source="../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs" id="Snippet7":::

アンセーフ コードを使用して固定ブロック内の文字列を変更することは可能ですが、文字列が作成された後に文字列の内容を変更することは**強く**お勧めしません。 そうすると、予期できない方法で中断が発生します。 たとえば、誰かがあなたの文字列と同じ内容の文字列をインターン処理する場合、その人はあなたのコピーを取得し、あなたが文字列を変更しようとしているとは想定しません。

## <a name="see-also"></a>関連項目

- [.NET Framework の正規表現](../../standard/base-types/regular-expressions.md)
- [正規表現言語 - クイック リファレンス](../../standard/base-types/regular-expression-language-quick-reference.md)
