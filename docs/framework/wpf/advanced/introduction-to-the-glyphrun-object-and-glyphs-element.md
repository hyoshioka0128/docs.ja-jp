---
title: GlyphRun オブジェクトと Glyphs 要素の概要
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], Glyphs element
- Glyphs elements [WPF]
- GlyphRun object [WPF]
- text [WPF], glyphs
- glyphs [WPF]
- typography [WPF], GlyphRun object
ms.assetid: 746ca769-a331-4435-9b95-f72a883b67c1
ms.openlocfilehash: 32e8ab7104b8ea2f985395065868ed154ca1e378
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181961"
---
# <a name="introduction-to-the-glyphrun-object-and-glyphs-element"></a>GlyphRun オブジェクトと Glyphs 要素の概要
このトピックでは、<xref:System.Windows.Media.GlyphRun> オブジェクトと <xref:System.Windows.Documents.Glyphs> 要素について説明します。  

<a name="text_glyphrunovw_intro"></a>
## <a name="introduction-to-glyphrun"></a>GlyphRun の概要  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、書式設定後のテキストをインターセプトして保存したいユーザーのために <xref:System.Windows.Documents.Glyphs> に直接アクセスするグリフ レベルのマークアップなど、高度なテキスト サポートが提供されています。 これらの機能は、下記のようなシナリオでのさまざまなテキスト レンダリング要件をサポートする不可欠なものです。  
  
1. 固定形式のドキュメントの画面表示。  
  
2. 印刷シナリオ。  
  
    - デバイス プリンター言語としての [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  
  
    - Microsoft XPS Document Writer。  
  
    - 以前のプリンター ドライバー、Win32 アプリケーションから固定形式への出力。  
  
    - 印刷スプール形式。  
  
3. 以前のバージョンの Windows のクライアントおよびその他のコンピューティング デバイスを含む、固定形式のドキュメント表示。  
  
> [!NOTE]
> <xref:System.Windows.Documents.Glyphs> および <xref:System.Windows.Media.GlyphRun> は、固定形式のドキュメント表示と印刷シナリオ向けに設計されています。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、一般的なレイアウトおよび <xref:System.Windows.Controls.Label> や <xref:System.Windows.Controls.TextBlock> などの [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] シナリオのための要素が提供されています。 レイアウトと [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] シナリオの詳細については、[WPF のタイポグラフィ](typography-in-wpf.md)を参照してください。  
  
<a name="text_glyphrunovw_glyphrunobject"></a>
## <a name="the-glyphrun-object"></a>GlyphRun オブジェクト  
 <xref:System.Windows.Media.GlyphRun> オブジェクトでは、1 つのサイズで 1 つのフォントの 1 つの書体からグリフのシーケンスが、1 つのレンダリング スタイルで表されます。  
  
 <xref:System.Windows.Media.GlyphRun> には、グリフ <xref:System.Windows.Documents.Glyphs.Indices%2A> などのフォントの詳細と個々のグリフ位置の両方が含まれます。 run の生成元の元の Unicode コード ポイント、文字とグリフのバッファー オフセット マッピングの情報、および文字ごとのフラグとグリフごとのフラグも含まれます。  
  
 <xref:System.Windows.Media.GlyphRun> には、対応する高度な <xref:System.Windows.FrameworkElement> である <xref:System.Windows.Documents.Glyphs> があります。 <xref:System.Windows.Documents.Glyphs> は、<xref:System.Windows.Media.GlyphRun> の出力を表すために、要素ツリーおよび [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップで使用できます。  
  
<a name="text_glyphrunovw_glyphselement"></a>
## <a name="the-glyphs-element"></a>Glyphs 要素  
 <xref:System.Windows.Documents.Glyphs> 要素では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] での <xref:System.Windows.Media.GlyphRun> の出力が表されます。 <xref:System.Windows.Documents.Glyphs> 要素を記述するには、次のマークアップ構文が使用されます。  
  
 [!code-xaml[GlyphsOvwSample1#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
 次のプロパティの定義は、サンプルのマークアップ内の最初の 4 つの属性に対応しています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Windows.Documents.Glyphs.FontUri%2A>|リソース識別子を指定します: ファイル名、Web Uniform Resource Identifier (URI)、またはアプリケーションの .exe またはコンテナー内のリソース参照。|  
|<xref:System.Windows.Documents.Glyphs.FontRenderingEmSize%2A>|フォント サイズを描画サーフェイスの単位で指定します (既定値は .96 インチ)。|  
|<xref:System.Windows.Documents.Glyphs.StyleSimulations%2A>|太字や斜体のスタイルのフラグを指定します。|  
|<xref:System.Windows.Documents.Glyphs.BidiLevel%2A>|双方向のレイアウト レベルを指定します。 偶数とゼロの値は左から右のレイアウトを意味し、奇数の値は右から左のレイアウトを意味します。|  
  
<a name="text_glyphrunovw_indicesproperty"></a>
### <a name="indices-property"></a>Indices プロパティ  
 <xref:System.Windows.Documents.Glyphs.Indices%2A> プロパティは、グリフ仕様の文字列です。 グリフのシーケンスが 1 つのクラスターを形成している場合、クラスター内の最初のグリフの仕様は、クラスターを形成するために組み合わせるグリフの数とコード ポイントの数の仕様によって先行されます。 <xref:System.Windows.Documents.Glyphs.Indices%2A> プロパティでは、1 つの文字列内で次のプロパティが収集されます。  
  
- グリフ インデックス  
  
- グリフのアドバンス幅  
  
- グリフ添付ベクターの結合  
  
- コード ポイントからグリフへのクラスター マッピング  
  
- グリフ フラグ  
  
 各グリフの仕様には、次の形式があります。  
  
 `[GlyphIndex][,[Advance][,[uOffset][,[vOffset][,[Flags]]]]]`  
  
<a name="text_glyphrunovw_glyphmetrics"></a>
## <a name="glyph-metrics"></a>グリフのメトリック  
 各グリフでは、他の <xref:System.Windows.Documents.Glyphs> とどのように位置合わせするかを指定するメトリックが定義されています。 次の図では、2 つの異なるグリフ文字のさまざまな印刷用品質を定義しています。  
  
 ![グリフ単位のダイアグラム](./media/glyph-example.png "glyph_example")  
  
<a name="text_glyphrunovw_glyphsmarkup"></a>
## <a name="glyphs-markup"></a>グリフ マークアップ  
 次のコード例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で <xref:System.Windows.Documents.Glyphs> 要素のさまざまなプロパティを使用する方法を示します。  
  
 [!code-xaml[GlyphsOvwSamp2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSamp2/CS/default.xaml#1)]  
  
## <a name="see-also"></a>関連項目

- [WPF のタイポグラフィ](typography-in-wpf.md)
- [WPF のドキュメント](documents-in-wpf.md)
- [[テキスト]](optimizing-performance-text.md)
