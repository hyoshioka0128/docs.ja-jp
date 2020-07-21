---
title: '方法: テキスト選択を取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF], retrieving
- TextBox control [WPF], retrieving text
- retrieving text [WPF]
ms.assetid: d5793172-1e11-4a39-9be0-73f336ed858d
ms.openlocfilehash: b7f0b9ee02a7ace717787fc8eeb6e15649829a49
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770787"
---
# <a name="how-to-retrieve-a-text-selection"></a>方法: テキスト選択を取得する
この例では、<xref:System.Windows.Controls.TextBox.SelectedText%2A> プロパティを使用して、ユーザーが <xref:System.Windows.Controls.TextBox> コントロールで選択したテキストを取得する方法の 1 つを示します。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の例は、"some text to select" を含む <xref:System.Windows.Controls.TextBox> コントロールの定義と、指定された <xref:System.Windows.Controls.Button.OnClick%2A> メソッドの <xref:System.Windows.Controls.Button> コントロールを示しています。  
  
 この例では、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが関連付けられているボタンを使用して、テキスト選択を取得します。 ユーザーがボタンをクリックすると、<xref:System.Windows.Controls.Button.OnClick%2A> メソッドによって、テキストボックス内の選択したテキストが文字列にコピーされます。 テキスト選択を取得する特定の状況 (ボタンをクリックする)、およびその選択によって実行されるアクション (テキスト選択を文字列にコピーする) は、さまざまなシナリオに対応するように簡単に変更できます。  
  
 [!code-xaml[TextBox_MiscCode#_TextBoxSelectTextXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxselecttextxaml)]  
  
## <a name="example"></a>例  
 次の C# の例は、この例の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で定義されているボタンの <xref:System.Windows.Controls.Button.OnClick%2A> イベント ハンドラーを示しています。  
  
 [!code-csharp[TextBox_MiscCode#_SelectText](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_selecttext)]
 [!code-vb[TextBox_MiscCode#_SelectText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_selecttext)]  
  
## <a name="see-also"></a>関連項目

- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
