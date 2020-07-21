---
title: '方法: ToolStrip コントロールのカスタム レンダラーを作成および設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], custom rendering
- toolbars [Windows Forms], rendering
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], rendering
ms.assetid: 88a804ba-679f-4ba3-938a-0dc396199c5b
ms.openlocfilehash: 49db0d785155f19b7220ac64011eaf4253aaa7e9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182401"
---
# <a name="how-to-create-and-set-a-custom-renderer-for-the-toolstrip-control-in-windows-forms"></a>方法 : Windows フォームに ToolStrip コントロールのカスタム レンダラーを作成して設定する
<xref:System.Windows.Forms.ToolStrip>コントロールは、テーマやスタイルに簡単にサポートを提供します。 プロパティまたはプロパティをカスタム レンダラに設定することで、完全にカスタムの<xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType>外観と<xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType>動作 (ルック アンド フィール) を実現できます。  
  
 レンダラーは<xref:System.Windows.Forms.ToolStrip>、 、 、<xref:System.Windows.Forms.MenuStrip><xref:System.Windows.Forms.ContextMenuStrip>または<xref:System.Windows.Forms.StatusStrip>コントロールに割り当てることも、<xref:System.Windows.Forms.ToolStripManager.Renderer%2A>プロパティを使用して すべてのオブジェクト<xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=nameWithType>に影響<xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode?displayProperty=nameWithType>を与える場合は、 プロパティを に設定します。  
  
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>の<xref:System.Windows.Forms.ToolStripRenderMode.Custom>値<xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType>がでない`null`場合にのみ返されます。  
  
### <a name="to-create-a-custom-renderer"></a>カスタム レンダラーを作成するには  
  
1. クラスを<xref:System.Windows.Forms.ToolStripRenderer>拡張します。  
  
2. 適切な*On..* をオーバーライドして、目的のカスタム レンダリングを実装します。 members  
  
    ```vb  
    Public Class RedTextRenderer  
        Inherits System.Windows.Forms.ToolStripRenderer  
        Protected Overrides Sub OnRenderItemText(ByVal e As _  
            ToolStripItemTextRenderEventArgs)
            e.TextColor = Color.Red  
            e.TextFont = New Font("Helvetica", 7, FontStyle.Bold)  
            MyBase.OnRenderItemText(e)  
        End Sub  
    End Class  
    ```  
  
    ```csharp  
    public class RedTextRenderer : _  
        System.Windows.Forms.ToolStripRenderer  
    {  
        protected override void _  
            OnRenderItemText(ToolStripItemTextRenderEventArgs e)  
        {  
            e.TextColor = Color.Red;  
            e.TextFont = new Font("Helvetica", 7, FontStyle.Bold);  
           base.OnRenderItemText(e);  
        }  
    }  
    ```  
  
### <a name="to-set-the-custom-renderer-to-be-the-current-renderer"></a>カスタム レンダラーを現在のレンダラーに設定するには  
  
1. カスタム レンダラーを 1<xref:System.Windows.Forms.ToolStrip>つに設定<xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType>するには、プロパティをカスタム レンダラーに設定します。  
  
    ```vb  
    toolStrip1.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.Renderer = new RedTextRenderer();  
    ```  
  
2. または、アプリケーションに<xref:System.Windows.Forms.ToolStrip>含まれるすべてのクラスにカスタム レンダラーを設定するには<xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType>、次の手順に<xref:System.Windows.Forms.ToolStrip.RenderMode%2A>従います。 <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>  
  
    ```vb  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode  
    ToolStripManager.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode;  
    ToolStripManager.Renderer = new RedTextRenderer();  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ToolStripManager.Renderer%2A>
- <xref:System.Windows.Forms.ToolStripRenderer>
- <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>
- [ToolStrip コントロールの概要](toolstrip-control-overview-windows-forms.md)
- [ToolStrip コントロールのアーキテクチャ](toolstrip-control-architecture.md)
- [ToolStrip テクノロジの概要](toolstrip-technology-summary.md)
