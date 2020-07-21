---
title: 双方向機能の概要
ms.date: 03/30/2017
helpviewer_keywords:
- Span elements [WPF]
- bidirectional features [WPF]
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
ms.openlocfilehash: 17167b1afa5037998d9ea8ed679a66c89babe242
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76741635"
---
# <a name="bidirectional-features-in-wpf-overview"></a>WPF の双方向機能の概要

他のどの開発プラットフォームとも異なり、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には双方向コンテンツ (たとえば、同じドキュメント内で左から右へ記述される情報と右から左へ記述されるデータが混在している状態) の迅速な開発をサポートする多数の機能があります。 また、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、アラビア語やヘブライ語を話すユーザーなど、双方向機能を必要とするユーザーに優れた操作性を提供します。

以降のセクションでは、多数の双方向機能と双方向コンテンツを最適に表示した例について説明します。 ほとんどのサンプルには XAML が使用されていますが、その概念は C# または Microsoft Visual Basic コードに簡単に適用できます。

<a name="FlowDirection"></a>

## <a name="flowdirection"></a>FlowDirection

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでコンテンツのフロー方向を定義する基本的なプロパティは <xref:System.Windows.FrameworkElement.FlowDirection%2A> です。 このプロパティは、2 つの列挙値 <xref:System.Windows.FlowDirection.LeftToRight> または <xref:System.Windows.FlowDirection.RightToLeft> のいずれかに設定できます。 このプロパティは、<xref:System.Windows.FrameworkElement> から継承されるすべての [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素で使用できます。

次の例では、<xref:System.Windows.Controls.TextBox> 要素のフロー方向を設定します。

**左から右へ記述するフロー方向**

[!code-xaml[LTRRTL#LTR](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]

**右から左へ記述するフロー方向**

[!code-xaml[LTRRTL#RTL](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]

次の図は、前のコードがどのように表示されるのかを示します。

![さまざまなフロー方向を示す図。](./media/bidirectional-features-in-wpf-overview/left-right-right-left.png)

[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] ツリー内の要素には、そのコンテナーから <xref:System.Windows.FrameworkElement.FlowDirection%2A> が継承されます。 次の例では、<xref:System.Windows.Controls.TextBlock> は、<xref:System.Windows.Window> 内の <xref:System.Windows.Controls.Grid> 内にあります。 <xref:System.Windows.Window> に <xref:System.Windows.FrameworkElement.FlowDirection%2A> を設定することは、<xref:System.Windows.Controls.Grid> と <xref:System.Windows.Controls.TextBlock> にも設定することを意味します。

次に <xref:System.Windows.FrameworkElement.FlowDirection%2A> の設定例を示します。

[!code-xaml[FlowDirection#FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]

最上位の <xref:System.Windows.Window> には <xref:System.Windows.FlowDirection.RightToLeft><xref:System.Windows.FlowDirection> があるため、その中に含まれるすべての要素にも同じ <xref:System.Windows.FrameworkElement.FlowDirection%2A> が継承されます。 指定された <xref:System.Windows.FrameworkElement.FlowDirection%2A> を要素でオーバーライドするには、前の例の 2 つ目の <xref:System.Windows.Controls.TextBlock> のように <xref:System.Windows.FlowDirection.LeftToRight> に変更するという明示的な方向変更を追加する必要があります。 <xref:System.Windows.FrameworkElement.FlowDirection%2A> が定義されていない場合は、既定の <xref:System.Windows.FlowDirection.LeftToRight> が適用されます。

次の図は、前の例の出力を示しています。

![明示的なフロー方向の変化を示す図。](./media/bidirectional-features-in-wpf-overview/explicit-direction-change.png)

<a name="FlowDocument"></a>

## <a name="flowdocument"></a>FlowDocument

HTML、Win32、Java などの多数の開発プラットフォームは、双方向コンテンツ開発を特別にサポートしています。 HTML などのマークアップ言語では、コンテンツの作成者が任意の必要な方向にテキストを表示するために必要なマークアップを使用できます。たとえば、"rtl" または "ltr" を値として解釈する HTML 4.0 タグの "dir" などです。 このタグは <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティに似ていますが、<xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティはテキスト コンテンツのレイアウト時により高度な方法で動作し、テキスト以外のコンテンツに使用できます。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の <xref:System.Windows.Documents.FlowDocument> は、テキスト、テーブル、画像、その他の要素の組み合わせをホストできる、汎用性のある [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素です。 以下のセクションのサンプルでは、この要素を使用します。

<xref:System.Windows.Documents.FlowDocument> へのテキストの追加は、さまざまな方法で行うことができます。 その簡単な方法は、テキストなどのコンテンツをグループ化するために使用されるブロックレベルの要素である <xref:System.Windows.Documents.Paragraph> を使用することです。 インラインレベルの要素にテキストを追加するために、このサンプルでは <xref:System.Windows.Documents.Span> と <xref:System.Windows.Documents.Run> を使用します。 <xref:System.Windows.Documents.Span> は、他のインライン要素のグループ化に使用されるインラインレベルのフロー コンテンツ要素です。一方、<xref:System.Windows.Documents.Run> は、一連の書式設定されていないテキストを含めることを目的としたインラインレベルのフロー コンテンツ要素です。 <xref:System.Windows.Documents.Span> には、複数の <xref:System.Windows.Documents.Run> 要素を含めることができます。

最初のドキュメント例には、いくつかのネットワーク共有名 (`\\server1\folder\file.ext` など) があるドキュメントが含まれます。 このネットワーク リンクがアラビア語または英語のいずれのドキュメントにあっても、常に同じように表示する必要があります。 次の図は、Span 要素の使用方法と、アラビア語の <xref:System.Windows.FlowDirection.RightToLeft> ドキュメント内のリンクを示しています。

![Span 要素の使用を示す図](./media/bidirectional-features-in-wpf-overview/flow-direction-span-element.png "FlowDocument")

テキストは <xref:System.Windows.FlowDirection.RightToLeft> であるため、"\\" などのすべての特殊文字では、右から左の順序でテキストが区切られます。 その結果、リンクが正しい順序で表示されなくなるため、問題を解決するには、テキストを埋め込み、フローが <xref:System.Windows.FlowDirection.LeftToRight> の <xref:System.Windows.Documents.Run> を別に保持する必要があります。 この問題を解決するには、言語ごとに個別の <xref:System.Windows.Documents.Run> を使用するのではなく、使用頻度の低い英語のテキストをより大きなアラビア語の <xref:System.Windows.Documents.Span> に埋め込む方法が適しています。

次の図は、Span 要素に埋め込まれた Run 要素を使用してこれを示しています。

![Span 要素に埋め込まれた Run 要素の使用を示す図](./media/bidirectional-features-in-wpf-overview/embedded-span-element.png)

次の例は、ドキュメントでの <xref:System.Windows.Documents.Run> および <xref:System.Windows.Documents.Span> 要素の使用を示しています。

[!code-xaml[RunSpan#RunSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]

<a name="SpanElements"></a>

## <a name="span-elements"></a>Span 要素

<xref:System.Windows.Documents.Span> 要素は、フロー方向が異なるテキスト間の境界区切り記号として機能します。  同じフロー方向の <xref:System.Windows.Documents.Span> 要素でも、双方向のスコープが異なると見なされます。つまり、<xref:System.Windows.Documents.Span> 要素はコンテナーの <xref:System.Windows.FlowDirection> で順序付けられ、<xref:System.Windows.Documents.Span> 要素内のコンテンツのみが <xref:System.Windows.Documents.Span> の <xref:System.Windows.FlowDirection> に従います。

次の図は、複数の <xref:System.Windows.Controls.TextBlock> 要素のフロー方向を示しています。

![フロー方向が異なるテキスト ブロックを示す図。](./media/bidirectional-features-in-wpf-overview/flow-direction-text-blocks.png)

次の例は、<xref:System.Windows.Documents.Span> および <xref:System.Windows.Documents.Run> 要素を使用して、前の図に示されている結果を生成する方法を示しています。

[!code-xaml[Span#Span](~/samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]

サンプルの <xref:System.Windows.Controls.TextBlock> 要素では、<xref:System.Windows.Documents.Span> 要素は親の <xref:System.Windows.FlowDirection>に従ってレイアウトされますが、各 <xref:System.Windows.Documents.Span> 要素内のテキストは独自の <xref:System.Windows.FlowDirection> に従ってフローします。 これは、ラテン語やアラビア語だけでなく、他のどの言語にも当てはまります。

### <a name="adding-xmllang"></a>xml:lang の追加

次の図は、`"200.0+21.4=221.4"` などの番号と算術式を使用する別の例を示します。 <xref:System.Windows.FlowDirection> のみが設定されていることに注意してください。

![FlowDirection のみを使用して数値を表示する図](./media/bidirectional-features-in-wpf-overview/numbers-flow-right-left.png)

このアプリケーションのユーザーは出力に失望するでしょう。<xref:System.Windows.FlowDirection> が正しいにもかかわらず、数字の形状がアラビア数字の本来の形状ではないからです。

XAML 要素には、各要素の言語を定義する XML 属性 (`xml:lang`) を含めることができます。 また、XAML では、ツリーの親要素に XML 値を適用すると、子要素にもその属性が適用されるという `xml:lang` 言語の原則も遵守されます。 前の例では、<xref:System.Windows.Documents.Run> 要素またはその最上位要素に言語が定義されていないため、既定の `xml:lang` (XAML の場合は `en-US`) が使用されました。 また、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の内部数字形成アルゴリズムによって、対応する言語 (この場合は英語) の数字が選択されます。 アラビア数字を正しく表示するためには、`xml:lang` を設定する必要があります。

次の図は、`xml:lang` を追加した例を示しています。

![右から左にフローするアラビア数字を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/arabic-numbers-flow-right-left.png)

次の例では、アプリケーションに `xml:lang` が追加されています。

[!code-xaml[LangAttribute#LangAttribute](~/samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]

多くの言語では、対象となる地域に応じて異なる `xml:lang` 値があります。たとえば、`"ar-SA"` と `"ar-EG"` はアラビア語の 2 つのバリエーションです。 前の例は、`xml:lang` と <xref:System.Windows.FlowDirection> の両方の値を定義する必要があることを示しています。

<a name="FlowDirectionNontext"></a>

## <a name="flowdirection-with-non-text-elements"></a>非テキスト要素のある FlowDirection

<xref:System.Windows.FlowDirection> を使用すると、テキスト要素内のテキストのフローだけでなく、他のほとんどすべての [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素のフロー方向も定義できます。 次の図は、水平方向の <xref:System.Windows.Media.LinearGradientBrush> を使用して、左から右へのグラデーションを付けて背景を描画する <xref:System.Windows.Controls.ToolBar> を示しています。

![左から右へのグラデーションを付けたツール バーを示す図](./media/bidirectional-features-in-wpf-overview/toolbar-left-right-gradient.png)

<xref:System.Windows.FlowDirection> を <xref:System.Windows.FlowDirection.RightToLeft> に設定すると、<xref:System.Windows.Controls.ToolBar> ボタンが右から左に配置されるだけでなく、<xref:System.Windows.Media.LinearGradientBrush> でもオフセットが右から左にフローするように再配置されます。

次の図は、<xref:System.Windows.Media.LinearGradientBrush> の再配置を示しています。

![右から左へのグラデーションを付けたツール バーを示す図](./media/bidirectional-features-in-wpf-overview/toolbar-right-left-gradient.png)

次の例では、<xref:System.Windows.FlowDirection.RightToLeft><xref:System.Windows.Controls.ToolBar> を描画します (左から右に描画するには、<xref:System.Windows.Controls.ToolBar> の <xref:System.Windows.FlowDirection> 属性を削除します)。

[!code-xaml[Gradient#Gradient](~/samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]

<a name="FlowDirectionExceptions"></a>

### <a name="flowdirection-exceptions"></a>FlowDirection の例外

<xref:System.Windows.FlowDirection> が想定どおりに動作しない場合がいくつかあります。 ここでは、そのような例外を 2 つ取り上げて説明します。

**イメージ**

<xref:System.Windows.Controls.Image> は、画像を表示するコントロールを表します。 XAML では、表示する <xref:System.Windows.Controls.Image> の Uniform Resource Identifier (URI) を定義する <xref:System.Windows.Controls.Image.Source%2A> プロパティでこれを使用できます。

他の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素とは異なり、<xref:System.Windows.Controls.Image> はコンテナーから <xref:System.Windows.FlowDirection> を継承しません。 ただし、<xref:System.Windows.FlowDirection> が明示的に <xref:System.Windows.FlowDirection.RightToLeft> に設定されている場合、<xref:System.Windows.Controls.Image> は左右反転して表示されます。 これは、双方向コンテンツの開発者にとって便利な機能として実装されています。場合によっては、イメージを左右反転して表示することで必要な効果が得られるためです。

次の図は、反転された <xref:System.Windows.Controls.Image> を示しています。

![反転された画像を示す図](./media/bidirectional-features-in-wpf-overview/flipped-image-example.png)

次の例は、<xref:System.Windows.Controls.Image> で、それを含む <xref:System.Windows.Controls.StackPanel> から <xref:System.Windows.FlowDirection> を継承できないことを示しています。

> [!NOTE]
> この例を実行するには、C:\ ドライブに **ms_logo.jpg** という名前のファイルが必要です。

[!code-xaml[Image#Image](~/samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]

> [!NOTE]
> ダウンロード ファイルには、**ms_logo.jpg** ファイルが含まれています。 コードは、この .jpg ファイルがプロジェクト内ではなく、C:\ ドライブ上にあることを前提としています。 プロジェクト内のファイルを検索するためには、プロジェクト ファイルから C:\ドライブに .jpg をコピーするかコードを変更する必要があります。 これを行うには、`Source="file://c:/ms_logo.jpg"` を `Source="ms_logo.jpg"` に変更します。

**パス**

<xref:System.Windows.Controls.Image> に加えて、もう 1 つの興味深い要素は <xref:System.Windows.Shapes.Path> です。 パスは、接続された一連の線と曲線を描画できるオブジェクトです。 <xref:System.Windows.FlowDirection> に関しては、<xref:System.Windows.Controls.Image> と同様に動作します。たとえば、<xref:System.Windows.FlowDirection.RightToLeft><xref:System.Windows.FlowDirection> は <xref:System.Windows.FlowDirection.LeftToRight> の水平方向のミラーです。 ただし、<xref:System.Windows.Controls.Image> とは異なり、<xref:System.Windows.Shapes.Path> ではコンテナーから <xref:System.Windows.FlowDirection> が継承されるので、明示的に指定する必要はありません。

次の例では、3 本の線を使用して単純な矢印を描画します。 最初の矢印では、<xref:System.Windows.FlowDirection.RightToLeft> のフロー方向が <xref:System.Windows.Controls.StackPanel> から継承されているため、その始点と終点は右側のルートから測定されます。 また、明示的な <xref:System.Windows.FlowDirection.RightToLeft><xref:System.Windows.FlowDirection> がある 2 つ目の矢印も右側から始まります。 ただし、3 番目の矢印の起点は左側です。 描画の詳細については、<xref:System.Windows.Media.LineGeometry> と <xref:System.Windows.Media.GeometryGroup> を参照してください。

[!code-xaml[Paths#Paths](~/samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]

次の図は、`Path` 要素を使用して矢印が描画された前の例の出力を示しています。

![Path 要素を使用して描画された矢印を示す図](./media/bidirectional-features-in-wpf-overview/arrows-drawn-path-element.png)

<xref:System.Windows.Controls.Image> と <xref:System.Windows.Shapes.Path> は、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] に <xref:System.Windows.FlowDirection> を使用する方法の 2 つの例です。 コンテナー内の特定の方向に [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素をレイアウトする以外に、<xref:System.Windows.FlowDirection> は、サーフェイスにインクをレンダリングする <xref:System.Windows.Controls.InkPresenter>、<xref:System.Windows.Media.LinearGradientBrush>、<xref:System.Windows.Media.RadialGradientBrush> などの要素と共に使用できます。 左から右への動作を模したコンテンツに対して右から左への動作が必要な場合、またはその逆の場合には、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] を使用すればその動作が可能になります。

<a name="NumberSubstitution"></a>

## <a name="number-substitution"></a>数字の置換

従来から、Windows は、同じ数字をカルチャによって異なる形状で表現できるようにすると同時に、ロケールが異なってもこれらの数字の内部ストレージを統一する (たとえば、数字をごく一般的な 16 進値である 0x40 や 0x41 で格納しながら、表示は選択された言語で行う) ことによって、数字の置換をサポートしてきました。

これによって、言語間での変換を行わなくてもアプリケーションが数値を処理することができます。たとえば、ローカライズされたアラビア語 Windows の Microsoft Excel スプレッドシートを開いて、アラビア語の形状の数字を表示することができますが、このスプレッドシートを Windows のヨーロッパ言語バージョンで開き、同じ数字のヨーロッパ語表現を表示することもできます。 これは、コンマ区切りやパーセント記号などの他の記号でも必要です。これらの記号は、通常同じドキュメント内で数字を伴っているからです。

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は引き続きこの機能を備え、置換を使用するタイミングと方法をユーザーがさらに制御できるようにこの機能のサポートが強化されています。 この機能はすべての言語向けに設計されていますが、アプリケーションが実行される可能性のあるカルチャが多岐にわたるために特定の言語に合わせて数字の形状を設定することがアプリケーション開発者にとって通常は問題となる双方向コンテンツに対して特に有用です。

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] での数字の置換動作を制御するコア プロパティは、<xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 依存関係プロパティです。 <xref:System.Windows.Media.NumberSubstitution> クラスには、テキスト内の数値の表示方法を指定します。 その動作を定義する 3 つのパブリック プロパティがあります。 以下は、各プロパティの概要です。

**CultureSource:**

このプロパティは、数字のカルチャを決定する方法を指定します。 これは、3 つの <xref:System.Windows.Media.NumberCultureSource> 列挙値のいずれかを受け取ります。

- オーバーライド:数値カルチャは、<xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> プロパティのカルチャです。

- テキスト:数字カルチャは、テキスト ランのカルチャです。 マークアップでは、これは `xml:lang` またはそのエイリアス `Language` プロパティ (<xref:System.Windows.FrameworkElement.Language%2A> または <xref:System.Windows.FrameworkContentElement.Language%2A>) になります。 また、これは <xref:System.Windows.FrameworkContentElement> から派生したクラスの既定値です。 このようなクラスには、<xref:System.Windows.Documents.Paragraph?displayProperty=nameWithType>、<xref:System.Windows.Documents.Table?displayProperty=nameWithType>、<xref:System.Windows.Documents.TableCell?displayProperty=nameWithType> などがあります。

- ユーザー:数値カルチャは、現在のスレッドのカルチャです。 このプロパティは、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Window>、<xref:System.Windows.Controls.TextBlock> などの <xref:System.Windows.FrameworkElement> のすべてのサブクラスの既定値です。

**CultureOverride**:

<xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> プロパティは、<xref:System.Windows.Media.NumberSubstitution.CultureSource%2A> プロパティが <xref:System.Windows.Media.NumberCultureSource.Override> に設定されている場合にのみ使用され、それ以外の場合は無視されます。 このプロパティは数字カルチャを指定します。 既定値である `null` の値は、en-US として解釈されます。

**Substitution**:

このプロパティは、実行する数字の置換の種類を指定します。 次の <xref:System.Windows.Media.NumberSubstitutionMethod> 列挙値のいずれかを受け取ります。

- <xref:System.Windows.Media.NumberSubstitutionMethod.AsCulture>:置換方法は、数字カルチャの <xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=nameWithType> プロパティに基づいて決まります。 既定値です。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Context>:数字カルチャがアラビアまたはペルシャのカルチャである場合に、数字がコンテキストによって異なるように指定します。

- <xref:System.Windows.Media.NumberSubstitutionMethod.European>:数字は常にヨーロッパの数字としてレンダリングされます。

- <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>:数字は、カルチャの <xref:System.Globalization.CultureInfo.NumberFormat%2A> で指定されているように、数字カルチャの国番号を使用してレンダリングされます。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Traditional>:数字は、数字カルチャの通常の数字を使用してレンダリングされます。 ほとんどのカルチャでは、これは <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> と同じです。 ただし、<xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> の結果は、一部のアラビア カルチャではラテン数字になりますが、この値の結果は、すべてのアラビア カルチャでアラビア数字になります。

これらの値は双方向コンテンツ開発者にとってどういった意味があるのでしょうか。 ほとんどの場合、開発者は <xref:System.Windows.FlowDirection> と各テキストの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素の言語を定義するだけで済みます。たとえば、`Language="ar-SA"` と <xref:System.Windows.Media.NumberSubstitution> ロジックは、正しい [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] に従って数字を表示します。 次の例は、Windows のアラビア語版で実行されている [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションでアラビア数字と英語数字を使用する方法を示します。

[!code-xaml[Numbers#Numbers](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]

次の図は、アラビア語と英語の数字が表示されるアラビア語バージョンの Windows で、前のサンプルを実行した場合の出力を示しています。

![アラビア語と英語の数字を示す図](./media/bidirectional-features-in-wpf-overview/arabic-english-numbers.png)

この場合は <xref:System.Windows.FlowDirection> を <xref:System.Windows.FlowDirection.LeftToRight> に設定するとヨーロッパの数字が得られるため、<xref:System.Windows.FlowDirection> が重要でした。 以下のセクションでは、ドキュメント全体で数字の表示を統一する方法について説明します。 この例では、アラビア語版 Windows で実行されていなければ、すべての数字がヨーロッパ数字として表示されます。

**置換ルールの定義**

実際のアプリケーションでは、プログラムでの言語設定が必要となる場合があります。 たとえば、`xml:lang` 属性をシステムの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] により使用されている属性と同じものに設定する場合もあり、アプリケーション状態に応じて言語を変更する場合もあります。

アプリケーションの状態に基づいて変更を行う場合には、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で提供される他の機能を使用してください。

アプリケーション コンポーネントの `NumberSubstitution.CultureSource="Text"` を最初に設定します。 この設定を使用すると、<xref:System.Windows.Controls.TextBlock> など、既定値として "User" を持つテキスト要素の設定が [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] から取得されないようになります。

次に例を示します。

```xaml
<TextBlock
   Name="text1" NumberSubstitution.CultureSource="Text">
   1234+5679=6913
</TextBlock>
```

対応する C# コードで、たとえば `Language` プロパティを `"ar-SA"` に設定します。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");
```

`Language` プロパティを現在のユーザーの UI 言語に設定する必要がある場合は、次のコードを使用します。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage(System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);
```

<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> は、実行時にその時点のスレッドによって使用されているその時点のカルチャを表します。

最終的な XAML 例は次の例のようになります。

[!code-xaml[Numbers2#Numbers2](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]

最終的な C# 例は次のようなものになります。

[!code-csharp[NumbersCSharp#NumbersCSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]

次の図は、いずれのプログラミング言語でも、アラビア数字がウィンドウにどのように表示されるかを示しています。

![アラビア数字を表示した図](./media/bidirectional-features-in-wpf-overview/displays-arabic-numbers.png)

**Substitution プロパティの使用**

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] での数字の置換動作は、テキスト要素の言語とその <xref:System.Windows.FlowDirection> の両方によって変わります。 <xref:System.Windows.FlowDirection> が左から右の場合、ヨーロッパの数字がレンダリングされます。 ただし、前にアラビア語のテキストがある場合、または言語が "ar" に設定されていて <xref:System.Windows.FlowDirection> が <xref:System.Windows.FlowDirection.RightToLeft> の場合は、代わりにアラビア数字が表示されます。

ただし、たとえば、すべてのユーザーに対してヨーロッパ数字を表示するなどの、統一されたアプリケーションを作成する必要がある場合もあります。 または、特定の <xref:System.Windows.Style> を持つ <xref:System.Windows.Documents.Table> セルにアラビア数字を使用します。 これを行う簡単な方法の 1 つは、<xref:System.Windows.Media.NumberSubstitution.Substitution%2A> プロパティを使用することです。

次の例では、最初の <xref:System.Windows.Controls.TextBlock> には <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> プロパティが設定されていないため、アルゴリズムによって想定どおりにアラビア数字が表示されます。 ただし、2 つ目の <xref:System.Windows.Controls.TextBlock> では、置換はヨーロッパに設定され、アラビア数字の既定の置換がオーバーライドされているため、ヨーロッパ数字が表示されます。

[!code-xaml[Numbers3#Numbers3](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]
