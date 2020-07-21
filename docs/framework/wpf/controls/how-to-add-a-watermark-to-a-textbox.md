---
title: '方法: TextBox へのウォーターマークの追加'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- displaying a background image inside a text box to aid user input [WPF]
- aid usability of a TextBox using a background image [WPF]
ms.assetid: df89bdd8-a0fb-45e0-b312-dd53332d01a8
ms.openlocfilehash: abe276c686d394ded13ec03f08deae65e4098d03
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923577"
---
# <a name="how-to-add-a-watermark-to-a-textbox"></a>方法: TextBox へのウォーターマークの追加
次の例では、<xref:System.Windows.Controls.TextBox> 内に説明のための背景画像を表示し、ユーザーがテキストを入力すると消えるようにすることで、<xref:System.Windows.Controls.TextBox> の利便性を向上させる方法を示しています。 また、ユーザーが入力を削除すると、背景画像が再び表示されます。 次の図を参照してください。  
  
 ![TextBox と背景画像](./media/editing-textbox-using-background-image.png " Editing_TextBox_using_background_image")  
  
> [!NOTE]
> この例で、<xref:System.Windows.Controls.TextBox> の <xref:System.Windows.Controls.TextBox.Text%2A> プロパティを操作するのではなく、背景画像が使用されているのは、背景画像がデータ バインディングに干渉しないという理由からです。  
  
## <a name="example"></a>例  
 [!code-xaml[TextBoxMiscSnippets_snip#TextBoxBackgroundExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml#textboxbackgroundexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml.cs#textboxbackgroundcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/textbox_with_background_image.xaml.vb#textboxbackgroundcodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
