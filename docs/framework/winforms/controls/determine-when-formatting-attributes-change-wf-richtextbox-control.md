---
title: リッチテキスト ボックス コントロールで書式属性が変更されるタイミングを決定する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], text boxes
- RichTextBox control [Windows Forms], determining font changes
- text boxes [Windows Forms], determining font changes
- SelChange event
ms.assetid: bdfed015-f77a-41e5-b38f-f8629b2fa166
ms.openlocfilehash: a190c3479b58464763e0eefdd32d14e88a1f05e1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142265"
---
# <a name="how-to-determine-when-formatting-attributes-change-in-the-windows-forms-richtextbox-control"></a>方法 : Windows フォームの RichTextBox コントロールにおける書式属性の変更を確認する
Windows フォーム<xref:System.Windows.Forms.RichTextBox>コントロールの一般的な用途は、フォント オプションや段落スタイルなどの属性を使用してテキストを書式設定することです。 多くのワープロ アプリケーションのように、ツールバーを表示するために、アプリケーションでテキストの書式設定の変更を追跡する必要がある場合があります。  
  
### <a name="to-respond-to-changes-in-formatting-attributes"></a>書式属性の変更に応答するには  
  
1. イベント ハンドラーに<xref:System.Windows.Forms.RichTextBox.SelectionChanged>コードを記述して、属性の値に応じて適切なアクションを実行します。 次の使用例は、プロパティの値に応じてツール バー ボタン<xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A>の外観を変更します。 ツール バー ボタンは、コントロール内でカーソルが移動したときにのみ更新されます。  
  
     次の例では、コントロールとツール<xref:System.Windows.Forms.RichTextBox>バー<xref:System.Windows.Forms.ToolBar>ボタンを含むコントロールを持つフォームを想定しています。 ツールバーとツールバー ボタンの詳細については、「方法[: ツール バー コントロールにボタンを追加する](how-to-add-buttons-to-a-toolbar-control.md)」を参照してください。  
  
    ```vb  
    ' The following code assumes the existence of a toolbar control  
    ' with at least one toolbar button.  
    Private Sub RichTextBox1_SelectionChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles RichTextBox1.SelectionChanged  
       If RichTextBox1.SelectionBullet = True Then  
          ' Bullet button on toolbar should appear pressed  
          ToolBarButton1.Pushed = True  
       Else  
           ' Bullet button on toolbar should appear unpressed  
           ToolBarButton1.Pushed = False  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private void richTextBox1_SelectionChanged(object sender,  
    System.EventArgs e)  
    {  
       if (richTextBox1.SelectionBullet == true)
       {  
          // Bullet button on toolbar should appear pressed  
          toolBarButton1.Pushed = true;  
       }  
       else
       {  
          // Bullet button on toolbar should appear unpressed  
          toolBarButton1.Pushed = false;  
       }  
    }  
    ```  
  
    ```cpp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private:  
       System::Void richTextBox1_SelectionChanged(  
          System::Object ^  sender, System::EventArgs ^  e)  
       {  
          if (richTextBox1->SelectionBullet == true)  
          {  
             // Bullet button on toolbar should appear pressed  
             toolBarButton1->Pushed = true;  
          }  
          else  
          {  
             // Bullet button on toolbar should appear unpressed  
             toolBarButton1->Pushed = false;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.RichTextBox.SelectionChanged>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox コントロール](richtextbox-control-windows-forms.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
