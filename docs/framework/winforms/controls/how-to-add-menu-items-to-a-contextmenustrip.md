---
title: '方法 : メニュー項目を ContextMenuStrip に追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ContextMenuStrips [Windows Forms], adding menu items
- shortcut menus [Windows Forms], adding items
- context menus [Windows Forms], adding menu items
ms.assetid: 1ec14776-3ea2-4752-bd22-4fae0fd19e1a
ms.openlocfilehash: 7e3480c5a56170ce94d5b5bde0208542c82e7702
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182313"
---
# <a name="how-to-add-menu-items-to-a-contextmenustrip"></a>方法 : メニュー項目を ContextMenuStrip に追加する
メニュー項目は 1 つだけ、または複数の項目を一度<xref:System.Windows.Forms.ContextMenuStrip>に追加できます。  
  
### <a name="to-add-a-single-menu-item-to-a-contextmenustrip"></a>単一のメニュー項目を追加するには、コンテキスト メニューストリップ  
  
- このメソッド<xref:System.Windows.Forms.ToolStripItemCollection.Add%2A>を使用して、 にメニュー項目<xref:System.Windows.Forms.ContextMenuStrip>を 1 つ追加します。  
  
    ```vb  
    Me.contextMenuStrip1.Items.Add(Me.toolStripMenuItem1)  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.Add(toolStripMenuItem1);  
    ```  
  
### <a name="to-add-several-menu-items-to-a-contextmenustrip"></a>複数のメニュー項目を追加するには、次の方法を実行します。  
  
- メソッドを<xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A>使用して、複数のメニュー項目を<xref:System.Windows.Forms.ContextMenuStrip>に追加します。  
  
    ```vb  
    Me.contextMenuStrip1.Items.AddRange(New _  
       System.Windows.Forms.ToolStripItem() {Me.toolStripMenuItem1, _  
          Me.toolStripMenuItem2})  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.AddRange(new
       System.Windows.Forms.ToolStripItem[] {  
          this.toolStripMenuItem1, this.toolStripMenuItem2});  
    ```  
  
## <a name="see-also"></a>関連項目

- [ContextMenuStrip コントロール](contextmenustrip-control.md)
