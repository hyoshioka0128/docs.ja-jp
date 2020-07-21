---
title: '方法 : ユーザーのコンピュータに接続されているプリンタを選択する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- printing [Windows Forms], choosing printers
- printers [Windows Forms], choosing
ms.assetid: 63c1172b-2931-4ac0-953f-37f629494bbf
ms.openlocfilehash: 2afbccd02ef42a78d5eac1a01841516fca27c92e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182613"
---
# <a name="how-to-choose-the-printers-attached-to-a-users-computer-in-windows-forms"></a>方法 : Windows フォームでユーザーのコンピューターに接続されたプリンターを選択する
既定のプリンター以外のプリンターに印刷することがよくあります。 <xref:System.Windows.Forms.PrintDialog> コンポーネントを使用すると、現在インストールされているプリンターからユーザーに選択させることができます。 <xref:System.Windows.Forms.PrintDialog> コンポーネントでは、 <xref:System.Windows.Forms.DialogResult> コンポーネントの <xref:System.Windows.Forms.PrintDialog> がキャプチャされ、プリンターの選択に使用されます。  
  
 次の手順では、既定のプリンターに印刷するテキスト ファイルを選択します。 <xref:System.Windows.Forms.PrintDialog> クラスがインスタンス化されます。  
  
### <a name="to-choose-a-printer-and-then-print-a-file"></a>プリンターを選択してファイルを印刷するには  
  
1. コンポーネントを使用して使用するプリンタを<xref:System.Windows.Forms.PrintDialog>選択します。  
  
     次のコード例では、2 つのイベントを処理しています。 最初の例では、<xref:System.Windows.Forms.Button>コントロールの<xref:System.Windows.Forms.Control.Click>イベント、<xref:System.Windows.Forms.PrintDialog>クラスがインスタンス化され、ユーザーが選択したプリンターがプロパティに<xref:System.Windows.Forms.DialogResult>キャプチャされます。  
  
     2番目のイベントでは、<xref:System.Drawing.Printing.PrintDocument.PrintPage><xref:System.Drawing.Printing.PrintDocument>コンポーネントのイベントは、指定されたプリンタにサンプルドキュメントが印刷されます。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim PrintDialog1 As New PrintDialog()  
       PrintDialog1.Document = PrintDocument1  
       Dim result As DialogResult = PrintDialog1.ShowDialog()  
  
       If (result = DialogResult.OK) Then  
         PrintDocument1.Print()  
       End If
  
    End Sub  
  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       PrintDialog printDialog1 = new PrintDialog();  
       printDialog1.Document = printDocument1;  
       DialogResult result = printDialog1.ShowDialog();  
       if (result == DialogResult.OK)  
       {  
          printDocument1.Print();  
       }  
    }  
  
    private void printDocument1_PrintPage(object sender,
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,
         new Rectangle(500, 500, 500, 500));  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          PrintDialog ^ printDialog1 = gcnew PrintDialog();  
          printDialog1->Document = printDocument1;  
          System::Windows::Forms::DialogResult result =
             printDialog1->ShowDialog();  
          if (result == DialogResult::OK)  
          {  
             printDocument1->Print();  
          }  
       }  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     (ビジュアル C# およびビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>関連項目

- [Windows フォームにおける印刷のサポート](windows-forms-print-support.md)
