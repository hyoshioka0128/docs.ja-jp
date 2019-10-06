---
title: WPF の双方向機能の概要
ms.date: 03/30/2017
helpviewer_keywords:
- Span elements [WPF]
- bidirectional features [WPF]
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
ms.openlocfilehash: 2a599322ef955b9f702f8960f294f5d093ede74a
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834747"
---
# <a name="bidirectional-features-in-wpf-overview"></a>WPF の双方向機能の概要

他の開発プラットフォームとは[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]異なり、には、双方向のコンテンツの迅速な開発をサポートする多くの機能があります。たとえば、左から右へ、および同じドキュメント内の右から左へのデータの配置をサポートします。 また、は、 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]アラビア語やヘブライ語圏のユーザーなどの双方向機能を必要とするユーザーに優れたエクスペリエンスを提供します。

以降のセクションでは、多数の双方向機能と双方向コンテンツを最適に表示した例について説明します。 ほとんどのサンプルでは[!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)]を使用しますが、または Microsoft C# Visual Basic コードに簡単に概念を適用できます。

<a name="FlowDirection"></a>

## <a name="flowdirection"></a>FlowDirection

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]アプリケーションのコンテンツフローの方向を定義する基本プロパティは<xref:System.Windows.FrameworkElement.FlowDirection%2A>です。 このプロパティは、2つの列挙値 (または<xref:System.Windows.FlowDirection.LeftToRight> <xref:System.Windows.FlowDirection.RightToLeft>) のいずれかに設定できます。 プロパティは、から[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.FrameworkElement>継承されるすべての要素で使用できます。

次の例では、 <xref:System.Windows.Controls.TextBox>要素のフロー方向を設定します。

**左から右へ記述するフロー方向**

[!code-xaml[LTRRTL#LTR](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]

**右から左へ記述するフロー方向**

[!code-xaml[LTRRTL#RTL](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]

次の図は、前のコードがどのように表示されるのかを示します。

![さまざまなフロー方向を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/left-right-right-left.png)

[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]ツリー内の要素は、 <xref:System.Windows.FrameworkElement.FlowDirection%2A>コンテナーからを継承します。 次の例<xref:System.Windows.Controls.TextBlock>では<xref:System.Windows.Controls.Grid>、は内に存在する、内に<xref:System.Windows.Window>あります。 を<xref:System.Windows.FrameworkElement.FlowDirection%2A> <xref:System.Windows.Controls.Grid>に設定すると、と<xref:System.Windows.Controls.TextBlock>にも設定されます。 <xref:System.Windows.Window>

を設定<xref:System.Windows.FrameworkElement.FlowDirection%2A>する例を次に示します。

[!code-xaml[FlowDirection#FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]

最上位レベル<xref:System.Windows.Window>には<xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.FlowDirection>があるため、その中に含まれるすべての<xref:System.Windows.FrameworkElement.FlowDirection%2A>要素も同じを継承します。 要素が指定され<xref:System.Windows.FrameworkElement.FlowDirection%2A>たをオーバーライドするには、前の例の2番目<xref:System.Windows.Controls.TextBlock>の例で、に<xref:System.Windows.FlowDirection.LeftToRight>変更する明示的な方向の変更を追加する必要があります。 が定義<xref:System.Windows.FrameworkElement.FlowDirection%2A>されていない<xref:System.Windows.FlowDirection.LeftToRight>場合、既定値が適用されます。

次の図は、前の例の出力を示しています。

![明示的なフロー方向の変更を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/explicit-direction-change.png)

<a name="FlowDocument"></a>

## <a name="flowdocument"></a>FlowDocument

HTML や Java などの多くの[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]開発プラットフォームでは、双方向のコンテンツ開発に対して特別なサポートを提供しています。 HTML などのマークアップ言語では、必要な方向にテキストを表示するために必要なマークアップがコンテンツライターに与えられます。たとえば、HTML 4.0 タグでは、"rtl" または "ltr" を値として受け取ります。 このタグは<xref:System.Windows.FrameworkElement.FlowDirection%2A>プロパティに似ていますが<xref:System.Windows.FrameworkElement.FlowDirection%2A> 、プロパティはテキストコンテンツをレイアウトするより高度な方法で動作し、テキスト以外のコンテンツに使用できます。

で[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]は、は、テキスト[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 、テーブル、イメージ、およびその他の要素の組み合わせをホストできる、汎用性のある要素です。 <xref:System.Windows.Documents.FlowDocument> 以下のセクションのサンプルでは、この要素を使用します。

へのテキストの<xref:System.Windows.Documents.FlowDocument>追加は、1つの方法で行うことができます。 これを行う簡単な方法は、テキスト<xref:System.Windows.Documents.Paragraph>などのコンテンツをグループ化するために使用されるブロックレベルの要素であるを使用することです。 インラインレベルの要素にテキストを追加するには<xref:System.Windows.Documents.Span> 、 <xref:System.Windows.Documents.Run>サンプルでおよびを使用します。 <xref:System.Windows.Documents.Span>はインラインレベルのフローコンテンツ要素で、他のインライン要素をグループ化する<xref:System.Windows.Documents.Run>ために使用されます。は、書式設定されていないテキストの実行を格納するためのインラインレベルのフローコンテンツ要素です。 に<xref:System.Windows.Documents.Span>は、複数<xref:System.Windows.Documents.Run>の要素を含めることができます。

最初のドキュメントの例には、多数のネットワーク共有名を持つドキュメントが含まれています。たとえば`\\server1\folder\file.ext`、のようになります。 このネットワーク リンクがアラビア語または英語のいずれのドキュメントにあっても、常に同じように表示する必要があります。 次の図は、Span 要素を使用して、アラビア語<xref:System.Windows.FlowDirection.RightToLeft>ドキュメントにリンクを示しています。

![Span 要素の使用方法を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/flow-direction-span-element.png "FlowDocument")

テキストは<xref:System.Windows.FlowDirection.RightToLeft>であるため、"\\" などのすべての特殊文字は、右から左の順序でテキストを区切ります。 その結果、リンクが正しい順序で表示されなくなるため、問題を解決するには、別<xref:System.Windows.Documents.Run>のフロー <xref:System.Windows.FlowDirection.LeftToRight>を維持するためにテキストを埋め込む必要があります。 この問題を解決する<xref:System.Windows.Documents.Run>には、言語ごとに個別のを用意するのではなく、使用頻度の低い英語のテキストを<xref:System.Windows.Documents.Span>より大きなアラビア語に埋め込むことをお勧めします。

次の図は、Span 要素に埋め込まれた Run 要素を使用してこれを示しています。

![Span 要素に埋め込まれている Run 要素を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/embedded-span-element.png)

次の例では<xref:System.Windows.Documents.Run> 、 <xref:System.Windows.Documents.Span>ドキュメントで要素と要素を使用する方法を示します。

[!code-xaml[RunSpan#RunSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]

<a name="SpanElements"></a>

## <a name="span-elements"></a>Span 要素

要素<xref:System.Windows.Documents.Span>は、フロー方向が異なるテキスト間の境界区切り記号として機能します。  同じ<xref:System.Windows.Documents.Span>フロー方向を持つ要素でも、異なる双方向のスコープを持つと見なさ<xref:System.Windows.Documents.Span>れます。つまり、要素は<xref:System.Windows.FlowDirection>コンテナー内で順序付けら<xref:System.Windows.Documents.Span>れ、要素内のコンテンツのみが順序付けされます。のに<xref:System.Windows.FlowDirection>従います。<xref:System.Windows.Documents.Span>

次の図は、複数<xref:System.Windows.Controls.TextBlock>の要素のフロー方向を示しています。

![フロー方向が異なるテキストブロックを示すグラフィック。](./media/bidirectional-features-in-wpf-overview/flow-direction-text-blocks.png)

次の例では、要素<xref:System.Windows.Documents.Span>と<xref:System.Windows.Documents.Run>要素を使用して、前の図に示した結果を生成する方法を示します。

[!code-xaml[Span#Span](~/samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]

<xref:System.Windows.Documents.Span> <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection>このサンプル<xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Documents.Span>の要素では、要素は親のに従ってレイアウトされますが、各要素内のテキストは独自の要素によって流れます。 これは、ラテン語やアラビア語だけでなく、他のどの言語にも当てはまります。

### <a name="adding-xmllang"></a>xml:lang の追加

次の図は、数値と算術式 (など) `"200.0+21.4=221.4"`を使用する別の例を示しています。 <xref:System.Windows.FlowDirection>が設定されていることに注意してください。

![System.windows.flowdirection> のみを使用して数値を表示するグラフィック。](./media/bidirectional-features-in-wpf-overview/numbers-flow-right-left.png)

<xref:System.Windows.FlowDirection>が正しい場合でも、このアプリケーションのユーザーには出力が表示されます。数字は、アラビア数字が整形されるように整形されません。

XAML 要素には、 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]各要素`xml:lang`の言語を定義する属性 () を含めることができます。 XAML では、 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]ツリー内の`xml:lang`親要素に適用される値が子要素によって使用される言語の原則もサポートされています。 前の例では、言語が<xref:System.Windows.Documents.Run>要素または最上位レベルの要素に対して定義されていないため、XAML `en-US`の既定値`xml:lang`が使用されていました。 の[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]内部数値整形アルゴリズムでは、対応する言語 (この場合は英語) の数値が選択されます。 アラビア数字を正しく`xml:lang`表示するには、設定する必要があります。

次の図は、を追加`xml:lang`した例を示しています。

![右から左に記述されるアラビア数字を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/arabic-numbers-flow-right-left.png)

次の例で`xml:lang`は、をアプリケーションに追加します。

[!code-xaml[LangAttribute#LangAttribute](~/samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]

多くの言語は、対象と`xml:lang`なる地域によって異なる値を持つこと`"ar-SA"`に`"ar-EG"`注意してください。たとえば、はアラビア語の2つのバリエーションを表します。 前の例では、と`xml:lang` <xref:System.Windows.FlowDirection>の両方の値を定義する必要があることを示しています。

<a name="FlowDirectionNontext"></a>

## <a name="flowdirection-with-non-text-elements"></a>非テキスト要素のある FlowDirection

<xref:System.Windows.FlowDirection>テキスト要素内のテキストフローだけでなく、ほぼすべての[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]要素のフロー方向も定義します。 次の図は、 <xref:System.Windows.Controls.ToolBar>水平方向<xref:System.Windows.Media.LinearGradientBrush>のを使用して、左から右へのグラデーションで背景を描画するを示しています。

![左から右へのグラデーションが表示されたツールバーを示すグラフィック。](./media/bidirectional-features-in-wpf-overview/toolbar-left-right-gradient.png)

<xref:System.Windows.FlowDirection>をに設定する<xref:System.Windows.FlowDirection.RightToLeft>と、 <xref:System.Windows.Controls.ToolBar>ボタンが右<xref:System.Windows.Media.LinearGradientBrush>から左に配置されるだけでなく、右から左へのフローに再配置されます。

次の図は、 <xref:System.Windows.Media.LinearGradientBrush>の再編成を示しています。

![右から左にグラデーションが表示されたツールバーを示すグラフィック。](./media/bidirectional-features-in-wpf-overview/toolbar-right-left-gradient.png)

を描画する<xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.Controls.ToolBar>例を次に示します。 (左から右に描画するには、 <xref:System.Windows.FlowDirection>の<xref:System.Windows.Controls.ToolBar>属性を削除します。

[!code-xaml[Gradient#Gradient](~/samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]

<a name="FlowDirectionExceptions"></a>

### <a name="flowdirection-exceptions"></a>FlowDirection の例外

<xref:System.Windows.FlowDirection>が予期したとおりに動作しないケースがいくつかあります。 ここでは、そのような例外を 2 つ取り上げて説明します。

**[イメージ]**

は<xref:System.Windows.Controls.Image> 、イメージを表示するコントロールを表します。 で[!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)]は、 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] <xref:System.Windows.Controls.Image.Source%2A> 表示<xref:System.Windows.Controls.Image>するのを定義するプロパティと共に使用できます。

他の[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]要素<xref:System.Windows.Controls.Image>とは異なり、はコンテナー <xref:System.Windows.FlowDirection>からを継承しません。 ただし、が明示<xref:System.Windows.FlowDirection>的にに設定され<xref:System.Windows.Controls.Image>ている場合、は水平方向に<xref:System.Windows.FlowDirection.RightToLeft>反転して表示されます。 これは、双方向コンテンツの開発者にとって便利な機能として実装されています。場合によっては、イメージを左右反転して表示することで必要な効果が得られるためです。

次の図は、反転<xref:System.Windows.Controls.Image>されたを示しています。

![反転された画像を示す図。](./media/bidirectional-features-in-wpf-overview/flipped-image-example.png)

次の例は、 <xref:System.Windows.Controls.Image>がそれを含む<xref:System.Windows.FlowDirection>から<xref:System.Windows.Controls.StackPanel>を継承できないことを示しています。

> [!NOTE]
> C:\ に ms_logo という名前のファイルが必要**です。** この例を実行するドライブです。

[!code-xaml[Image#Image](~/samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]

> [!NOTE]
> ダウンロードファイルには、 **ms_logo**ファイルが含まれています。 コードは、この .jpg ファイルがプロジェクト内ではなく、C:\ ドライブ上にあることを前提としています。 プロジェクト内のファイルを検索するためには、プロジェクト ファイルから C:\ドライブに .jpg をコピーするかコードを変更する必要があります。 これを行うに`Source="file://c:/ms_logo.jpg"`は`Source="ms_logo.jpg"`、をに変更します。

**パス**

に<xref:System.Windows.Controls.Image>加えて、もう1つの興味<xref:System.Windows.Shapes.Path>深い要素はです。 パスは、接続された一連の線と曲線を描画できるオブジェクトです。 これ<xref:System.Windows.Controls.Image> <xref:System.Windows.FlowDirection>は、に<xref:System.Windows.FlowDirection>関するに似た方法で動作します。 <xref:System.Windows.FlowDirection.RightToLeft>たとえば、はその<xref:System.Windows.FlowDirection.LeftToRight> 1 つの水平方向のミラーです。 ただし、とは<xref:System.Windows.Controls.Image>異なり<xref:System.Windows.Shapes.Path> 、は<xref:System.Windows.FlowDirection>コンテナーからを継承し、1つを明示的に指定する必要はありません。

次の例では、3 本の線を使用して単純な矢印を描画します。 最初の矢印はから<xref:System.Windows.FlowDirection.RightToLeft>のフロー方向を<xref:System.Windows.Controls.StackPanel>継承するため、始点と終点が右側のルートから測定されます。 また、明示的<xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.FlowDirection>なを含む2番目の矢印も右側から開始します。 ただし、3 番目の矢印の起点は左側です。 描画の詳細について<xref:System.Windows.Media.LineGeometry>は<xref:System.Windows.Media.GeometryGroup>、「」および「」を参照してください。

[!code-xaml[Paths#Paths](~/samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]

次の図は、 `Path`要素を使用して描画された矢印を含む前の例の出力を示しています。

![Path 要素を使用して描画された矢印を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/arrows-drawn-path-element.png)

と<xref:System.Windows.Controls.Image> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.FlowDirection>は、がを使用する方法の2つの例です。 <xref:System.Windows.Shapes.Path> コンテナー内の[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]特定の方向に要素をレイアウトすると<xref:System.Windows.FlowDirection> <xref:System.Windows.Controls.InkPresenter> 、などの要素で使用でき<xref:System.Windows.Media.RadialGradientBrush>ます。この要素は、画面<xref:System.Windows.Media.LinearGradientBrush>上でインクを描画します。 左から右への動作を模倣するコンテンツに対して右から左の動作が必要な場合、 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]またはその逆の場合は、その機能を提供します。

<a name="NumberSubstitution"></a>

## <a name="number-substitution"></a>数字の置換

従来、Windows では数字の置換がサポートされています。これにより、さまざまなカルチャを同じ数字で表現できるようになり、数字の内部ストレージを異なるロケール間で統合できるようになりました。たとえば、数値はよく知られている16進値0x40、0x41。ただし、選択した言語に従って表示されます。

これにより、アプリケーションで数値を処理できるようになりました。これらの値は、ある言語から別の言語[!INCLUDE[TLA#tla_xl](../../../../includes/tlasharptla-xl-md.md)]に変換する必要がありません。たとえば、ローカライズされたアラビア語ウィンドウでスプレッドシートを開き、アラビア語の数字を表示し、Windows の欧州バージョンと、同じ数値の欧州表現を参照してください。 これは、コンマ区切りやパーセント記号などの他の記号でも必要です。これらの記号は、通常同じドキュメント内で数字を伴っているからです。

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は引き続きこの機能を備え、置換を使用するタイミングと方法をユーザーがさらに制御できるようにこの機能のサポートが強化されています。 この機能はすべての言語向けに設計されていますが、アプリケーションが実行される可能性のあるカルチャが多岐にわたるために特定の言語に合わせて数字の形状を設定することがアプリケーション開発者にとって通常は問題となる双方向コンテンツに対して特に有用です。

での[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]数値置換の動作を制御するコアプロパティ<xref:System.Windows.Media.NumberSubstitution.Substitution%2A>は、依存関係プロパティです。 クラス<xref:System.Windows.Media.NumberSubstitution>は、テキスト内の数字を表示する方法を指定します。 その動作を定義する 3 つのパブリック プロパティがあります。 各プロパティの概要を次に示します。

**CultureSource:**

このプロパティは、数字のカルチャを決定する方法を指定します。 3 <xref:System.Windows.Media.NumberCultureSource>つの列挙値のいずれかを受け取ります。

- オーバーライド数値カルチャは、プロパティ<xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A>の値です。

- 本文数値カルチャは、テキストランのカルチャです。 マークアップ`xml:lang`では、、またはそのエイリアス`Language`プロパティ (<xref:System.Windows.FrameworkElement.Language%2A>また<xref:System.Windows.FrameworkContentElement.Language%2A>は) になります。 また、から<xref:System.Windows.FrameworkContentElement>派生するクラスの既定値です。 このような<xref:System.Windows.Documents.Paragraph?displayProperty=nameWithType>クラスには<xref:System.Windows.Documents.Table?displayProperty=nameWithType>、 、などがあります。<xref:System.Windows.Documents.TableCell?displayProperty=nameWithType>

- ユーザー:数値カルチャは、現在のスレッドのカルチャです。 この<xref:System.Windows.FrameworkElement>プロパティは<xref:System.Windows.Controls.Page>、、、など、 <xref:System.Windows.Window> <xref:System.Windows.Controls.TextBlock>のすべてのサブクラスの既定値です。

**CultureOverride**:

プロパティは、 <xref:System.Windows.Media.NumberSubstitution.CultureSource%2A>プロパティがに設定されている<xref:System.Windows.Media.NumberCultureSource.Override>場合にのみ使用され、それ以外の場合は無視されます。 <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> このプロパティは数字カルチャを指定します。 値`null`(既定値) は en-us として解釈されます。

**Substitution**:

このプロパティは、実行する数字の置換の種類を指定します。 次<xref:System.Windows.Media.NumberSubstitutionMethod>の列挙値のいずれかを取得します。

- <xref:System.Windows.Media.NumberSubstitutionMethod.AsCulture>:置換メソッドは、数値カルチャの<xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=nameWithType>プロパティに基づいて決定されます。 既定値です。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Context>:数字カルチャがアラビア語またはペルシャ語のカルチャである場合は、数字がコンテキストに依存することを指定します。

- <xref:System.Windows.Media.NumberSubstitutionMethod.European>:数値は常にヨーロッパの数字としてレンダリングされます。

- <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>:数字は、カルチャの<xref:System.Globalization.CultureInfo.NumberFormat%2A>で指定されているように、数字カルチャの national 数字を使用して表示されます。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Traditional>:数値は、数字カルチャに対して従来の数字を使用してレンダリングされます。 ほとんどのカルチャでは、これはと<xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>同じです。 ただし、 <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>アラビア語カルチャによってはラテン数字が使用されますが、この値はすべてのアラビアカルチャでアラビア数字になります。

これらの値は双方向コンテンツ開発者にとってどういった意味があるのでしょうか。 ほとんどの場合、開発者は、 <xref:System.Windows.FlowDirection>各テキスト[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]要素の言語を定義するだけで済みます。 `Language="ar-SA"`たとえば、 <xref:System.Windows.Media.NumberSubstitution>ロジックは正しい[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]値に従って数値を表示します。 アラビア語版の Windows で実行されている[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]アプリケーションでアラビア数字と英語番号を使用する例を次に示します。

[!code-xaml[Numbers#Numbers](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]

アラビア語と英語の数字が表示されたアラビア語版の Windows で実行している場合は、前の例の出力を次の図に示します。

![アラビア数字と英語番号を示すグラフィック。](./media/bidirectional-features-in-wpf-overview/arabic-english-numbers.png)

をに<xref:System.Windows.FlowDirection>設定する<xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection.LeftToRight>と、ヨーロッパの数字が生成されるため、この場合はが重要でした。 以下のセクションでは、ドキュメント全体で数字の表示を統一する方法について説明します。 この例では、アラビア語版 Windows で実行されていなければ、すべての数字がヨーロッパ数字として表示されます。

**置換ルールの定義**

実際のアプリケーションでは、プログラムでの言語設定が必要となる場合があります。 たとえば、システムによって使用さ`xml:lang`れている属性と同じ属性を設定したり、アプリケーション[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]の状態に応じて言語を変更したりすることができます。

アプリケーションの状態に基づいて変更を行う場合は、によっ[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]て提供される他の機能を使用します。

最初に、アプリケーションコンポーネントの`NumberSubstitution.CultureSource="Text"`を設定します。 この設定を使用すると[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] <xref:System.Windows.Controls.TextBlock>、のように、既定値として "User" を持つテキスト要素の設定がから取得されないようにします。

以下に例を示します。

```xaml
<TextBlock
   Name="text1" NumberSubstitution.CultureSource="Text">
   1234+5679=6913
</TextBlock>
```

対応C#するコードで、などの`Language`プロパティをに`"ar-SA"`設定します。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");
```

`Language`プロパティを現在のユーザーの UI 言語に設定する必要がある場合は、次のコードを使用します。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage(System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);
```

<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>実行時に現在のスレッドによって使用されている現在のカルチャを表します。

最後[!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)]の例は、次の例のようになります。

[!code-xaml[Numbers2#Numbers2](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]

最後C#の例は次のようになります。

[!code-csharp[NumbersCSharp#NumbersCSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]

次の図は、いずれかのプログラミング言語でのウィンドウの外観を示しています。アラビア数字が表示されています。

![アラビア数字を表示するグラフィック。](./media/bidirectional-features-in-wpf-overview/displays-arabic-numbers.png)

**Substitution プロパティの使用**

での[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]数値置換の動作は、テキスト要素の言語とその<xref:System.Windows.FlowDirection>の言語によって異なります。 <xref:System.Windows.FlowDirection>が左から右にある場合は、ヨーロッパの数字が表示されます。 ただし、その前にアラビア語のテキストが含まれている場合、または言語が<xref:System.Windows.FlowDirection> " <xref:System.Windows.FlowDirection.RightToLeft>ar" に設定されていて、がの場合は、アラビア数字が代わりに表示されます。

ただし、たとえば、すべてのユーザーに対してヨーロッパ数字を表示するなどの、統一されたアプリケーションを作成する必要がある場合もあります。 または、特定<xref:System.Windows.Documents.Table> <xref:System.Windows.Style>のを持つセルにアラビア数字を使用します。 これを行う簡単な方法の1つ<xref:System.Windows.Media.NumberSubstitution.Substitution%2A>は、プロパティを使用することです。

次の例では、最初<xref:System.Windows.Controls.TextBlock>のに<xref:System.Windows.Media.NumberSubstitution.Substitution%2A>プロパティが設定されていないため、アルゴリズムではアラビア数字が想定どおりに表示されます。 ただし、2番<xref:System.Windows.Controls.TextBlock>目の方法では、置換はヨーロッパに設定され、アラビア数字の既定の置換が上書きされ、ヨーロッパの数字が表示されます。

[!code-xaml[Numbers3#Numbers3](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]
