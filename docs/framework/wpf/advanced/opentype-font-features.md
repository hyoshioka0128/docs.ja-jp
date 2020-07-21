---
title: OpenType フォントの機能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- fonts [WPF], OpenType
- typography [WPF], OpenType font technology
- OpenType font technology [WPF]
ms.assetid: 4061a9d1-fe8b-4921-9e17-18ec7d2e3ea2
ms.openlocfilehash: 52fe73bccd625c9508b398874fd6b075af2445e0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186803"
---
# <a name="opentype-font-features"></a>OpenType フォントの機能

このトピックでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] における OpenType フォント技術の主要機能の概要を説明します。  
  
<a name="overview"></a>
## <a name="opentype-font-format"></a>OpenType フォントの書式  
 OpenType フォント形式は TrueType® フォント形式が拡張されたものであり、PostScript フォント データのサポートが追加されています。 OpenType フォント形式は、Microsoft と Adobe Corporation により共同開発されました。 OpenType フォントおよび OpenType フォントをサポートするオペレーティング システム サービスでは、フォントに TrueType アウトラインまたは CFF (PostScript) アウトラインのどちらが含まれていても、ユーザーは簡単な方法でフォントをインストールして使用できます。  
  
 OpenType フォント形式では、次のような開発者の課題が対処されています。  
  
- より広範なマルチプラットフォームのサポート。  
  
- 国際文字セットのサポート強化。  
  
- フォント データの保護強化。  
  
- ファイルのサイズを小さくして、より効率的にフォントを配布。  
  
- 高度なテキスト編集コントロールの幅広いサポート。  
  
> [!NOTE]
> Windows SDK には、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションで使用できるサンプルの OpenType フォント セットが含まれています。 これらのフォントでは、このトピックで説明していく機能の大半が提供されています。 詳細については、「[OpenType フォント パックのサンプル](sample-opentype-font-pack.md)」をご覧ください。  
  
