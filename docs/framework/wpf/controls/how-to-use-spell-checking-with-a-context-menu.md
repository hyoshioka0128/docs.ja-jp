---
title: '方法: コンテキスト メニューでスペル チェックを使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling spell checking in a text box [WPF]
- reenabling spell checking in a text box [WPF]
- spell checking with a context menu [WPF]
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
ms.openlocfilehash: 72b24c386eb99140c9c2729688994b81f92e1a6f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699150"
---
# <a name="how-to-use-spell-checking-with-a-context-menu"></a>方法: コンテキスト メニューでスペル チェックを使用する
既定では、<xref:System.Windows.Controls.TextBox> や <xref:System.Windows.Controls.RichTextBox> のような編集コントロールでスペルチェックを有効にすると、コンテキスト メニューにスペルチェックの選択肢が表示されます。 たとえば、綴りが間違っている単語をユーザーがクリックすると、綴り案がひととおり表示されるか、 **[すべて無視]** オプションが表示されます。 ただし、既定のコンテキスト メニューを独自のコンテキスト メニューでオーバーライドすると、この機能は失われます。コンテキスト メニューでスペルチェック機能を再び有効にするコードを記述する必要があります。 次の例では、<xref:System.Windows.Controls.TextBox> でこれを有効にする方法を示します。  
  
## <a name="example"></a>例  
 次の例では、コンテキスト メニューの実装に使用されるイベントをいくつか含む <xref:System.Windows.Controls.TextBox> を作成する [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を示します。  
  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## <a name="example"></a>例  
 次の例では、コンテキスト メニューを実装するコードを示します。  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 <xref:System.Windows.Controls.RichTextBox> でこれを行うためのコードも似ています。 主な違いは、`GetSpellingError` メソッドに渡されるパラメーターです。 <xref:System.Windows.Controls.TextBox> の場合、カーソル位置の整数インデックスが渡されます。  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 <xref:System.Windows.Controls.RichTextBox> の場合、キャレット位置を指定する <xref:System.Windows.Documents.TextPointer> が渡されます。  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## <a name="see-also"></a>関連項目

- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
- [テキスト編集コントロールでスペル チェックを有効にする](how-to-enable-spell-checking-in-a-text-editing-control.md)
- [TextBox でカスタム コンテキスト メニューを使用する](how-to-use-a-custom-context-menu-with-a-textbox.md)
