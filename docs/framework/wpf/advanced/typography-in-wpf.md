---
title: タイポグラフィ
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], about typography
ms.assetid: 06cbf17b-6eff-4fe5-949d-2dd533e4e1f4
ms.openlocfilehash: 501a4221c99d405484a2fb908641d27d1f38f266
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187349"
---
# <a name="typography-in-wpf"></a>WPF のタイポグラフィ
このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の主要な文字体裁の機能について説明します。 これらの機能には、テキスト レンダリングの品質とパフォーマンスの向上、OpenType タイポグラフィのサポート、国際対応テキストの強化、フォントのサポートの強化、新しいテキスト API (アプリケーション プログラミング インターフェイス) が含まれます。  
  
<a name="Improved_Quality_and_Performance_of_Text"></a>
## <a name="improved-quality-and-performance-of-text"></a>テキストに関する品質とパフォーマンスの向上  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のテキストは、テキストのわかりやすさと読みやすさを高める Microsoft ClearType を使用して描画されます。 ClearType は、ラップトップや Pocket PC の画面、フラット パネル モニターなど、既存の LCD (液晶ディスプレイ) でのテキストの読みやすさを向上させるために Microsoft によって開発されたソフトウェア テクノロジです。 ClearType では、ピクセルの画素レベルで文字を表示調整することで実際の形状を忠実に再現したテキストを表示できる、サブピクセル レンダリングが採用されています。 解像度が上がるとテキスト表示の微細部の鮮明度が高くなるため、長時間にわたって読んでも苦になりません。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での ClearType のもう 1 つの改良点は、y 方向のアンチエイリアシングです。これにより、テキスト文字の緩やかな曲線部の上下が滑らかになります。 ClearType の機能の詳細については、「[ClearType の概要](cleartype-overview.md)」を参照してください。  
  
 ![ClearType y 方向アンチエイリアシングを含むテキスト](./media/typography-in-wpf/text-y-direction-antialiasing.gif)  
ClearType の y 方向アンチエイリアシングを適用したテキスト  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、コンピューターがハードウェアの最小要件を満たしている限り、テキスト レンダリング パイプライン全体に対してハードウェア アクセラレータを使用できます。 ハードウェアを使用して実行できないレンダリングは、ソフトウェア レンダリングとなります。 ハードウェア アクセラレータは、個々のグリフの格納から始まり、グリフ実行への複数のグリフの合成、効果の適用、最終的な表示出力への ClearType ブレンディング アルゴリズムの適用まで、テキスト レンダリング パイプラインのすべてのフェーズに影響します。 ハードウェア アクセラレータの詳細については、「[グラフィックスの描画層](graphics-rendering-tiers.md)」をご覧ください。  
  
 ![パイプラインを描画するテキストのダイアグラム](./media/typography-in-wpf/text-rendering-pipeline.png)  
  
 また、アニメーション化されたテキストは、文字とグリフのいずれによる場合でも、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で有効化されているグラフィックス ハードウェア機能をすべて利用できます。 これにより、テキスト アニメーションが滑らかになります。  
  
<a name="Rich_Typography"></a>
## <a name="rich-typography"></a>多彩な文字体裁  
 OpenType フォント形式は、TrueType® フォント形式の拡張です。 OpenType フォント形式は、Microsoft と Adobe が共同で開発したもので、高度なタイポグラフィ機能を豊富に備えています。 <xref:System.Windows.Documents.Typography> オブジェクトでは、スタイル代替グリフや飾り付きなど、OpenType フォントの高度な機能の多くが公開されています。 Windows SDK には、Pericles フォントや Pescadero フォントなど、豊富な機能を持つ OpenType フォント サンプルが用意されています。 詳細については、「[OpenType フォント パックのサンプル](sample-opentype-font-pack.md)」をご覧ください。  
  
 Pericles OpenType フォントには、標準グリフ セットにスタイル代替グリフを提供する追加グリフが含まれています。 次のテキストでは、スタイル代替グリフが表示されています。  
  
 ![OpenType のスタイル代替グリフを使用するテキスト](./media/typography-in-wpf/opentype-stylistic-alternate-glyphs.gif "OpenType のスタイル代替グリフを使用するテキスト")  
  
 スワッシュは装飾的なグリフで、カリグラフィを連想させることがよくある、手の込んだ装飾が使用されます。 次のテキストは、Pescadero フォントの標準および飾り付きグリフを示したものです。  
  
 ![OpenType の標準グリフとスワッシュ グリフを使用するテキスト](./media/typography-in-wpf/opentype-standard-swash-glyphs.gif "OpenType の標準グリフと飾り付きグリフを使用するテキスト")  
  
 OpenType の機能の詳細については、「[OpenType フォントの機能](opentype-font-features.md)」を参照してください。  
  
