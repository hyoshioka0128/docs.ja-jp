---
title: '方法: 標準の Windows フォーム印刷ジョブを作成する'
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
ms.openlocfilehash: 816da93218e20f73f16c14769ed1a549dd3d8eb3
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59335408"
---
# <a name="how-to-create-standard-windows-forms-print-jobs"></a>方法: 標準の Windows フォーム印刷ジョブを作成する
Windows フォームにおける印刷の基盤は、<xref:System.Drawing.Printing.PrintDocument>コンポーネント、具体的には、<xref:System.Drawing.Printing.PrintDocument.PrintPage>イベント。 処理するコードを記述することで、<xref:System.Drawing.Printing.PrintDocument.PrintPage>イベント、印刷と印刷方法を指定できます。  
  
### <a name="to-create-a-print-job"></a>印刷ジョブを作成するには  
  
1. 追加、<xref:System.Drawing.Printing.PrintDocument>コンポーネントをフォームにします。  
  
2. <xref:System.Drawing.Printing.PrintDocument.PrintPage> イベントを処理するコードを記述します。  
  
     独自の印刷ロジックをコーディングする必要があります。 さらに、印刷する対象を指定する必要があります。  
  
     次のコード例で赤い四角形内にサンプル グラフィックを作成、<xref:System.Drawing.Printing.PrintDocument.PrintPage>印刷対象として機能するイベント ハンドラー。  
  
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
  
     (Visual # と[!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)])、イベント ハンドラーを登録するフォームのコンス トラクターで、次のコードを配置します。  
  
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
  
     コードを記述することも、<xref:System.Drawing.Printing.PrintDocument.BeginPrint>と<xref:System.Drawing.Printing.PrintDocument.EndPrint>などページの総数を表す印刷を整数デクリメントされる各ページの印刷イベント。  
  
    > [!NOTE]
    >  追加することができます、<xref:System.Windows.Forms.PrintDialog>コンポーネントをフォームをユーザーに、クリーンで効率的なユーザー インターフェイス (UI) を提供します。 設定、<xref:System.Windows.Forms.PrintDialog.Document%2A>のプロパティ、<xref:System.Windows.Forms.PrintDialog>コンポーネント有効にするドキュメントの印刷に関連するプロパティを設定することがフォーム上で使用します。 詳細については、<xref:System.Windows.Forms.PrintDialog>コンポーネントを参照してください[PrintDialog コンポーネント](../controls/printdialog-component-windows-forms.md)します。  
  
     Windows フォームの詳細詳細については、プログラムで印刷ジョブを作成する方法など、印刷ジョブを参照してください<xref:System.Drawing.Printing.PrintPageEventArgs>します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Printing.PrintDocument>
- [Windows フォームにおける印刷のサポート](windows-forms-print-support.md)
