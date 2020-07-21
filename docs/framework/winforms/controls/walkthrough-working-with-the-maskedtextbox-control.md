---
title: 'チュートリアル : MaskedTextBox コントロールの使用'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- input [Windows Forms], controlling to ensure validity
- MaskedTextBox control [Windows Forms], walkthroughs
- MaskedTextBox control [Windows Forms], validation
- user input [Windows Forms], controlling
- text [Windows Forms], controls for input
ms.assetid: df60565e-5447-4110-92a6-be1f6ff5faa3
ms.openlocfilehash: db32b3ec88a07747ea3e286af9f04edce3f1ba3b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182052"
---
# <a name="walkthrough-working-with-the-maskedtextbox-control"></a>チュートリアル : MaskedTextBox コントロールの使用
このチュートリアルでは、以下のタスクを行います。  
  
- コントロールの<xref:System.Windows.Forms.MaskedTextBox>初期化  
  
- 文字が<xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected>マスクに準拠していない場合にイベント ハンドラーを使用してユーザーに警告する  
  
- <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A>プロパティに型を割り当て、イベント<xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted>ハンドラーを使用して、コミットしようとしている値が型に対して無効な場合にユーザーに警告する  
  
## <a name="creating-the-project-and-adding-a-control"></a>プロジェクトの作成とコントロールの追加  
  
#### <a name="to-add-a-maskedtextbox-control-to-your-form"></a>フォームにマスクテキスト ボックス コントロールを追加するには  
  
1. <xref:System.Windows.Forms.MaskedTextBox>コントロールを配置するフォームを開きます。  
  
2. <xref:System.Windows.Forms.MaskedTextBox>**ツールボックス**からフォームにコントロールをドラッグします。  
  
3. コントロールを右クリックし、[**プロパティ]** をクリックします。 [**プロパティ]** ウィンドウで **、Mask**プロパティを選択し、プロパティ名の横にある **[...]** (省略記号) ボタンをクリックします。  
  
4. [**定型入力**] ダイアログ ボックスで、[**短い日付**] マスクを選択し **、[OK]** をクリックします。  
  
5. **[プロパティ]** ウィンドウで<xref:System.Windows.Forms.MaskedTextBox.BeepOnError%2A>プロパティを`true`に設定します。 このプロパティを使用すると、マスク定義に違反する文字を入力しようとすると、短いビープ音が鳴ります。  
  
 Mask プロパティがサポートする文字の概要については、プロパティの「解説」セクションを<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>参照してください。  
  
## <a name="alert-the-user-to-input-errors"></a>ユーザーにエラー入力を警告する  
  
#### <a name="add-a-balloon-tip-for-rejected-mask-input"></a>拒否されたマスク入力のバルーン ヒントを追加する  
  
1. **ツールボックス**に戻り、 フォーム<xref:System.Windows.Forms.ToolTip>に を追加します。  
  
2. 入力エラー<xref:System.Windows.Forms.ToolTip>が発生したときにイベント<xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected>を発生させるイベント ハンドラーを作成します。 バルーン ヒントは、5 秒間、またはユーザーがクリックするまで表示されます。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)
    {  
        ... // Other initialization code  
        maskedTextBox1.Mask = "00/00/0000";  
        maskedTextBox1.MaskInputRejected += new MaskInputRejectedEventHandler(maskedTextBox1_MaskInputRejected)  
    }  
  
    void maskedTextBox1_MaskInputRejected(object sender, MaskInputRejectedEventArgs e)  
    {  
        toolTip1.ToolTipTitle = "Invalid Input";  
        toolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", maskedTextBox1, maskedTextBox1.Location, 5000);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load  
        Me.ToolTip1.IsBalloon = True  
        Me.MaskedTextBox1.Mask = "00/00/0000"  
    End Sub  
  
    Private Sub MaskedTextBox1_MaskInputRejected(sender as Object, e as MaskInputRejectedEventArgs) Handles MaskedTextBox1.MaskInputRejected  
        ToolTip1.ToolTipTitle = "Invalid Input"  
        ToolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", MaskedTextBox1, 5000)  
    End Sub  
    ```  
  
## <a name="alert-the-user-to-a-type-that-is-not-valid"></a>無効な型をユーザーに通知する  
  
#### <a name="add-a-balloon-tip-for-invalid-data-types"></a>無効なデータ型のバルーン ヒントを追加する  
  
1. フォーム<xref:System.Windows.Forms.Form.Load>のイベント ハンドラで、<xref:System.Type><xref:System.DateTime>型を表すオブジェクトをコントロールの<xref:System.Windows.Forms.MaskedTextBox><xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A>プロパティに割り当てます。  
  
    ```csharp  
    private void Form1_Load(Object sender, EventArgs e)  
    {  
        // Other code  
        maskedTextBox1.ValidatingType = typeof(System.DateTime);  
        maskedTextBox1.TypeValidationCompleted += new TypeValidationEventHandler(maskedTextBox1_TypeValidationCompleted);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(sender as Object, e as EventArgs)  
        // Other code  
        MaskedTextBox1.ValidatingType = GetType(System.DateTime)  
    End Sub  
    ```  
  
2. <xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted> イベントのイベント ハンドラーを追加します。  
  
    ```csharp  
    public void maskedTextBox1_TypeValidationCompleted(object sender, TypeValidationEventArgs e)  
    {  
        if (!e.IsValidInput)  
        {  
           toolTip1.ToolTipTitle = "Invalid Date Value";  
           toolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000);  
           e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Public Sub MaskedTextBox1_TypeValidationCompleted(sender as Object, e as TypeValidationEventArgs)  
        If Not e.IsValidInput Then  
           ToolTip1.ToolTipTitle = "Invalid Date Value"  
           ToolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000)  
           e.Cancel = True  
        End If  
    End Sub  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.MaskedTextBox>
- [MaskedTextBox コントロール](maskedtextbox-control-windows-forms.md)
