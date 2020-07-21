---
title: '方法: 描画する Graphics オブジェクトを作成する'
description: GDI + を使用して、線や図形を描画したり、テキストをレンダリングしたり、イメージを表示および操作したりするために必要なグラフィックオブジェクトを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- graphics [Windows Forms], creating
- images [Windows Forms], creating
- GDI+, creating images
ms.assetid: 162861f9-f050-445e-8abb-b2c43a918b8b
ms.openlocfilehash: 1a0884c1e9956dc6f4608e32372deeea24ef4670
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903208"
---
# <a name="how-to-create-graphics-objects-for-drawing"></a>方法: 描画する Graphics オブジェクトを作成する
GDI + を使用して、線や形状の描画、テキストのレンダリング、イメージの表示と操作を行うには、オブジェクトを作成する必要があり <xref:System.Drawing.Graphics> ます。 <xref:System.Drawing.Graphics>オブジェクトは GDI + の描画サーフェイスを表し、はグラフィックイメージを作成するために使用されるオブジェクトです。  
  
 グラフィックスを操作するには、次の2つの手順を実行します。  
  
1. オブジェクトを作成 <xref:System.Drawing.Graphics> しています。  
  
2. オブジェクトを使用して、 <xref:System.Drawing.Graphics> 線と形状を描画したり、テキストを表示したり、イメージを表示および操作したりします。  
  
## <a name="creating-a-graphics-object"></a>グラフィックスオブジェクトの作成  
 グラフィックスオブジェクトは、さまざまな方法で作成できます。  
  
#### <a name="to-create-a-graphics-object"></a>グラフィックスオブジェクトを作成するには  
  
- <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.Control.Paint> フォームまたはコントロールのイベントで、の一部としてグラフィックスオブジェクトへの参照を受け取ります。 これは、通常、コントロールの描画コードを作成するときに、グラフィックスオブジェクトへの参照を取得する方法です。 同様に、のイベントを処理するときに、グラフィックスオブジェクトをのプロパティとして取得することもでき <xref:System.Drawing.Printing.PrintPageEventArgs> <xref:System.Drawing.Printing.PrintDocument.PrintPage> <xref:System.Drawing.Printing.PrintDocument> ます。  
  
     または  
  
- コントロールまたはフォームのメソッドを呼び出して、 <xref:System.Windows.Forms.Control.CreateGraphics%2A> <xref:System.Drawing.Graphics> そのコントロールまたはフォームの描画サーフェイスを表すオブジェクトへの参照を取得します。 既に存在するフォームまたはコントロールに描画する場合は、このメソッドを使用します。  
  
     または  
  
- <xref:System.Drawing.Graphics>を継承する任意のオブジェクトからオブジェクトを作成 <xref:System.Drawing.Image> します。 この方法は、既存のイメージを変更する場合に便利です。  
  
     次のセクションでは、これらの各プロセスについて詳しく説明します。  
  
## <a name="painteventargs-in-the-paint-event-handler"></a>描画イベントハンドラーの PaintEventArgs  
 コントロールまたはのをプログラミングする場合、 <xref:System.Windows.Forms.PaintEventHandler> <xref:System.Drawing.Printing.PrintDocument.PrintPage> <xref:System.Drawing.Printing.PrintDocument> グラフィックスオブジェクトはまたはのプロパティの1つとして提供され <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Drawing.Printing.PrintPageEventArgs> ます。  
  
#### <a name="to-obtain-a-reference-to-a-graphics-object-from-the-painteventargs-in-the-paint-event"></a>描画イベントの PaintEventArgs からグラフィックスオブジェクトへの参照を取得するには  
  
1. オブジェクトを宣言 <xref:System.Drawing.Graphics> します。  
  
2. 変数を割り当て <xref:System.Drawing.Graphics> て、の一部として渡されたオブジェクトを参照し <xref:System.Windows.Forms.PaintEventArgs> ます。  
  
3. フォームまたはコントロールを描画するためのコードを挿入します。  
  
     次の例は、イベントでからオブジェクトを参照する方法を示してい <xref:System.Drawing.Graphics> <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.Control.Paint> ます。  
  
    ```vb  
    Private Sub Form1_Paint(sender As Object, pe As PaintEventArgs) Handles _  
       MyBase.Paint  
       ' Declares the Graphics object and sets it to the Graphics object  
       ' supplied in the PaintEventArgs.  
       Dim g As Graphics = pe.Graphics  
       ' Insert code to paint the form here.  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_Paint(object sender,
       System.Windows.Forms.PaintEventArgs pe)
    {  
       // Declares the Graphics object and sets it to the Graphics object  
       // supplied in the PaintEventArgs.  
       Graphics g = pe.Graphics;  
       // Insert code to paint the form here.  
    }  
    ```  
  
    ```cpp  
    private:  
       void Form1_Paint(System::Object ^ sender,  
          System::Windows::Forms::PaintEventArgs ^ pe)  
       {  
          // Declares the Graphics object and sets it to the Graphics object  
          // supplied in the PaintEventArgs.  
          Graphics ^ g = pe->Graphics;  
          // Insert code to paint the form here.  
       }  
    ```  
  
