---
title: ComboBox と ListBox
description: Windows フォーム ComboBox と Windows フォーム ListBox を使用する方法について説明します。また、タスクに適しているかどうかを判断する方法についても説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- ListBox control [Windows Forms], adding and removing items
- ListBox control [Windows Forms], vs. ComboBox
- bound controls [Windows Forms], combo boxes
- Windows Forms controls, data binding
- ComboBox control [Windows Forms], compared to ListBox
- combo boxes [Windows Forms], compared to list boxes
- ListBox control [Windows Forms], accessing items
- ListCount property
ms.assetid: 7bcaea58-1cfa-46db-9baf-b75a69d8f9ec
ms.openlocfilehash: ca6ad6bec2dbc30128ea09808af2806687b17a8c
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174420"
---
# <a name="when-to-use-a-windows-forms-combobox-instead-of-a-listbox"></a>ListBox の代わりに Windows フォーム ComboBox を使用する場合
とのコントロールには <xref:System.Windows.Forms.ComboBox> <xref:System.Windows.Forms.ListBox> 同様の動作があり、場合によっては交換可能である場合もあります。 ただし、タスクにより適切なものがある場合もあります。  
  
 一般的に、コンボボックスは、推奨される選択肢のリストがある場合に適しています。また、リストボックスは、入力を一覧の内容に限定する場合に適しています。 コンボボックスにはテキストボックスフィールドが含まれているので、一覧にない選択肢を入力することもできます。 この例外は、 <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> プロパティがに設定されている場合に発生し <xref:System.Windows.Forms.ComboBoxStyle.DropDownList> ます。 この場合、最初の文字を入力すると、コントロールによって項目が選択されます。  
  
 また、コンボボックスでは、フォーム上の領域が節約されます。 ユーザーが下矢印をクリックするまでは完全な一覧が表示されないため、コンボボックスは、リストボックスが収まらない小さなスペースに簡単に収めることができます。 例外は、プロパティがに設定されている場合です <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> <xref:System.Windows.Forms.ComboBoxStyle.Simple> 。完全な一覧が表示されます。コンボボックスは、リストボックスの場合よりも多くの領域を必要とします。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- [方法: Windows フォームの ComboBox、ListBox、または CheckedListBox コントロールに項目を追加または削除する](add-and-remove-items-from-a-wf-combobox.md)
- [方法: Windows フォーム ComboBox、ListBox、または CheckedListBox コントロールを並べ替える](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [オプションのリストを表示するための Windows フォーム コントロール](windows-forms-controls-used-to-list-options.md)
