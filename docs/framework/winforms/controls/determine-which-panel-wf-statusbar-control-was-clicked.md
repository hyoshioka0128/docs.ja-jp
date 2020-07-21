---
title: StatusBar コントロールでクリックされたパネルを確認する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- status bars [Windows Forms], determining panel clicked
- panels [Windows Forms], determining clicked
- StatusBar control [Windows Forms], coding panel click events
- StatusBar control [Windows Forms], determining panel clicked
- PanelClick event [Windows Forms], determining panel clicked
- Panel control [Windows Forms], determining click
ms.assetid: d14c6092-04b2-4a07-8ddf-0dd11277ff5f
ms.openlocfilehash: eb3b10d515ba5b62236594e063ca7f060b34b73e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182364"
---
# <a name="how-to-determine-which-panel-in-the-windows-forms-statusbar-control-was-clicked"></a>方法 : Windows フォームの StatusBar コントロールでクリックされたパネルを確認する
> [!IMPORTANT]
> コントロール<xref:System.Windows.Forms.StatusStrip>と<xref:System.Windows.Forms.ToolStripStatusLabel>コントロールは、 コントロールと<xref:System.Windows.Forms.StatusBar><xref:System.Windows.Forms.StatusBarPanel>コントロールに機能を置き換え、追加します。ただし、下位<xref:System.Windows.Forms.StatusBar>互換性<xref:System.Windows.Forms.StatusBarPanel>と将来の使用の両方を目的として、コントロールと コントロールは保持されます。  
  
 ユーザーのクリックに応答するように[StatusBar コントロール](statusbar-control-windows-forms.md)をプログラムするには、イベント内で case<xref:System.Windows.Forms.StatusBar.PanelClick>ステートメントを使用します。 イベントには、クリックされた<xref:System.Windows.Forms.StatusBarPanel>. この参照を使用して、クリックされたパネルのインデックスを判別し、それに応じてプログラムすることができます。  
  
> [!NOTE]
> コントロールの<xref:System.Windows.Forms.StatusBar><xref:System.Windows.Forms.StatusBar.ShowPanels%2A>プロパティが`true`に設定されていることを確認します。  
  
### <a name="to-determine-which-panel-was-clicked"></a>クリックされたパネルを確認するには  
  
1. <xref:System.Windows.Forms.StatusBar.PanelClick>イベント ハンドラーで`Select Case`、(Visual Basic の)`switch case`または (Visual C# または Visual C++) ステートメントを使用して、イベント引数でクリックされたパネルのインデックスを調べて、クリックされたパネルを特定します。  
  
     次のコード例では、<xref:System.Windows.Forms.StatusBar>フォーム上、コントロール、および 2 つの`StatusBar1`<xref:System.Windows.Forms.StatusBarPanel>オブジェクト、`StatusBarPanel1`および`StatusBarPanel2`が存在している必要があります。  
  
    ```vb  
    Private Sub StatusBar1_PanelClick(ByVal sender As System.Object, ByVal e As System.Windows.Forms.StatusBarPanelClickEventArgs) Handles StatusBar1.PanelClick  
       Select Case StatusBar1.Panels.IndexOf(e.StatusBarPanel)  
         Case 0  
           MessageBox.Show("You have clicked Panel One.")  
         Case 1  
           MessageBox.Show("You have clicked Panel Two.")  
       End Select  
    End Sub  
    ```  
  
    ```csharp  
    private void statusBar1_PanelClick(object sender,
    System.Windows.Forms.StatusBarPanelClickEventArgs e)  
    {  
       switch (statusBar1.Panels.IndexOf(e.StatusBarPanel))  
       {  
          case 0 :  
             MessageBox.Show("You have clicked Panel One.");  
             break;  
          case 1 :  
             MessageBox.Show("You have clicked Panel Two.");  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void statusBar1_PanelClick(System::Object ^  sender,  
          System::Windows::Forms::StatusBarPanelClickEventArgs ^  e)  
       {  
          switch (statusBar1->Panels->IndexOf(e->StatusBarPanel))  
          {  
             case 0 :  
                MessageBox::Show("You have clicked Panel One.");  
                break;  
             case 1 :  
                MessageBox::Show("You have clicked Panel Two.");  
                break;  
          }  
       }  
    ```  
  
     (ビジュアル C#、ビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.statusBar1.PanelClick += new
       System.Windows.Forms.StatusBarPanelClickEventHandler
       (this.statusBar1_PanelClick);  
    ```  
  
    ```cpp  
    this->statusBar1->PanelClick += gcnew  
       System::Windows::Forms::StatusBarPanelClickEventHandler  
       (this, &Form1::statusBar1_PanelClick);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [方法 : ステータス バー パネルのサイズを設定する](how-to-set-the-size-of-status-bar-panels.md)
- [チュートリアル : ステータス バー情報の実行時更新](walkthrough-updating-status-bar-information-at-run-time.md)
- [StatusBar コントロールの概要](statusbar-control-overview-windows-forms.md)
