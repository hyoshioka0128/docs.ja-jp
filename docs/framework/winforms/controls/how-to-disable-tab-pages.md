---
title: '方法 : タブ ページを無効化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tab pages [Windows Forms], hiding in forms
- TabControl control [Windows Forms], disabling pages
ms.assetid: adcc6618-8a34-4ee1-bbe3-47e732de6a59
ms.openlocfilehash: 9074aedb81a485267dc4faff92e0fe8d0d3b467f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182174"
---
# <a name="how-to-disable-tab-pages"></a>方法 : タブ ページを無効化する
Windows フォーム アプリケーション内で使用できるデータへのアクセスを制限する場合があります。 この例の 1 つとして、タブ コントロールのタブ ページにデータが表示されている場合があります。管理者は、ゲストレベルまたは下位レベルのユーザーから制限する必要がある情報をタブ ページに含める場合があります。  
  
### <a name="to-disable-tab-pages-programmatically"></a>プログラムでタブ ページを無効にするには  
  
1. タブ コントロールのイベントを処理するコード<xref:System.Windows.Forms.TabControl.SelectedIndexChanged>を記述します。 これは、ユーザーがタブを切り替えたときに発生するイベントです。  
  
2. 資格情報を確認します。 表示される情報によっては、ユーザーがログインしたユーザー名や、ユーザーがタブを表示できるようにする前に、その他の形式の資格情報を確認する必要があります。  
  
3. ユーザーが適切な資格情報を持っている場合は、クリックされたタブを表示します。 ユーザーが適切な資格情報を持っていない場合は、アクセス権を持っていないというメッセージ ボックスまたはその他のユーザー インターフェイスを表示し、最初のタブに戻ります。  
  
    > [!NOTE]
    > この機能を実稼働アプリケーションに実装する場合、フォームの<xref:System.Windows.Forms.Form.Load>イベント中にこの資格情報チェックを実行できます。 これにより、ユーザーインターフェイスが表示される前にタブを非表示にすることが可能になり、プログラミングに対するはるかにクリーンなアプローチです。 以下で使用する方法 (資格情報の確認、イベント中のタブの<xref:System.Windows.Forms.TabControl.SelectedIndexChanged>無効化) は、説明の目的で使用されます。  
  
4. 必要に応じて、3 つ以上のタブ ページがある場合は、元のタブ ページとは異なるタブ ページを表示します。  
  
     次の例では、タブ<xref:System.Windows.Forms.CheckBox>へのアクセス基準はアプリケーションによって異なるため、資格情報をチェックする代わりにコントロールが使用されます。 <xref:System.Windows.Forms.TabControl.SelectedIndexChanged>イベントが発生した場合、資格情報チェックが true (つまり、チェック ボックスがチェックされている) で、選択された`TabPage2`タブ (この例では機密情報が含まれているタブ)`TabPage2`が表示されます。 それ以外`TabPage3`の場合は、適切なアクセス権を持っていなかったことを示すメッセージ ボックスが表示されます。 次のコードでは、<xref:System.Windows.Forms.CheckBox>コントロール ( )`CredentialCheck`と<xref:System.Windows.Forms.TabControl>3 つのタブ ページを持つコントロールを持つフォームを想定しています。  
  
    ```vb  
    Private Sub TabControl1_SelectedIndexChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles TabControl1.SelectedIndexChanged  
       ' Check Credentials Here  
  
       If CredentialCheck.Checked = True And _
       TabControl1.SelectedTab Is TabPage2 Then  
          TabControl1.SelectedTab = TabPage2  
       ElseIf CredentialCheck.Checked = False _
       And TabControl1.SelectedTab Is TabPage2 Then  
          MessageBox.Show _
         ("Unable to load tab. You have insufficient access privileges.")  
          TabControl1.SelectedTab = TabPage3  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void tabControl1_SelectedIndexChanged(object sender, System.EventArgs e)  
    {  
        // Check Credentials Here  
  
        if ((CredentialCheck.Checked == true) && (tabControl1.SelectedTab == tabPage2))
        {  
            tabControl1.SelectedTab = tabPage2;  
        }  
        else if ((CredentialCheck.Checked == false) && (tabControl1.SelectedTab == tabPage2))  
        {  
            MessageBox.Show("Unable to load tab. You have insufficient access privileges.");  
            tabControl1.SelectedTab = tabPage3;  
        }  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void tabControl1_SelectedIndexChanged(  
          System::Object ^ sender,  
          System::EventArgs ^  e)  
       {  
          // Check Credentials Here  
          if ((CredentialCheck->Checked == true) &&  
              (tabControl1->SelectedTab == tabPage2))  
          {  
             tabControl1->SelectedTab = tabPage2;  
          }  
          else if ((CredentialCheck->Checked == false) &&  
                   (tabControl1->SelectedTab == tabPage2))  
          {  
             MessageBox::Show(String::Concat("Unable to load tab. ",  
                "You have insufficient access privileges."));  
             tabControl1->SelectedTab = tabPage3;  
          }  
       }  
    ```  
  
     (ビジュアル C#、ビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.tabControl1.SelectedIndexChanged +=
       new System.EventHandler(this.tabControl1_SelectedIndexChanged);  
    ```  
  
    ```cpp  
    this->tabControl1->SelectedIndexChanged +=  
       gcnew System::EventHandler(this, &Form1::tabControl1_SelectedIndexChanged);  
    ```  
  
## <a name="see-also"></a>関連項目

- [TabControl コントロールの概要](tabcontrol-control-overview-windows-forms.md)
- [方法 : タブ ページにコントロールを追加する](how-to-add-a-control-to-a-tab-page.md)
- [方法 : Windows フォーム TabControl のタブを追加および削除する](how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)
- [方法 : Windows フォーム TabControl の表示形式を変更する](how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)
