---
title: RichTextBox の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], RichTextBox
- RichTextBox control [WPF], about RichTextBox control
ms.assetid: c94548b2-c1e9-4b62-b10c-dd8740eb23d8
ms.openlocfilehash: bfed42bcf3693ef744b3ed2b54ebe070931513a9
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855735"
---
# <a name="richtextbox-overview"></a>RichTextBox の概要

<xref:System.Windows.Controls.RichTextBox> コントロールでは、段落、イメージ、テーブルなどのフロー コンテンツを表示または編集できます。 このトピックでは、<xref:System.Windows.Controls.TextBox> クラスを紹介し、それを [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] と C# の両方で使用する方法の例を示します。

<a name="textbox_or_richtextbox"></a>

## <a name="textbox-or-richtextbox"></a>TextBox か RichTextBox か

<xref:System.Windows.Controls.RichTextBox> と <xref:System.Windows.Controls.TextBox> の両方で、ユーザーはテキストを編集できますが、2 つのコントロールは異なるシナリオで使用されます。 <xref:System.Windows.Controls.RichTextBox> は、ユーザーが書式設定されたテキスト、イメージ、テーブル、またはその他のリッチ コンテンツを編集する必要がある場合に適しています。 たとえば、書式設定やイメージなどを必要とするドキュメント、記事、またはブログを編集する場合は、<xref:System.Windows.Controls.RichTextBox> を使用することをお勧めします。 <xref:System.Windows.Controls.TextBox> で必要なシステム リソースは、<xref:System.Windows.Controls.RichTextBox> よりも少なく、プレーン テキストのみを編集する必要がある場合 (つまり、フォームでの使用) に最適です。 <xref:System.Windows.Controls.TextBox> の詳細については、「[TextBox の概要](textbox-overview.md)」を参照してください。 次の表は、<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.RichTextBox> の主な機能をまとめたものです。

|Control|リアルタイム スペル チェック|コンテキスト メニュー|<xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> (Ctr + B) のような書式設定コマンド|イメージ、段落、テーブルのような <xref:System.Windows.Documents.FlowDocument> コンテンツ|
|-------------|------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|<xref:System.Windows.Controls.TextBox>|はい|はい|いいえ|いいえ。|
|<xref:System.Windows.Controls.RichTextBox>|はい|はい|はい|はい|

> [!NOTE]
> <xref:System.Windows.Controls.TextBox> では <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> (Ctr + B) のような書式設定関連のコマンドはサポートされませんが、<xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A> などの多くの基本的なコマンドは両方のコントロールでサポートされます。

上の表の機能については、後で詳しく説明します。

<a name="creating_a_richtextbox"></a>

## <a name="creating-a-richtextbox"></a>RichTextBox の作成

以下のコードには、ユーザーがリッチ コンテンツを編集できる <xref:System.Windows.Controls.RichTextBox> を作成する方法が示されています。