## <a name="creategraphics-method"></a>CreateGraphics メソッド  
 また、コントロールまたはフォームのメソッドを使用して、 <xref:System.Windows.Forms.Control.CreateGraphics%2A> <xref:System.Drawing.Graphics> そのコントロールまたはフォームの描画サーフェイスを表すオブジェクトへの参照を取得することもできます。  
  
#### <a name="to-create-a-graphics-object-with-the-creategraphics-method"></a>CreateGraphics メソッドを使用してグラフィックスオブジェクトを作成するには  
  
- <xref:System.Windows.Forms.Control.CreateGraphics%2A>グラフィックスをレンダリングするフォームまたはコントロールのメソッドを呼び出します。  
  
    ```vb  
    Dim g as Graphics  
    ' Sets g to a Graphics object representing the drawing surface of the  
    ' control or form g is a member of.  
    g = Me.CreateGraphics  
    ```  
  
    ```csharp  
    Graphics g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this.CreateGraphics();  
    ```  
  
    ```cpp  
    Graphics ^ g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this->CreateGraphics();  
    ```  
  
## <a name="create-from-an-image-object"></a>イメージオブジェクトから作成する  
 さらに、クラスから派生した任意のオブジェクトからグラフィックスオブジェクトを作成することもでき <xref:System.Drawing.Image> ます。  
  
#### <a name="to-create-a-graphics-object-from-an-image"></a>イメージからグラフィックスオブジェクトを作成するには  
  
- オブジェクトを <xref:System.Drawing.Graphics.FromImage%2A?displayProperty=nameWithType> 作成するイメージ変数の名前を指定して、メソッドを呼び出し <xref:System.Drawing.Graphics> ます。  
  
     次の例は、オブジェクトの使用方法を示してい <xref:System.Drawing.Bitmap> ます。  
  
    ```vb  
    Dim myBitmap as New Bitmap("C:\Documents and Settings\Joe\Pics\myPic.bmp")  
    Dim g as Graphics = Graphics.FromImage(myBitmap)  
    ```  
  
    ```csharp  
    Bitmap myBitmap = new Bitmap(@"C:\Documents and
       Settings\Joe\Pics\myPic.bmp");  
    Graphics g = Graphics.FromImage(myBitmap);  
    ```  
  
    ```cpp  
    Bitmap ^ myBitmap = gcnew  
       Bitmap("D:\\Documents and Settings\\Joe\\Pics\\myPic.bmp");  
    Graphics ^ g = Graphics::FromImage(myBitmap);  
    ```  
  
> [!NOTE]
> オブジェクトを作成できるのは、 <xref:System.Drawing.Graphics> 16 ビット、24ビット、32ビットの .bmp ファイルなど、インデックスのない .bmp ファイルのオブジェクトだけです。 インデックス付けされていない .bmp ファイルの各ピクセルには、カラーテーブルのインデックスを保持するインデックス付き .bmp ファイルのピクセルとは対照的に、色が保持されます。  
  
## <a name="drawing-and-manipulating-shapes-and-images"></a>図形とイメージの描画と操作  
 オブジェクトを作成した後、オブジェクトを使用して、 <xref:System.Drawing.Graphics> 線や図形の描画、テキストの表示、画像の表示と操作を行うことができます。 オブジェクトで使用されるプリンシパルオブジェクト <xref:System.Drawing.Graphics> は次のとおりです。  
  
- <xref:System.Drawing.Pen>クラス。線の描画、図形のアウトライン表示、またはその他の幾何学的表現のレンダリングに使用されます。  
  
- <xref:System.Drawing.Brush>塗りつぶされた図形、画像、テキストなど、グラフィックスの領域を塗りつぶすために使用されるクラス。  
  
- <xref:System.Drawing.Font>クラス: テキストを表示するときに使用する図形の説明を提供します。  
  
- <xref:System.Drawing.Color>構造体は、表示するさまざまな色を表します。  
  
#### <a name="to-use-the-graphics-object-you-have-created"></a>作成したグラフィックスオブジェクトを使用するには  
  
- 上記の適切なオブジェクトを使用して、必要なものを描画します。  
  
     詳細については、次のトピックを参照してください。  
  
    |レンダリングするには|解決方法については、|  
    |---------------|---------|  
    |路線|[方法: Windows フォームに直線を描画する](how-to-draw-a-line-on-a-windows-form.md)|  
    |図形|[方法: 形状のアウトラインを描画する](how-to-draw-an-outlined-shape.md)|  
    |テキスト|[方法: Windows フォームにテキストを描画する](how-to-draw-text-on-a-windows-form.md)|  
    |イメージ|[方法: GDI+ を使用してイメージをレンダリングする](how-to-render-images-with-gdi.md)|  
  
## <a name="see-also"></a>こちらもご覧ください

- [グラフィックス プログラミングについて](getting-started-with-graphics-programming.md)
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [直線、曲線、および図形](lines-curves-and-shapes.md)
- [方法: GDI+ を使用してイメージをレンダリングする](how-to-render-images-with-gdi.md)
