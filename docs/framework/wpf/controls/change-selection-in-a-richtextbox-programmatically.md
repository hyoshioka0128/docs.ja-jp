---
title: プログラムによる RichTextBox での選択の変更
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- changing selections in a text box [WPF]
- changing selections in a RichTextBox [WPF]
ms.assetid: f1213205-1ad7-4cd2-b115-460173cc5aa3
ms.openlocfilehash: b8acfe7cde1fe5dae96cd6324f75c5b146be9ec9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001716"
---
# <a name="change-selection-in-a-richtextbox-programmatically"></a>プログラムによる RichTextBox での選択の変更
この例では、<xref:System.Windows.Controls.RichTextBox> の現在の選択を、プログラムを使って変更する方法を示します。 この選択は、ユーザーがユーザー インターフェイスを使用してコンテンツを選択した場合と同じです。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] コードでは、単純コンテンツが含まれる名前付き <xref:System.Windows.Controls.RichTextBox> コントロールについて説明します。  
  
 [!code-xaml[RichTextBoxMiscSnippets_snip#ChangeSelectionProgrammaticalyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/ChangeSelectionProgrammaticaly.xaml#changeselectionprogrammaticalyexamplewholepage)]  
  
## <a name="example"></a>例  
 次のコードでは、ユーザーが <xref:System.Windows.Controls.RichTextBox> 内をクリックすると、任意のテキストがプログラムで選択されます。  
  
 [!code-csharp[RichTextBoxMiscSnippets_snip#ChangeSelectionProgrammaticalyCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/ChangeSelectionProgrammaticaly.xaml.cs#changeselectionprogrammaticalycodeexamplewholepage)]
 [!code-vb[RichTextBoxMiscSnippets_snip#ChangeSelectionProgrammaticalyCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/VisualBasic/ChangeSelectionProgrammaticaly.xaml.vb#changeselectionprogrammaticalycodeexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- [RichTextBox の概要](richtextbox-overview.md)
- [TextBox の概要](textbox-overview.md)
