---
title: TextBox コントロール内のテキストを選択する
description: Windows フォーム TextBox コントロールでプログラムによってテキストを選択する方法について説明します。 また、検出された文字列の位置を視覚的に通知する方法についても説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TextBox control [Windows Forms], selecting text programmatically
- text boxes [Windows Forms], selecting text programmatically
- text [Windows Forms], selecting in text boxes programmatically
ms.assetid: 8c591546-6a01-45c7-8e03-f78431f903b1
ms.openlocfilehash: b8fdaff76461c4d6766dfc6afaef5e814d982834
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621562"
---
# <a name="how-to-select-text-in-the-windows-forms-textbox-control"></a>方法: Windows フォーム TextBox コントロールでテキストを選択する
Windows フォームコントロールで、プログラムによってテキストを選択でき <xref:System.Windows.Forms.TextBox> ます。 たとえば、特定の文字列を検索する関数を作成する場合、テキストを選択して、検出された文字列の位置のリーダーを視覚的に警告することができます。  
  
### <a name="to-select-text-programmatically"></a>プログラムによってテキストを選択するには  
  
1. プロパティを、 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 選択するテキストの先頭に設定します。  
  
     プロパティは、 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> テキストの文字列内の挿入ポイントを示す数値です。0は左端の位置を表します。 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A>プロパティがテキストボックス内の文字数以上に設定されている場合、挿入ポイントは最後の文字の後に配置されます。  
  
2. プロパティを、 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 選択するテキストの長さに設定します。  
  
     プロパティは、 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 挿入ポイントの幅を設定する数値です。 を <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 0 より大きい数値に設定すると、現在の挿入ポイントから始まる文字数が選択されます。  
  
3. Optionalプロパティを使用して、選択したテキストにアクセスし <xref:System.Windows.Forms.TextBoxBase.SelectedText%2A> ます。  
  
     次のコードでは、コントロールのイベントが発生したときにテキストボックスの内容を選択し <xref:System.Windows.Forms.Control.Enter> ます。 この例では、テキストボックスに、または空の文字列ではないプロパティの値があるかどうかを確認 <xref:System.Windows.Forms.TextBox.Text%2A> `null` します。 テキストボックスがフォーカスを受け取ると、テキストボックス内の現在のテキストが選択されます。 `TextBox1_Enter`イベントハンドラーはコントロールにバインドされている必要があります。詳細については、「[方法: 実行時にイベントハンドラーを作成](../how-to-create-event-handlers-at-run-time-for-windows-forms.md)する」を参照して Windows フォームしてください。  
  
     この例をテストするには、テキストボックスにフォーカスが移動するまで Tab キーを押します。 テキストボックス内をクリックすると、テキストは選択されません。  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       If (Not String.IsNullOrEmpty(TextBox1.Text)) Then  
          TextBox1.SelectionStart = 0  
          TextBox1.SelectionLength = TextBox1.Text.Length  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_Enter(object sender, System.EventArgs e){  
       if (!String.IsNullOrEmpty(textBox1.Text))  
       {  
          textBox1.SelectionStart = 0;  
          textBox1.SelectionLength = textBox1.Text.Length;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^ sender,  
          System::EventArgs ^ e) {  
       if (!System::String::IsNullOrEmpty(textBox1->Text))  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = textBox1->Text->Length;  
       }  
    }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.TextBox>
- [TextBox コントロールの概要](textbox-control-overview-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールでのカーソル位置を制御する](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [方法: Windows フォームの TextBox コントロールを使用してパスワード テキスト ボックスを作成する](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [方法: 読み取り専用テキスト ボックスを作成する](how-to-create-a-read-only-text-box-windows-forms.md)
- [方法: 文字列に引用符を挿入する](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールで複数行を表示する](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox コントロール](textbox-control-windows-forms.md)
