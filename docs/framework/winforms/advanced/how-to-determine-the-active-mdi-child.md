---
title: '方法 : アクティブな MDI 子フォームを特定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Clipboard [Windows Forms], copying data to
- MDI [Windows Forms], child windows
- child forms
- MDI [Windows Forms], activating forms
- MDI [Windows Forms], locating focus
ms.assetid: 33880ec3-0207-4c2b-a616-ff140443cc0f
ms.openlocfilehash: 57491faa10c182630d41565ba236d65e393929b3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182546"
---
# <a name="how-to-determine-the-active-mdi-child"></a>方法 : アクティブな MDI 子フォームを特定する
場合によっては、現在アクティブな子フォームにフォーカスがあるコントロールを操作するコマンドを提供します。 たとえば、選択したテキストを子フォームのテキスト ボックスからクリップボードにコピーするとします。 標準の [編集] メニューの [コピー]<xref:System.Windows.Forms.Control.Click>メニュー項目のイベントを使用して、選択したテキストをクリップボードにコピーするプロシージャを作成します。  
  
 MDI アプリケーションは同じ子フォームのインスタンスを多数持つことができるので、プロシージャはどのフォームを使用するかを知る必要があります。 正しいフォームを指定するには、フォーカス<xref:System.Windows.Forms.Form.ActiveMdiChild%2A>のある子フォームまたは最後にアクティブだった子フォームを返すプロパティを使用します。  
  
 フォームに複数のコントロールがある場合は、アクティブにするコントロールも指定する必要があります。 プロパティと<xref:System.Windows.Forms.Form.ActiveMdiChild%2A>同様に、<xref:System.Windows.Forms.ContainerControl.ActiveControl%2A>このプロパティは、アクティブな子フォームにフォーカスを設定したコントロールを返します。 次の手順は、子フォーム メニュー、MDI フォームのメニュー、またはツール バー ボタンから呼び出すことができるコピー 手順を示しています。  
  
### <a name="to-determine-the-active-mdi-child-to-copy-its-text-to-the-clipboard"></a>アクティブな MDI 子を確認するには (テキストをクリップボードにコピーする)  
  
1. メソッド内で、アクティブな子フォームのアクティブ なコントロールのテキストをクリップボードにコピーします。  
  
    > [!NOTE]
    > この例では、`Form1`<xref:System.Windows.Forms.RichTextBox>コントロールを含む 1 つ以上の MDI 子ウィンドウを持つ MDI 親フォーム ( ) があることを前提としています。 詳細については、「 [MDI 親フォームの作成](how-to-create-mdi-parent-forms.md)」を参照してください。  
  
    ```vb  
    Public Sub mniCopy_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniCopy.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Dim theBox As RichTextBox = _  
            TryCast(activeChild.ActiveControl, RichTextBox)  
  
          If (Not theBox Is Nothing) Then  
             'Put selected text on Clipboard.  
             Clipboard.SetDataObject(theBox.SelectedText)  
          Else  
             MessageBox.Show("You need to select a RichTextBox.")  
          End If  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    protected void mniCopy_Click (object sender, System.EventArgs e)  
    {  
       // Determine the active child form.  
       Form activeChild = this.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {
          try  
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Put the selected text on the Clipboard.  
                Clipboard.SetDataObject(theBox.SelectedText);  
  
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
- [方法 : アクティブな MDI 子フォームにデータを送信する](how-to-send-data-to-the-active-mdi-child.md)
- [方法: MDI 子フォームを配置する](how-to-arrange-mdi-child-forms.md)
