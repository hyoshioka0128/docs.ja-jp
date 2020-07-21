---
title: '方法: テキスト編集コントロールでスペル チェックを有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- spellchecking [WPF]
- real-time spellchecking
- TextBox control [WPF], real-time spellchecking
- spelling checker [WPF]
- checking spelling [WPF]
ms.assetid: 6f953d2b-67e8-4012-84ce-53c0e958da47
ms.openlocfilehash: 7381bafc349506d89058581e9ed62a4348a72865
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62031944"
---
# <a name="how-to-enable-spell-checking-in-a-text-editing-control"></a>方法: テキスト編集コントロールでスペル チェックを有効にする
次の例では、<xref:System.Windows.Controls.SpellCheck> クラスの <xref:System.Windows.Controls.SpellCheck.IsEnabled%2A> プロパティを使用し、<xref:System.Windows.Controls.TextBox> でリアルタイムのスペル チェックを有効にする方法を示します。  
  
## <a name="example"></a>例  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellCheckExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/spellcheckexample.xaml#spellcheckexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/CSharp/SpellCheckExample.cs#spellcheckcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/visualbasic/spellcheckexample.vb#spellcheckcodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [コンテキスト メニューでスペル チェックを使用する](how-to-use-spell-checking-with-a-context-menu.md)
- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