<a name="Enhanced_International_Text_Support"></a>
## <a name="enhanced-international-text-support"></a>国際対応テキストのサポートの強化  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、次の機能を提供することで、国際対応テキストのサポートを強化しています。  
  
- すべての書記体系における、適用可能な単位を使用した自動行間隔設定。  
  
- 国際対応テキストの幅広いサポート。 詳細については、「[WPF のグローバリゼーション](globalization-for-wpf.md)」をご覧ください。  
  
- 言語に合わせた改行、ハイフネーション、両端揃え。  
  
<a name="Enhanced_Font_Support"></a>
## <a name="enhanced-font-support"></a>フォントのサポートの強化  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、次の機能を提供することで、フォントのサポートを強化しています。  
  
- すべてのテキストに対応する Unicode。 フォントの動作や選択に文字セットやコードページが不要になりました。  
  
- システム ロケールなど、グローバル設定に左右されないフォント動作。  
  
- <xref:System.Windows.Media.FontFamily> を定義するための個別の <xref:System.Windows.FontWeight>、<xref:System.Windows.FontStretch>、<xref:System.Windows.FontStyle> 型。 これにより、斜体と太字のブール値の組み合わせでフォント ファミリを定義する Win32 プログラミングよりも優れた柔軟性が提供されます。  
  
- フォント名とは関係なく処理される書き込み方向 (横書きまたは縦書き)。  
  
- 複合フォント技術を使用した、移植可能な XML ファイルにおけるフォント リンクとフォントの代替。 複合フォントは、完全な多言語フォントの構築を可能にします。 また、複合フォントは、欠落グリフの表示を防ぐ機能も備えています。 詳細については、<xref:System.Windows.Media.FontFamily> クラスの「解説」を参照してください。  
  
- 単一言語フォントのグループを使用した、複合フォントから構築される国際対応フォント。 これにより、複数言語に対応するフォントの開発時にリソースのコストを節約できます。  
  
- ドキュメントに埋め込むことで移植性が得られる複合フォント。 詳細については、<xref:System.Windows.Media.FontFamily> クラスの「解説」を参照してください。  
  
<a name="New_Text_APIs"></a>
## <a name="new-text-application-programming-interfaces-apis"></a>新しいテキスト API (アプリケーション プログラミング インターフェイス)  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、開発者がアプリケーションにテキストを含めるときに使用できるいくつかのテキスト API が提供されています。 これらの API は、次の 3 つのカテゴリに分類されます。  
  
- **レイアウトとユーザー インターフェイス**: グラフィカル ユーザー インターフェイス (GUI) に対応した一般的なテキスト コントロールです。  
  
- **軽量テキスト描画**: オブジェクトにテキストを直接描画できます。  
  
- **テキストの高度な書式設定**: カスタム テキスト エンジンを実装できます。  
  
### <a name="layout-and-user-interface"></a>レイアウトとユーザー インターフェイス  
 最上位の機能レベルでは、テキスト API により、<xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.TextBlock>、<xref:System.Windows.Controls.TextBox> などの一般的な [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] コントロールが提供されます。 これらのコントロールは、アプリケーション内に基本的な [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素を提供し、テキストの表示や操作を簡単に実行できるようにします。 <xref:System.Windows.Controls.RichTextBox> や <xref:System.Windows.Controls.PasswordBox> などのコントロールを使用すると、より高度で特殊なテキスト処理が可能になります。 そして、<xref:System.Windows.Documents.TextRange>、<xref:System.Windows.Documents.TextSelection>、<xref:System.Windows.Documents.TextPointer> などのクラスにより、便利なテキスト操作を実行できます。 これらの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] コントロールには、<xref:System.Windows.Controls.Control.FontFamily%2A>、<xref:System.Windows.Controls.Control.FontSize%2A>、<xref:System.Windows.Controls.Control.FontStyle%2A> などのプロパティがあり、テキストの描画に使用するフォントを制御できます。  
  
