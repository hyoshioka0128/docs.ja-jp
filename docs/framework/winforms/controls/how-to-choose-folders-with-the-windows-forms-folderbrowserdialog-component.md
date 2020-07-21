---
title: FolderBrowserDialog コンポーネントを使用したフォルダーの選択
description: 作成した Windows アプリケーション内で Windows フォーム FolderBrowserDialog コンポーネントを使用して、ユーザーにフォルダーの選択を求める方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- directories [Windows Forms], choosing
- FolderBrowserDialog component [Windows Forms], choosing directories
- folders [Windows Forms], selecting
- folders [Windows Forms], choosing
- directories [Windows Forms], selecting
ms.assetid: 4593670e-7c7d-4661-b46b-4ffb63258adb
ms.openlocfilehash: 11d01bbaec3b82bc221960ebab5e33ca1aa302db
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903676"
---
# <a name="how-to-choose-folders-with-the-windows-forms-folderbrowserdialog-component"></a>方法: Windows フォーム FolderBrowserDialog コンポーネントを使用してフォルダーを選択する

多くの場合、作成した Windows アプリケーション内で、フォルダーを選択するようにユーザーに促す必要があります。とりわけ、一連のファイルを保存するように求める場合が多いです。 Windows フォーム <xref:System.Windows.Forms.FolderBrowserDialog> コンポーネントを使用すると、このタスクを簡単に実行できます。

### <a name="to-choose-folders-with-the-folderbrowserdialog-component"></a>FolderBrowserDialog コンポーネントを使用してフォルダーを選択するには

1. プロシージャで、コンポーネントのプロパティを調べて、 <xref:System.Windows.Forms.FolderBrowserDialog> <xref:System.Windows.Forms.Form.DialogResult%2A> ダイアログボックスがどのように閉じられたかを確認し、コンポーネントのプロパティの値を取得し <xref:System.Windows.Forms.FolderBrowserDialog> <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> ます。

2. ダイアログボックスのツリービュー内に表示される最上位のフォルダーを設定する必要がある場合は、 <xref:System.Windows.Forms.FolderBrowserDialog.RootFolder%2A> 列挙体のメンバーを取得するプロパティを設定し <xref:System.Environment.SpecialFolder> ます。

3. また、プロパティを設定することもできます。このプロパティは、 <xref:System.Windows.Forms.FolderBrowserDialog.Description%2A> フォルダーブラウザーのツリービューの上部に表示されるテキスト文字列を指定します。

    次の例では、 <xref:System.Windows.Forms.FolderBrowserDialog> Visual Studio でプロジェクトを作成する場合と同様に、コンポーネントを使用してフォルダーを選択し、保存先のフォルダーを選択するように求められます。 この例では、フォルダー名が <xref:System.Windows.Forms.TextBox> フォーム上のコントロールに表示されます。 <xref:System.Windows.Forms.TextBox>エラーやその他の問題が発生した場合にユーザーが選択内容を編集できるように、コントロールなどの編集可能な領域に場所を配置することをお勧めします。 この例では、コンポーネントとコントロールを含むフォームが想定されてい <xref:System.Windows.Forms.FolderBrowserDialog> <xref:System.Windows.Forms.TextBox> ます。

    ```vb
    Public Sub ChooseFolder()
        If FolderBrowserDialog1.ShowDialog() = DialogResult.OK Then
            TextBox1.Text = FolderBrowserDialog1.SelectedPath
        End If
    End Sub
    ```

    ```csharp
    public void ChooseFolder()
    {
        if (folderBrowserDialog1.ShowDialog() == DialogResult.OK)
        {
            textBox1.Text = folderBrowserDialog1.SelectedPath;
        }
    }
    ```

    ```cpp
    public:
       void ChooseFolder()
       {
          if (folderBrowserDialog1->ShowDialog() == DialogResult::OK)
          {
             textBox1->Text = folderBrowserDialog1->SelectedPath;
          }
       }
    ```

    > [!IMPORTANT]
    > このクラスを使用するには、アセンブリに、 <xref:System.Security.Permissions.FileIOPermissionAttribute.PathDiscovery%2A> 列挙体の一部であるプロパティによって付与される特権レベルが必要です <xref:System.Security.Permissions.FileIOPermissionAccess> 。 部分的に信頼されたコンテキストで実行している場合、プロセスは、特権がないため例外をスローする可能性があります。 詳しくは、「[コード アクセス セキュリティの基礎](../../misc/code-access-security-basics.md)」をご覧ください。

ファイルの保存方法については、「[方法: SaveFileDialog コンポーネントを使用してファイルを保存する](how-to-save-files-using-the-savefiledialog-component.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Windows.Forms.FolderBrowserDialog>
- [FolderBrowserDialog コンポーネントの概要 (Windows フォーム)](folderbrowserdialog-component-overview-windows-forms.md)
- [FolderBrowserDialog コンポーネント](folderbrowserdialog-component-windows-forms.md)
