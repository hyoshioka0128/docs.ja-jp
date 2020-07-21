---
title: CheckBox のクリックに応答する
description: チェックボックスの状態に応じて、何らかのアクションを実行するように Windows フォームアプリケーションをプログラミングする方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Click event [Windows Forms], CheckBox control
- CheckBox control [Windows Forms], Click events
- events [Windows Forms], Click events
- double-clicks
- check boxes [Windows Forms], responding to events
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
ms.openlocfilehash: 58944bc421f990343b6c58484aaab3d79c8bda5e
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174498"
---
# <a name="how-to-respond-to-windows-forms-checkbox-clicks"></a>方法 : Windows フォーム CheckBox のクリックに応答する
ユーザーが Windows フォームコントロールをクリックするたび <xref:System.Windows.Forms.CheckBox> に、 <xref:System.Windows.Forms.Control.Click> イベントが発生します。 チェックボックスの状態に応じて、何らかのアクションを実行するようにアプリケーションをプログラミングできます。  
  
### <a name="to-respond-to-checkbox-clicks"></a>チェックボックスのクリックに応答するには  
  
1. イベントハンドラーで、プロパティを使用して <xref:System.Windows.Forms.Control.Click> <xref:System.Windows.Forms.CheckBox.Checked%2A> コントロールの状態を確認し、必要な操作を実行します。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    > ユーザーがコントロールをダブルクリックしようとすると <xref:System.Windows.Forms.CheckBox> 、各クリックは個別に処理されます。つまり、 <xref:System.Windows.Forms.CheckBox> コントロールはダブルクリックイベントをサポートしていません。  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.CheckBox.AutoCheck%2A>プロパティが `true` (既定値) の場合、が <xref:System.Windows.Forms.CheckBox> クリックされると、が自動的に選択またはクリアされます。 それ以外の場合は、 <xref:System.Windows.Forms.CheckBox.Checked%2A> イベントが発生したときにプロパティを手動で設定する必要があり <xref:System.Windows.Forms.Control.Click> ます。  
  
     また、コントロールを使用して、一連 <xref:System.Windows.Forms.CheckBox> のアクションを決定することもできます。  
  
### <a name="to-determine-a-course-of-action-when-a-check-box-is-clicked"></a>チェックボックスがクリックされたときの動作を確認するには  
  
1. Case ステートメントを使用してプロパティの値を照会し、一連の <xref:System.Windows.Forms.CheckBox.CheckState%2A> アクションを決定します。 プロパティがに設定されている場合、プロパティは、 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> `true` チェックする <xref:System.Windows.Forms.CheckBox.CheckState%2A> ボックスを表す3つの値、チェックをオフにするボックス、またはオプションが使用できないことを示すために淡色表示された状態でボックスが表示される3番目の中間状態を返すことができます。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.CheckBox.ThreeState%2A>プロパティがに設定されている場合、 `true` プロパティは <xref:System.Windows.Forms.CheckBox.Checked%2A> `true` との両方に対してを返し <xref:System.Windows.Forms.CheckState.Checked> <xref:System.Windows.Forms.CheckState.Indeterminate> ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.CheckBox>
- [CheckBox コントロールの概要](checkbox-control-overview-windows-forms.md)
- [方法 : Windows フォームの CheckBox コントロールでオプションを設定する](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [CheckBox コントロール](checkbox-control-windows-forms.md)
