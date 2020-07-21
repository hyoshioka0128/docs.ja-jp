---
title: ツリー ビュー コントロールを使用したノードの追加と削除
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- TreeView control [Windows Forms], removing nodes
- tree nodes in TreeView control
- TreeView control [Windows Forms], adding nodes
ms.assetid: de1b82db-4905-449a-9f59-af271a6b6673
ms.openlocfilehash: f1e74e6d2f827167c32a6955b3010b59cb2f85b8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142213"
---
# <a name="how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control"></a>方法 : Windows フォーム TreeView コントロールでノードを追加および削除する
Windows フォーム<xref:System.Windows.Forms.TreeView>コントロールは、最上位のノードを<xref:System.Windows.Forms.TreeView.Nodes%2A>コレクションに格納します。 また<xref:System.Windows.Forms.TreeNode>、子ノードを<xref:System.Windows.Forms.TreeNode.Nodes%2A>格納する独自のコレクションも用意されています。 どちらのコレクション プロパティも<xref:System.Windows.Forms.TreeNodeCollection>type で、ノード階層の単一レベルでノードを追加、削除、および再配置できる標準コレクション メンバーを提供します。  
  
### <a name="to-add-nodes-programmatically"></a>プログラムでノードを追加するには  
  
1. ツリー<xref:System.Windows.Forms.TreeNodeCollection.Add%2A>ビューのプロパティの<xref:System.Windows.Forms.TreeView.Nodes%2A>メソッドを使用します。  
  
    ```vb  
    ' Adds new node as a child node of the currently selected node.  
    Dim newNode As TreeNode = New TreeNode("Text for new node")  
    TreeView1.SelectedNode.Nodes.Add(newNode)  
    ```  
  
    ```csharp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode newNode = new TreeNode("Text for new node");  
    treeView1.SelectedNode.Nodes.Add(newNode);  
    ```  
  
    ```cpp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode ^ newNode = new TreeNode("Text for new node");  
    treeView1->SelectedNode->Nodes->Add(newNode);  
    ```  
  
### <a name="to-remove-nodes-programmatically"></a>プログラムによってノードを削除するには  
  
1. ツリー<xref:System.Windows.Forms.TreeNodeCollection.Remove%2A>ビューのプロパティのメソッドを使用<xref:System.Windows.Forms.TreeView.Nodes%2A>して単一のノードを削除するか、<xref:System.Windows.Forms.TreeNodeCollection.Clear%2A>すべてのノードをクリアするメソッドを使用します。  
  
    ```vb  
    ' Removes currently selected node, or root if nothing is selected.  
    TreeView1.Nodes.Remove(TreeView1.SelectedNode)  
    ' Clears all nodes.  
    TreeView1.Nodes.Clear()  
    ```  
  
    ```csharp  
    // Removes currently selected node, or root if nothing
    // is selected.  
    treeView1.Nodes.Remove(treeView1.SelectedNode);  
    // Clears all nodes.  
    TreeView1.Nodes.Clear();  
    ```  
  
    ```cpp  
    // Removes currently selected node, or root if nothing  
    // is selected.  
    treeView1->Nodes->Remove(treeView1->SelectedNode);  
    // Clears all nodes.  
    treeView1->Nodes->Clear();  
    ```  
  
## <a name="see-also"></a>関連項目

- [TreeView コントロール](treeview-control-windows-forms.md)
- [TreeView コントロールの概要](treeview-control-overview-windows-forms.md)
- [方法: Windows フォーム TreeView コントロールのアイコンを設定する](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [方法 : Windows フォーム TreeView コントロールのすべてのノードを反復処理する](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [方法 : クリックされた TreeView ノードを判別する](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [方法 : TreeView コントロールまたは ListView コントロール (Windows フォーム) にカスタム情報を追加する](add-custom-information-to-a-treeview-or-listview-control-wf.md)
