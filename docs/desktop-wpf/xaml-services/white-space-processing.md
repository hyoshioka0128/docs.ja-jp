---
title: XAML での空白の処理
ms.date: 03/30/2017
helpviewer_keywords:
- East Asian characters [XAML Services]
- XAML [XAML Services], white-space processing
- white-space processing in XAML [XAML Services]
- characters [XAML Services], East Asian
ms.assetid: cc9cc377-7544-4fd0-b65b-117b90bb0b23
ms.openlocfilehash: 05f28c9115326424164b92e1b704c52bba31cf35
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432846"
---
# <a name="white-space-processing-in-xaml"></a>XAML での空白の処理

プロセッサの実装によって重要な空白を処理する必要があるという XAML[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]の状態の言語ルール。 この記事では、これらの XAML 言語ルールについて説明します。 また、XAML プロセッサの[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]実装とシリアル化用の XAML ライターによって定義される追加の空白の処理についても説明します。

## <a name="white-space-definition"></a>空白の定義

XML と一致する、空白文字[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]は、スペース、改行、およびタブです。これらは、それぞれ Unicode 値 0020、000A、および 0009 に対応します。

## <a name="white-space-normalization"></a>空白の正規化

デフォルトでは、プロセッサがファイルを処理するときに、次の[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]空白の正規化が[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]行われます。

1. 東アジア言語の文字間の改行文字が削除されます。 この用語の定義については、後の「東アジア言語の文字」を参照してください。

2. 空白文字 (スペース、改行、タブ) はすべてスペースに変換されます。

3. 連続した複数のスペースはすべて削除され、1 つのスペースに置換されます。

4. 開始タグの直後にあるスペースは削除されます。

5. 終了タグの直前にあるスペースは削除されます。

"既定" とは、 [xml:space](xml-space-handling.md) 属性の既定値で表される状態に対応します。

## <a name="white-space-in-inner-text-and-string-primitives"></a>内部テキスト内の空白文字と文字列プリミティブ

前の正規化規則は、XAML 要素内で検出された内部テキストに適用されます。 正規化の後、XAML プロセッサは、次のようにして、すべての内部テキストを適切な型に変換します。

- プロパティの型がコレクションでなく、直接的に <xref:System.Object> 型でもない場合、XAML プロセッサはその型の型コンバーターを使用して、その型への変換を試みます。 その際、変換に失敗すると、コンパイル時のエラーが発生します。

- プロパティの型がコレクションで、内部テキストが連続している (間に要素タグがない) 場合、その内部テキストは単一の <xref:System.String>として解析されます。 そのコレクション型が <xref:System.String>を受け入れない場合にも、コンパイル時のエラーが発生します。

- プロパティの型が <xref:System.Object>である場合、その内部テキストは単一の <xref:System.String>として解析されます。 その内部テキストの中に要素タグが含まれている場合には、コンパイル時のエラーが発生します。これは、 <xref:System.Object> 型は単一のオブジェクト (<xref:System.String> またはそれ以外) であることを意味しているためです。

- プロパティの型がコレクションであり、内部テキストが連続していないことがあります。この場合、最初の部分文字列は <xref:System.String> に変換されてコレクション項目として追加されます。中間にある要素はコレクション項目として追加され、この要素の後に続く部分文字列 (存在する場合) は 3 番目の <xref:System.String> 項目としてコレクションに追加されます。

## <a name="preserving-white-space"></a>空白の保存

最終的な表示のために、プロセッサの空白の正規化の影響を[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]受[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]けない、ソース内の空白を保持するためのいくつかの手法があります。

**xml:space="preserve"**: この属性は、空白の保存が望まれる要素のレベルで指定します。 この場合、要素を視覚的にわかりやすい入れ子として "美しく表示する" ためにコード編集アプリケーションによって追加されたスペースも含めて、すべての空白が保持されます。 ただし、これらのスペースが表示されるかどうかは、スペースを含んでいる要素のコンテンツ モデルによって決まります。 ほとんどのオブジェクト`xml:space="preserve"`モデルでは、属性の設定方法に関係なく、空白を有意と見なさないため、ルート レベルでの指定は避けてください。 グローバルに `xml:space` を設定すると、一部の実装で XAML 処理 (特にシリアル化) のパフォーマンスに影響することがあります。 文字列内の空白を描画する要素のレベル、または空白の重要なコレクションである要素のレベルでのみ属性を設定することをお勧めします。

