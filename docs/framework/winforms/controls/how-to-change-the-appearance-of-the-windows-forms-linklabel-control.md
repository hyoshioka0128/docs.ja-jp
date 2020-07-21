---
title: リンクラベル コントロールの外観を変更する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- LinkLabel properties
- LinkLabel control [Windows Forms], changing appearance of links
- links [Windows Forms], changing appearance
- examples [Windows Forms], LinkLabel control
- LinkLabel control [Windows Forms], examples
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
ms.openlocfilehash: df66991289373a05fc7c27b7768a96643e3bbae0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142131"
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-linklabel-control"></a>方法 : Windows フォーム LinkLabel コントロールの表示形式を変更する
コントロールによって表示されるテキストは、<xref:System.Windows.Forms.LinkLabel>さまざまな目的に合わせて変更できます。 たとえば、テキストを特定の色で下線で表示するように設定することで、テキストをクリックできることをユーザーに示すのが一般的です。 ユーザーがテキストをクリックすると、色が別の色に変わります。 この<xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>動作を制御するには、 、 、 、<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>および<xref:System.Windows.Forms.LinkLabel.LinkColor%2A><xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>プロパティの 5<xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>つの異なるプロパティを設定できます。  
  
### <a name="to-change-the-appearance-of-a-linklabel-control"></a>リンク ラベル コントロールの外観を変更するには  
  
1. プロパティ<xref:System.Windows.Forms.LinkLabel.LinkColor%2A>と<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>プロパティを目的の色に設定します。  
  
     これは、プログラムによって、またはデザイン時に **[プロパティ]** ウィンドウで実行できます。  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2. プロパティを<xref:System.Windows.Forms.LinkLabel.Text%2A>適切なキャプションに設定します。  
  
     これは、プログラムによって、またはデザイン時に **[プロパティ]** ウィンドウで実行できます。  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3. キャプションのどの<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>部分をリンクとして示すかを決定するには、プロパティを設定します。  
  
     値<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>は、開始文字の<xref:System.Windows.Forms.LinkArea>位置と文字数の 2 つの数字を含むで表されます。 これは、プログラムによって、またはデザイン時に **[プロパティ]** ウィンドウで実行できます。  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4. プロパティを<xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>、 <xref:System.Windows.Forms.LinkBehavior.AlwaysUnderline> <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>、または<xref:System.Windows.Forms.LinkBehavior.NeverUnderline>に設定します。  
  
     に<xref:System.Windows.Forms.LinkBehavior.HoverUnderline>設定されている場合、指定された<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>キャプションの部分は、ポインタが上にある場合にのみ下線が引かれます。  
  
5. イベント<xref:System.Windows.Forms.LinkLabel.LinkClicked>ハンドラーで、プロパティを<xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>に`true`設定します。  
  
     リンクが訪れた場合、通常は色によって外観を変更するのが一般的です。 テキストは、プロパティで指定された色に<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>変更されます。  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>
- [LinkLabel コントロールの概要](linklabel-control-overview-windows-forms.md)
- [方法 : Windows フォーム LinkLabel コントロールでオブジェクトまたは Web ページにリンクする](link-to-an-object-or-web-page-with-wf-linklabel-control.md)
- [LinkLabel コントロール](linklabel-control-windows-forms.md)
