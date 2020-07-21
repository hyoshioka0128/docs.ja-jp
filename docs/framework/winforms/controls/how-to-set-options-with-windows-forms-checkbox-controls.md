---
title: CheckBox コントロールでオプションを設定する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- checked
helpviewer_keywords:
- CheckBox control [Windows Forms], checked state
- check boxes [Windows Forms], using to set options
- CheckBox control [Windows Forms], using to set options
ms.assetid: 2ac70498-7e3e-4e07-8901-ccabaeb5fd3e
ms.openlocfilehash: 00b467836d8e60aeee51a010a6384abf7dd73c56
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141849"
---
# <a name="how-to-set-options-with-windows-forms-checkbox-controls"></a>方法 : Windows フォームの CheckBox コントロールでオプションを設定する
Windows フォーム<xref:System.Windows.Forms.CheckBox>コントロールは、ユーザーに True/False または Yes/No オプションを提供するために使用されます。 コントロールを選択すると、チェック マークが表示されます。  
  
### <a name="to-set-options-with-checkbox-controls"></a>チェック ボックス コントロールでオプションを設定するには  
  
1. プロパティの値を<xref:System.Windows.Forms.CheckBox.Checked%2A>調べて状態を確認し、その値を使用してオプションを設定します。  
  
     次のコード サンプルでは、コントロール<xref:System.Windows.Forms.CheckBox>の<xref:System.Windows.Forms.CheckBox.CheckedChanged>イベントが発生したときに、チェック ボックスがオン<xref:System.Windows.Forms.Control.AllowDrop%2A>`false`になっている場合にフォームのプロパティが設定されます。 これは、ユーザーの操作を制限する場合に便利です。  
  
    ```vb  
    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged  
       ' Determine the CheckState of the check box.  
       If CheckBox1.CheckState = CheckState.Checked Then  
          ' If checked, do not allow items to be dragged onto the form.  
          Me.AllowDrop = False  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_CheckedChanged(object sender, System.EventArgs e)  
    {  
       // Determine the CheckState of the check box.  
       if (checkBox1.CheckState == CheckState.Checked)
       {  
          // If checked, do not allow items to be dragged onto the form.  
          this.AllowDrop = false;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Determine the CheckState of the check box.  
          if (checkBox1->CheckState == CheckState::Checked)
          {  
             // If checked, do not allow items to be dragged onto the form.  
             this->AllowDrop = false;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.CheckBox>
- [CheckBox コントロールの概要](checkbox-control-overview-windows-forms.md)
- [方法 : Windows フォーム CheckBox のクリックに応答する](how-to-respond-to-windows-forms-checkbox-clicks.md)
- [チェック ボックス コントロール](checkbox-control-windows-forms.md)
