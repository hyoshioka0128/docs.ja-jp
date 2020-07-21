---
title: '方法: ツール バー ボタンのメニュー イベントをトリガーする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], toolbars
- ToolBar control [Windows Forms], click event handlers
- ToolBar control [Windows Forms], coding button click events
- toolbars [Windows Forms], click event handlers
ms.assetid: 98374f70-993d-4ca4-89fb-48fea6ce5b45
ms.openlocfilehash: 99db077b41a59fe9263f7283b58b8c31959c7c79
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182078"
---
# <a name="how-to-trigger-menu-events-for-toolbar-buttons"></a>方法: ツール バー ボタンのメニュー イベントをトリガーする
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip> コントロールは、<xref:System.Windows.Forms.ToolBar> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.ToolBar> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。  
  
 Windows フォームにツール<xref:System.Windows.Forms.ToolBar>バー ボタンを備えたコントロールがある場合は、ユーザーがクリックしたボタンを確認する必要があります。  
  
 コントロールの<xref:System.Windows.Forms.ToolBar.ButtonClick>イベントで、クラスのプロパティを<xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A><xref:System.Windows.Forms.ToolBarButtonClickEventArgs>評価できます。 <xref:System.Windows.Forms.ToolBar> 次の例では、クリックされたボタンを示すメッセージ ボックスが表示されます。 詳細については、<xref:System.Windows.Forms.MessageBox> を参照してください。  
  
 次の例では、<xref:System.Windows.Forms.ToolBar>コントロールが Windows フォームに追加されていることを前提としています。  
  
### <a name="to-handle-the-click-event-on-a-toolbar"></a>ツール バーの Click イベントを処理するには  
  
1. プロシージャで、コントロールにツール バー<xref:System.Windows.Forms.ToolBar>ボタンを追加します。  
  
    ```vb  
    Public Sub ToolBarConfig()  
    ' Instantiate the toolbar buttons, set their Text properties  
    ' and add them to the ToolBar control.  
       ToolBar1.Buttons.Add(New ToolBarButton("One"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Two"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Three"))  
    ' Add the event handler delegate.  
       AddHandler ToolBar1.ButtonClick, AddressOf Me.ToolBar1_ButtonClick  
    End Sub  
    ```  
  
    ```csharp  
    public void ToolBarConfig()
    {  
       toolBar1.Buttons.Add(new ToolBarButton("One"));  
       toolBar1.Buttons.Add(new ToolBarButton("Two"));  
       toolBar1.Buttons.Add(new ToolBarButton("Three"));  
  
       toolBar1.ButtonClick +=
          new ToolBarButtonClickEventHandler(this.toolBar1_ButtonClick);  
    }  
    ```  
  
    ```cpp  
    public:  
       void ToolBarConfig()  
       {  
          toolBar1->Buttons->Add(gcnew ToolBarButton("One"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Two"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Three"));  
  
          toolBar1->ButtonClick +=
             gcnew ToolBarButtonClickEventHandler(this,  
             &Form1::toolBar1_ButtonClick);  
       }  
    ```  
  
2. コントロールのイベント ハンドラーを<xref:System.Windows.Forms.ToolBar>追加<xref:System.Windows.Forms.ToolBar.ButtonClick>します。 ケース切り替えステートメントと<xref:System.Windows.Forms.ToolBarButtonClickEventArgs>クラスを使用して、クリックされたツールバー ボタンを決定します。 この結果に基づいて、適切なメッセージ ボックスが表示されます。  
  
    > [!NOTE]
    > この例では、メッセージ ボックスは、プレースホルダーとして単独で使用されています。 ツール バーのボタンがクリックされたときに実行するコードは、自由に追加できます。  
  
    ```vb  
    Protected Sub ToolBar1_ButtonClick(ByVal sender As Object, _  
    ByVal e As ToolBarButtonClickEventArgs)  
    ' Evaluate the Button property of the ToolBarButtonClickEventArgs  
    ' to determine which button was clicked.  
       Select Case ToolBar1.Buttons.IndexOf(e.Button)  
         Case 0  
           MessageBox.Show("First toolbar button clicked")  
         Case 1  
           MessageBox.Show("Second toolbar button clicked")  
         Case 2  
           MessageBox.Show("Third toolbar button clicked")  
       End Select  
    End Sub  
    ```  
  
    ```csharp  
    protected void toolBar1_ButtonClick(object sender,  
    ToolBarButtonClickEventArgs e)  
    {  
       // Evaluate the Button property of the ToolBarButtonClickEventArgs  
       // to determine which button was clicked.  
       switch (toolBar1.Buttons.IndexOf(e.Button))  
       {  
          case 0 :  
             MessageBox.Show("First toolbar button clicked");  
             break;  
          case 1 :  
             MessageBox.Show("Second toolbar button clicked");  
             break;  
          case 2 :  
             MessageBox.Show("Third toolbar button clicked");  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    protected:  
       void toolBar1_ButtonClick(System::Object ^ sender,  
          ToolBarButtonClickEventArgs ^ e)  
       {  
         // Evaluate the Button property of the ToolBarButtonClickEventArgs  
         // to determine which button was clicked.  
          switch (toolBar1->Buttons->IndexOf(e->Button))  
          {  
             case 0 :  
                MessageBox::Show("First toolbar button clicked");  
                break;  
             case 1 :  
                MessageBox::Show("Second toolbar button clicked");  
                break;  
             case 2 :  
                MessageBox::Show("Third toolbar button clicked");  
                break;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ToolBar>
- [方法: ToolBar コントロールにボタンを追加する](how-to-add-buttons-to-a-toolbar-control.md)
- [方法: ToolBar ボタンのアイコンを定義する](how-to-define-an-icon-for-a-toolbar-button.md)
- [ToolBar コントロール](toolbar-control-windows-forms.md)
