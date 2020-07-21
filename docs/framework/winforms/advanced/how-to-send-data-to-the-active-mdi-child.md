---
title: '方法 : アクティブな MDI 子フォームにデータを送信する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- child forms
- MDI [Windows Forms], sending data to forms
- Clipboard [Windows Forms], pasting
- Clipboard [Windows Forms], getting data from
ms.assetid: 1047d2fe-1235-46db-aad9-563aea1d743b
ms.openlocfilehash: 563be8494cb84dc74b45985d3ba74e4b6a07eb8a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182492"
---
# <a name="how-to-send-data-to-the-active-mdi-child"></a>方法 : アクティブな MDI 子フォームにデータを送信する
多くの場合、マルチ[ドキュメント インターフェイス (MDI) アプリケーション](multiple-document-interface-mdi-applications.md)のコンテキスト内では、ユーザーがクリップボードから MDI アプリケーションにデータを貼り付ける場合など、アクティブな子ウィンドウにデータを送信する必要があります。  
  
> [!NOTE]
> フォーカスがある子ウィンドウの確認と、その内容のクリップボードへの送信については、「[アクティブな MDI 子ウィンドウの判別](how-to-determine-the-active-mdi-child.md)」を参照してください。  
  
### <a name="to-send-data-to-the-active-mdi-child-window-from-the-clipboard"></a>クリップボードからアクティブな MDI 子ウィンドウにデータを送信するには  
  
1. メソッド内で、クリップボードのテキストをアクティブな子フォームのアクティブなコントロールにコピーします。  
  
    > [!NOTE]
    > この例では、`Form1`<xref:System.Windows.Forms.RichTextBox>コントロールを含む 1 つ以上の MDI 子ウィンドウを持つ MDI 親フォーム ( ) があることを前提としています。 詳細については、「 [MDI 親フォームの作成](how-to-create-mdi-parent-forms.md)」を参照してください。  
  
    ```vb  
    Public Sub mniPaste_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniPaste.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ParentForm.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Try  
             Dim theBox As RichTextBox = Ctype(activeChild.ActiveControl, RichTextBox)  
             If (Not theBox Is Nothing) Then  
                ' Create a new instance of the DataObject interface.  
                Dim data As IDataObject = Clipboard.GetDataObject()  
                ' If the data is text, then set the text of the
                ' RichTextBox to the text in the clipboard.  
                If (data.GetDataPresent(DataFormats.Text)) Then  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString()  
                End If  
             End If  
          Catch  
             MessageBox.Show("You need to select a RichTextBox.")  
          End Try  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    protected void mniPaste_Click (object sender, System.EventArgs e)  
    {  
      // Determine the active child form.  
       Form activeChild = this.ParentForm.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {  
          try
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Create a new instance of the DataObject interface.  
                IDataObject data = Clipboard.GetDataObject();  
                // If the data is text, then set the text of the
                // RichTextBox to the text in the clipboard.  
                if (data.GetDataPresent(DataFormats.Text))  
                {  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString();
                }  
             }  
          }  
          catch
          {  
             MessageBox.Show("You need to select a RichTextBox.");  
          }  
       }  
    }  
    ```  
  
## <a name="see-also"></a>関連項目

- [マルチ ドキュメント インターフェイス (MDI) アプリケーション](multiple-document-interface-mdi-applications.md)
- [方法 : MDI 親フォームを作成する](how-to-create-mdi-parent-forms.md)
- [方法 : MDI 子フォームを作成する](how-to-create-mdi-child-forms.md)
- [方法: アクティブな MDI 子フォームを特定する](how-to-determine-the-active-mdi-child.md)
- [方法: MDI 子フォームを配置する](how-to-arrange-mdi-child-forms.md)
