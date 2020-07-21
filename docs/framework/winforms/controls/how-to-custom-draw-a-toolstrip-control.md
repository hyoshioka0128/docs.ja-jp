---
title: '方法 : ToolStrip コントロールをカスタム描画する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms], custom drawing
- drawing [Windows Forms], owner
- ProfessionalColorTable class [Windows Forms], overriding
- examples [Windows Forms], toolbars
- drawing [Windows Forms], custom
- toolbars [Windows Forms], changing colors
- ToolStrip control [Windows Forms], drawing
- ToolStrip control [Windows Forms], changing colors
- custom drawing
- owner drawing
ms.assetid: 94e7d7bd-a752-441c-b5b3-7acf98881163
ms.openlocfilehash: a9f603efdb4b4a5f68154da9c6a8bd05b55b8f46
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182225"
---
# <a name="how-to-custom-draw-a-toolstrip-control"></a>方法 : ToolStrip コントロールをカスタム描画する
<xref:System.Windows.Forms.ToolStrip> コントロールに、次のレンダリング (描画) クラスが関連付けられています。  
  
- <xref:System.Windows.Forms.ToolStripSystemRenderer> は、オペレーティング システムの外観とスタイルを提供します。  
  
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer> は、Microsoft Office の外観とスタイルを提供します。  
  
- <xref:System.Windows.Forms.ToolStripRenderer> は、その他の 2 つのレンダリング クラスの抽象基本クラスです。  
  
 <xref:System.Windows.Forms.ToolStrip> をカスタムで描画 (オーナー描画) するために、レンダラー クラスの 1 つをオーバーライドして表示ロジックの特定の側面を変更できます。  
  
 次の手順は、カスタムの描画のさまざまな側面について説明します。  
  
### <a name="to-switch-between-the-provided-renderers"></a>設定されているレンダラー間で切り替えるには  
  
- <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> プロパティを任意の <xref:System.Windows.Forms.ToolStripRenderMode> の値に設定します。  
  
     <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode> と共に、静的な <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> がアプリケーションのレンダラーを決定します。 <xref:System.Windows.Forms.ToolStripRenderMode> のその他の値は、<xref:System.Windows.Forms.ToolStripRenderMode.Custom>、<xref:System.Windows.Forms.ToolStripRenderMode.Professional>、および <xref:System.Windows.Forms.ToolStripRenderMode.System> です。  
  
### <a name="to-change-the-microsoft-officestyle-borders-to-straight"></a>Microsoft Office スタイルの境界を直線に変更するには  
  
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer.OnRenderToolStripBorder%2A?displayProperty=nameWithType> をオーバーライドしますが、基本クラスは呼び出しません。  
  
> [!NOTE]
> <xref:System.Windows.Forms.ToolStripRenderer>、<xref:System.Windows.Forms.ToolStripSystemRenderer>、および <xref:System.Windows.Forms.ToolStripProfessionalRenderer> に対して、このメソッドのバージョンがあります。  
  
### <a name="to-change-the-professionalcolortable"></a>ProfessionalColorTable を変更するには  
  
- <xref:System.Windows.Forms.ProfessionalColorTable> をオーバーライドして必要な色を変更します。  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As _  
    System.EventArgs) Handles Me.Load  
        Dim t As MyColorTable = New MyColorTable  
        ToolStrip1.Renderer = New ToolStripProfessionalRenderer(t)  
    End Sub  
  
    Class MyColorTable
    Inherits ProfessionalColorTable  
  
    Public Overrides ReadOnly Property ButtonPressedGradientBegin() As Color  
        Get  
            Return Color.Red  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientMiddle() _  
    As System.Drawing.Color  
        Get  
            Return Color.Blue  
        End Get  
            End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Green  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientBegin() _  
    As Color  
        Get  
            Return Color.Yellow  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientMiddle() As System.Drawing.Color  
        Get  
            Return Color.Orange  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Violet  
        End Get  
    End Property  
    End Class  
    ```  
  
### <a name="to-change-the-rendering-for-all-toolstrip-controls-in-your-application"></a>アプリケーション内のすべての ToolStrip コントロールのレンダリングを変更するには  
  
1. <xref:System.Windows.Forms.ToolStripManager.RenderMode%2A?displayProperty=nameWithType> プロパティを使用して、設定されているレンダラーのいずれかを選択します。  
  
2. <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType> を使用して、カスタム レンダラーを割り当てます。  
  
3. <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=nameWithType> が既定値の <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode> に設定されていることを確認します。  
  
### <a name="to-turn-off-the-microsoft-office-colors-for-the-entire-application"></a>アプリケーション全体で Microsoft Office の色をオフにするには  
  
- <xref:System.Windows.Forms.ToolStripManager.VisualStylesEnabled%2A?displayProperty=nameWithType> を `false` に設定します。  
  
### <a name="to-turn-off-the-microsoft-office-colors-for-one-toolstrip-control"></a>1 つの ToolStrip コントロールで Microsoft Office の色をオフにするには  
  
- 次のコード例に似たコードを使用します。  
  
    ```vb  
    Dim colorTable As ProfessionalColorTable()  
    colorTable.UseSystemColors = True  
    Dim toolStrip.Renderer As ToolStripProfessionalRenderer(colorTable)  
    ```  
  
    ```csharp  
    ProfessionalColorTable colorTable = new ProfessionalColorTable();  
    colorTable.UseSystemColors = true;  
    toolStrip.Renderer = new ToolStripProfessionalRenderer(colorTable);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ToolStripSystemRenderer>
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer>
- <xref:System.Windows.Forms.ToolStripRenderer>
- [組み込みのオーナー描画サポートを備えたコントロール](controls-with-built-in-owner-drawing-support.md)
- [方法 : Windows フォームに ToolStrip コントロールのカスタム レンダラーを作成して設定する](create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)
- [ToolStrip コントロールの概要](toolstrip-control-overview-windows-forms.md)
