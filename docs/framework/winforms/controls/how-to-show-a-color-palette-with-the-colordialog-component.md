---
title: '方法 : ColorDialog コンポーネントを使用してカラー パレットを表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- palettes [Windows Forms], showing color
- color dialog box [Windows Forms], showing color palettes
- colors [Windows Forms], allowing users to select
- color palettes [Windows Forms], dialog box
- ColorDialog component [Windows Forms], showing color palettes
- color palettes [Windows Forms], showing in ColorDialog component
- colors [Windows Forms], showing palettes
ms.assetid: ee050f61-dbc8-4436-ba22-51360981ab48
ms.openlocfilehash: 0406ef7a32678bd149c0024348a7adf1f0b72926
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141784"
---
# <a name="how-to-show-a-color-palette-with-the-colordialog-component"></a>方法 : ColorDialog コンポーネントを使用してカラー パレットを表示する
[ColorDialog](colordialog-component-windows-forms.md)コンポーネントは、色のパレットを表示し、ユーザーが選択した色を含むプロパティを返します。  
  
### <a name="to-choose-a-color-using-the-colordialog-component"></a>色ダイアログ コンポーネントを使用して色を選択するには  
  
1. メソッドを使用してダイアログ<xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>ボックスを表示します。  
  
2. このプロパティ<xref:System.Windows.Forms.DialogResult>を使用して、ダイアログ ボックスがどのように閉じられたかを調べます。  
  
3. コンポーネントの<xref:System.Windows.Forms.ColorDialog.Color%2A>プロパティを使用<xref:System.Windows.Forms.ColorDialog>して、選択した色を設定します。  
  
     次の例では、コントロール<xref:System.Windows.Forms.Button>のイベント<xref:System.Windows.Forms.Control.Click>ハンドラーによってコンポーネントが<xref:System.Windows.Forms.ColorDialog>開きます。 色を選択し、ユーザーが **[OK]** を<xref:System.Windows.Forms.Button>クリックすると、コントロールの背景色が選択した色に設定されます。 この例では、フォームに<xref:System.Windows.Forms.Button>コントロールとコンポーネントが<xref:System.Windows.Forms.ColorDialog>含まれています。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       If ColorDialog1.ShowDialog() = DialogResult.OK Then  
          Button1.BackColor = ColorDialog1.Color  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(colorDialog1.ShowDialog() == DialogResult.OK)  
       {  
          button1.BackColor = colorDialog1.Color;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,
          System::EventArgs ^ e)  
       {  
          if(colorDialog1->ShowDialog() == DialogResult::OK)  
          {  
             button1->BackColor = colorDialog1->Color;  
          }  
       }  
    ```  
  
     (ビジュアル C#、ビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click +=
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog コンポーネント](colordialog-component-windows-forms.md)
