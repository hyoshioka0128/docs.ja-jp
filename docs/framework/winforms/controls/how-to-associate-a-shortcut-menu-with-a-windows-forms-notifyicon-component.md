---
title: ショートカット メニューを NotifyIcon コンポーネントに関連付ける
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- context menus [Windows Forms], for background processes
- NotifyIcon component [Windows Forms], associating shortcut menus
- shortcut menus [Windows Forms], for background processes
ms.assetid: d68f3926-08d3-4f7d-949f-1981b29cf188
ms.openlocfilehash: 15a4a06726de348745e5eef03217d693db496a42
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182263"
---
# <a name="how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component"></a>方法 : ショートカット メニューを Windows フォーム NotifyIcon コンポーネントに関連付ける
> [!NOTE]
> 以前<xref:System.Windows.Forms.MenuStrip>の<xref:System.Windows.Forms.ContextMenuStrip>バージョンの<xref:System.Windows.Forms.MainMenu>コントロールと<xref:System.Windows.Forms.ContextMenu>コントロールに機能を置き換えて<xref:System.Windows.Forms.MainMenu>追加<xref:System.Windows.Forms.ContextMenu>しますが、後方互換性と将来の使用の両方を選択した場合は保持されます。  
  
 コンポーネント<xref:System.Windows.Forms.NotifyIcon>は、タスク バーの状態通知領域にアイコンを表示します。 通常、アプリケーションでは、このアイコンを右クリックして、それが表すアプリケーションにコマンドを送信できます。 <xref:System.Windows.Forms.ContextMenu>コンポーネントを<xref:System.Windows.Forms.NotifyIcon>コンポーネントに関連付けることで、この機能をアプリケーションに追加できます。  
  
> [!NOTE]
> タスク バーに<xref:System.Windows.Forms.NotifyIcon>コンポーネントのインスタンスを表示しながら起動時にアプリケーションを最小化する場合は、メイン フォームの<xref:System.Windows.Forms.Form.WindowState%2A>プロパティを に<xref:System.Windows.Forms.FormWindowState.Minimized>設定し、<xref:System.Windows.Forms.NotifyIcon>コンポーネントの<xref:System.Windows.Forms.NotifyIcon.Visible%2A>プロパティが に`true`設定されていることを確認します。  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-at-design-time"></a>デザイン時にショートカット メニューを NotifyIcon コンポーネントに関連付けるには  
  
1. フォームに<xref:System.Windows.Forms.NotifyIcon>コンポーネントを追加し、 プロパティや プロパティなどの重要なプロパティ<xref:System.Windows.Forms.NotifyIcon.Icon%2A>を<xref:System.Windows.Forms.NotifyIcon.Visible%2A>設定します。  
  
     詳細については、「[方法 : Windows フォームの NotifyIcon コンポーネントを使用してタスク バーにアプリケーション アイコンを追加](app-icons-to-the-taskbar-with-wf-notifyicon.md)する 」を参照してください。  
  
2. コンポーネントを<xref:System.Windows.Forms.ContextMenu>Windows フォームに追加します。  
  
     実行時に使用できるようにするコマンドを表すメニュー項目をショートカット メニューに追加します。 また、アクセス キーなどのメニュー項目にメニューの機能強化を追加する場合にも適しています。  
  
3. 追加した<xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A>ショートカット メニュー<xref:System.Windows.Forms.NotifyIcon>にコンポーネントのプロパティを設定します。  
  
     このプロパティを設定すると、タスク バーのアイコンをクリックするとショートカット メニューが表示されます。  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-programmatically"></a>プログラムでショートカット メニューを NotifyIcon コンポーネントに関連付けるには  
  
1. <xref:System.Windows.Forms.NotifyIcon>アプリケーションに必要な<xref:System.Windows.Forms.ContextMenu>プロパティ設定 (<xref:System.Windows.Forms.NotifyIcon.Icon%2A><xref:System.Windows.Forms.NotifyIcon.Visible%2A><xref:System.Windows.Forms.NotifyIcon>およびコンポーネントのプロパティ、コンポーネントのメニュー項目) を使用して、クラスとクラスのインスタンスを<xref:System.Windows.Forms.ContextMenu>作成します。  
  
