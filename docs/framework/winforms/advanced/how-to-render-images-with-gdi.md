---
title: '方法 : GDI+ を使用してイメージをレンダリングする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- images [Windows Forms], creating
- GDI+, rendering existing images
ms.assetid: c128b79a-3e31-47d8-9e66-3470f570a056
ms.openlocfilehash: fffe1f1052d7323d234985b7e752866f2e89657d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182503"
---
# <a name="how-to-render-images-with-gdi"></a>方法 : GDI+ を使用してイメージをレンダリングする
GDI+ を使用して、アプリケーション内のファイルとして存在するイメージをレンダリングできます。 そのためには、<xref:System.Drawing.Image><xref:System.Drawing.Bitmap>クラスの新しいオブジェクト (など) を作成し、<xref:System.Drawing.Graphics>使用する描画サーフェイスを参照するオブジェクトを作成し、オブジェクトの<xref:System.Drawing.Graphics.DrawImage%2A>メソッドを<xref:System.Drawing.Graphics>呼び出します。 イメージは、グラフィックス クラスで表される描画サーフェイス上に描画されます。 イメージ エディターを使用すると、デザイン時にイメージ ファイルを作成および編集し、実行時に GDI+ でレンダリングできます。 詳細については、「[アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)」を参照してください。  
  
### <a name="to-render-an-image-with-gdi"></a>GDI + を使用してイメージをレンダリングするには  
  
1. 表示するイメージを表すオブジェクトを作成します。 このオブジェクトは、<xref:System.Drawing.Image>や<xref:System.Drawing.Bitmap><xref:System.Drawing.Imaging.Metafile>などから継承するクラスのメンバーである必要があります。 次に例を示します。  
  
    ```vb  
    ' Uses the System.Environment.GetFolderPath to get the path to the
    ' current user's MyPictures folder.  
    Dim myBitmap as New Bitmap _  
       (System.Environment.GetFolderPath _  
          (System.Environment.SpecialFolder.MyPictures))  
    ```  
  
    ```csharp  
    // Uses the System.Environment.GetFolderPath to get the path to the
    // current user's MyPictures folder.  
    Bitmap myBitmap = new Bitmap  
       (System.Environment.GetFolderPath  
          (System.Environment.SpecialFolder.MyPictures));  
    ```  
  
    ```cpp  
    // Uses the System.Environment.GetFolderPath to get the path to the
    // current user's MyPictures folder.  
    Bitmap^ myBitmap = gcnew Bitmap  
       (System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::MyPictures));  
    ```  
  
2. 使用する<xref:System.Drawing.Graphics>描画サーフェイスを表すオブジェクトを作成します。 詳細については、「[方法 : 描画する Graphics オブジェクトを作成する](how-to-create-graphics-objects-for-drawing.md)」を参照してください。  
  
    ```vb  
    ' Creates a Graphics object that represents the drawing surface of
    ' Button1.  
    Dim g as Graphics = Button1.CreateGraphics  
    ```  
  
    ```csharp  
    // Creates a Graphics object that represents the drawing surface of
    // Button1.  
    Graphics g = Button1.CreateGraphics();  
    ```  
  
    ```cpp  
    // Creates a Graphics object that represents the drawing surface of
    // Button1.  
    Graphics^ g = button1->CreateGraphics();  
    ```  
  
3. グラフィックス<xref:System.Drawing.Graphics.DrawImage%2A>オブジェクトを呼び出して、イメージをレンダリングします。 描画対象のイメージとイメージを描画する場所の座標を指定する必要があります。  
  
    ```vb  
    g.DrawImage(myBitmap, 1, 1)  
    ```  
  
    ```csharp  
    g.DrawImage(myBitmap, 1, 1);  
    ```  
  
    ```cpp  
    g->DrawImage(myBitmap, 1, 1);  
    ```  
  
## <a name="see-also"></a>関連項目

- [グラフィックス プログラミングについて](getting-started-with-graphics-programming.md)
- [方法 : 描画する Graphics オブジェクトを作成する](how-to-create-graphics-objects-for-drawing.md)
- [GDI+ でのペン、直線、および四角形](pens-lines-and-rectangles-in-gdi.md)
- [方法 : Windows フォームにテキストを描画する](how-to-draw-text-on-a-windows-form.md)
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [線または閉じた図形の描画](/cpp/windows/drawing-lines-or-closed-figures-image-editor-for-icons)
- [アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)
