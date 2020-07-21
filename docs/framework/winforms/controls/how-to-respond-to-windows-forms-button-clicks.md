---
title: Button のクリックに応答する
description: Windows フォームボタンのクリックに応答する方法について説明します。 Windows フォームボタンコントロールの最も基本的な用途は、ボタンがクリックされたときにコードを実行することです。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- buttons [Windows Forms], responding to Click events
- events [Windows Forms], Click events
- Click event [Windows Forms], Button control
- MouseDown event
- Button control [Windows Forms], click response
- double-clicks
- examples [Windows Forms], controls
- Click event [Windows Forms], responding to
ms.assetid: 7a4951bd-369c-4662-b246-28ad83eda484
ms.openlocfilehash: 5c458d56dbd6f1cab8e88bdbb86ede958367e5c4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619729"
---
# <a name="how-to-respond-to-windows-forms-button-clicks"></a>方法 : Windows フォームのボタンのクリックに応答する
Windows フォームコントロールの最も基本的な用途 <xref:System.Windows.Forms.Button> は、ボタンがクリックされたときにコードを実行することです。  
  
 コントロールをクリックすると <xref:System.Windows.Forms.Button> 、、、イベントなどの他のイベントも多数生成さ <xref:System.Windows.Forms.Control.MouseEnter> <xref:System.Windows.Forms.Control.MouseDown> <xref:System.Windows.Forms.Control.MouseUp> れます。 これらの関連イベントにイベントハンドラーをアタッチする場合は、それらのアクションが競合していないことを確認してください。 たとえば、ボタンをクリックすると、ユーザーがテキストボックスに入力した情報がクリアされた場合、ボタンの上にマウスポインターを置くと、その時点で存在しない情報を示すツールヒントが表示されません。  
  
 ユーザーがコントロールをダブルクリックしようとすると <xref:System.Windows.Forms.Button> 、各クリックは個別に処理されます。つまり、コントロールはダブルクリックイベントをサポートしていません。  
  
### <a name="to-respond-to-a-button-click"></a>ボタンのクリックに応答するには  
  
- ボタンの [実行するコードを記述してください] をクリックし `Click` <xref:System.EventHandler> ます。 `Button1_Click`コントロールにバインドされている必要があります。 詳細については、「[方法: Windows フォームの実行時にイベントハンドラーを作成](../how-to-create-event-handlers-at-run-time-for-windows-forms.md)する」を参照してください。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       MessageBox.Show("Button1 was clicked")  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       MessageBox.Show("button1 was clicked");  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          MessageBox::Show("button1 was clicked");  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- [Button コントロールの概要](button-control-overview-windows-forms.md)
- [Windows フォームの Button コントロールを選択する方法](ways-to-select-a-windows-forms-button-control.md)
- [Button コントロール](button-control-windows-forms.md)