#### <a name="using-bitmap-effects-transforms-and-text-effects"></a>ビットマップ効果、変換、テキスト効果の使用  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、ビットマップ効果、変換、テキスト効果などの機能を利用して、人の目をひきつけるテキストを作成できます。 テキストに標準タイプのドロップ シャドウ効果を適用した例を次に示します。  
  
 ![ぼかし &#61; 0.25 のテキスト シャドウ](./media/typography-in-wpf/drop-shadow-text-effect.jpg)
  
 テキストにドロップ シャドウ効果とノイズを適用した例を次に示します。  
  
 ![ノイズを含むテキスト シャドウ](./media/typography-in-wpf/drop-shadow-noise-text.jpg)
  
 テキストの外縁にグロー効果を適用した例を次に示します。  
  
 ![OuterGlowBitmapEffect を使用するテキスト シャドウ](./media/typography-in-wpf/text-shadow-glow-effect.jpg)
  
 テキストにぼかし効果が適用されている例を次に示します。  
  
 ![BlurBitmapEffect を使用するテキスト シャドウ](./media/typography-in-wpf/text-shadow-blur-effect.jpg)  

 テキストの 2 行目を x 軸に沿って 150% 拡大し、3 行目を y 軸に沿って 150% 拡大した例を次に示します。  
  
 ![ScaleTransform を使用してスケールされたテキスト](./media/typography-in-wpf/scaled-text-scaletransform.jpg)
  
 x 軸に沿って傾斜させたテキストの例を次に示します。  
  
 ![SkewTransform を使用して傾斜させたテキスト](./media/typography-in-wpf/skewed-transformed-text.jpg)
  
 <xref:System.Windows.Media.TextEffect> オブジェクトは、テキスト文字列内の 1 つまたは複数の文字列のグループとしてテキストを処理できるヘルパー オブジェクトです。 次の例は、回転する個々の文字を示しています。 各文字は、1 秒間隔で個別に回転します。  
  
 ![テキストを回転するテキスト効果のスクリーンショット](./media/typography-in-wpf/rotating-text-effect.jpg)
  
#### <a name="using-flow-documents"></a>フロー ドキュメントの使用  
 一般的な [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] コントロールに加えて、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、テキスト表示に使用するレイアウト コントロール (<xref:System.Windows.Documents.FlowDocument> 要素) があります。 <xref:System.Windows.Documents.FlowDocument> 要素を <xref:System.Windows.Controls.DocumentViewer> 要素と組み合わせると、さまざまなレイアウト要件を含む大量のテキストに対応するコントロールを作成できます。 レイアウト コントロールでは、<xref:System.Windows.Documents.Typography> オブジェクトと他の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] コントロールのフォント関連プロパティを通じて、高度なタイポグラフィへのアクセスが提供されます。  
  
 検索、ナビゲーション、改ページ位置の自動修正、コンテンツ スケーリングをサポートする <xref:System.Windows.Controls.FlowDocumentReader> でホストされているテキスト コンテンツを次の例に示します。  
  
 ![OpenType フォントを示すスクリーンショット。](./media/typography-in-wpf/typography-text-flowdocumentreader.png)
  
 詳細については、「[WPF のドキュメント](documents-in-wpf.md)」を参照してください。  
  
