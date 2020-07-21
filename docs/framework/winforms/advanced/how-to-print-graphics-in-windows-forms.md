---
title: '方法 : グラフィックスを印刷する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- graphics [Windows Forms], printing
- printing [Windows Forms], graphics
ms.assetid: 32b891e6-52ff-4fea-a9ff-2ce5db20a4c6
ms.openlocfilehash: 15f3a507839430ce058302e7f5abd317ef84626f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182538"
---
# <a name="how-to-print-graphics-in-windows-forms"></a>方法 : Windows フォームでグラフィックスを印刷する
多くの場合、Windows ベースのアプリケーションでグラフィックスを印刷する必要があります。 この<xref:System.Drawing.Graphics>クラスには、画面やプリンタなどのデバイスにオブジェクトを描画するためのメソッドが用意されています。  
  
### <a name="to-print-graphics"></a>グラフィックスを印刷するには  
  
1. フォームに<xref:System.Drawing.Printing.PrintDocument>コンポーネントを追加します。  
  
2. <xref:System.Drawing.Printing.PrintDocument.PrintPage>イベント ハンドラーで、クラスの<xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A>プロパティを<xref:System.Drawing.Printing.PrintPageEventArgs>使用して、印刷するグラフィックスの種類をプリンターに指示します。  
  
     外接する四角形内に青い楕円を作成するために使用するイベント ハンドラーのコード例を次に示します。 長方形の位置と寸法は、100 から始まり、幅が 250、高さが 250 の 150 から始まる。  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillEllipse(Brushes.Blue, New Rectangle(100, 150, 250, 250))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Blue,
         new Rectangle(100, 150, 250, 250));  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Blue,  
             Rectangle(100, 150, 250, 250));  
       }  
    ```  
  
     (ビジュアル C# およびビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    ```  
  
    ```cpp  
    this->printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Brush>
- [Windows フォームにおける印刷のサポート](windows-forms-print-support.md)
