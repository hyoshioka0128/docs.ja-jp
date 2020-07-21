---
title: テキストの高度な書式設定
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [WPF]
- text [WPF]
- typography [WPF], text formatting
ms.assetid: f0a7986e-f5b2-485c-a27d-f8e922022212
ms.openlocfilehash: 745d20e0bd4f877f9d4559f9fc7829b56689d35c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185942"
---
# <a name="advanced-text-formatting"></a>テキストの高度な書式設定
Windows Presentation Foundation (WPF) では、アプリケーションにテキストを含めるための堅牢な API のセットが提供されています。 レイアウトと <xref:System.Windows.Controls.TextBlock> のような [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] API により、テキスト表示のための最も一般的な要素が提供されます。 <xref:System.Windows.Media.GlyphRunDrawing> や <xref:System.Windows.Media.FormattedText> のような描画 API は、描画に書式設定されたテキストを追加する手段です。 最も高度なレベルでは、WPF によって提供される拡張テキスト書式設定エンジンにより、テキスト保管管理、テキスト ラン書式設定管理、埋め込みオブジェクト管理など、テキスト表示のあらゆる側面が制御されます。  
  
 このトピックでは、WPF でのテキスト書式設定の概要について説明します。 WPF のテキスト書式設定エンジンのクライアントでの実装と使用について主に取り上げます。  
  
> [!NOTE]
> ドキュメント内のすべてのコード サンプルは、「[テキストの高度な書式設定サンプル](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI/TextFormatting)」にあります。  

<a name="prereq"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックは、テキスト表示に使用されるレベルの高い API に関する知識があることを前提に書かれています。 ほとんどのユーザー シナリオでは、このトピックにあるようなテキストの高度な書式設定 API は必要ありません。 他のテキスト API の概要については、「[WPF のドキュメント](documents-in-wpf.md)」を参照してください。  
  
