---
title: LinkLabel コントロールを使用してオブジェクトまたは Web ページにリンクする
description: Windows フォーム LinkLabel コントロールを使用して、オブジェクトまたは web ページへの Web スタイルのリンクを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Windows Forms, linking to objects
- Web page link control
- linking [Windows Forms], to other forms
- Windows Forms, linking to Web pages
- links [Windows Forms], to other forms
- LinkLabel control [Windows Forms], linking to object or Web page
- LinkLabel control [Windows Forms], examples
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
ms.openlocfilehash: a5fb1c03e9a8d82fe77f4133ba04c42114787d23
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618313"
---
# <a name="how-to-link-to-an-object-or-web-page-with-the-windows-forms-linklabel-control"></a>方法: Windows フォーム LinkLabel コントロールでオブジェクトまたは Web ページにリンクする

Windows フォーム <xref:System.Windows.Forms.LinkLabel> コントロールを使用すると、フォーム上に Web スタイルのリンクを作成できます。 リンクをクリックすると、その色を変更してリンクがアクセスされたことを示すことができます。 色の変更の詳細については、「[方法: Windows フォーム LinkLabel コントロールの外観を変更する](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)」を参照してください。

## <a name="linking-to-another-form"></a>リンク (別のフォームに)

#### <a name="to-link-to-another-form-with-a-linklabel-control"></a>LinkLabel コントロールを使用して別のフォームにリンクするには

1. プロパティを <xref:System.Windows.Forms.LinkLabel.Text%2A> 適切なキャプションに設定します。

2. プロパティを設定し <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> て、キャプションのどの部分がリンクとして示されるかを決定します。 どのように表示されるかは、リンクラベルの外観に関連するプロパティによって異なります。 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>値は、 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 2 つの数値、開始文字の位置、および文字数を含むオブジェクトによって表されます。 プロパティは、 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 次のような方法でプロパティウィンドウまたはコードで設定できます。

    ```vb
    ' In this code example, the link area has been set to begin
    ' at the first character and extend for eight characters.
    ' You may need to modify this based on the text entered in Step 1.
    LinkLabel1.LinkArea = New LinkArea(0, 8)
    ```

    ```csharp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1.LinkArea = new LinkArea(0,8);
    ```

    ```cpp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1->LinkArea = LinkArea(0,8);
    ```

3. <xref:System.Windows.Forms.LinkLabel.LinkClicked>イベントハンドラーで、メソッドを呼び出し <xref:System.Windows.Forms.Form.Show%2A> て、プロジェクト内の別のフォームを開き、 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> プロパティをに設定し `true` ます。

    > [!NOTE]
    > クラスのインスタンスは、 <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> クリックされたコントロールへの参照を保持して <xref:System.Windows.Forms.LinkLabel> いるため、オブジェクトをキャストする必要はありません `sender` 。

    ```vb
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       ' Show another form.
       Dim f2 As New Form()
       f2.Show
       LinkLabel1.LinkVisited = True
    End Sub
    ```

    ```csharp
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       // Show another form.
       Form f2 = new Form();
       f2.Show();
       linkLabel1.LinkVisited = true;
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          // Show another form.
          Form ^ f2 = new Form();
          f2->Show();
          linkLabel1->LinkVisited = true;
       }
    ```

## <a name="linking-to-a-web-page"></a>Web ページへのリンク

<xref:System.Windows.Forms.LinkLabel>コントロールを使用して、既定のブラウザーで Web ページを表示することもできます。

#### <a name="to-start-internet-explorer-and-link-to-a-web-page-with-a-linklabel-control"></a>Internet Explorer を起動し、LinkLabel コントロールを使用して Web ページにリンクするには

1. プロパティを <xref:System.Windows.Forms.LinkLabel.Text%2A> 適切なキャプションに設定します。

2. プロパティを設定し <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> て、キャプションのどの部分がリンクとして示されるかを決定します。

3. イベントハンドラーでは、 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 例外処理ブロックの途中で、2番目のプロシージャを呼び出します。このプロシージャは、プロパティをに設定し、メソッドを使用して <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> `true` <xref:System.Diagnostics.Process.Start%2A> URL で既定のブラウザーを起動します。 メソッドを使用するには、 <xref:System.Diagnostics.Process.Start%2A> 名前空間への参照を追加する必要があり <xref:System.Diagnostics?displayProperty=nameWithType> ます。

    > [!IMPORTANT]
    > 以下のコードを部分信頼環境 (共有ドライブなど) で実行すると、メソッドが呼び出されたときに JIT コンパイラが失敗し `VisitLink` ます。 `System.Diagnostics.Process.Start`ステートメントにより、リンク確認要求が失敗します。 メソッドが呼び出されたときに例外をキャッチすることにより、 `VisitLink` 次のコードは、JIT コンパイラが失敗した場合にエラーが適切に処理されることを確認します。

    ```vb
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       Try
          VisitLink()
       Catch ex As Exception
          ' The error message
          MessageBox.Show("Unable to open link that was clicked.")
       End Try
    End Sub

    Sub VisitLink()
       ' Change the color of the link text by setting LinkVisited
       ' to True.
       LinkLabel1.LinkVisited = True
       ' Call the Process.Start method to open the default browser
       ' with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com")
    End Sub
    ```

    ```csharp
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       try
       {
          VisitLink();
       }
       catch (Exception ex )
       {
          MessageBox.Show("Unable to open link that was clicked.");
       }
    }

    private void VisitLink()
    {
       // Change the color of the link text by setting LinkVisited
       // to true.
       linkLabel1.LinkVisited = true;
       //Call the Process.Start method to open the default browser
       //with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com");
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          try
          {
             VisitLink();
          }
          catch (Exception ^ ex)
          {
             MessageBox::Show("Unable to open link that was clicked.");
          }
       }
    private:
       void VisitLink()
       {
          // Change the color of the link text by setting LinkVisited
          // to true.
          linkLabel1->LinkVisited = true;
          // Call the Process.Start method to open the default browser
          // with a URL:
          System::Diagnostics::Process::Start("http://www.microsoft.com");
       }
    ```

## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- [LinkLabel コントロールの概要](linklabel-control-overview-windows-forms.md)
- [方法: Windows フォーム LinkLabel コントロールの表示形式を変更する](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
- [LinkLabel コントロール](linklabel-control-windows-forms.md)
