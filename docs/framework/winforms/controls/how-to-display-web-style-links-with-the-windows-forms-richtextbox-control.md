---
title: RichTextBox コントロールを使用して Web スタイルのリンクを表示する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], displaying Web links
- examples [Windows Forms], text boxes
- RichTextBox control [Windows Forms], linking to Web pages
ms.assetid: 95089a37-a202-4f7a-94ee-6ee312908851
ms.openlocfilehash: 06ed304e566bb437a2353dd330d7de5328f2a729
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144826"
---
# <a name="how-to-display-web-style-links-with-the-windows-forms-richtextbox-control"></a>方法: Windows フォームの RichTextBox コントロールを使用して Web スタイルのリンクを表示する

Windows フォーム <xref:System.Windows.Forms.RichTextBox> コントロールでは、Web リンクを色分けおよび下線付きで表示できます。 リンクがクリックされたときに、リンクテキストで指定された Web サイトを表示するブラウザーウィンドウを開くコードを記述できます。

### <a name="to-link-to-a-web-page-with-the-richtextbox-control"></a>RichTextBox コントロールを使用して Web ページにリンクするには

1. プロパティを、 <xref:System.Windows.Forms.RichTextBox.Text%2A> 有効な URL (たとえば "") を含む文字列に設定し https://www.microsoft.com/ ます。

2. <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>プロパティが (既定値) に設定されていることを確認し `true` ます。

3. オブジェクトの新しいグローバルインスタンスを作成 <xref:System.Diagnostics.Process> します。

4. <xref:System.Windows.Forms.RichTextBox.LinkClicked>目的のテキストをブラウザーに送信するイベントのイベントハンドラーを作成します。

    次の例では、イベントによって、 <xref:System.Windows.Forms.RichTextBox.LinkClicked> Internet Explorer のインスタンスが、コントロールのプロパティで指定された URL に開かれ <xref:System.Windows.Forms.RichTextBox.Text%2A> <xref:System.Windows.Forms.RichTextBox> ます。 この例では、フォームにコントロールがあることを前提としてい <xref:System.Windows.Forms.RichTextBox> ます。

    > [!IMPORTANT]
    > <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> <xref:System.Security.SecurityException> 権限が不十分であるために部分信頼コンテキストでコードを実行している場合、メソッドを呼び出すと例外が発生します。 詳しくは、「[コード アクセス セキュリティの基礎](../../misc/code-access-security-basics.md)」をご覧ください。

    ```vb
    Public p As New System.Diagnostics.Process
    Private Sub RichTextBox1_LinkClicked _
       (ByVal sender As Object, ByVal e As _
       System.Windows.Forms.LinkClickedEventArgs) _
       Handles RichTextBox1.LinkClicked
          ' Call Process.Start method to open a browser
          ' with link text as URL.
          p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText)
    End Sub
    ```

    ```csharp
    public System.Diagnostics.Process p = new System.Diagnostics.Process();

    private void richTextBox1_LinkClicked(object sender,
    System.Windows.Forms.LinkClickedEventArgs e)
    {
       // Call Process.Start method to open a browser
       // with link text as URL.
       p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText);
    }
    ```

    ```cpp
    public:
       System::Diagnostics::Process ^ p;

    private:
       void richTextBox1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkClickedEventArgs ^  e)
       {
          // Call Process.Start method to open a browser
          // with link text as URL.
          p = System::Diagnostics::Process::Start("IExplore.exe",
             e->LinkText);
       }
    ```

    (Visual C++)プロセスを初期化する必要があります。これを `p` 行うには、次のステートメントをフォームのコンストラクターに含めます。

    ```cpp
    p = gcnew System::Diagnostics::Process();
    ```

    (Visual C#、Visual C++)フォームのコンストラクターに次のコードを配置して、イベントハンドラーを登録します。

    ```csharp
    this.richTextBox1.LinkClicked += new
       System.Windows.Forms.LinkClickedEventHandler
       (this.richTextBox1_LinkClicked);
    ```

    ```cpp
    this->richTextBox1->LinkClicked += gcnew
       System::Windows::Forms::LinkClickedEventHandler
       (this, &Form1::richTextBox1_LinkClicked);
    ```

    作業が終了したら、作成したプロセスをすぐに停止することが重要です。 上記のコードを参照すると、プロセスを停止するためのコードは次のようになります。

    ```vb
    Public Sub StopWebProcess()
       p.Kill()
    End Sub
    ```

    ```csharp
    public void StopWebProcess()
    {
       p.Kill();
    }
    ```

    ```cpp
    public: void StopWebProcess()
    {
       p->Kill();
    }
    ```

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>
- <xref:System.Windows.Forms.RichTextBox.LinkClicked>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox コントロール](richtextbox-control-windows-forms.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
