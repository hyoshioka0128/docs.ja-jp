---
title: '方法: TextBox コントロールを読み取り専用にする'
ms.date: 03/30/2017
helpviewer_keywords:
- read-only TextBox controls [WPF]
- TextBox control read-only
ms.assetid: e707ec59-8b22-473e-b77c-3060a237517a
ms.openlocfilehash: 7f24458eb98bd669d59f15c49d1d9e3beb6833b1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770943"
---
# <a name="how-to-make-a-textbox-control-read-only"></a>方法: TextBox コントロールを読み取り専用にする
この例では、ユーザーの入力または変更を許可しないように、<xref:System.Windows.Controls.TextBox> コントロールを構成する方法を示します。  
  
## <a name="example"></a>例  
 ユーザーが <xref:System.Windows.Controls.TextBox> コントロールのコンテンツを変更できないようにするには、<xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 属性を **true** に設定します。  
  
 [!code-xaml[TextBox_MiscCode#_ReadOnlyTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_readonlytextboxxaml)]  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 属性は、ユーザー入力のみに影響します。<xref:System.Windows.Controls.TextBox> コントロールの [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 説明のテキスト セットや、<xref:System.Windows.Controls.TextBox.Text%2A> プロパティを使用してプログラムによって設定されたテキストに影響することはありません。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> の既定値は **false** です。  
  
## <a name="see-also"></a>関連項目

- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
