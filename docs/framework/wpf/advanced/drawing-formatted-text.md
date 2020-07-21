---
title: 書式設定されたテキストの描画
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF]
- typography [WPF], drawing formatted text
- formatted text [WPF]
- drawing [WPF], formatted text
ms.assetid: b1d851c1-331c-4814-9964-6fe769db6f1f
ms.openlocfilehash: 1e82795afbdd5b1b0a05f95600ebdb92fc134b7d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186562"
---
# <a name="drawing-formatted-text"></a>書式設定されたテキストの描画
ここでは、<xref:System.Windows.Media.FormattedText> オブジェクトの機能の概要について説明します。 このオブジェクトは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションでのテキストの描画に対する低レベルの制御を提供します。  

## <a name="technology-overview"></a>テクノロジの概要  
 <xref:System.Windows.Media.FormattedText> オブジェクトを使用すると、複数行のテキストを描画できます。このテキストでは、テキスト内の各文字を個々に書式設定できます。 複数の書式が適用されたテキストを次の例に示します。  
  
 ![FormattedText オブジェクトを使用して表示されるテキスト](./media/typography-in-wpf/text-formatted-linear-gradient.jpg)  
  
> [!NOTE]
> Win32 API から移行する開発者のために、「[Win32 の移行](#win32_migration)」の表に Win32 DrawText フラグと [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] におけるほぼ同等のものを示します。  
  
### <a name="reasons-for-using-formatted-text"></a>書式設定されたテキストを使用する理由  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には画面にテキストを描画するための複数のコントロールが含まれています。 各コントロールは異なるシナリオを対象にしており、それぞれに一連の機能と制限があります。 一般的に、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] で短い文を使用するなど限定的なテキストのサポートが必要な場合は、<xref:System.Windows.Controls.TextBlock> 要素を使用する必要があります。 最小限のテキスト サポートが必要な場合は、<xref:System.Windows.Controls.Label> を使用できます。 詳細については、「[WPF のドキュメント](documents-in-wpf.md)」を参照してください。  
  
 <xref:System.Windows.Media.FormattedText> オブジェクトは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] テキスト コントロールより強力なテキスト書式設定機能を備えており、テキストを装飾的要素として使用する場合に役立ちます。 詳細については、後の「[書式設定されたテキストのジオメトリへの変換](#converting_formatted_text)」を参照してください。  
  
 また、<xref:System.Windows.Media.FormattedText> オブジェクトは、テキスト指向の <xref:System.Windows.Media.DrawingVisual> 派生オブジェクトを作成する場合に役立ちます。 <xref:System.Windows.Media.DrawingVisual> は、図形、イメージ、またはテキストのレンダリングに使用する軽量の描画クラスです。 詳細については、「[DrawingVisuals を使用したヒット テストのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Visual%20Layer/DrawingVisual)」を参照してください。  
  
## <a name="using-the-formattedtext-object"></a>FormattedText オブジェクトの使用  
 書式設定されたテキストを作成するには、<xref:System.Windows.Media.FormattedText.%23ctor%2A> コンストラクターを呼び出して <xref:System.Windows.Media.FormattedText> オブジェクトを作成します。 最初の書式設定済みテキスト文字列を作成したら、書式スタイルの範囲を適用できます。  
  
 テキストを特定の幅に制限するには、<xref:System.Windows.Media.FormattedText.MaxTextWidth%2A> プロパティを使用します。 テキストは、指定された幅を超えないように自動的に折り返されます。 テキストを特定の高さに制限するには、<xref:System.Windows.Media.FormattedText.MaxTextHeight%2A> プロパティを使用します。 テキストは、指定された高さを超えた部分に省略記号 "…" を表示します。  
  
 ![右端の折り返しと省略記号を使用して表示されているテキスト。](./media/drawing-formatted-text/formatted-text-wordwrap-ellipsis.png)
  
 複数の書式スタイルを 1 つ以上の文字に適用できます。 たとえば、<xref:System.Windows.Media.FormattedText.SetFontSize%2A> メソッドと <xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A> メソッドの両方を呼び出して、テキストの最初の 5 文字の書式設定を変更できます。  
  
 <xref:System.Windows.Media.FormattedText> オブジェクトを作成し、複数の書式設定スタイルをテキストに適用するコード例を次に示します。  
  
 [!code-csharp[FormattedTextSnippets#FormattedTextSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
 [!code-vb[FormattedTextSnippets#FormattedTextSnippets1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]  
  
### <a name="font-size-unit-of-measure"></a>フォント サイズの単位  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションの他のテキスト オブジェクトと同様に、<xref:System.Windows.Media.FormattedText> オブジェクトでは、単位としてデバイス非依存ピクセルが使用されます。 ただし、ほとんどの Win32 アプリケーションでは、単位としてポイントが使用されます。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションでポイント単位の表示テキストを使用する場合は、デバイスに依存しない単位 (1 単位は 1/96 インチ) をポイントに変換する必要があります。 この変換を実行する方法を次のコード例に示します。  
  
 [!code-csharp[FormattedTextSnippets#FormattedTextSnippets2](~/samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets2)]
 [!code-vb[FormattedTextSnippets#FormattedTextSnippets2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets2)]  
  
<a name="converting_formatted_text"></a>
### <a name="converting-formatted-text-to-a-geometry"></a>書式設定されたテキストのジオメトリへの変換  
 書式設定したテキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換し、人の目をひきつける他の種類のテキストを作成できます。 たとえば、テキスト文字列のアウトラインに基づいて <xref:System.Windows.Media.Geometry> オブジェクトを作成できます。  
  
 ![線形グラデーション ブラシを使用するテキスト アウトライン](./media/typography-in-wpf/text-outline-linear-gradient.jpg)
  
 変換されたテキストのストローク、塗りつぶし、強調表示を変更して、人の目をひく視覚効果を作成するいくつかの方法を次の例に示します。  
  
 ![塗りつぶしとストロークに別の色を使用するテキスト](./media/typography-in-wpf/fill-stroke-text-effect.jpg)  
  
 ![ストロークに適用されるイメージ ブラシを含むテキスト](./media/typography-in-wpf/image-brush-application.jpg)
  
 ![ストロークと強調表示に適用されるイメージ ブラシを含むテキスト](./media/typography-in-wpf/image-brush-text-application.jpg)
  
 テキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換すると、テキストは文字の集まりではなくなります。つまり、文字列内の文字を変更することはできません。 ただし、変換されたテキストのストロークおよび塗りつぶしのプロパティを変更することで、テキストの外観を変えることができます。 ストロークは、変換したテキストのアウトラインを参照します。塗りつぶしは、変換したテキストのアウトラインの内側の領域を参照します。 詳細については、「[方法: 中抜きの文字列を作成する](how-to-create-outlined-text.md)」を参照してください。  
  
 書式設定されたテキストを <xref:System.Windows.Media.PathGeometry> オブジェクトに変換し、そのオブジェクトをテキストの強調表示に使用することもできます。 たとえば、<xref:System.Windows.Media.PathGeometry> オブジェクトに 1 つのアニメーションを適用することができ、これによりアニメーションは書式設定されたテキストのアウトラインに従うようになります。  
  
 次の例では、<xref:System.Windows.Media.PathGeometry> オブジェクトに変換された書式付きテキストを示します。 アニメーション化された楕円は、レンダリングされたテキストのストロークのパスに従います。  
  
 ![テキストのパス ジオメトリに続く球](./media/drawing-formatted-text/sphere-following-geometry-path.gif)  
テキストのパス ジオメトリに続く球  
  
 詳細については、「[方法: テキストの PathGeometry アニメーションを作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms743610(v=vs.100))」を参照してください。  
  
 書式設定したテキストを <xref:System.Windows.Media.PathGeometry> オブジェクトに変換したら、他の有意義な効果を作成することができます。 たとえば、ビデオをクリップしてテキスト内に表示することができます。  
  
 ![テキストのパス ジオメトリに表示されるビデオ](./media/drawing-formatted-text/video-displaying-text-path-geometry.png)
  
<a name="win32_migration"></a>
## <a name="win32-migration"></a>Win32 の移行  
 テキストを描画するための <xref:System.Windows.Media.FormattedText> の機能は、Win32 DrawText 関数の機能に似ています。 Win32 API から移行する開発者のために、Win32 DrawText フラグと [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] におけるほぼ同等のものを次の表に示します。  
  
|DrawText フラグ|同等の WPF 操作|メモ|  
|-------------------|--------------------|-----------|  
|DT_BOTTOM|<xref:System.Windows.Media.FormattedText.Height%2A>|適切な Win32 DrawText の "y" 位置を計算するには、<xref:System.Windows.Media.FormattedText.Height%2A> プロパティを使用します。|  
|DT_CALCRECT|<xref:System.Windows.Media.FormattedText.Height%2A>、<xref:System.Windows.Media.FormattedText.Width%2A>|出力四角形を計算するには、<xref:System.Windows.Media.FormattedText.Height%2A> プロパティと <xref:System.Windows.Media.FormattedText.Width%2A> プロパティを使用します。|  
|DT_CENTER|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|<xref:System.Windows.Media.FormattedText.TextAlignment%2A> プロパティを使用して値を <xref:System.Windows.TextAlignment.Center> に設定します。|  
|DT_EDITCONTROL|None|不要。 スペースの幅および最後の行のレンダリングは、フレームワークのエディット コントロールと同じです。|  
|DT_END_ELLIPSIS|<xref:System.Windows.Media.FormattedText.Trimming%2A>|<xref:System.Windows.Media.FormattedText.Trimming%2A> プロパティを使用して値を <xref:System.Windows.TextTrimming.CharacterEllipsis> にします。<br /><br /> <xref:System.Windows.TextTrimming.WordEllipsis> を使用して、DT_WORD_ELIPSIS の末尾の省略記号が設定された Win32 DT_END_ELLIPSIS を取得します。この場合、省略記号は 1 行に収まらない単語にのみ表示されます。|  
|DT_EXPAND_TABS|None|不要。 タブは自動的に全角 4 文字分ごとに展開されます。これは、言語非依存文字の約 8 文字分の幅です。|  
|DT_EXTERNALLEADING|None|不要。 外部レディングは、常に行間隔に含まれます。 <xref:System.Windows.Media.FormattedText.LineHeight%2A> プロパティを使用して、ユーザー定義の行間隔を作成します。|  
|DT_HIDEPREFIX|None|サポートされていません。 <xref:System.Windows.Media.FormattedText> オブジェクトを構築する前に、文字列から "&" を削除します。|  
|DT_LEFT|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|これは、テキストの配置の既定値です。 <xref:System.Windows.Media.FormattedText.TextAlignment%2A> プロパティを使用して値を <xref:System.Windows.TextAlignment.Left> に設定します。 (WPF のみ)。|  
|DT_MODIFYSTRING|None|サポートされていません。|  
|DT_NOCLIP|<xref:System.Windows.Media.Visual.VisualClip%2A>|クリッピングは自動的には行われません。 テキストをクリップする場合は、<xref:System.Windows.Media.Visual.VisualClip%2A> プロパティを使用します。|  
|DT_NOFULLWIDTHCHARBREAK|None|サポートされていません。|  
|DT_NOPREFIX|None|不要。 文字列内の '&' 文字は、常に通常の文字として扱われます。|  
|DT_PATHELLIPSIS|None|<xref:System.Windows.Media.FormattedText.Trimming%2A> プロパティを使用して値を <xref:System.Windows.TextTrimming.WordEllipsis> にします。|  
|DT_PREFIX|None|サポートされていません。 アクセラレータ キーやリンクなどのテキストにアンダースコアを使用する場合は、<xref:System.Windows.Media.FormattedText.SetTextDecorations%2A> メソッドを使用します。|  
|DT_PREFIXONLY|None|サポートされていません。|  
|DT_RIGHT|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|<xref:System.Windows.Media.FormattedText.TextAlignment%2A> プロパティを使用して値を <xref:System.Windows.TextAlignment.Right> に設定します。 (WPF のみ)。|  
|DT_RTLREADING|<xref:System.Windows.Media.FormattedText.FlowDirection%2A>|<xref:System.Windows.Media.FormattedText.FlowDirection%2A> プロパティを <xref:System.Windows.FlowDirection.RightToLeft>に設定します。|  
|DT_SINGLELINE|None|不要。 <xref:System.Windows.Media.FormattedText.MaxTextWidth%2A> プロパティが設定されていない場合、またはテキストに改行コード (CR/LF) が含まれていない場合、<xref:System.Windows.Media.FormattedText> オブジェクトは単一行コントロールとして動作します。|  
|DT_TABSTOP|None|ユーザー定義のタブ位置はサポートされていません。|  
|DT_TOP|<xref:System.Windows.Media.FormattedText.Height%2A>|不要。 上端揃えが既定値です。 その他の垂直方向の配置の値を定義するには、<xref:System.Windows.Media.FormattedText.Height%2A> プロパティを使用して、適切な Win32 DrawText の "y" 位置を計算します。|  
|DT_VCENTER|<xref:System.Windows.Media.FormattedText.Height%2A>|適切な Win32 DrawText の "y" 位置を計算するには、<xref:System.Windows.Media.FormattedText.Height%2A> プロパティを使用します。|  
|DT_WORDBREAK|None|不要。 単語の区切りは、<xref:System.Windows.Media.FormattedText> オブジェクトで自動的に行われます。 無効にすることはできません。|  
|DT_WORD_ELLIPSIS|<xref:System.Windows.Media.FormattedText.Trimming%2A>|<xref:System.Windows.Media.FormattedText.Trimming%2A> プロパティを使用して値を <xref:System.Windows.TextTrimming.WordEllipsis> にします。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.FormattedText>
- [WPF のドキュメント](documents-in-wpf.md)
- [WPF のタイポグラフィ](typography-in-wpf.md)
- [中抜きの文字列を作成する](how-to-create-outlined-text.md)
- [方法: テキストの PathGeometry アニメーションを作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms743610(v=vs.100))
