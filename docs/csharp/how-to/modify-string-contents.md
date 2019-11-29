---
title: 文字列の内容を変更する方法 - C# ガイド
ms.date: 02/26/2018
helpviewer_keywords:
- strings [C#], modifying
ms.openlocfilehash: 539e313173d46c2c92399cefe94207c8beed03b4
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73973264"
---
# <a name="how-to-modify-string-contents-in-c"></a>C\# で文字列の内容を変更する方法

この記事では、既存の `string` を変更して `string` を生成するためのいくつかの手法を示します。 紹介するすべての手法で、変更の結果が `string` オブジェクトとして返されます。 これを明確に示すため、すべての例で、新しい変数に結果を格納します。 これで、それぞれの例を実行したときに、元の `string` と、変更から生じる `string` の両方を確認できます。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

この記事ではいくつかの手法を示します。 既存のテキストは置き換えることができます。 パターンを検索して、一致するテキストを他のテキストに置き換えることができます。 文字列は、一連の文字として扱うことができます。 空白を削除する便利なメソッドも使用できます。 シナリオに最も近い手法を選択する必要があります。

## <a name="replace-text"></a>テキストの置換

次のコードでは、既存のテキストを代替のテキストと置き換えることで新しい文字列が作成されます。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#1)]

先のコードは、文字列のこの*不変*プロパティを示しています。 先の例では、元の文字列 `source` が変更されていないことがわかります。 <xref:System.String.Replace%2A?displayProperty=nameWithType> メソッドによって、変更を含む新しい `string` が生成されます。

<xref:System.String.Replace%2A> メソッドは、文字列または単一の文字のどちらかを置き換えることができます。 どちらの場合も、検索で見つかったすべてのテキストが置き換えられます。  次の例では、すべての ' ' の文字が '\_' に置き換えられます。

[!code-csharp-interactive[replace characters](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#2)]

ソース文字列は変更されず、置き換えられた新しい文字列が返されます。

## <a name="trim-white-space"></a>空白のトリミング

<xref:System.String.Trim%2A?displayProperty=nameWithType>、<xref:System.String.TrimStart%2A?displayProperty=nameWithType>、および <xref:System.String.TrimEnd%2A?displayProperty=nameWithType> メソッドを使用して、先頭または末尾の空白を削除することができます。  次のコードは、それぞれの例を示しています。 ソース文字列は変更されません。これらのメソッドは、変更した内容を含む新しい文字列を返します。

[!code-csharp-interactive[trim white space](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#3)]

## <a name="remove-text"></a>テキストの削除

<xref:System.String.Remove%2A?displayProperty=nameWithType> メソッドを使用して文字列からテキストを削除することができます。 このメソッドによって、特定のインデックスから始まる文字が削除されます。 次の例は、<xref:System.String.IndexOf%2A?displayProperty=nameWithType> とそれに続く <xref:System.String.Remove%2A> を使用して文字列からテキストを削除する方法を示しています。

[!code-csharp-interactive[remove text](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#4)]

## <a name="replace-matching-patterns"></a>一致パターンの置換

[正規表現](../../standard/base-types/regular-expressions.md)を使用すると、テキスト一致パターンを新しいテキストに置き換えることができます (パターンで定義されている場合もあります)。 次の例では、<xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> クラスを使用してソース文字列でパターンを検索し、適切な大文字と小文字に置き換えています。 <xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.Text.RegularExpressions.MatchEvaluator,System.Text.RegularExpressions.RegexOptions)?displayProperty=nameWithType> メソッドは、置換のロジックをその引数の 1 つとして提供する機能を受け取ります。 この例で、関数 `LocalReplaceMatchCase` は、サンプル メソッド内で宣言された**ローカル関数**です。 `LocalReplaceMatchCase` は、<xref:System.Text.StringBuilder?displayProperty=nameWithType> クラスを使用して大文字と小文字が適切な置換文字列を作成します。

正規表現は、既知のテキストよりもパターンに従ったテキストを検索して置き換える場合に特に役立ちます。 詳細については、「[文字列を検索する方法](search-strings.md)」を参照してください。 検索パターン "the\s" は、単語 "the" とその後の空白文字を検索します。 パターンのこの部分により、ソース文字列の "there" は一致しなくなります。 正規表現言語要素の詳細については、「[正規表現言語 - クイック リファレンス](../../standard/base-types/regular-expression-language-quick-reference.md)」をご覧ください。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#5)]

<xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> メソッドによって、<xref:System.Text.StringBuilder> オブジェクトの内容と不変の文字列が返されます。

## <a name="modifying-individual-characters"></a>各文字の変更

文字列から文字配列を生成し、配列の内容を変更して、変更された配列の内容から新しい文字列を作成できます。

次の例は、文字列の文字のセットを置き換える方法を示しています。 最初に、<xref:System.String.ToCharArray?displayProperty=nameWithName> メソッドを使用して文字の配列が作成されます。 <xref:System.String.IndexOf%2A> メソッドを使用して "fox" という単語の開始インデックスを検索します。 次の 3 つの文字が、別の単語に置き換えられます。 最後に、新しい文字列が更新された文字配列から構築されます。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#6)]

## <a name="unsafe-modifications-to-string"></a>文字列のアンセーフな変更

**アンセーフ** コードを使用すると、文字列の作成後に "インプレース" で変更することができます。 アンセーフ コードでは、コード内の特定の種類のバグが最小化されるように設計された .NET の多くの機能がバイパスされます。 文字列クラスは**不変**型として設計されているため、文字列を変更するにはアンセーフ コードを使用する必要があります。 一度作成されると、その値は変わりません。 アンセーフ コードでは、標準の `string` メソッドを使用せずに `string` で使用されたメモリにアクセスして変更できるため、このプロパティが回避されます。
次の例は、アンセーフ コードを使用して文字列をインプレース変更するような、まれな状況のために提供されています。 この例では、`fixed` キーワードの使用方法を示します。 `fixed` キーワードにより、コードがアンセーフ ポインターを使用してメモリにアクセスしている間、ガベージ コレクター (GC) でメモリ内の文字列オブジェクトが移動しなくなります。 また、文字列に対してアンセーフ操作を実行すると発生する可能性のある副作用を示します。この副作用の原因は、C# コンパイラが文字列を内部に格納する (保持する) 方法にあります。 通常、この方法は、特に必要な場合以外は使用しないでください。 [unsafe](../language-reference/keywords/unsafe.md) と [fixed](../language-reference/keywords/fixed-statement.md) についての詳細を各記事でご確認ください。 <xref:System.String.Intern%2A> の API 参照には文字列インターンの情報も含まれています。

[!code-csharp[unsafe ways to create a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#7)]

[GitHub リポジトリ](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/strings)のコードを見て、これらのサンプルを試すことができます。 または、サンプルを [zip ファイルとして](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/strings.zip)ダウンロードすることができます。

## <a name="see-also"></a>関連項目

- [.NET Framework 正規表現](../../standard/base-types/regular-expressions.md)
- [正規表現言語 - クイック リファレンス](../../standard/base-types/regular-expression-language-quick-reference.md)
