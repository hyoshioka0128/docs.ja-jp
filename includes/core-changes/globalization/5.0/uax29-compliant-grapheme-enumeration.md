---
ms.openlocfilehash: c0c1c9c9d8e3aeb6f689f754d09b50b208b54112
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83702313"
---
### <a name="stringinfo-and-textelementenumerator-are-now-uax29-compliant"></a>StringInfo と TextElementEnumerator は現在 UAX29 に準拠する

この変更の前に、<xref:System.Globalization.StringInfo?displayProperty=fullName> と <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName> によって一部の書記素クラスターが正しく処理されていませんでした。 一部の書記素がまとめて保持されずに、構成要素に分割されていました。 現在は、<xref:System.Globalization.StringInfo> と <xref:System.Globalization.TextElementEnumerator> によって最新バージョンの Unicode 標準に従って書記素クラスターが処理されるようになりました。

また、Visual Basic 内の文字列の文字を反転する <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> メソッドも、書記素クラスターの Unicode 標準に従うようになりました。

#### <a name="change-description"></a>変更の説明

[書記素](https://www.unicode.org/glossary/#grapheme)または[拡張書記素クラスター](https://www.unicode.org/glossary/#extended_grapheme_cluster)は、ユーザーが認識できる単一の文字であり、複数の Unicode コード ポイントで構成される場合があります。 たとえば、タイ語の文字 "kam" (:::no-loc text="กำ":::) を含む文字列は、次の 2 つの文字で構成されます。

- :::no-loc text="ก"::: (= '\u0e01') タイ語の文字 KO KAI
- :::no-loc text=" ำ"::: (= '\u0e33') タイ語の文字 SARA AM

ユーザーに表示されると、オペレーティング システムではこれらの 2 つの文字が結合されて、1 つの表示文字 (書記素) "kam" (:::no-loc text="กำ":::) が形成されます。 また、絵文字も同様に、結合して表示する複数の文字で構成できます。

> [!TIP]
> .NET ドキュメントでは、書記素を表す際に "テキスト要素" という用語が使用されることがあります。

<xref:System.Globalization.StringInfo> クラスと <xref:System.Globalization.TextElementEnumerator> クラスによって文字列が検査され、含まれている書記素に関する情報が返されます。 .NET Framework (すべてのバージョン) および .NET Core 3.x 以前では、これらの 2 つのクラスにより、いくつかの結合クラスを処理するカスタム ロジックが使用されますが、これらのクラスは [Unicode 標準](https://www.unicode.org/reports/tr29/tr29-35.html#Grapheme_Cluster_Boundaries)に完全には準拠していません。 たとえば、<xref:System.Globalization.StringInfo> クラスと <xref:System.Globalization.TextElementEnumerator> クラスにより、1 つのタイ語の文字 "kam" がまとめて保持されずに、その構成要素に誤って分割されます。 また、これらのクラスにより、絵文字文字 "🤷🏽♀️" が 1 つの書記素クラスターとして保持されずに、4 つのクラスター (肩をすくめる人、肌色修飾子、性別修飾子、および非表示のコンバイナー) に誤って分割されます。

.NET 5 以降では、<xref:System.Globalization.StringInfo> クラスと <xref:System.Globalization.TextElementEnumerator> クラスにより、[Unicode 標準の付属書 \#29、リビジョン 35、セクション 3](https://www.unicode.org/reports/tr29/tr29-35.html) で定義されている Unicode 標準が実装されます。 具体的には、すべての結合クラスで、[拡張書記素クラスター](https://www.unicode.org/glossary/#extended_grapheme_cluster)が返されるようになりました。

次の C# コードについて考えてみましょう。

```cs
using System.Globalization;

static void Main(string[] args)
{
    PrintGraphemes("กำ");
    PrintGraphemes("🤷🏽‍♀️");
}

static void PrintGraphemes(string str)
{
    Console.WriteLine($"Printing graphemes of \"{str}\"...");
    int i = 0;

    TextElementEnumerator enumerator = StringInfo.GetTextElementEnumerator(str);
    while (enumerator.MoveNext())
    {
        Console.WriteLine($"Grapheme {++i}: \"{enumerator.Current}\"");
    }

    Console.WriteLine($"({i} grapheme(s) total.)");
    Console.WriteLine();
}
```

.NET Framework と .NET Core 3.x 以前のバージョンでは、書記素は分割され、コンソールの出力は次のようになります。

```txt
Printing graphemes of "กำ"...
Grapheme 1: "ก"
Grapheme 2: "ำ"
(2 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷"
Grapheme 2: "🏽"
Grapheme 3: "‍"
Grapheme 4: "♀️"
(4 grapheme(s) total.)
```

.NET 5 以降のバージョンでは、書記素はまとめて保持され、コンソールの出力は次のようになります。

```txt
Printing graphemes of "กำ"...
Grapheme 1: "กำ"
(1 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷🏽‍♀️"
(1 grapheme(s) total.)
```

また、.NET 5 以降では、Visual Basic 内の文字列の文字を反転する <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> メソッドも、書記素クラスターの Unicode 標準に従うようになりました。

これらの変更は、.NET での Unicode と UTF-8 のさまざまな機能強化の一環です。これには、.NET Core 3.0 の <xref:System.Text.Rune?displayProperty=fullName> 型で導入された Unicode スカラー値列挙 API を補完する拡張書記素クラスター列挙 API などが含まれます。

#### <a name="version-introduced"></a>導入されたバージョン

.NET 5.0 Preview 1

#### <a name="recommended-action"></a>推奨アクション

何らかのアクションをとる必要はありません。 アプリは、さまざまなグローバリゼーション関連のシナリオで、標準に準拠した方法で自動的に動作します。

#### <a name="category"></a>カテゴリ

グローバリゼーション

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Globalization.StringInfo?displayProperty=fullName>
- <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName>
- <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Globalization.StringInfo`
- `T:System.Globalization.TextElementEnumerator`
- `Overload:Microsoft.VisualBasic.Strings.StrReverse`

-->