[!code-xaml[RichTextBoxMiscSnippets_snip#BasicRichTextBoxExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/BasicRichTextBoxExample.xaml#basicrichtextboxexamplewholepage)]

具体的には、<xref:System.Windows.Controls.RichTextBox> で編集されるコンテンツはフロー コンテンツです。 フロー コンテンツは、書式設定されたテキスト、イメージ、リスト、テーブルなどのさまざまな種類の要素を格納できます。 フロー ドキュメントの詳細については、[フロー ドキュメントの概要](../advanced/flow-document-overview.md)を参照してください。 フロー コンテンツを含めるために、<xref:System.Windows.Controls.RichTextBox> では <xref:System.Windows.Documents.FlowDocument> オブジェクトがホストされ、次にそれには編集可能なコンテンツが含まれます。 <xref:System.Windows.Controls.RichTextBox> のフロー コンテンツを示すために、次のコードでは、段落と何らかの太字のテキストを使用して <xref:System.Windows.Controls.RichTextBox> を作成する方法を示します。

[!code-xaml[RichTextBoxMiscSnippets_snip#RichTextBoxWithContentExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/RichTextBoxWithContentExample.xaml#richtextboxwithcontentexamplewholepage)]

[!code-csharp[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/CSharp/BasicRichTextBoxWithContentExample.cs#basicrichtextboxwithcontentcodeonlyexample)]
[!code-vb[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/visualbasic/basicrichtextboxwithcontentexample.vb#basicrichtextboxwithcontentcodeonlyexample)]

次の図は、このサンプルがレンダリングする方法を示しています。

![RichTextBox with content](./media/editing-richtextbox-with-content.png "Editing_RichTextBox_with_Content")

<xref:System.Windows.Documents.Paragraph> や <xref:System.Windows.Documents.Bold> などの要素で、<xref:System.Windows.Controls.RichTextBox> 内のコンテンツがどのように表示されるかが決まります。 ユーザーが <xref:System.Windows.Controls.RichTextBox> コンテンツを編集すると、このフロー コンテンツが変更されます。 フロー コンテンツの機能およびその操作方法の詳細については、[フロー ドキュメントの概要](../advanced/flow-document-overview.md)を参照してください。

> [!NOTE]
> <xref:System.Windows.Controls.RichTextBox> 内のフロー コンテンツは、他のコントロールに含まれているフロー コンテンツと一部異なる動作をします。 たとえば、<xref:System.Windows.Controls.RichTextBox> に列がないと、自動サイズ変更動作は行われません。 また、検索、表示モード、ページ ナビゲーション、ズームなどの組み込み機能は、<xref:System.Windows.Controls.RichTextBox> 内では利用できません。

<a name="realtime_spellechecking"></a>

## <a name="real-time-spell-checking"></a>リアルタイム スペル チェック

<xref:System.Windows.Controls.TextBox> または <xref:System.Windows.Controls.RichTextBox> で、リアルタイム スペル チェックを有効にすることができます。 スペル チェックをオンにすると、スペル ミスの語句の下に赤色の線が表示されます (下図を参照)。

![スペル チェックを含む Textbox](./media/editing-textbox-with-spellchecking.png "Editing_TextBox_with_Spellchecking")

スペル チェックを有効にする方法については、「[テキスト編集コントロールでスペル チェックを有効にする](how-to-enable-spell-checking-in-a-text-editing-control.md)」を参照してください。

<a name="context_menu"></a>

## <a name="context-menu"></a>コンテキスト メニュー

既定では、<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.RichTextBox> の両方に、ユーザーがコントロール内を右クリックしたときに表示されるコンテキスト メニューがあります。 コンテキスト メニューでは、ユーザーは、切り取り、コピー、または貼り付けをできます (下図を参照)。

![コンテキスト メニューを含む TextBox](./media/editing-textbox-with-context-menu.png "Editing_TextBox_with_Context_Menu")

独自のカスタム コンテキスト メニューを作成して、既定のコンテキスト メニューをオーバーライドできます。 詳細については、[カスタム コンテキスト メニューを RichTextBox に配置](how-to-position-a-custom-context-menu-in-a-richtextbox.md)を参照してください。

<a name="detect_when_content_changes"></a>

## <a name="editing-commands"></a>コマンドの編集

コマンドの編集では、ユーザーは、<xref:System.Windows.Controls.RichTextBox> 内の編集可能なコンテンツの書式を設定できます。 <xref:System.Windows.Controls.RichTextBox> には、基本的な編集コマンドのほかに、<xref:System.Windows.Controls.TextBox> ではサポートされない書式設定コマンドが含まれています。 たとえば、<xref:System.Windows.Controls.RichTextBox> で編集する場合、ユーザーは、Ctr + B キーを押して太字テキストの書式設定を切り替えることができます。 使用できるコマンドの完全な一覧については、「<xref:System.Windows.Documents.EditingCommands>」を参照してください。 キーボード ショートカットを使用するだけでなく、ボタンのようにコマンドをフックしてその他のコントロールにすることができます。 次の例では、テキストの書式設定を変更するためにユーザーが使用できるボタンを含む簡単なツールバーを作成する方法を示します。

[!code-xaml[RichTextBox_InputPanel_snip#RichTextBoxWithToolBarExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_InputPanel_snip/CS/Window1.xaml#richtextboxwithtoolbarexamplewholepage)]

次の図は、このサンプルの表示方法を示しています。

![ツールバーを含む RichTextBox](./media/editing-richtextbox-with-toobar.gif "Editing_RichTextBox_with_TooBar")

<a name="editing_commands"></a>

## <a name="detect-when-content-changes"></a>コンテンツがいつ変更されたかの検出

通常、<xref:System.Windows.Controls.TextBox> または <xref:System.Windows.Controls.RichTextBox> のテキストが変更されたときには常に、予想どおり、<xref:System.Windows.UIElement.KeyDown> ではなく、<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> イベントを使用して検出する必要があります。 例については、「[TextBox のテキストがいつ変更されたかを検出する](how-to-detect-when-text-in-a-textbox-has-changed.md)」を参照してください。

<a name="save_load_and_print_richtextbox_content"></a>

## <a name="save-load-and-print-richtextbox-content"></a>RichTextBox コンテンツの保存、読み込み、および印刷

次の例では、<xref:System.Windows.Controls.RichTextBox> のコンテンツをファイルに保存し、そのコンテンツを <xref:System.Windows.Controls.RichTextBox> に再度読み込み、コンテンツを印刷する方法を示します。 この例のマークアップを次に示します。

[!code-xaml[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml#saveloadprintrtbexamplewholepage)]

この例のコードを次に示します。

[!code-csharp[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml.cs#saveloadprintrtbcodeexamplewholepage)]
[!code-vb[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/VisualBasic/SaveLoadPrintRTB.xaml.vb#saveloadprintrtbcodeexamplewholepage)]

## <a name="see-also"></a>関連項目

- [方法トピック](richtextbox-how-to-topics.md)
- [TextBox の概要](textbox-overview.md)
