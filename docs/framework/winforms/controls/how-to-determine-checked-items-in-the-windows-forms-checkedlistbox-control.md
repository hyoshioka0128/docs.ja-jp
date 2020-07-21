---
title: CheckedListBox コントロールでチェックされている項目を確認する
description: CheckedItems プロパティに格納されているコレクションを反復処理して、Windows フォーム CheckedListBox コントロールでチェックされている項目を確認する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- check boxes [Windows Forms], determining checked state
- CheckedListBox control [Windows Forms], determining checked state
ms.assetid: 178b477d-27c9-489c-8914-44a9623a4d41
ms.openlocfilehash: fd8845ef83da7406ff4f1468506a23e3f4d386a0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618351"
---
# <a name="how-to-determine-checked-items-in-the-windows-forms-checkedlistbox-control"></a>方法: Windows フォーム CheckedListBox コントロールでオンになっている項目を判断する
Windows フォームコントロールにデータを表示する場合は、 <xref:System.Windows.Forms.CheckedListBox> プロパティに格納されているコレクションを反復処理するか、 <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> メソッドを使用してリストをステップ実行し、 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> どの項目がチェックされるかを決定できます。 メソッドは、 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 引数として項目のインデックス番号を取得し、 `true` またはを返し `false` ます。 期待しているものとは異なり、 <xref:System.Windows.Forms.ListBox.SelectedItems%2A> プロパティとプロパティではどの <xref:System.Windows.Forms.ListBox.SelectedIndices%2A> 項目がチェックされるかが決定されないため、どの項目が強調表示されるかが決まります。  
  
### <a name="to-determine-checked-items-in-a-checkedlistbox-control"></a>CheckedListBox コントロールでチェックされている項目を確認するには  
  
1. コレクションが0から始まる <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> ため、コレクションを反復処理して0から開始します。 このメソッドは、リスト全体ではなく、チェックされた項目の一覧に項目番号を提供します。 このため、リストの最初の項目がチェックされず、2番目の項目がオンになっている場合は、次のコードに "Checked Item 1 = MyListItem2" のようなテキストが表示されます。  
  
    ```vb  
    ' Determine if there are any items checked.  
    If CheckedListBox1.CheckedItems.Count <> 0 Then  
       ' If so, loop through all checked items and print results.  
       Dim x As Integer  
       Dim s As String = ""  
       For x = 0 To CheckedListBox1.CheckedItems.Count - 1  
          s = s & "Checked Item " & (x + 1).ToString & " = " & CheckedListBox1.CheckedItems(x).ToString & ControlChars.CrLf  
       Next x  
       MessageBox.Show(s)  
    End If  
    ```  
  
    ```csharp  
    // Determine if there are any items checked.  
    if(checkedListBox1.CheckedItems.Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       string s = "";  
       for(int x = 0; x < checkedListBox1.CheckedItems.Count ; x++)  
       {  
          s = s + "Checked Item " + (x+1).ToString() + " = " + checkedListBox1.CheckedItems[x].ToString() + "\n";  
       }  
       MessageBox.Show(s);  
    }  
    ```  
  
    ```cpp  
    // Determine if there are any items checked.  
    if(checkedListBox1->CheckedItems->Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       String ^ s = "";  
       for(int x = 0; x < checkedListBox1->CheckedItems->Count; x++)  
       {  
          s = String::Concat(s, "Checked Item ", (x+1).ToString(),  
             " = ", checkedListBox1->CheckedItems[x]->ToString(),  
             "\n");  
       }  
       MessageBox::Show(s);  
    }  
    ```  
  
     - または  
  
2. コレクションをステップ実行します。コレクションは0から始まり、 <xref:System.Windows.Forms.CheckedListBox.Items%2A> <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 各項目に対してメソッドを呼び出します。 この方法では、一覧の項目番号が表示されるので、リスト内の最初の項目がチェックされず、2番目の項目がオンになっている場合は、"Item 2 = MyListItem2" のような内容が表示されます。  
  
    ```vb  
    Dim i As Integer  
    Dim s As String  
    s = "Checked Items:" & ControlChars.CrLf  
    For i = 0 To (CheckedListBox1.Items.Count - 1)  
       If CheckedListBox1.GetItemChecked(i) = True Then  
          s = s & "Item " & (i + 1).ToString & " = " & CheckedListBox1.Items(i).ToString & ControlChars.CrLf  
       End If  
    Next  
    MessageBox.Show(s)  
    ```  
  
    ```csharp  
    int i;  
    string s;
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1.Items.Count-1); i++)  
    {  
       if (checkedListBox1.GetItemChecked(i))  
       {  
          s = s + "Item " + (i+1).ToString() + " = " + checkedListBox1.Items[i].ToString() + "\n";  
       }  
    }  
    MessageBox.Show (s);  
    ```  
  
    ```cpp  
    int i;  
    String ^ s;
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1->Items->Count-1); i++)  
    {  
       if (checkedListBox1->GetItemChecked(i))  
       {  
          s = String::Concat(s, "Item ", (i+1).ToString(), " = ",  
             checkedListBox1->Item[i]->ToString(), "\n");  
       }  
    }  
    MessageBox::Show(s);  
    ```  
  
## <a name="see-also"></a>関連項目

- [オプションのリストを表示するための Windows フォーム コントロール](windows-forms-controls-used-to-list-options.md)