**エンティティと改行しないスペース**:[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]テキスト オブジェクト モデル内に Unicode エンティティを配置できます。 非改行スペース (&\#160、 UTF-8 エンコード) などの専用エンティティーを使用できます。 また、改行しないスペース文字をサポートするリッチ テキスト コントロールを使用することもできます。 インデントなどのレイアウト特性をシミュレートするためにエンティティを使用する場合には、エンティティの実行時出力が、一般的なレイアウト システムにおけるインデントの生成機能を使用した場合よりも多くの要因 (パネルや余白の適切な使用など) に基づいて変化するため、注意が必要です。 たとえば、エンティティはフォントにマッピングされ、ユーザーのフォント選択に応じてサイズが変わる可能性があります。

## <a name="east-asian-characters"></a>東アジア言語の文字

「東アジア文字」は、U+20000 から U+2FFFD、U+30000 から U+3FFFD までの Unicode 文字範囲のセットとして定義されます。 このサブセットは、「CJK 表意文字」と呼ばれることもあります。 詳細については、「<https://www.unicode.org>」を参照してください。

## <a name="white-space-and-text-content-models"></a>空白およびテキスト コンテンツ モデル

実際には、空白を保持することは、考えられるすべてのコンテンツ モデルのサブセットに対してのみ重要です。 このサブセットに含まれるのは、ある種のシングルトン <xref:System.String> 型、専用の <xref:System.String> コレクション、または <xref:System.String> や <xref:System.Collections.IList> コレクションでの <xref:System.Collections.Generic.ICollection%601> と他の型の組み合わせをとることのできるコンテンツ モデルです。

### <a name="white-space-and-text-content-models-in-wpf"></a>WPF の空白とテキスト コンテンツ モデル

一例として、このセクションの残りの部分では、WPF によって定義されている特定の型について説明します。 この資料で説明する空白の処理機能は、.NET XAML サービスと WPF の両方に関連しています。 これらの動作を実際に見るには、何かの WPF XAML マークアップを使用し、オブジェクト グラフでその結果を確認し、再度マークアップにシリアル化してください。

文字列を受け取ることができるコンテンツ モデルの場合でも、これらのコンテンツ モデル内の既定の動作では、残っている空白は重要なものとして扱われないようにします。 たとえば、<xref:System.Windows.Controls.ListBox>は、<xref:System.Collections.IList>が、各<xref:System.Windows.Controls.ListBoxItem>間のライン フィードなどの空白は保持されず、レンダリングされません。 改行文字を <xref:System.Windows.Controls.ListBoxItem> 項目の文字列間の区切り記号として使用しても、まったく機能しません。改行文字で区切られた文字列は、1 つの文字列および 1 つの項目として扱われます。

空白を重要なものとして扱うコレクションは、通常、フロー ドキュメント モデルの一部です。 空白の保持動作をサポートする主なコレクションは<xref:System.Windows.Documents.InlineCollection>です。 このコレクション クラスは、<xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>で宣言されています。この属性が見つかると、[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]プロセッサはコレクション内の空白を有意な領域として扱います。 表記されたコレクション`xml:space="preserve"`内<xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>の空白と空白の組み合わせは、すべての空白が保持され、レンダリングされます。 空白と空白`xml:space="default"`の組み合わせ<xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>が原因で、空白の最初の正規化は、特定の位置に 1 つのスペースを残し、それらのスペースが保持され、レンダリングされます。 どちらの動作が望ましいかは、開発者の意図によって異なります。そのため、 `xml:space` は、必要な動作が有効となるように、選択的に使用する必要があります。

また、フロー ドキュメント モデルで改行を示す特定のインライン要素は、空白の重要なコレクションであっても、意図的に余分なスペースを追加しないようにする必要があります。 たとえば、<xref:System.Windows.Documents.LineBreak>要素は HTML の\<BR/> タグと同じ目的を持ち、マークアップでの読み<xref:System.Windows.Documents.LineBreak>やすさを実現するために、通常は、作成された改行によって後続のテキストから分離されます。 その改行は、正規化されて後続の行の先頭のスペースになってはなりません。 この動作<xref:System.Windows.Documents.LineBreak>を有効にするために、要素のクラス定義は<xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>、プロセッサによって解釈され、周囲[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]<xref:System.Windows.Documents.LineBreak>の空白が常にトリミングされることを意味します。

## <a name="see-also"></a>関連項目

- [XAML の概要 (WPF)](../fundamentals/xaml.md)
- [XML 文字エンティティと XAML](xml-character-entities.md)
- [xml: XAML での空間処理](xml-space-handling.md)
