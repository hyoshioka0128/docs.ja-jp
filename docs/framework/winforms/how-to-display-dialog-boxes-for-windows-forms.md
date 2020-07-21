---
title: '[方法] ダイアログ ボックスを表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, displaying
- Windows Forms dialog boxes [Windows Forms], displaying
- Windows Forms, calling one form from another
- dialog boxes [Windows Forms], displaying for Windows Forms
ms.assetid: aaac1b38-c651-495a-8d3d-5a9bfb32fee3
ms.openlocfilehash: 3625080c7c322e297a9de92e4f95a40c0caf3e72
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181970"
---
# <a name="how-to-display-dialog-boxes-for-windows-forms"></a>方法 : Windows フォームのダイアログ ボックスを表示する
ダイアログ ボックスは、アプリケーションで他のフォームを表示する場合と同じ方法で表示します。 アプリケーションの実行時にスタートアップ フォームが自動的に読み込まれます。 アプリケーションに 2 番目のフォームまたはダイアログ ボックスを表示するには、読み込んで表示するコードを記述します。 同様に、フォームまたはダイアログ ボックスを非表示にするには、アンロードまたは非表示にするコードを記述します。  
  
### <a name="to-display-a-dialog-box"></a>ダイアログ ボックスを表示するには  
  
1. ダイアログ ボックスを開くイベント ハンドラーに移動します。 これは、メニュー コマンドが選択されたとき、ボタンがクリックされたとき、またはその他のイベントが発生したときに発生します。  
  
2. イベント ハンドラーで、ダイアログ ボックスを開くコードを追加します。 この例では、ボタンクリックイベントを使用してダイアログ ボックスを表示します。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim dlg1 as new Form()  
       dlg1.ShowDialog()  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)
    {  
       Form dlg1 = new Form();  
       dlg1.ShowDialog();  
    }  
    ```  
  
    ```cpp  
    private:
      void button1_Click(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        Form ^ dlg1 = gcnew Form();  
        dlg1->ShowDialog();  
      }  
    ```
