---
title: '方法: ToolStrip 項目の間隔と配置を変更する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], aligning items
- examples [Windows Forms], toolbars
- toolbars [Windows Forms], aligning items
ms.assetid: cd483466-0f49-43df-addf-e2b5fcd64027
ms.openlocfilehash: 550ac1660a077e8d766a01bfa8d102c07f0fbfeb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182239"
---
# <a name="how-to-change-the-spacing-and-alignment-of-toolstrip-items-in-windows-forms"></a>方法 : Windows フォーム内の ToolStrip 項目の間隔と配置を変更する
この<xref:System.Windows.Forms.ToolStrip>コントロールは、サイズ変更、相互に相対的なコントロールの<xref:System.Windows.Forms.ToolStripItem>間隔、<xref:System.Windows.Forms.ToolStrip>コントロールの配置、コントロールの間隔などのレイアウト機能を完全にサポートしています<xref:System.Windows.Forms.ToolStrip>。  
  
 プロパティの既定値は に<xref:System.Windows.Forms.ToolStripItem.AutoSize%2A>設定されている`true`場合、<xref:System.Windows.Forms.ToolStripItem.AutoSize%2A>プロパティのサイズは自動的に`false`変更されます。  
  
### <a name="to-manually-size-a-toolstripitem"></a>手動でサイズを変更するには  
  
1. 関連付<xref:System.Windows.Forms.ToolStripItem.AutoSize%2A>けられたコントロール`false`の プロパティを に設定します。  
  
    ```vb  
    ToolStripButton1.AutoSize = False  
    ```  
  
    ```csharp  
    toolStripButton1.AutoSize = false;  
    ```  
  
2. 関連付<xref:System.Windows.Forms.ToolStripItem.Size%2A>けられた<xref:System.Windows.Forms.ToolStripItem>.  
  
### <a name="to-set-the-spacing-of-a-toolstripitem"></a>ツールストリップ アイテムの間隔を設定するには  
  
1. 関連付けられたコントロールのプロパティに、必要な<xref:System.Windows.Forms.ToolStripItem.Margin%2A>値をピクセル単位で挿入します。  
  
     <xref:System.Windows.Forms.ToolStripItem.Margin%2A>このプロパティの値は、アイテムと隣接するアイテムの間隔を、左、上、右、下の順に指定します。  
  
    ```vb  
    ToolStripTextBox1.Margin = New System.Windows.Forms.Padding _  
        (3, 0, 3, 0)  
    ```  
  
    ```csharp  
    toolStripTextBox1.Margin = new System.Windows.Forms.Padding
        (3, 0, 3, 0);  
    ```  
  
### <a name="to-align-a-toolstripitem-to-the-right-side-of-the-toolstrip"></a>ツールストリップアイテムをツールストリップの右側に揃えるには  
  
1. 関連付<xref:System.Windows.Forms.ToolStripItem.Alignment%2A>けられたコントロール<xref:System.Windows.Forms.ToolStripItemAlignment.Right>の プロパティを に設定します。 既定では、 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> <xref:System.Windows.Forms.ToolStripItemAlignment.Left>は に設定され、コントロールは<xref:System.Windows.Forms.ToolStrip>の左側に揃えます。  
  
    ```vb  
    ToolStripSplitButton1.Alignment = _  
        System.Windows.Forms.ToolStripItemAlignment.Right  
    ```  
  
    ```csharp  
    toolStripSplitButton1.Alignment =
        System.Windows.Forms.ToolStripItemAlignment.Right;  
    ```  
  
### <a name="to-arrange-toolstrip-items-on-the-toolstrip"></a>ツールストリップの項目を配置するには  
  
- プロパティを<xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>目的の<xref:System.Windows.Forms.ToolStripLayoutStyle>値に設定します。  
  
    ```vb  
    ToolStripDropDown1.LayoutStyle = _  
        System.Windows.Forms.ToolStripLayoutStyle.Flow  
    ```  
  
    ```csharp  
    toolStripDropDown1.LayoutStyle =
        System.Windows.Forms.ToolStripLayoutStyle.Flow;  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.Control.Layout>
- <xref:System.Windows.Forms.ToolStrip.LayoutCompleted>
- <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>
- <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A>
- <xref:System.Windows.Forms.ToolStripItem.Placement%2A>
- <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>
- [ToolStrip コントロールの概要](toolstrip-control-overview-windows-forms.md)
- [ToolStrip コントロールのアーキテクチャ](toolstrip-control-architecture.md)
- [ToolStrip テクノロジの概要](toolstrip-technology-summary.md)
