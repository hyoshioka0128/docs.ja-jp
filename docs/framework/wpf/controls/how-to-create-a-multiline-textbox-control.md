---
title: '方法: 複数行の TextBox コントロールを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], multiple lines of text
ms.assetid: 05914a93-d0ea-4a9a-b693-09df7d4e2ac2
ms.openlocfilehash: 29fb4c9498fe163c36e71680242d3ef8cf98c089
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001274"
---
# <a name="how-to-create-a-multiline-textbox-control"></a>方法: 複数行の TextBox コントロールを作成する
次の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して、複数行のテキストに合わせて自動的に拡張する <xref:System.Windows.Controls.TextBox> コントロールを定義する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.TextBox.TextWrapping%2A> 属性を **Wrap** に設定すると、入力されたテキストは <xref:System.Windows.Controls.TextBox> コントロールの端に達すると新しい行に折り返され、必要に応じて新しい行の空間が含まれるように <xref:System.Windows.Controls.TextBox> コントロールが自動的に拡張されます。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> 属性を **true** に設定すると、RETURN キーが押されたときに新しい行が挿入されて、必要に応じて新しい行の空間が含まれるようにもう一度 <xref:System.Windows.Controls.TextBox> が自動的に拡張されます。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> 属性によってスクロール バーが <xref:System.Windows.Controls.TextBox> に追加されるため、<xref:System.Windows.Controls.TextBox> がこれを囲むフレームまたはウィンドウのサイズよりも大きくなった場合、スクロール バーを使用して <xref:System.Windows.Controls.TextBox> の内容をスクロールできます。  
  
 [!code-xaml[TextBox_MiscCode#_MultilineTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.TextWrapping>
- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
