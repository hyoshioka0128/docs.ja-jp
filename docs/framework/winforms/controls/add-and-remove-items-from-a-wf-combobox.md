---
title: ComboBox、ListBox、または CheckedListBox コントロールの項目を追加および削除する
ms.date: 03/30/2017
description: Windows フォーム ComboBox、ListBox、CheckedListBox の各コントロールを、データバインディングなしで簡単に追加および削除する方法について説明します。
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- combo boxes [Windows Forms], adding items
- list boxes [Windows Forms], removing items
- ComboBox control [Windows Forms], adding and removing items
- ListBox control [Windows Forms], adding and removing items
- list boxes [Windows Forms], adding items
- combo boxes [Windows Forms], removing items
- CheckedListBox control [Windows Forms], adding and removing items
ms.assetid: 7224c8d2-4118-443e-ae1e-d7c17d1e69ee
ms.openlocfilehash: f3701257bbe410bf03c4c21700705e87b581bf2e
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904443"
---
# <a name="how-to-add-and-remove-items-from-a-windows-forms-combobox-listbox-or-checkedlistbox-control"></a>方法: Windows フォームの ComboBox、ListBox、または CheckedListBox コントロールに項目を追加または削除する
項目は、さまざまな方法で Windows フォームコンボボックス、リストボックス、またはチェックリストボックスに追加できます。これらのコントロールはさまざまなデータソースにバインドできるためです。 ただし、このトピックでは、最も簡単な方法について説明し、データバインディングは不要です。 通常、表示される項目は文字列です。ただし、任意のオブジェクトを使用できます。 コントロールに表示されるテキストは、オブジェクトのメソッドによって返される値です `ToString` 。  
  
### <a name="to-add-items"></a>項目を追加するには  
  
1. クラスのメソッドを使用して、文字列またはオブジェクトをリストに追加し `Add` `ObjectCollection` ます。 コレクションは、次のプロパティを使用して参照され `Items` ます。  
  
    ```vb  
    ComboBox1.Items.Add("Tokyo")  
    ```  
  
    ```csharp  
    comboBox1.Items.Add("Tokyo");  
    ```  
  
    ```cpp  
    comboBox1->Items->Add("Tokyo");  
    ```  
  
     - または  
  
2. メソッドを使用して、リスト内の目的の位置に文字列またはオブジェクトを挿入し `Insert` ます。  
  
    ```vb  
    CheckedListBox1.Items.Insert(0, "Copenhagen")  
    ```  
  
    ```csharp  
    checkedListBox1.Items.Insert(0, "Copenhagen");  
    ```  
  
    ```cpp  
    checkedListBox1->Items->Insert(0, "Copenhagen");  
    ```  
  
     - または  
  
3. 配列全体をコレクションに割り当て `Items` ます。  
  
    ```vb  
    Dim ItemObject(9) As System.Object  
    Dim i As Integer  
       For i = 0 To 9  
       ItemObject(i) = "Item" & i  
    Next i  
    ListBox1.Items.AddRange(ItemObject)  
    ```  
  
    ```csharp  
    System.Object[] ItemObject = new System.Object[10];  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = "Item" + i;  
    }  
    listBox1.Items.AddRange(ItemObject);  
    ```  
  
    ```cpp  
    Array<System::Object^>^ ItemObject = gcnew Array<System::Object^>(10);  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = String::Concat("Item", i.ToString());  
    }  
    listBox1->Items->AddRange(ItemObject);  
    ```  
  
### <a name="to-remove-an-item"></a>アイテムを削除するには  
  
1. `Remove` `RemoveAt` 項目を削除するには、メソッドまたはメソッドを呼び出します。  
  
     `Remove`には、削除する項目を指定する引数が1つあります。`RemoveAt` 指定したインデックス番号の項目を削除します。  
  
    ```vb  
    ' To remove item with index 0:  
    ComboBox1.Items.RemoveAt(0)  
    ' To remove currently selected item:  
    ComboBox1.Items.Remove(ComboBox1.SelectedItem)  
    ' To remove "Tokyo" item:  
    ComboBox1.Items.Remove("Tokyo")  
    ```  
  
    ```csharp  
    // To remove item with index 0:  
    comboBox1.Items.RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1.Items.Remove(comboBox1.SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1.Items.Remove("Tokyo");  
    ```  
  
    ```cpp  
    // To remove item with index 0:  
    comboBox1->Items->RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1->Items->Remove(comboBox1->SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1->Items->Remove("Tokyo");  
    ```  
  
### <a name="to-remove-all-items"></a>すべての項目を削除するには  
  
1. メソッドを呼び出して `Clear` 、コレクションからすべての項目を削除します。  
  
    ```vb  
    ListBox1.Items.Clear()  
    ```  
  
    ```csharp  
    listBox1.Items.Clear();  
    ```  
  
    ```cpp  
    listBox1->Items->Clear();  
    ```  
  
## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- <xref:System.Windows.Forms.CheckedListBox>
- [方法: Windows フォーム ComboBox、ListBox、または CheckedListBox コントロールを並べ替える](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [ListBox の代わりに Windows フォーム ComboBox を使用する場合](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)
- [オプションのリストを表示するための Windows フォーム コントロール](windows-forms-controls-used-to-list-options.md)
