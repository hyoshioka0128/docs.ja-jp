---
title: TextBox の概要
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], TextBox
- TextBox control [WPF], about TextBox control
ms.assetid: 1ba6dc5b-11a7-4247-9213-36c6729ee35f
ms.openlocfilehash: 86b2cf8cb0c72186fd92bdad0af6bf5bd3fa9f3f
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174433"
---
# <a name="textbox-overview"></a>TextBox の概要
<xref:System.Windows.Controls.TextBox> クラスでは、書式設定されていないテキストを表示または編集できます。 <xref:System.Windows.Controls.TextBox> の一般的な用途は、フォームで書式設定されていないテキストを編集することです。 たとえば、ユーザーの名前、電話番号などの入力を求めるフォームでは、テキスト入力用に <xref:System.Windows.Controls.TextBox> コントロールを使用します。 このトピックでは、<xref:System.Windows.Controls.TextBox> クラスを紹介し、それを [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] と C# の両方で使用する方法の例を示します。  

<a name="textbox_or_richtextbox"></a>
## <a name="textbox-or-richtextbox"></a>TextBox か RichTextBox か  
 <xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.RichTextBox> のどちらを使用しても、ユーザーはテキストを入力できますが、この 2 つのコントロールは異なるシナリオで使用されます。 <xref:System.Windows.Controls.TextBox> は、必要なシステム リソースが <xref:System.Windows.Controls.RichTextBox> より少ないため、プレーンテキストのみを編集する必要がある場合に理想的です (つまりフォームでの使用)。 <xref:System.Windows.Controls.RichTextBox> は、書式設定されたテキスト、イメージ、テーブルなどのサポート対象コンテンツを編集する必要がある場合に適しています。 たとえば、書式設定やイメージなどを必要とするドキュメント、記事、またはブログを編集する場合は、<xref:System.Windows.Controls.RichTextBox> を使用することをお勧めします。 次の表は、<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.RichTextBox> の主な機能をまとめたものです。  
  
|Control|リアルタイム スペル チェック|コンテキスト メニュー|<xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> (Ctrl + B) のような書式設定コマンド|イメージ、段落、テーブルのような <xref:System.Windows.Documents.FlowDocument> コンテンツ|  
|-------------|------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.TextBox>|はい|はい|いいえ|いいえ。|  
|<xref:System.Windows.Controls.RichTextBox>|はい|はい|はい (「[RichTextBox の概要](richtextbox-overview.md)」を参照)|はい (「[RichTextBox の概要](richtextbox-overview.md)」を参照)|  
  
> [!NOTE]
> <xref:System.Windows.Controls.TextBox> では <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> (Ctrl + B) のような書式設定関連の編集コマンドはサポートされていませんが、<xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A> などの多くの基本的なコマンドは両方のコントロールでサポートされています。 詳細については、「<xref:System.Windows.Documents.EditingCommands>」を参照してください。  
  
 <xref:System.Windows.Controls.TextBox> でサポートされる機能については、以下の各セクションで説明します。 <xref:System.Windows.Controls.RichTextBox> の詳細については、「[RichTextBox の概要](richtextbox-overview.md)」を参照してください。  
  
### <a name="real-time-spellchecking"></a>リアルタイム スペル チェック  
 <xref:System.Windows.Controls.TextBox> または <xref:System.Windows.Controls.RichTextBox> で、リアルタイム スペル チェックを有効にすることができます。 スペル チェックをオンにすると、スペル ミスの語句の下に赤色の線が表示されます (下図を参照)。  
  
 ![スペル チェックを含む TextBox](./media/editing-textbox-with-spellchecking.png "Editing_TextBox_with_Spellchecking")  
  
 スペル チェックを有効にする方法については、「[テキスト編集コントロールでスペル チェックを有効にする](how-to-enable-spell-checking-in-a-text-editing-control.md)」を参照してください。  
  
### <a name="context-menu"></a>コンテキスト メニュー  
 既定では、<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.RichTextBox> の両方に、ユーザーがコントロール内を右クリックしたときに表示されるコンテキスト メニューがあります。 コンテキスト メニューでは、切り取り、コピー、または貼り付けをできます (下図を参照)。  
  
 ![コンテキスト メニューを含む TextBox](./media/editing-textbox-with-context-menu.png "Editing_TextBox_with_Context_Menu")  
  
 既定の動作をオーバーライドする独自のカスタム コンテキスト メニューを作成できます。 詳細については、「[TextBox でカスタム コンテキスト メニューを使用する](how-to-use-a-custom-context-menu-with-a-textbox.md)」を参照してください。  
  
<a name="creating_textboxes"></a>
## <a name="creating-textboxes"></a>TextBox の作成  
 <xref:System.Windows.Controls.TextBox> は、1 行の高さにしたり、複数行で構成したりできます。 単一行の <xref:System.Windows.Controls.TextBox> は、少量のプレーン テキストの入力に最適です (たとえば、「名前」、「電話番号」などのフォームへの入力)。 次の例では、単一行の <xref:System.Windows.Controls.TextBox> を作成する方法を示します。  
  
 [!code-xaml[TextBoxMiscSnippets_snip#BasicTextBoxExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/basictextboxexample.xaml#basictextboxexamplewholepage)]  
  
 ユーザーが複数行のテキストを入力できる <xref:System.Windows.Controls.TextBox> を作成することもできます。 たとえば、ユーザーの経歴の入力を求めるフォームの場合、複数行のテキストをサポートする <xref:System.Windows.Controls.TextBox> を使用できます。 次の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して複数行のテキストに合わせて自動的に拡張する <xref:System.Windows.Controls.TextBox> コントロールを定義する方法を示します。  
  
 [!code-xaml[TextBox_MiscCode#_MultilineTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
 <xref:System.Windows.Controls.TextBox.TextWrapping%2A> 属性を `Wrap` に設定すると、テキストは <xref:System.Windows.Controls.TextBox> コントロールの端に達すると新しい行に折り返され、必要に応じて新しい行の空間が含まれるように <xref:System.Windows.Controls.TextBox> コントロールが自動的に拡張されます。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> 属性を `true` に設定すると、RETURN キーが押されると新しい行が挿入され、必要に応じて新しい行の空間が含まれるようにもう一度 <xref:System.Windows.Controls.TextBox> が自動的に拡張されます。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> 属性によってスクロール バーが <xref:System.Windows.Controls.TextBox> に追加されるため、<xref:System.Windows.Controls.TextBox> がこれを囲むフレームまたはウィンドウのサイズよりも大きくなった場合、スクロール バーを使用して <xref:System.Windows.Controls.TextBox> の内容をスクロールできます。  
  
 <xref:System.Windows.Controls.TextBox> の使用に関係するさまざまなタスクの詳細については、「[方法のトピック](textbox-how-to-topics.md)」を参照してください。  
  
<a name="editing_commands"></a>
## <a name="detect-when-content-changes"></a>内容が変更されたときに検出する  
 通常、<xref:System.Windows.Controls.TextBox> または <xref:System.Windows.Controls.RichTextBox> のテキストが変更されたときには常に、予想されるような <xref:System.Windows.UIElement.KeyDown> ではなく、<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> イベントを使用して検出する必要があります。 例については、「[TextBox のテキストがいつ変更されたかを検出する](how-to-detect-when-text-in-a-textbox-has-changed.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [方法トピック](textbox-how-to-topics.md)
- [RichTextBox の概要](richtextbox-overview.md)
