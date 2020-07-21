---
title: '方法 : StatusBar コントロールにパネルを追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- panels [Windows Forms], status bars
- status bars [Windows Forms], adding panels
- StatusBar control [Windows Forms], adding panels
ms.assetid: 835e3902-288c-4c38-9d69-0696d8695009
ms.openlocfilehash: 386c8cae425c458ddf4c446a454ae4213761e651
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142200"
---
# <a name="how-to-add-panels-to-a-statusbar-control"></a>方法 : StatusBar コントロールにパネルを追加する
> [!IMPORTANT]
> コントロール<xref:System.Windows.Forms.StatusStrip>と<xref:System.Windows.Forms.ToolStripStatusLabel>コントロールは、 コントロールと<xref:System.Windows.Forms.StatusBar><xref:System.Windows.Forms.StatusBarPanel>コントロールに機能を置き換え、追加します。ただし、下位<xref:System.Windows.Forms.StatusBar>互換性<xref:System.Windows.Forms.StatusBarPanel>と将来の使用の両方を目的として、コントロールと コントロールは保持されます。  
  
 [StatusBar コントロール](statusbar-control-windows-forms.md)内のプログラム可能な領域は、クラスのインスタンスで<xref:System.Windows.Forms.StatusBarPanel>構成されます。 これらは、クラスに追加して追加されます<xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection>。  
  
### <a name="to-add-panels-to-a-status-bar"></a>ステータス バーにパネルを追加するには  
  
1. プロシージャで、ステータス バー パネルを に追加して作成します<xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection>。 プロパティを通過するインデックスを使用して、個々のパネルのプロパティ<xref:System.Windows.Forms.StatusBar.Panels%2A>設定を指定します。  
  
     次のコード例では、アイコンの場所に設定されているパスは**マイ ドキュメント**フォルダーです。 この場所は、Windows オペレーティング システムを実行しているほとんどのコンピュータにこのフォルダが含まれると仮定できるため、使用されます。 この場所を選択すると、最小限のシステム アクセス レベルを持つユーザーがアプリケーションを安全に実行できるようになります。 次の例では、コントロールが既<xref:System.Windows.Forms.StatusBar>に追加されているフォームが必要です。  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection>は 0 から始まるコレクションなので、コードはこれに従って進む必要があります。  
  
    ```vb  
    Public Sub CreateStatusBarPanels()  
    ' Create panels and set text property.  
       StatusBar1.Panels.Add("One")  
       StatusBar1.Panels.Add("Two")  
       StatusBar1.Panels.Add("Three")  
    ' Set properties of StatusBar panels.  
    ' Set AutoSize property of panels.  
       StatusBar1.Panels(0).AutoSize = StatusBarPanelAutoSize.Spring  
       StatusBar1.Panels(1).AutoSize = StatusBarPanelAutoSize.Contents  
       StatusBar1.Panels(2).AutoSize = StatusBarPanelAutoSize.Contents  
    ' Set BorderStyle property of panels.  
       StatusBar1.Panels(0).BorderStyle = StatusBarPanelBorderStyle.Raised  
       StatusBar1.Panels(1).BorderStyle = StatusBarPanelBorderStyle.Sunken  
       StatusBar1.Panels(2).BorderStyle = StatusBarPanelBorderStyle.Raised  
    ' Set Icon property of third panel. You should replace the bolded  
    ' icon in the sample below with an icon of your own choosing.  
       StatusBar1.Panels(2).Icon = New _
       System.Drawing.Icon(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Icon.ico")  
       StatusBar1.ShowPanels = True  
    End Sub  
    ```  
  
    ```csharp  
    public void CreateStatusBarPanels()  
    {  
       // Create panels and set text property.  
       statusBar1.Panels.Add("One");  
       statusBar1.Panels.Add("Two");  
       statusBar1.Panels.Add("Three");  
       // Set properties of StatusBar panels.  
       // Set AutoSize property of panels.  
       statusBar1.Panels[0].AutoSize = StatusBarPanelAutoSize.Spring;  
       statusBar1.Panels[1].AutoSize = StatusBarPanelAutoSize.Contents;  
       statusBar1.Panels[2].AutoSize = StatusBarPanelAutoSize.Contents;  
       // Set BorderStyle property of panels.  
       statusBar1.Panels[0].BorderStyle =  
          StatusBarPanelBorderStyle.Raised;  
       statusBar1.Panels[1].BorderStyle = StatusBarPanelBorderStyle.Sunken;  
       statusBar1.Panels[2].BorderStyle = StatusBarPanelBorderStyle.Raised;  
       // Set Icon property of third panel. You should replace the bolded  
       // icon in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       statusBar1.Panels[2].Icon =
          new System.Drawing.Icon (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\Icon.ico");  
       statusBar1.ShowPanels = true;  
    }  
    ```  
  
    ```cpp  
    public:  
       void CreateStatusBarPanels()  
       {  
          // Create panels and set text property.  
          statusBar1->Panels->Add("One");  
          statusBar1->Panels->Add("Two");  
          statusBar1->Panels->Add("Three");  
          // Set properties of StatusBar panels.  
          // Set AutoSize property of panels.  
          statusBar1->Panels[0]->AutoSize =  
             StatusBarPanelAutoSize::Spring;  
          statusBar1->Panels[1]->AutoSize =  
             StatusBarPanelAutoSize::Contents;  
          statusBar1->Panels[2]->AutoSize =  
             StatusBarPanelAutoSize::Contents;  
          // Set BorderStyle property of panels.  
          statusBar1->Panels[0]->BorderStyle =  
             StatusBarPanelBorderStyle::Raised;  
          statusBar1->Panels[1]->BorderStyle =  
             StatusBarPanelBorderStyle::Sunken;  
          statusBar1->Panels[2]->BorderStyle =  
             StatusBarPanelBorderStyle::Raised;  
          // Set Icon property of third panel.  
          // You should replace the bolded image
          // in the sample below with an icon of your own choosing.  
          statusBar1->Panels[2]->Icon =  
             gcnew System::Drawing::Icon(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Icon.ico"));  
          statusBar1->ShowPanels = true;  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [[コレクション エディター] ダイアログ ボックス](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/xc4yyekt(v=vs.100))
- [方法 : ステータス バー パネルのサイズを設定する](how-to-set-the-size-of-status-bar-panels.md)
- [チュートリアル : ステータス バー情報の実行時更新](walkthrough-updating-status-bar-information-at-run-time.md)
- [方法 : Windows フォームの StatusBar コントロールでクリックされたパネルを確認する](determine-which-panel-wf-statusbar-control-was-clicked.md)
- [StatusBar コントロールの概要](statusbar-control-overview-windows-forms.md)
