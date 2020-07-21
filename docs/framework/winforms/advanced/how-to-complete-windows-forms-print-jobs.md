---
title: 印刷ジョブの完了
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print jobs [Windows Forms], completing in Windows Forms
- printing [Windows Forms], print jobs
ms.assetid: 23ec74f7-34c5-4710-82a0-ee2914518548
ms.openlocfilehash: 62f67002bfbaf46e73bae06fdaff26efde865c06
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182595"
---
# <a name="how-to-complete-windows-forms-print-jobs"></a>方法 : Windows フォームの印刷ジョブを完了する
多くの場合、印刷に関連するワード プロセッサやその他のアプリケーションでは、印刷ジョブが完了したことを示すメッセージをユーザーに表示するオプションが提供されます。 コンポーネントの<xref:System.Drawing.Printing.PrintDocument.EndPrint>イベントを処理することで、Windows フォームでこの機能を<xref:System.Drawing.Printing.PrintDocument>提供できます。  
  
 次の手順では、<xref:System.Drawing.Printing.PrintDocument>コンポーネントを含む Windows ベースのアプリケーションを作成する必要があります。 コンポーネントを使用して Windows フォームから印刷<xref:System.Drawing.Printing.PrintDocument>する方法の詳細については、「[方法 : 標準の Windows フォーム印刷ジョブを作成する](how-to-create-standard-windows-forms-print-jobs.md)」を参照してください。  
  
### <a name="to-complete-a-print-job"></a>印刷ジョブを完了するには  
  
1. コンポーネントの<xref:System.Drawing.Printing.PrintDocument.DocumentName%2A>プロパティを<xref:System.Drawing.Printing.PrintDocument>設定します。  
  
    ```vb  
    PrintDocument1.DocumentName = "MyTextFile"  
    ```  
  
    ```csharp  
    printDocument1.DocumentName = "MyTextFile";  
    ```  
  
    ```cpp  
    printDocument1->DocumentName = "MyTextFile";  
    ```  
  
2. <xref:System.Drawing.Printing.PrintDocument.EndPrint> イベントを処理するコードを記述します。  
  
     次のコード例では、ドキュメントの印刷が完了したことを示すメッセージ ボックスが表示されます。  
  
    ```vb  
    Private Sub PrintDocument1_EndPrint(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintEventArgs) Handles PrintDocument1.EndPrint  
       MessageBox.Show(PrintDocument1.DocumentName + " has finished printing.")  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_EndPrint(object sender,
    System.Drawing.Printing.PrintEventArgs e)  
    {  
       MessageBox.Show(printDocument1.DocumentName +
          " has finished printing.");  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_EndPrint(System::Object ^ sender,  
          System::Drawing::Printing::PrintEventArgs ^ e)  
       {  
          MessageBox::Show(String::Concat(printDocument1->DocumentName,  
             " has finished printing."));  
       }  
    ```  
  
     (ビジュアル C# およびビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.printDocument1.EndPrint += new  
       System.Drawing.Printing.PrintEventHandler  
       (this.printDocument1_EndPrint);  
    ```  
  
    ```cpp  
    this->printDocument1->EndPrint += gcnew  
       System::Drawing::Printing::PrintEventHandler  
       (this, &Form1::printDocument1_EndPrint);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Printing.PrintDocument>
- [Windows フォームにおける印刷のサポート](windows-forms-print-support.md)
