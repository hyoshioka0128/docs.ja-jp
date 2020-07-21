---
title: 標準印刷ジョブの作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- printing [Windows Forms]
- printing [Windows Forms], creating print jobs
- printing [Visual Basic], in Windows applications
ms.assetid: 03342b90-9cfe-40b2-838b-b479a13c5dea
ms.openlocfilehash: d9607de7c74132e0d7dce605b16d62c79b7dbccb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182568"
---
# <a name="how-to-create-standard-windows-forms-print-jobs"></a>方法 : 標準の Windows フォーム印刷ジョブを作成する
Windows フォームでの印刷の基礎は<xref:System.Drawing.Printing.PrintDocument>、コンポーネント、つまり、イベント<xref:System.Drawing.Printing.PrintDocument.PrintPage>です。 イベントを処理するコードを<xref:System.Drawing.Printing.PrintDocument.PrintPage>記述することにより、印刷する内容と印刷方法を指定できます。  
  
### <a name="to-create-a-print-job"></a>印刷ジョブを作成するには  
  
1. フォームに<xref:System.Drawing.Printing.PrintDocument>コンポーネントを追加します。  
  
2. <xref:System.Drawing.Printing.PrintDocument.PrintPage> イベントを処理するコードを記述します。  
  
     独自の印刷ロジックをコーディングする必要があります。 また、印刷する品目を指定する必要があります。  
  
     次のコード例では、赤い四角形の形をしたサンプル グラフィックが<xref:System.Drawing.Printing.PrintDocument.PrintPage>、印刷するマテリアルとして機能するイベント ハンドラーに作成されます。  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,
         new Rectangle(500, 500, 500, 500));  
    }  
    ```  
  
    ```cpp  
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
    ```  
  
    ```cpp  
    printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
     また、<xref:System.Drawing.Printing.PrintDocument.BeginPrint>イベントと<xref:System.Drawing.Printing.PrintDocument.EndPrint>イベントのコードを記述することもできます 。  
  
    > [!NOTE]
    > フォームにコンポーネントを<xref:System.Windows.Forms.PrintDialog>追加すると、ユーザーにクリーンで効率的なユーザー インターフェイス (UI) を提供できます。 コンポーネントの<xref:System.Windows.Forms.PrintDialog.Document%2A>プロパティを<xref:System.Windows.Forms.PrintDialog>設定すると、フォームで作業している印刷ドキュメントに関連するプロパティを設定できます。 コンポーネントの<xref:System.Windows.Forms.PrintDialog>詳細については、「 [PrintDialog コンポーネント](../controls/printdialog-component-windows-forms.md)」を参照してください。  
  
     Windows フォーム印刷ジョブの詳細 (プログラムによる印刷ジョブの作成方法など) の詳細については、「 <xref:System.Drawing.Printing.PrintPageEventArgs>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Printing.PrintDocument>
- [Windows フォームにおける印刷のサポート](windows-forms-print-support.md)
