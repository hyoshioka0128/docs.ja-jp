---
title: '方法: JPEG 圧縮レベルの設定'
description: Windows フォームで圧縮レベルを変更して、JPEG イメージの品質を調整する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], changing encoder parameters
- JPEG images [Windows Forms], setting quality level
ms.assetid: 4b9a74e3-9504-43c1-9f28-ace651d0772e
ms.openlocfilehash: 1f6a96e8a05fff40eb08da0ce318faa86a06cc3a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618715"
---
# <a name="how-to-set-jpeg-compression-level"></a>方法: JPEG 圧縮レベルの設定
イメージをディスクに保存するときに、ファイル サイズを最小化したり品質を向上させるために、イメージのパラメーターを修正したりする必要がある場合があります。 圧縮レベルを修正して、JPEG イメージの品質を調整することができます。 JPEG イメージを保存するときに圧縮レベルを指定するには、オブジェクトを作成 <xref:System.Drawing.Imaging.EncoderParameters> し、そのオブジェクトをクラスのメソッドに渡す必要があり <xref:System.Drawing.Image.Save%2A> <xref:System.Drawing.Image> ます。 オブジェクトを初期化して、 <xref:System.Drawing.Imaging.EncoderParameters> 1 つの配列が含まれるようにし <xref:System.Drawing.Imaging.EncoderParameter> ます。 を作成するときに <xref:System.Drawing.Imaging.EncoderParameter> 、 <xref:System.Drawing.Imaging.Encoder.Quality> エンコーダーと必要な圧縮レベルを指定します。  
  
## <a name="example"></a>例  
 次のコード例では、 <xref:System.Drawing.Imaging.EncoderParameter> オブジェクトを作成し、3つの JPEG イメージを保存します。 各 JPEG イメージは、 `long` コンストラクターに渡される値を変更することによって、異なる品質レベルで保存され <xref:System.Drawing.Imaging.EncoderParameter> ます。 品質レベル 0 は最も圧縮率が高く、品質レベル 100 は最も低い圧縮率に対応します。  
  
```csharp  
private void VaryQualityLevel()  
    {  
        // Get a bitmap. The using statement ensures objects  
        // are automatically disposed from memory after use.  
        using (Bitmap bmp1 = new Bitmap(@"C:\TestPhoto.jpg"))  
        {  
            ImageCodecInfo jpgEncoder = GetEncoder(ImageFormat.Jpeg);  
  
            // Create an Encoder object based on the GUID  
            // for the Quality parameter category.  
            System.Drawing.Imaging.Encoder myEncoder =  
                System.Drawing.Imaging.Encoder.Quality;  
  
            // Create an EncoderParameters object.  
            // An EncoderParameters object has an array of EncoderParameter  
            // objects. In this case, there is only one  
            // EncoderParameter object in the array.  
            EncoderParameters myEncoderParameters = new EncoderParameters(1);  
  
            EncoderParameter myEncoderParameter = new EncoderParameter(myEncoder, 50L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"c:\TestPhotoQualityFifty.jpg", jpgEncoder, myEncoderParameters);  
  
            myEncoderParameter = new EncoderParameter(myEncoder, 100L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"C:\TestPhotoQualityHundred.jpg", jpgEncoder, myEncoderParameters);  
  
            // Save the bitmap as a JPG file with zero quality level compression.  
            myEncoderParameter = new EncoderParameter(myEncoder, 0L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"C:\TestPhotoQualityZero.jpg", jpgEncoder, myEncoderParameters);  
        }  
    }  
```  
  
```vb  
Private Sub VaryQualityLevel()  
    ' Get a bitmap. The Using statement ensures objects  
    ' are automatically disposed from memory after use.  
    Using bmp1 As New Bitmap("C:\test\TestPhoto.jpg")  
        Dim jpgEncoder As ImageCodecInfo = GetEncoder(ImageFormat.Jpeg)  
  
        ' Create an Encoder object based on the GUID  
        ' for the Quality parameter category.  
        Dim myEncoder As System.Drawing.Imaging.Encoder = System.Drawing.Imaging.Encoder.Quality  
  
        ' Create an EncoderParameters object.  
        ' An EncoderParameters object has an array of EncoderParameter  
        ' objects. In this case, there is only one  
        ' EncoderParameter object in the array.  
        Dim myEncoderParameters As New EncoderParameters(1)  
  
        Dim myEncoderParameter As New EncoderParameter(myEncoder, 50L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("c:\test\TestPhotoQualityFifty.jpg", jpgEncoder, myEncoderParameters)  
  
        myEncoderParameter = New EncoderParameter(myEncoder, 100L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("C:\test\TestPhotoQualityHundred.jpg", jpgEncoder, myEncoderParameters)  
  
        ' Save the bitmap as a JPG file with zero quality level compression.  
        myEncoderParameter = New EncoderParameter(myEncoder, 0L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("C:\test\TestPhotoQualityZero.jpg", jpgEncoder, myEncoderParameters)  
    End Using  
End Sub  
```  
  
```csharp  
private ImageCodecInfo GetEncoder(ImageFormat format)  
{  
    ImageCodecInfo[] codecs = ImageCodecInfo.GetImageDecoders();  
    foreach (ImageCodecInfo codec in codecs)  
    {  
        if (codec.FormatID == format.Guid)  
        {  
            return codec;  
        }  
    }  
    return null;  
}  
```  
  
```vb  
Private Function GetEncoder(ByVal format As ImageFormat) As ImageCodecInfo  
  
    Dim codecs As ImageCodecInfo() = ImageCodecInfo.GetImageDecoders()  
    Dim codec As ImageCodecInfo  
    For Each codec In codecs  
        If codec.FormatID = format.Guid Then  
            Return codec  
        End If  
    Next codec  
    Return Nothing  
  
End Function  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- Windows フォーム アプリケーション  
  
- <xref:System.Windows.Forms.PaintEventArgs>のパラメーターである <xref:System.Windows.Forms.PaintEventHandler> 。  
  
- `TestPhoto.jpg` という名前のイメージ ファイル。保存場所は **c:\\** です。  
  
## <a name="see-also"></a>関連項目

- [方法: エンコーダーがサポートするパラメーターの確認](how-to-determine-the-parameters-supported-by-an-encoder.md)
- [ビットマップの種類](types-of-bitmaps.md)
- [マネージド GDI+ でのイメージ エンコーダーおよびイメージ デコーダーの使用](using-image-encoders-and-decoders-in-managed-gdi.md)
