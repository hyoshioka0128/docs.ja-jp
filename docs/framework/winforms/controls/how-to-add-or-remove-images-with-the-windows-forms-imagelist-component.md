---
title: イメージリスト コンポーネントを使用したイメージの追加または削除
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- images [Windows Forms], removing from ImageList component
- images [Windows Forms], storing for controls
- ImageList component [Windows Forms], adding images
- ImageList component [Windows Forms], removing images
- images [Windows Forms], adding to ImageList component
- images [Windows Forms], displaying with controls
ms.assetid: c5eacc56-f769-4e2e-bfb7-f756620913db
ms.openlocfilehash: e045be7ea9407bc379b0c22282fcd2184ff5db51
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182297"
---
# <a name="how-to-add-or-remove-images-with-the-windows-forms-imagelist-component"></a>方法 : Windows フォームの ImageList コンポーネントにイメージを追加または削除する
Windows フォーム<xref:System.Windows.Forms.ImageList>コンポーネントは、通常、コントロールに関連付けられる前にイメージを設定します。 ただし、イメージ リストをコントロールに関連付けた後で、イメージを追加および削除できます。  
  
> [!NOTE]
> イメージを削除する場合は、関連<xref:System.Windows.Forms.ButtonBase.ImageIndex%2A>付けられているコントロールのプロパティがまだ有効であることを確認します。  
  
### <a name="to-add-images-programmatically"></a>プログラムでイメージを追加するには  
  
- イメージ<xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A>リストの<xref:System.Windows.Forms.ImageList.Images%2A>プロパティのメソッドを使用します。  
  
     次のコード例では、イメージの場所に設定されているパスは**マイ ドキュメント**フォルダーです。 この場所は、Windows オペレーティング システムを実行しているほとんどのコンピュータにこのフォルダが含まれると仮定できるため、使用されます。 この場所を選択すると、最小限のシステム アクセス レベルを持つユーザーがアプリケーションをより安全に実行できるようになります。 次のコード例では、コントロールが既に追加されている<xref:System.Windows.Forms.ImageList>フォームが必要です。  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    End Sub  
    ```  
  
    ```csharp  
    public void addImage()  
    {  
    // Be sure that you use an appropriate escape sequence (such as the
    // @) when specifying the location of the file.  
       System.Drawing.Image myImage =
         Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
    }  
    ```  
  
    ```cpp  
    public:  
       void addImage()  
       {  
       // Replace the bold image in the following sample
       // with your own icon.  
       // Be sure that you use an appropriate escape sequence (such as
       // \\) when specifying the location of the file.  
          System::Drawing::Image ^ myImage =
             Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
       }  
    ```  
  
### <a name="to-add-images-with-a-key-value"></a>キー値を持つイメージを追加します。  
  
- キー値を<xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A>受け取るイメージ リストの<xref:System.Windows.Forms.ImageList.Images%2A>プロパティのいずれかのメソッドを使用します。  
  
     次のコード例では、イメージの場所に設定されているパスは**マイ ドキュメント**フォルダーです。 この場所は、Windows オペレーティング システムを実行しているほとんどのコンピュータにこのフォルダが含まれると仮定できるため、使用されます。 この場所を選択すると、最小限のシステム アクセス レベルを持つユーザーがアプリケーションをより安全に実行できるようになります。 次のコード例では、コントロールが既に追加されている<xref:System.Windows.Forms.ImageList>フォームが必要です。  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add("myPhoto", myImage)  
    End Sub  
    ```  
  
```csharp  
public void addImage()  
{  
// Be sure that you use an appropriate escape sequence (such as the
// @) when specifying the location of the file.  
   System.Drawing.Image myImage =
     Image.FromFile  
   (System.Environment.GetFolderPath  
   (System.Environment.SpecialFolder.Personal)  
   + @"\Image.gif");  
   imageList1.Images.Add("myPhoto", myImage);  
}  
```  
  
### <a name="to-remove-all-images-programmatically"></a>プログラムによってすべてのイメージを削除するには  
  
- このメソッド<xref:System.Windows.Forms.ImageList.ImageCollection.Remove%2A>を使用して 1 つのイメージを削除する  
  
     、または-  
  
     この方法<xref:System.Windows.Forms.ImageList.ImageCollection.Clear%2A>を使用して、イメージ リスト内のすべてのイメージをクリアします。  
  
    ```vb  
    ' Removes the first image in the image list  
    ImageList1.Images.Remove(myImage)  
    ' Clears all images in the image list  
    ImageList1.Images.Clear()  
    ```  
  
```csharp  
// Removes the first image in the image list.  
imageList1.Images.Remove(myImage);  
// Clears all images in the image list.  
imageList1.Images.Clear();  
```  
  
### <a name="to-remove-images-by-key"></a>キーでイメージを削除するには  
  
- このメソッド<xref:System.Windows.Forms.ImageList.ImageCollection.RemoveByKey%2A>を使用して、キーで 1 つのイメージを削除します。  
  
    ```vb  
    ' Removes the image named "myPhoto" from the list.  
    ImageList1.Images.RemoveByKey("myPhoto")  
    ```  
  
```csharp  
// Removes the image named "myPhoto" from the list.  
imageList1.Images.RemoveByKey("myPhoto");  
```  
  
## <a name="see-also"></a>関連項目

- [ImageList コンポーネント](imagelist-component-windows-forms.md)
- [ImageList コンポーネントの概要](imagelist-component-overview-windows-forms.md)
- [イメージ、ビットマップ、およびメタファイル](../advanced/images-bitmaps-and-metafiles.md)
