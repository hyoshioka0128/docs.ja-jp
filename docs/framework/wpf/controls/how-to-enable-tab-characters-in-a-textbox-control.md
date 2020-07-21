---
title: '方法: TextBox コントロールでタブ文字を有効にする'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], enabling tab characters
- tab characters [WPF], enabling
ms.assetid: 14b1b064-61f7-4958-be63-88d85b868d03
ms.openlocfilehash: 9a01ae93d1b75c604fbe4f15f720e0a84086bd1a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910573"
---
# <a name="how-to-enable-tab-characters-in-a-textbox-control"></a>方法: TextBox コントロールでタブ文字を有効にする
この例からは、<xref:System.Windows.Controls.TextBox> コントロールの通常の入力としてタブ文字を受け取る方法がわかります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.TextBox> コントロールの入力としてタブ文字を受け取るには、<xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsTab%2A> 属性を **true** に設定します。  
  
 [!code-xaml[TextBox_EnablingTab#_AcceptsTab](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_EnablingTab/CS/Window1.xaml#_acceptstab)]  
  
## <a name="see-also"></a>関連項目

- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
