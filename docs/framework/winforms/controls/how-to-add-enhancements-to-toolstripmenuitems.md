---
title: '方法 : ToolStripMenuItems に拡張機能を追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- commands [Windows Forms], grouping on menus
- check marks [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], displaying access keys
- menus [Windows Forms], grouping commands
- menu items [Windows Forms], displaying shortcut keys
- ToolStripMenuItems
- separators [Windows Forms], displaying on menus
- menu items [Windows Forms], showing separators
- menu items [Windows Forms], adding check marks
- ToolStripMenuItems [Windows Forms], adding check marks
- menu items [Windows Forms], adding images
- ToolStripSeparators [Windows Forms], displaying on MenuStrips
- menu items [Windows Forms], displaying access keys
- ToolStripMenuItems [Windows Forms], displaying shortcut keys
- ToolStripMenuItems [Windows Forms], adding images
- keyboard shortcuts [Windows Forms], displaying on menus
- images [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], showing separator bars
ms.assetid: aa5f19bb-b545-4378-bfa6-36ba592f0d7c
ms.openlocfilehash: 61a79b9bbe101d7bf694240bdffdecee5187adf2
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182321"
---
# <a name="how-to-add-enhancements-to-toolstripmenuitems"></a>方法 : ToolStripMenuItems に拡張機能を追加する
以下の方法で、コントロールと<xref:System.Windows.Forms.MenuStrip><xref:System.Windows.Forms.ContextMenuStrip>コントロールの操作性を向上させることができます。  
  
- ワープロ アプリケーションの余白にルーラーを表示するかどうか、またはウィンドウ**メニューなど**、ファイルの一覧のどのファイルを表示するかを示すなど、機能をオンまたはオフにするかどうかを指定するチェック マークを追加します。  
  
- メニュー コマンドを視覚的に表すイメージを追加します。  
  
- ショートカット キーを表示して、コマンドを実行するためのマウスの代わりにキーボードを提供します。 たとえば、Ctrl キーを押しながら C キーを押すと **、コピー**コマンドが実行されます。  
  
- アクセス キーを表示して、メニュー ナビゲーション用のマウスに代わるキーボードを提供します。 たとえば、Alt キーを押しながら F キーを押すと、[**ファイル]** メニューが選択されます。  
  
- 関連するコマンドをグループ化し、メニューを読みやすくする区切りバーを表示します。  
  
### <a name="to-display-a-check-mark-on-a-menu-command"></a>メニュー コマンドにチェック マークを表示するには  
  
- プロパティを<xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A>に`true`設定します。  
  
     このプロパティもに<xref:System.Windows.Forms.ToolStripMenuItem.CheckState%2A>設定`true`されます。 この手順は、メニュー コマンドが選択されているかどうかに関係なく、既定でオンに表示される場合にのみ使用します。  
  
### <a name="to-display-a-check-mark-that-changes-state-with-each-click"></a>クリックするたびに状態が変化するチェック マークを表示するには  
  
- メニュー コマンドの<xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A>プロパティを に`true`設定します。  
  
### <a name="to-add-an-image-to-a-menu-command"></a>メニュー コマンドにイメージを追加するには  
  
- メニュー コマンドの<xref:System.Windows.Forms.ToolStripItem.Image%2A>プロパティをイメージの名前に設定します。 このメニュー<xref:System.Windows.Forms.ToolStripItemDisplayStyle>コマンドのプロパティが or<xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text><xref:System.Windows.Forms.ToolStripItemDisplayStyle.None>に設定されている場合、イメージを表示できません。  
  
> [!NOTE]
> 選択した場合、画像の余白にもチェック マークを表示できます。 また、イメージの<xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A>プロパティを に`true`設定すると、実行時に画像の周囲にハッチング境界が表示されます。  
  
### <a name="to-display-a-shortcut-key-for-a-menu-command"></a>メニュー コマンドのショートカット キーを表示するには  
  
- メニュー<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>コマンドのプロパティを、目的のキーボードの組み合わせ ([**開く**] メニュー コマンドの<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>Ctrl+ `true`O など) に設定し、プロパティを に設定します。  
  
### <a name="to-display-custom-shortcut-keys-for-a-menu-command"></a>メニュー コマンドのカスタム ショートカット キーを表示するには  
  
- メニュー コマンドの<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A>プロパティを、Shift キーを押しながら Ctrl キーを押しながら O キーを押すのではなく、Ctrl キー<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>を押`true`しながら Shift キーを押しながら O キーを押すなどのキーボードの組み合わせを設定し、プロパティを に設定します。  
  
### <a name="to-display-an-access-key-for-a-menu-command"></a>メニュー コマンドのアクセス キーを表示するには  
  
- メニュー コマンドの<xref:System.Windows.Forms.ToolStripItem.Text%2A>プロパティを設定する場合は、アクセス キーとして下線を付ける文字の前にアンパサンド (&) を入力します。 たとえば、メニュー項目`&Open`の<xref:System.Windows.Forms.ToolStripItem.Text%2A>プロパティとして入力すると、メニュー コマンドは<u>O</u>ペンとして表示されます。
  
     このメニュー コマンドに移動するには、 Alt キーを押<xref:System.Windows.Forms.MenuStrip>して にフォーカスを移動し、メニュー名のアクセス キーを押します。 メニューが開き、アクセスキーを持つ項目が表示されたら、アクセスキーを押してメニューコマンドを選択するだけです。  
  
> [!NOTE]
> 同じメニュー システムで Alt + F を 2 回定義するなど、重複するアクセス キーを定義しないようにします。 重複アクセス キーの選択順序は保証できません。  
  
### <a name="to-display-a-separator-bar-between-menu-commands"></a>メニュー コマンドの間に区切り線を表示するには  
  
- <xref:System.Windows.Forms.MenuStrip>を定義し、そのアイテムに含める項目を定義したら<xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A>、<xref:System.Windows.Forms.ToolStripItemCollection.Add%2A>または メソッドを使用して<xref:System.Windows.Forms.ToolStripSeparator>、メニュー<xref:System.Windows.Forms.MenuStrip>コマンドとコントロールを目的の順序で に追加します。  
  
    ```vb  
    ' This code adds a top-level File menu to the MenuStrip.  
    Me.menuStrip1.Items.Add(New ToolStripMenuItem() _  
    {Me.fileToolStripMenuItem})  
  
    ' This code adds the New and Open menu commands, a separator bar,
    ' and the Save and Exit menu commands to the top-level File menu,
    ' in that order.  
    Me.fileToolStripMenuItem.DropDownItems.AddRange(New _  
    ToolStripMenuItem() {Me.newToolStripMenuItem, _  
    Me.openToolStripMenuItem, Me.toolStripSeparator1, _  
    Me.saveToolStripMenuItem, Me.exitToolStripMenuItem})  
    ```  
  
    ```csharp  
    // This code adds a top-level File menu to the MenuStrip.  
    this.menuStrip1.Items.Add(new ToolStripItem[]_  
    {this.fileToolStripMenuItem});  
  
    // This code adds the New and Open menu commands, a separator bar,
    // and the Save and Exit menu commands to the top-level File menu,
    // in that order.  
    this.fileToolStripMenuItem.DropDownItems.AddRange(new _  
    ToolStripItem[] {  
    this.newToolStripMenuItem,  
    this.openToolStripMenuItem,  
    this.toolStripSeparator1,  
    this.saveToolStripMenuItem,  
    this.exitToolStripMenuItem});  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip コントロールの概要](menustrip-control-overview-windows-forms.md)