<a name="section1"></a>
## <a name="advanced-text-formatting"></a>テキストの高度な書式設定  
 WPF のテキスト レイアウトと [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のコントロールによって提供される書式設定プロパティを使用すると、書式設定されたテキストをアプリケーションに簡単に追加できます。 これらのコントロールでは、テキストの表示を処理するさまざまなプロパティが公開されます。書体、大きさ、色などです。 通常の状況では、これらのコントロールはアプリケーションの大半のテキスト表示を処理できます。 しかしながら、一部の高度なシナリオでは、テキスト表示と同様にテキスト保存を制御する必要があります。 WPF では、この目的のための拡張テキスト書式設定エンジンが提供されます。  
  
 WPF の高度なテキスト書式設定機能は、テキスト書式設定エンジン、テキスト ストア、テキスト ラン、書式設定プロパティで構成されます。 テキスト書式設定エンジン <xref:System.Windows.Media.TextFormatting.TextFormatter> では、表示に使用されるテキスト行が作成されます。 これは、行の書式設定プロセスを開始し、テキスト フォーマッタの <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> を呼び出すことで行われます。 テキスト フォーマッタでは、テキスト ストアの <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> メソッドを呼び出すことによって、ストアからテキスト ランが取得されます。 次に、テキスト フォーマッタにより <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトから書式設定された <xref:System.Windows.Media.TextFormatting.TextLine> オブジェクトが作成されて、検査または表示のためにアプリケーションに提供されます。  
  
<a name="section2"></a>
## <a name="using-the-text-formatter"></a>テキスト フォーマッタを使用する  
 <xref:System.Windows.Media.TextFormatting.TextFormatter> は WPF のテキスト書式設定エンジンであり、テキスト行を書式設定したり、改行したりするためのサービスを提供します。 テキスト フォーマッタは、さまざまなテキスト文字書式や段落スタイルを処理し、国際的なテキスト レイアウトに対応しています。  
  
 従来のテキスト API とは異なり、<xref:System.Windows.Media.TextFormatting.TextFormatter> では、一連のコールバック メソッドにより、テキスト レイアウト クライアントとの対話が行われます。 クライアントでは、<xref:System.Windows.Media.TextFormatting.TextSource> クラスの実装で、これらのメソッドを提供する必要があります。 次の図は、クライアント アプリケーションと <xref:System.Windows.Media.TextFormatting.TextFormatter> の間で行われるテキスト レイアウトの相互作用を示したものです。  
  
 ![テキスト レイアウト クライアントと TextFormatter のダイアグラム](./media/advanced-text-formatting/text-layout-textformatter-interaction.png)  
  
 テキスト フォーマッタは、<xref:System.Windows.Media.TextFormatting.TextSource> の実装であるテキスト ストアから書式設定されたテキスト行を取得するために使用されます。 これは、最初に <xref:System.Windows.Media.TextFormatting.TextFormatter.Create%2A> メソッドを使用してテキスト フォーマッタのインスタンスを作成することで行われます。 このメソッドはテキスト フォーマッタのインスタンスを作成し、行の高さと幅の最大値を設定します。 テキスト フォーマッタのインスタンスが作成されるとすぐに、<xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> メソッドが呼び出されることによって、行の作成プロセスが開始されます。 <xref:System.Windows.Media.TextFormatting.TextFormatter> では、テキスト ソースが再び呼び出されて、行を形成するテキスト ランのテキストと書式設定パラメーターが取得されます。  
  
 次の例は、テキスト ストアを書式設定するプロセスを示しています。 <xref:System.Windows.Media.TextFormatting.TextFormatter> オブジェクトを使用して、テキスト ストアからテキスト行が取得された後、<xref:System.Windows.Media.DrawingContext> に描画するためのテキスト行の書式設定が行われます。  
  
 [!code-csharp[TextFormatterExample#100](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextFormatterExample#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/Window1.xaml.vb#100)]  
  
<a name="section3"></a>
## <a name="implementing-the-client-text-store"></a>クライアント テキスト ストアを実装する  
 テキスト書式設定エンジンを拡張するとき、テキスト ストアのあらゆる側面を実装し、管理する必要があります。 これは簡単な作業ではありません。 テキスト ストアは、テキスト ランのプロパティ、段落のプロパティ、埋め込みオブジェクト、その他の同様のコンテンツの追跡を担当します。 また、テキスト フォーマッタに個々の <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトが提供されます。テキスト フォーマッタでは、このオブジェクトを使用して、<xref:System.Windows.Media.TextFormatting.TextLine> オブジェクトが作成されます。  
  
 テキスト ストアの仮想化を処理するため、テキスト ストアは <xref:System.Windows.Media.TextFormatting.TextSource> から派生される必要があります。 <xref:System.Windows.Media.TextFormatting.TextSource> では、テキスト ストアからテキスト ランを取得するためにテキスト フォーマッタによって使用されるメソッドが定義されています。 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> は、行の書式設定で使用されるテキスト ランを取得するためにテキスト フォーマッタによって使用されるメソッドです。 次のいずれかの条件が発生するまで、テキスト フォーマッタによって <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> が繰り返し呼び出されます。  
  
- <xref:System.Windows.Media.TextFormatting.TextEndOfLine> またはサブクラスが返される。  
  
- テキスト ランの累積の幅が、テキスト フォーマッタを作成するための呼び出し、またはテキスト フォーマッタの <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> メソッドの呼び出しのいずれかで指定されている行の最大幅を超過する。  
  
- "CF"、"LF"、"CRLF" など、Unicode の改行シーケンスが返される。  
  
<a name="section4"></a>
## <a name="providing-text-runs"></a>テキスト ランを提供する  
 テキスト書式設定プロセスの中心となるものは、テキスト フォーマッタとテキスト ストアの間のやりとりです。 <xref:System.Windows.Media.TextFormatting.TextSource> の実装で、テキスト フォーマッタに、<xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトとテキスト ランの書式設定プロパティを提供します。 このやりとりは、テキスト フォーマッタによって呼び出される <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> メソッドで処理されます。  
  
 次の表では、事前定義されている <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトの一部を示します。  
  
|TextRun の種類|使用方法|  
|------------------|-----------|  
|<xref:System.Windows.Media.TextFormatting.TextCharacters>|文字グリフの表示をテキスト フォーマッタに返すために使用される特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextEmbeddedObject>|テキスト内のボタンやイメージなど、測定、ヒット テスト、描画が全部行われるコンテンツを提供するための特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfLine>|行の終わりをマークするための特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>|段落の終わりをマークするための特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>|前の <xref:System.Windows.Media.TextFormatting.TextModifier> ランの影響を受ける範囲の終わりなど、セグメントの終わりをマークするための特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextHidden>|隠れ文字の範囲をマークするための特殊なテキスト ラン。|  
|<xref:System.Windows.Media.TextFormatting.TextModifier>|その範囲でテキスト ランのプロパティを変更するための特殊なテキスト ラン。 範囲は、次に一致する <xref:System.Windows.Media.TextFormatting.TextEndOfSegment> テキスト ランまで、または次の <xref:System.Windows.Media.TextFormatting.TextEndOfParagraph> まで拡張されます。|  
  
 事前定義されている <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトのどれでもサブクラス化できます。 それにより、テキスト ソースはテキスト フォーマッタにカスタム データを含むテキスト ランを提供できます。  
  
 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> メソッドの例を次に示します。 このテキスト ストアでは、処理のためにテキスト フォーマッタに <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトが返されます。  
  
 [!code-csharp[TextFormatterExample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/CustomTextSource.cs#101)]
 [!code-vb[TextFormatterExample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/CustomTextSource.vb#101)]  
  
> [!NOTE]
> この例では、テキスト ストアはすべてのテキストに同じテキスト プロパティを提供します。 高度なテキスト ストアでは、場合によっては、独自のスパン管理を実装し、個々の文字に異なるプロパティを与えるようにする必要があります。  
  
<a name="section5"></a>
## <a name="specifying-formatting-properties"></a>書式設定プロパティを指定する  
 <xref:System.Windows.Media.TextFormatting.TextRun> オブジェクトは、テキスト ストアによって提供されるプロパティを使用して書式設定されます。 これらのプロパティは、<xref:System.Windows.Media.TextFormatting.TextParagraphProperties> と <xref:System.Windows.Media.TextFormatting.TextRunProperties> の 2 つの型で渡されます。 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> では、<xref:System.Windows.TextAlignment> や <xref:System.Windows.FlowDirection> などの段落の包括的プロパティが処理されます。 <xref:System.Windows.Media.TextFormatting.TextRunProperties> は、前景ブラシ、<xref:System.Windows.Media.Typeface>、フォント サイズなど、段落内のテキスト ランごとに異なる場合があるプロパティです。 カスタム段落やカスタム テキストのラン プロパティ型を実装するには、アプリケーションでそれぞれ <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> および <xref:System.Windows.Media.TextFormatting.TextRunProperties> から派生するクラスを作成する必要があります。  
  
## <a name="see-also"></a>関連項目

- [WPF のタイポグラフィ](typography-in-wpf.md)
- [WPF のドキュメント](documents-in-wpf.md)