### <a name="lightweight-text-drawing"></a>軽量テキスト描画  
 <xref:System.Windows.Media.DrawingContext> オブジェクトの <xref:System.Windows.Media.DrawingContext.DrawText%2A> メソッドを使用すると、テキストを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のオブジェクトに直接描画できます。 このメソッドを使用するには、<xref:System.Windows.Media.FormattedText> オブジェクトを作成します。 このオブジェクトを使用すると、複数行のテキストを描画できます。このテキストでは、テキスト内の各文字を個々に書式設定できます。 <xref:System.Windows.Media.FormattedText> オブジェクトの機能には、Windows API の DrawText フラグの多くの機能が含まれています。 また、<xref:System.Windows.Media.FormattedText> オブジェクトは、テキストがその境界を越えたときに省略記号を表示する、省略記号のサポートなどの機能も備えています。 いくつかの書式を適用したテキストを次の例に示します。たとえば、2 番目と 3 番目の単語には線状グラデーションが適用されています。  
  
 ![FormattedText オブジェクトを使用して表示されるテキスト](./media/typography-in-wpf/text-formatted-linear-gradient.jpg)
  
 書式設定されたテキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換し、人の目をひきつける他の種類のテキストを作成できます。 たとえば、テキスト文字列のアウトラインに基づいて <xref:System.Windows.Media.Geometry> オブジェクトを作成できます。  
  
 ![線形グラデーション ブラシを使用するテキスト アウトライン](./media/typography-in-wpf/text-outline-linear-gradient.jpg)  
  
 変換されたテキストのストローク、塗りつぶし、強調表示を変更して、人の目をひく視覚効果を作成するいくつかの方法を次の例に示します。  
  
 ![塗りつぶしとストロークに別の色を使用するテキスト](./media/typography-in-wpf/fill-stroke-text-effect.jpg)  
  
 ![ストロークに適用されるイメージ ブラシを含むテキスト](./media/typography-in-wpf/image-brush-application.jpg)
  
 ![ストロークと強調表示に適用されるイメージ ブラシを含むテキスト](./media/typography-in-wpf/image-brush-text-application.jpg)
  
 <xref:System.Windows.Media.FormattedText> オブジェクトの詳細については、「[書式設定されたテキストの描画](drawing-formatted-text.md)」を参照してください。  
  
### <a name="advanced-text-formatting"></a>テキストの高度な書式設定  
 テキスト API の最も高度なレベルとして、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、<xref:System.Windows.Media.TextFormatting.TextFormatter> オブジェクトと <xref:System.Windows.Media.TextFormatting> 名前空間の他の型を使用して、カスタム テキスト レイアウトを作成する機能が用意されています。 <xref:System.Windows.Media.TextFormatting.TextFormatter> と関連クラスを使用して、ユーザー定義による文字形式、段落スタイル、改行ルール、国際対応テキストのその他のレイアウト機能をサポートするカスタム テキスト レイアウトを実装できます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] テキスト レイアウト サポートに関する既定の実装のオーバーライドが必要となるケースはほとんどありません。 ただし、テキストを編集するコントロールやアプリケーションを作成する場合は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の既定の実装とは異なる実装が必要になることがあります。  
  
 従来のテキスト API とは異なり、<xref:System.Windows.Media.TextFormatting.TextFormatter> では、一連のコールバック メソッドにより、テキスト レイアウト クライアントとの対話が行われます。 クライアントでは、<xref:System.Windows.Media.TextFormatting.TextSource> クラスの実装で、これらのメソッドを提供する必要があります。 次の図は、クライアント アプリケーションと <xref:System.Windows.Media.TextFormatting.TextFormatter> の間で行われるテキスト レイアウトの相互作用を示したものです。  
  
 ![テキスト レイアウト クライアントと TextFormatter のダイアグラム](./media/typography-in-wpf/text-layout-text-formatter-interaction.png)  
  
 カスタム テキスト レイアウトの作成の詳細については、「[テキストの高度な書式設定](advanced-text-formatting.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.FormattedText>
- <xref:System.Windows.Media.TextFormatting.TextFormatter>
- [ClearType の概要](cleartype-overview.md)
- [OpenType フォントの機能](opentype-font-features.md)
- [書式設定されたテキストの描画](drawing-formatted-text.md)
- [テキストの高度な書式設定](advanced-text-formatting.md)
- [[テキスト]](optimizing-performance-text.md)
- [Microsoft の文字体裁](https://docs.microsoft.com/typography/)
