---
title: '方法: SaveFileDialog コンポーネントを使用してファイルを保存する'
description: SaveFileDialog コンポーネントを使用してファイルシステムを参照し、保存するファイルを選択する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- saving files
- SaveFileDialog component [Windows Forms], saving files
- files [Windows Forms], saving
- OpenFile method [Windows Forms], saving files with SaveFileDialog component
ms.assetid: 02e8f409-b83f-4707-babb-e71f6b223d90
ms.openlocfilehash: cd773c3d4aa2b907eb09dd87c3fdbe138bf533bb
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904404"
---
# <a name="how-to-save-files-using-the-savefiledialog-component"></a>方法: SaveFileDialog コンポーネントを使用してファイルを保存する

この <xref:System.Windows.Forms.SaveFileDialog> コンポーネントを使用すると、ユーザーはファイルシステムを参照して、保存するファイルを選択できます。 このダイアログ ボックスは、ユーザーがダイアログ ボックス内で選択したファイルのパスと名前を返します。 ただし、ファイルを実際にディスクに書き込むためのコードを記述する必要があります。

### <a name="to-save-a-file-using-the-savefiledialog-component"></a>SaveFileDialog コンポーネントを使用してファイルを保存するには

- **[ファイルの保存]** ダイアログ ボックスを表示し、ユーザーによって選択されたファイルを保存するメソッドを呼び出します。

  <xref:System.Windows.Forms.SaveFileDialog>コンポーネントのメソッドを使用し <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> て、ファイルを保存します。 このメソッドは、 <xref:System.IO.Stream> 書き込み可能なオブジェクトを提供します。

  次の例では、プロパティを使用して <xref:System.Windows.Forms.DialogResult> ファイルの名前を取得し、メソッドを使用して <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> ファイルを保存します。 メソッドは、 <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> ファイルを書き込むストリームを提供します。

  次の例では、イメージが <xref:System.Windows.Forms.Button> 割り当てられたコントロールがあります。 このボタンをクリックすると、 <xref:System.Windows.Forms.SaveFileDialog> コンポーネントが、.gif、.jpeg、.bmp の種類のファイルを許可するフィルターでインスタンス化されます。 [ファイルの保存] ダイアログ ボックスでこれらの種類のファイルが選択されると、ボタンのイメージが保存されます。

  > [!IMPORTANT]
  > プロパティを取得または設定するには <xref:System.Windows.Forms.FileDialog.FileName%2A> 、アセンブリに、クラスによって付与された特権レベルが必要です <xref:System.Security.Permissions.FileIOPermission?displayProperty=nameWithType> 。 部分的に信頼されたコンテキストで実行している場合、プロセスは、特権がないために例外をスローする可能性があります。 詳しくは、「[コード アクセス セキュリティの基礎](../../misc/code-access-security-basics.md)」をご覧ください。

  この例では、フォームに、 <xref:System.Windows.Forms.Button> プロパティが <xref:System.Windows.Forms.ButtonBase.Image%2A> .gif、.jpeg、または .bmp のファイルに設定されたコントロールがあることを前提としています。

  > [!NOTE]
  > <xref:System.Windows.Forms.FileDialog>クラスの <xref:System.Windows.Forms.FileDialog.FilterIndex%2A> プロパティ (継承により、クラスに含まれる) は、 <xref:System.Windows.Forms.SaveFileDialog> 1 から始まるインデックスを使用します。 これは、ファイルをバイナリ形式ではなくプレーン テキストで保存する場合など、データを特定の形式で保存するコードを記述する場合に重要です。 このプロパティは、次のコード例に示されています。

  ```vb
  Private Sub Button2_Click(ByVal sender As System.Object, _
  ByVal e As System.EventArgs) Handles Button2.Click
      ' Displays a SaveFileDialog so the user can save the Image
      ' assigned to Button2.
      Dim saveFileDialog1 As New SaveFileDialog()
      saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif"
      saveFileDialog1.Title = "Save an Image File"
      saveFileDialog1.ShowDialog()

      ' If the file name is not an empty string open it for saving.
      If saveFileDialog1.FileName <> "" Then
        ' Saves the Image via a FileStream created by the OpenFile method.
        Dim fs As System.IO.FileStream = Ctype _
            (saveFileDialog1.OpenFile(), System.IO.FileStream)
        ' Saves the Image in the appropriate ImageFormat based upon the
        ' file type selected in the dialog box.
        ' NOTE that the FilterIndex property is one-based.
        Select Case saveFileDialog1.FilterIndex
            Case 1
              Me.button2.Image.Save(fs, _
                  System.Drawing.Imaging.ImageFormat.Jpeg)

            Case 2
              Me.button2.Image.Save(fs, _
                  System.Drawing.Imaging.ImageFormat.Bmp)

            Case 3
              Me.button2.Image.Save(fs, _
                  System.Drawing.Imaging.ImageFormat.Gif)
          End Select

          fs.Close()
      End If
  End Sub
  ```

  ```csharp
  private void button2_Click(object sender, System.EventArgs e)
  {
      // Displays a SaveFileDialog so the user can save the Image
      // assigned to Button2.
      SaveFileDialog saveFileDialog1 = new SaveFileDialog();
      saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";
      saveFileDialog1.Title = "Save an Image File";
      saveFileDialog1.ShowDialog();

      // If the file name is not an empty string open it for saving.
      if(saveFileDialog1.FileName != "")
      {
        // Saves the Image via a FileStream created by the OpenFile method.
        System.IO.FileStream fs =
            (System.IO.FileStream)saveFileDialog1.OpenFile();
        // Saves the Image in the appropriate ImageFormat based upon the
        // File type selected in the dialog box.
        // NOTE that the FilterIndex property is one-based.
        switch(saveFileDialog1.FilterIndex)
        {
            case 1 :
            this.button2.Image.Save(fs,
              System.Drawing.Imaging.ImageFormat.Jpeg);
            break;

            case 2 :
            this.button2.Image.Save(fs,
              System.Drawing.Imaging.ImageFormat.Bmp);
            break;

            case 3 :
            this.button2.Image.Save(fs,
              System.Drawing.Imaging.ImageFormat.Gif);
            break;
        }

      fs.Close();
      }
  }
  ```

  ```cpp
  private:
      System::Void button2_Click(System::Object ^ sender,
        System::EventArgs ^ e)
      {
        // Displays a SaveFileDialog so the user can save the Image
        // assigned to Button2.
        SaveFileDialog ^ saveFileDialog1 = new SaveFileDialog();
        saveFileDialog1->Filter =
            "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";
        saveFileDialog1->Title = "Save an Image File";
        saveFileDialog1->ShowDialog();
        // If the file name is not an empty string, open it for saving.
        if(saveFileDialog1->FileName != "")
        {
            // Saves the Image through a FileStream created by
            // the OpenFile method.
            System::IO::FileStream ^ fs =
              safe_cast\<System::IO::FileStream*>(
              saveFileDialog1->OpenFile());
            // Saves the Image in the appropriate ImageFormat based on
            // the file type selected in the dialog box.
            // Note that the FilterIndex property is one based.
            switch(saveFileDialog1->FilterIndex)
            {
              case 1 :
                  this->button2->Image->Save(fs,
                    System::Drawing::Imaging::ImageFormat::Jpeg);
                  break;
              case 2 :
                  this->button2->Image->Save(fs,
                    System::Drawing::Imaging::ImageFormat::Bmp);
                  break;
              case 3 :
                  this->button2->Image->Save(fs,
                    System::Drawing::Imaging::ImageFormat::Gif);
                  break;
            }
        fs->Close();
        }
      }
  ```

  (Visual C# および Visual C++)フォームのコンストラクターに次のコードを配置して、イベントハンドラーを登録します。

  ```csharp
  this.button2.Click += new System.EventHandler(this.button2_Click);
  ```

  ```cpp
  this->button2->Click += gcnew
      System::EventHandler(this, &Form1::button2_Click);
  ```

  ファイルストリームの書き込みの詳細については、「」および「」を参照してください <xref:System.IO.FileStream.BeginWrite%2A> <xref:System.IO.FileStream.Write%2A> 。

  > [!NOTE]
  > コントロールなどの特定のコントロールに <xref:System.Windows.Forms.RichTextBox> は、ファイルを保存する機能があります。

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Windows.Forms.SaveFileDialog>
- [SaveFileDialog コンポーネント](savefiledialog-component-windows-forms.md)