2. 追加した<xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A>ショートカット メニュー<xref:System.Windows.Forms.NotifyIcon>にコンポーネントのプロパティを設定します。  
  
     このプロパティを設定すると、タスク バーのアイコンをクリックするとショートカット メニューが表示されます。  
  
    > [!NOTE]
    > 基本的なメニュー構造を作成するコード例を次に示します。 開発中のアプリケーションに合わせてメニューの選択肢をカスタマイズする必要があります。 また、これらのメニュー項目の<xref:System.Windows.Forms.MenuItem.Click>イベントを処理するコードを記述する必要があります。  
  
    ```vb  
    Public ContextMenu1 As New ContextMenu  
    Public NotifyIcon1 As New NotifyIcon  
  
    Public Sub CreateIconMenuStructure()  
       ' Add menu items to shortcut menu.  
       ContextMenu1.MenuItems.Add("&Open Application")  
       ContextMenu1.MenuItems.Add("S&uspend Application")  
       ContextMenu1.MenuItems.Add("E&xit")  
  
       ' Set properties of NotifyIcon component.  
       NotifyIcon1.Icon = New System.Drawing.Icon _
          (System.Environment.GetFolderPath _
          (System.Environment.SpecialFolder.Personal)  _
          & "\Icon.ico")  
       NotifyIcon1.Text = "Right-click me!"  
       NotifyIcon1.Visible = True  
       NotifyIcon1.ContextMenu = ContextMenu1  
    End Sub  
    ```  
  
```csharp  
public NotifyIcon notifyIcon1 = new NotifyIcon();  
public ContextMenu contextMenu1 = new ContextMenu();  
  
public void createIconMenuStructure()  
{  
   // Add menu items to shortcut menu.  
   contextMenu1.MenuItems.Add("&Open Application");  
   contextMenu1.MenuItems.Add("S&uspend Application");  
   contextMenu1.MenuItems.Add("E&xit");  
  
   // Set properties of NotifyIcon component.  
   notifyIcon1.Icon = new System.Drawing.Icon  
      (System.Environment.GetFolderPath  
      (System.Environment.SpecialFolder.Personal)  
      + @"\Icon.ico");  
   notifyIcon1.Visible = true;  
   notifyIcon1.Text = "Right-click me!";  
   notifyIcon1.Visible = true;  
   notifyIcon1.ContextMenu = contextMenu1;  
}  
```  
  
```cpp  
public:  
   System::Windows::Forms::NotifyIcon ^ notifyIcon1;  
   System::Windows::Forms::ContextMenu ^ contextMenu1;  
  
   void createIconMenuStructure()  
   {  
      // Add menu items to shortcut menu.  
      contextMenu1->MenuItems->Add("&Open Application");  
      contextMenu1->MenuItems->Add("S&uspend Application");  
      contextMenu1->MenuItems->Add("E&xit");  
  
      // Set properties of NotifyIcon component.  
      notifyIcon1->Icon = gcnew System::Drawing::Icon  
          (String::Concat(System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::Personal),  
          "\\Icon.ico"));  
      notifyIcon1->Text = "Right-click me!";  
      notifyIcon1->Visible = true;  
      notifyIcon1->ContextMenu = contextMenu1;  
   }  
```  
  
> [!NOTE]
> フォームのコンストラクター`notifyIcon1`に`contextMenu1,`次のステートメントを含めることで、初期化し、実行できる操作を行う必要があります。  
  
```cpp  
notifyIcon1 = gcnew System::Windows::Forms::NotifyIcon();  
contextMenu1 = gcnew System::Windows::Forms::ContextMenu();  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [方法 : Windows フォームの NotifyIcon コンポーネントによってタスクバーにアプリケーション アイコンを追加する](app-icons-to-the-taskbar-with-wf-notifyicon.md)
- [NotifyIcon コンポーネント](notifyicon-component-windows-forms.md)
- [NotifyIcon コンポーネントの概要](notifyicon-component-overview-windows-forms.md)