OpenType フォント形式の詳細については、「[OpenType の仕様](https://docs.microsoft.com/typography/opentype/spec/)」を参照してください。  
  
### <a name="advanced-typographic-extensions"></a>高度なテキスト編集の拡張機能  
 高度な印刷用テーブル (OpenType レイアウト テーブル) では、TrueType または CFF のアウトラインを使用してフォントの機能が拡張されています。 OpenType レイアウトのフォントには、フォントの機能を拡張する追加の情報が含まれ、高品質の国際タイポグラフィがサポートされています。 ほとんどの OpenType フォントでは、利用可能な OpenType 機能全体のサブセットのみが公開されています。 OpenType フォントでは次のような機能が提供されています。  
  
- 合字、位置フォーム、代替、およびその他のフォント置換をサポートする、文字とグリフの間の充実したマッピング。  
  
- 2 次元配置とグリフ結合のサポート。  
  
- フォントには明示的なスクリプトと言語情報が含まれるため、テキスト処理アプリケーションはそれに従って動作を調整可能。  
  
 OpenType レイアウト テーブルについては、OpenType 仕様の ["フォント ファイル テーブル"](https://www.microsoft.com/typography/otspec/otff.htm) に関するセクションで詳しく説明されています。  
  
 この概要のこれ以降では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティによって公開される、視覚的に興味深い OpenType の機能の幅広さと柔軟性について説明します。 このオブジェクトの詳細については、「[タイポグラフィ クラス](#typography_class)」を参照してください。  
  
<a name="variants"></a>
## <a name="variants"></a>バリアント  
 バリアントを使用して、上付き文字と下付きなどのさまざまなタイポグラフィ スタイルを表示します。  
  
### <a name="superscripts-and-subscripts"></a>上付き/下付きの文字  
 <xref:System.Windows.Documents.Typography.Variants%2A> プロパティを使用すると、OpenType フォントに上付き文字と下付き文字の値を設定することができます。  
  
 次のテキストは、Palatino Linotype フォントの上付き文字を示したものです。  
  
 ![OpenType の上付き文字を使用するテキスト](./media/opentype-font-features/opentype-superscripts.gif "OpenType の上付き文字を使用するテキスト")  
  
 次に示すマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの上付き文字を定義する方法を示しています。  
  
 [!code-xaml[OpenTypeFontSamples#12](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#12)]  
  
 次のテキストは、Palatino Linotype フォントの下付き文字を示したものです。  
  
 ![OpenType の下付き文字を使用するテキスト](./media/opentype-font-features/opentype-subscripts.gif "OpenType の下付き文字を使用するテキスト")  
  
 次に示すマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの下付き文字を定義する方法を示しています。  
  
 [!code-xaml[OpenTypeFontSamples#13](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#13)]  
  
### <a name="decorative-uses-of-superscripts-and-subscripts"></a>上付き文字と下付き文字の装飾的な用途  
 上付き文字と下付き文字を使用して、大文字と小文字が混在したテキストに装飾的効果をつけることもできます。 次のテキストは、Palatino Linotype フォントの上付き文字と下付き文字を示したものです。 大文字には影響がないことに注目してください。  
  
 ![OpenType の上付き文字と下付き文字を使用するテキスト](./media/opentype-font-features/opentype-superscripts-subscripts.gif "OpenType の上付き文字と下付き文字を使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用してフォントの上付き文字と下付き文字を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#14](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#14)]  
  
<a name="capitals"></a>
## <a name="capitals"></a>大文字  
 大文字は、大文字スタイルのグリフでテキストをレンダリングするタイポグラフィ形式のセットです。 通常、テキストをすべて大文字で表示すると、文字間隔が狭すぎるように見え、文字の印象と縦横比が重すぎるように感じられます。 OpenType では、小型英大文字、超小型英大文字、タイトル用、大文字スペーシングを含め、大文字に関する多くのスタイル形式がサポートされています。 これらのスタイル形式を使用して、英大文字の外観を変えることができます。  
  
 次のテキストは、Pescadero フォントの標準の大文字と、その後に "SmallCaps" および "AllSmallCaps" のスタイルをあてた文字を示したものです。 この例では、3 つの単語すべてに同じフォント サイズが使用されています。  
  
 ![OpenType の大文字を使用するテキスト](./media/opentype-font-features/opentype-capitals.gif "OpenType の大文字を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pescadero フォントの大文字を定義する方法を示します。 "SmallCaps" 形式を使用する場合は、先頭の大文字は無視されます。  
  
 [!code-xaml[OpenTypeFontSamples#9](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
### <a name="titling-capitals"></a>タイトル用大文字  
 タイトル用大文字は、重みと縦横比が軽く、標準の大文字よりも洗練された印象を与えるように設計されています。 タイトル用大文字は通常、見出しとして大きいフォント サイズで使用されます。 次のテキストは、Pescadero フォントの標準の大文字とタイトル用大文字を示したものです。 2 行目のテキストの縦線の幅が狭いことに注意してください。  
  
 ![OpenType のタイトル大文字を使用するテキスト](./media/opentype-font-features/opentype-titling-capitals.gif "OpenType のタイトル大文字を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pescadero フォントのタイトル用大文字を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet17](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet17)]  
  
### <a name="capital-spacing"></a>大文字スペーシング  
 大文字スペーシングは、テキストをすべて大文字にする場合に間隔を広くする機能です。 大文字は、通常、小文字と調和するようにデザインされています。 大文字と小文字の間では適切に見えるスペーシングでも、大文字だけが使用されている場合は、狭すぎるように見えることがあります。 次のテキストは、Pescadero フォントの標準のスペーシングと大文字スペーシングを示したものです。  
  
 ![OpenType の大文字スペーシングを使用するテキスト](./media/opentype-font-features/opentype-capital-spacing.gif "OpenType の大文字スペーシングを使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pescadero フォントの大文字スペーシングを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet18](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet18)]  
  
<a name="ligatures"></a>
## <a name="ligatures"></a>合字  
 合字とは、2 つ以上のグリフを、より読みやすい、あるいはより魅力的なテキストにするために、1 つのグリフに形成したものです。 OpenType フォントでは、4 種類の合字がサポートされています。  
  
- **標準合字**。 読みやすさを高めるように設計されています。 標準合字には、"fi"、"fl" および "ff" があります。  
  
- **コンテキスト合字**。 合字を構成する文字の間の結合を向上させることによって、読みやすさを高めるよう設計されています。  
  
- **随意合字**。 装飾を加える設計で、特に読みやすくなるようには設計されていません。  
  
- **歴史的合字**。 歴史的な記述に相応しい設計で、特に読みやすくなるようには設計されていません。  
  
 次のテキストは、Pericles フォントの標準合字グリフを示したものです。  
  
 ![OpenType の標準合字を使用するテキスト](./media/opentype-font-features/opentype-standard-ligatures.gif "OpenType の標準合字を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pericles フォントの標準合字グリフを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#4](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#4)]  
  
 次のテキストは、Pericles フォントの随意合字グリフを示したものです。  
  
 ![OpenType の随意合字を使用するテキスト](./media/opentype-font-features/opentype-discretionary-ligatures.gif "OpenType の随意合字を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pericles フォントの随意合字グリフを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#5](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#5)]  
  
 既定では、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の OpenType フォントでは標準合字が有効です。 たとえば、Palatino Linotype フォントを使用する場合、標準合字 "fi"、"ff" および "fl" は組み合わせ文字グリフとして表示されます。 各標準合字では文字のペアが相互に接していることに注意してください。  
  
 ![Palatino Linotype で OpenType の標準合字を使用するテキスト](./media/opentype-font-features/opentype-standard-ligatures-palatino.gif "Palatino Linotype で OpenType の標準合字を使用するテキスト")

 ただし、標準合字機能を無効にして、"ff" などの標準合字が、組み合わせ文字グリフとしてではなく、2 つの別々のグリフとして表示されるようにできます。  
  
 ![OpenType の無効な標準合字を使用するテキスト](./media/opentype-font-features/disabled-opentype-standard-ligatures.gif "OpenType の無効な標準合字を使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの標準合字グリフを無効にする方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#6](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#6)]  
  
<a name="swashes"></a>
## <a name="swashes"></a>飾り付き  
 飾り付きは装飾的なグリフで、カリグラフィを連想させる、手の込んだ装飾が使用されます。 次のテキストは、Pescadero フォントの標準および飾り付きグリフを示したものです。  
  
 ![OpenType の標準グリフとスワッシュ グリフを使用するテキスト](./media/opentype-font-features/opentype-standard-swash-glyphs.gif "OpenType の標準グリフと飾り付きグリフを使用するテキスト")  

 飾り付きは、季節のご挨拶などの短いフレーズで装飾的な要素としてよく使用されます。 次のテキストでは、飾り付きを使用して、イベントの名前の大文字を強調しています。  
  
 ![OpenType の飾り付きを使用するテキスト](./media/opentype-font-features/opentype-swashes.gif "OpenType の巻き髭を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用してフォントの飾り付きを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#7](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#7)]  
  
### <a name="contextual-swashes"></a>コンテキスト飾り付き  
 飾り付きグリフの特定の組み合わせでは、隣りあう文字の下に延びる部分が重なり合うなど、美しくない外観になる可能性があります。 コンテキスト飾り付きを使用すると、より良い外観を生成する代替の飾り付きグリフを使用できます。 次のテキストでは、コンテキスト飾り付きが適用される前後の同じ単語を示します。  
  
 ![OpenType のコンテキスト飾り付きを使用するテキスト](./media/opentype-font-features/opentype-contextual-swashes.gif "OpenType のコンテキスト巻き髭を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pescadero フォントのコンテキスト飾り付きを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet16](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet16)]  
  
<a name="alternates"></a>
## <a name="alternates"></a>代替  
 代替文字は、標準的なグリフの代わりに使用できるグリフです。 次の例で使用される Pericles フォントなどの OpenType フォントには、テキストの異なる外観を作るのに使用できる代替グリフを含めることができます。 次のテキストは、Pericles フォントの標準グリフを示したものです。  
  
 ![OpenType の標準グリフを使用するテキスト](./media/opentype-font-features/opentype-standard-glyphs.gif "OpenType の標準グリフを使用するテキスト")  

 Pericles OpenType フォントには、標準グリフ セットにスタイル代替グリフを提供する追加グリフが含まれています。 次のテキストでは、スタイル代替グリフが表示されています。  
  
 ![OpenType のスタイル代替グリフを使用するテキスト](./media/opentype-font-features/opentype-stylistic-alternate-glyphs.gif "OpenType のスタイル代替グリフを使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pericles フォントのスタイル代替グリフを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#2](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#2)]  
  
 次のテキストは、Pericles フォントの他のスタイル代替グリフを示したものです。  
  
 ![Pericles フォントの OpenType スタイル代替グリフを使用するテキスト](./media/opentype-font-features/opentype-stylistic-alternate-glyphs-pericles.gif "Pericles フォントの OpenType スタイル代替グリフを使用するテキスト")

 次のマークアップの例では、これらの他のスタイル代替グリフを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#3](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#3)]  
  
### <a name="random-contextual-alternates"></a>ランダムなコンテキスト代替  
 ランダムなコンテキスト代替は、単一文字に複数の代替グリフを提供します。 スクリプト型フォントで実装されたこの機能では、ランダムに選択された外観がわずかに異なるグリフのセットを使用して、手書きをシミュレートできます。 次のテキストでは、Lindsey フォントに対してランダムなコンテキスト代替が使用されています。 文字 "a" の外観が少し異なることに注意してください  
  
 ![OpenType のランダムなコンテキスト代替を使用するテキスト](./media/opentype-font-features/opentype-random-contextual-alternates.gif "OpenType のランダムなコンテキスト代替を使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Lindsey フォントのランダムなコンテキスト代替を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet20](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet20)]  
  
### <a name="historical-forms"></a>歴史的形式  
 歴史的形式は、過去に一般的であった表示形式です。 次のテキストでは、Palatino Linotype フォントのグリフの歴史的形式を使用して、"Boston, Massachusetts" という語句が表示されています。  
  
 ![OpenType の歴史的形式を使用するテキスト](./media/opentype-font-features/opentype-historical-forms.gif "OpenType の履歴フォームを使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの歴史的形式を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#8](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#8)]  
  
<a name="numerical_styles"></a>
## <a name="numerical-styles"></a>数値スタイル  
 OpenType フォントでは、テキスト内の数値に使用できる数多くの機能をサポートします。  
  
### <a name="fractions"></a>小数  
 OpenType フォントでは、スラッシュや横棒を使用した小数スタイルがサポートされています。  
  
 次のテキストは、Palatino Linotype フォントの小数スタイルを示したものです。  
  
 ![OpenType の分数 (横) と分数 (縦) を使用するテキスト](./media/opentype-font-features/opentype-slashed-stacked-fractions.gif "OpenType の分数 (横) と分数 (縦) を使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの小数スタイルを定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#10](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#10)]  
  
### <a name="old-style-numerals"></a>旧式スタイルの数字  
 OpenType フォントでは、旧式スタイルの数字形式がサポートされています。 この形式は、もはや標準ではなくなったスタイルで数字を表示するのに便利です。 次のテキストは、Palatino Linotype フォントの標準と旧式のスタイルの数字形式で、18 世紀の日付を表示したものです。  
  
 ![OpenType の旧式スタイルの数字を使用するテキスト](./media/opentype-font-features/opentype-old-style-numerals.gif "OpenType の古いスタイルの数字を使用するテキスト")  

 次のテキストは、Palatino Linotype フォントの標準の数字と、旧式スタイルの数字を示したものです。  
  
 ![OpenType の旧式スタイルの数字セットを使用するテキスト](./media/opentype-font-features/opentype-old-style-numeral-sets.gif "OpenType の古いスタイルの数字セットを使用するテキスト")  
  
 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Palatino Linotype フォントの旧式スタイルの数値を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#11](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#11)]  
  
### <a name="proportional-and-tabular-figures"></a>プロポーショナルと表形式の数字  
 OpenType フォントでは、プロポーショナルと表形式の数字の機能がサポートされており、数字を使用するときの幅の調整が制御されます。 プロポーショナルの数字では、それぞれの数字は異なる幅を持つものとして扱われます。たとえば "1" は "5" より狭い幅です。 表形式の数字は、横が揃うように等幅の数字として処理されるため、財務に関する情報が読みやすくなります。  
  
 1 列目のテキストは、Miramonte フォントを使用して表示された 2 つのプロポーショナルの数字です。 数字 "5" と "1" の幅の違いに注意してください。 2 列目には、同じ 2 つの数値が表形式の数字機能を使用して横幅を調整されて表示されています。  
  
 ![OpenType のプロポーショナルと表形式の数字を使用するテキスト](./media/opentype-font-features/opentype-proportional-tabular-figures.gif "OpenType のプロポーショナルと表形式の数字を使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Miramonte フォントのプロポーショナルと表形式の数字を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet19](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet19)]  
  
### <a name="slashed-zero"></a>スラッシュ付きゼロ  
 OpenType フォントでは、英文字 "O" と数字の "0" の違いを強調するためのスラッシュ付きゼロの数字形式がサポートされています。 スラッシュ付きゼロは、財務およびビジネス情報における ID によく使用されます。  
  
 次のテキストは、Miramonte フォントを使用してサンプルの注文識別子を表示したものです。 1 行目では、標準の数字が使用されています。 2 行目では、大文字の "O" と区別しやすいように、スラッシュ付きゼロの数字が使用されています。  
  
 ![OpenType のスラッシュ付きのゼロを使用するテキスト](./media/opentype-font-features/opentype-slashed-zero-numerals.gif "OpenType のスラッシュ付きのゼロを使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Miramonte フォントのスラッシュ付きのゼロ数値を定義する方法を示します。  
  
 [!code-xaml[OpenTypeFontSamples#OpenTypeFontSnippet15](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet15)]  
  
<a name="typography_class"></a>
## <a name="typography-class"></a>タイポグラフィ クラス  
 <xref:System.Windows.Documents.Typography> オブジェクトでは、OpenType フォントでサポートされる機能セットが公開されています。 マークアップで <xref:System.Windows.Documents.Typography> プロパティを設定することにより、OpenType 機能を利用したドキュメントを簡単に作成できます。  
  
 次のテキストは、Pescadero フォントの標準の大文字と、その後に "SmallCaps" および "AllSmallCaps" のスタイルをあてた文字を示したものです。 この例では、3 つの単語すべてに同じフォント サイズが使用されています。  
  
 ![OpenType の大文字を使用するテキスト](./media/opentype-font-features/opentype-capitals.gif "OpenType の大文字を使用するテキスト")  

 次のマークアップの例では、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティを使用して Pescadero フォントの大文字を定義する方法を示します。 "SmallCaps" 形式を使用する場合は、先頭の大文字は無視されます。  
  
 [!code-xaml[OpenTypeFontSamples#9](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
 次のコード例では、前のマークアップの例と同じタスクを実行します。  
  
 [!code-csharp[TypographyCodeSnippets#TypographyCodeSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/TypographyCodeSnippets/CSharp/Page1.xaml.cs#typographycodesnippet1)]
 [!code-vb[TypographyCodeSnippets#TypographyCodeSnippet1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TypographyCodeSnippets/visualbasic/page1.xaml.vb#typographycodesnippet1)]  
  
### <a name="typography-class-properties"></a>タイポグラフィ クラスのプロパティ  
 次の表は、<xref:System.Windows.Documents.Typography> オブジェクトのプロパティ、値、既定値の一覧です。  
  
|プロパティ|値|既定値|  
|--------------|----------------|-------------------|  
|<xref:System.Windows.Documents.Typography.AnnotationAlternates%2A>|数値 - バイト|0|  
|<xref:System.Windows.Documents.Typography.Capitals%2A>|<xref:System.Windows.FontCapitals.AllPetiteCaps> &#124; <xref:System.Windows.FontCapitals.AllSmallCaps> &#124; <xref:System.Windows.FontCapitals.Normal> &#124; <xref:System.Windows.FontCapitals.PetiteCaps> &#124; <xref:System.Windows.FontCapitals.SmallCaps> &#124; <xref:System.Windows.FontCapitals.Titling> &#124; <xref:System.Windows.FontCapitals.Unicase>|<xref:System.Windows.FontCapitals.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.CapitalSpacing%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.CaseSensitiveForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.ContextualAlternates%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualSwashes%2A>|数値 - バイト|0|  
|<xref:System.Windows.Documents.Typography.DiscretionaryLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianExpertForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianLanguage%2A>|<xref:System.Windows.FontEastAsianLanguage.HojoKanji> &#124; <xref:System.Windows.FontEastAsianLanguage.Jis04> &#124; <xref:System.Windows.FontEastAsianLanguage.Jis78> &#124; <xref:System.Windows.FontEastAsianLanguage.Jis83> &#124; <xref:System.Windows.FontEastAsianLanguage.Jis90> &#124; <xref:System.Windows.FontEastAsianLanguage.NlcKanji> &#124; <xref:System.Windows.FontEastAsianLanguage.Normal> &#124; <xref:System.Windows.FontEastAsianLanguage.Simplified> &#124; <xref:System.Windows.FontEastAsianLanguage.Traditional> &#124; <xref:System.Windows.FontEastAsianLanguage.TraditionalNames>|<xref:System.Windows.FontEastAsianLanguage.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.EastAsianWidths%2A>|<xref:System.Windows.FontEastAsianWidths.Full> &#124; <xref:System.Windows.FontEastAsianWidths.Half> &#124; <xref:System.Windows.FontEastAsianWidths.Normal> &#124; <xref:System.Windows.FontEastAsianWidths.Proportional> &#124; <xref:System.Windows.FontEastAsianWidths.Quarter> &#124; <xref:System.Windows.FontEastAsianWidths.Third>|<xref:System.Windows.FontEastAsianWidths.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.Fraction%2A>|<xref:System.Windows.FontFraction.Normal> &#124; <xref:System.Windows.FontFraction.Slashed> &#124; <xref:System.Windows.FontFraction.Stacked>|<xref:System.Windows.FontFraction.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.HistoricalForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.HistoricalLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Kerning%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.MathematicalGreek%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.NumeralAlignment%2A>|<xref:System.Windows.FontNumeralAlignment.Normal> &#124; <xref:System.Windows.FontNumeralAlignment.Proportional> &#124; <xref:System.Windows.FontNumeralAlignment.Tabular>|<xref:System.Windows.FontNumeralAlignment.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.NumeralStyle%2A>|<xref:System.Boolean>|<xref:System.Windows.FontNumeralStyle.Normal?displayProperty=nameWithType>|  
|<xref:System.Windows.Documents.Typography.SlashedZero%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StandardLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.StandardSwashes%2A>|数値 - バイト|0|  
|<xref:System.Windows.Documents.Typography.StylisticAlternates%2A>|数値 - バイト|0|  
|<xref:System.Windows.Documents.Typography.StylisticSet1%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet2%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet3%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet4%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet5%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet6%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet7%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet8%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet9%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet10%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet11%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet12%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet13%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet14%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet15%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet16%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet17%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet18%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet19%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet20%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Variants%2A>|<xref:System.Windows.FontVariants.Inferior> &#124; <xref:System.Windows.FontVariants.Normal> &#124; <xref:System.Windows.FontVariants.Ordinal> &#124; <xref:System.Windows.FontVariants.Ruby> &#124; <xref:System.Windows.FontVariants.Subscript> &#124; <xref:System.Windows.FontVariants.Superscript>|<xref:System.Windows.FontVariants.Normal?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Documents.Typography>
- [OpenType 仕様](https://docs.microsoft.com/typography/opentype/spec/)
- [WPF のタイポグラフィ](typography-in-wpf.md)
- [OpenType フォント パックのサンプル](sample-opentype-font-pack.md)
- [アプリケーションでのフォントのパッケージング](packaging-fonts-with-applications.md)
