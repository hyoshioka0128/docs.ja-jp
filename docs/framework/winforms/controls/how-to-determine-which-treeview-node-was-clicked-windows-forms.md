---
title: '方法 : クリックされた TreeView ノードを判別する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TreeNode
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- tree nodes in TreeView control [Windows Forms], determining node clicked
- TreeView control [Windows Forms], determining node clicked
ms.assetid: 06a4a191-d918-42af-9f49-956c93eff261
ms.openlocfilehash: d960eaae2aa479e0be74e9a5e4fdbfec8ff411c1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182184"
---
# <a name="how-to-determine-which-treeview-node-was-clicked-windows-forms"></a>方法 : クリックされた TreeView ノード (Windows フォーム) を判別する
Windows フォーム<xref:System.Windows.Forms.TreeView>コントロールを操作する場合、一般的なタスクは、クリックされたノードを特定し、適切に応答することです。  
  
### <a name="to-determine-which-treeview-node-was-clicked"></a>クリックされたツリー ビュー ノードを確認するには  
  
1. オブジェクトを<xref:System.EventArgs>使用して、クリックされたノード オブジェクトへの参照を返します。  
  
2. イベントに関連するデータを含むクラス<xref:System.Windows.Forms.TreeViewEventArgs>をチェックして、どのノードがクリックされたかを確認します。  
  
    ```vb  
    Private Sub TreeView1_AfterSelect(ByVal sender As System.Object, _  
    ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       ' Determine by checking the Node property of the TreeViewEventArgs.  
       MessageBox.Show(e.Node.Text)  
    End Sub  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       // Determine by checking the Text property.  
       MessageBox.Show(e.Node.Text);  
    }  
    ```  
  
    ```cpp  
    private:  
       void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          // Determine by checking the Text property.  
          MessageBox::Show(e->Node->Text);  
       }  
    ```  
  
    > [!NOTE]
    > または<xref:System.Windows.Forms.MouseEventArgs><xref:System.Windows.Forms.Control.MouseDown><xref:System.Windows.Forms.Control.MouseUp>イベントの を使用して、クリック<xref:System.Drawing.Point.X%2A><xref:System.Drawing.Point.Y%2A><xref:System.Drawing.Point>が発生した場所の 座標値と座標値を取得することもできます。 次に、コントロール<xref:System.Windows.Forms.TreeView>の<xref:System.Windows.Forms.TreeView.GetNodeAt%2A>メソッドを使用して、クリックされたノードを特定します。  
  
## <a name="see-also"></a>関連項目

- [TreeView コントロール](treeview-control-windows-forms.md)
