---
title: Graphics オブジェクトの状態の管理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [Windows Forms], managing state
- graphics [Windows Forms], clipping
ms.assetid: 6207cad1-7a34-4bd6-bfc1-db823ca7a73e
ms.openlocfilehash: d1e7e6eac775ca779fb68605adcc9bc2b9915e49
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182456"
---
# <a name="managing-the-state-of-a-graphics-object"></a>Graphics オブジェクトの状態の管理
クラス<xref:System.Drawing.Graphics>はGDI+ の中心にあります。 描画するには、オブジェクトを取得し<xref:System.Drawing.Graphics>、そのプロパティを設定し、メソッド<xref:System.Drawing.Graphics.DrawLine%2A>、、<xref:System.Drawing.Graphics.DrawImage%2A>など<xref:System.Drawing.Graphics.DrawString%2A>を呼び出します。  
  
 オブジェクトのメソッドを呼<xref:System.Drawing.Graphics.DrawRectangle%2A>び出す<xref:System.Drawing.Graphics>例を次に示します。 メソッドに渡される最初の<xref:System.Drawing.Graphics.DrawRectangle%2A>引数はオブジェクト<xref:System.Drawing.Pen>です。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue) ' Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  // Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100);  
```  
  
## <a name="graphics-state"></a>グラフィックスの状態  
 オブジェクト<xref:System.Drawing.Graphics>は、 や などの<xref:System.Drawing.Graphics.DrawLine%2A>描画メソッドを提供する<xref:System.Drawing.Graphics.DrawRectangle%2A>以上の処理を行います。 オブジェクト<xref:System.Drawing.Graphics>は、次のカテゴリに分類できるグラフィックスの状態も保持します。  
  
- 品質設定  
  
- 変換  
  
- クリッピング領域  
  
### <a name="quality-settings"></a>品質設定  
 オブジェクト<xref:System.Drawing.Graphics>には、描画される項目の品質に影響を与えるプロパティがいくつかあります。 たとえば、テキストに適用される<xref:System.Drawing.Graphics.TextRenderingHint%2A>アンチエイリアスの種類を指定するプロパティを設定できます。 品質に影響するその他<xref:System.Drawing.Graphics.SmoothingMode%2A>の<xref:System.Drawing.Graphics.CompositingMode%2A>プロパティ<xref:System.Drawing.Graphics.CompositingQuality%2A>には、 <xref:System.Drawing.Graphics.InterpolationMode%2A>、 、および があります。  
  
 次の例では、2<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias><xref:System.Drawing.Drawing2D.SmoothingMode.HighSpeed>つの楕円を描画します。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue)  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias  
graphics.DrawEllipse(pen, 0, 0, 200, 100)  
graphics.SmoothingMode = SmoothingMode.HighSpeed  
graphics.DrawEllipse(pen, 0, 150, 200, 100)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias;  
graphics.DrawEllipse(pen, 0, 0, 200, 100);  
graphics.SmoothingMode = SmoothingMode.HighSpeed;  
graphics.DrawEllipse(pen, 0, 150, 200, 100);  
```  
  
### <a name="transformations"></a>変換  
 オブジェクト<xref:System.Drawing.Graphics>は、その<xref:System.Drawing.Graphics>オブジェクトによって描画されるすべての項目に適用される 2 つの変換 (ワールドとページ) を保持します。 アフィン変換は、ワールド変換に保存できます。 アフィン変換には、スケーリング、回転、反射、傾斜、および変換が含まれます。 ページ変換は、スケーリングや単位の変更 (ピクセルからインチなど) に使用できます。 詳細については、「[座標系と変換](coordinate-systems-and-transformations.md)」を参照してください。  
  
 次の例では、オブジェクトのワールド変換とページ変換<xref:System.Drawing.Graphics>を設定します。 ワールド変換は 30 度回転に設定されます。 ページ変換は、2 番目<xref:System.Drawing.Graphics.DrawEllipse%2A>に渡される座標がピクセルではなくミリメートルとして扱われるように設定されます。 コードは、メソッドに対して<xref:System.Drawing.Graphics.DrawEllipse%2A>2 つの同一の呼び出しを行います。 ワールド変換は最初<xref:System.Drawing.Graphics.DrawEllipse%2A>の呼び出しに適用され、両方の変換 (ワールドとページ) が<xref:System.Drawing.Graphics.DrawEllipse%2A>2 番目の呼び出しに適用されます。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Red)  
  
graphics.ResetTransform()  
graphics.RotateTransform(30) ' world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
graphics.PageUnit = GraphicsUnit.Millimeter ' page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Red);
  
graphics.ResetTransform();  
graphics.RotateTransform(30);                    // world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
graphics.PageUnit = GraphicsUnit.Millimeter;     // page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
```  
  
 次の図は、2 つの楕円を示しています。 30 度回転は、楕円の中心ではなく、座標系の原点 (クライアント領域の左上隅) に関するものです。 また、ペンの幅が 1 の場合は、最初の楕円の場合は 1 ピクセル、2 番目の楕円では 1 ミリメートルを意味します。  
  
 ![回転とペンの幅の 2 つの楕円を示す図。](./media/managing-the-state-of-a-graphics-object/set-rotation-pen-width-drawellipse-method.png)  
  
### <a name="clipping-region"></a>クリッピング領域  
 オブジェクト<xref:System.Drawing.Graphics>は、そのオブジェクトによって描画されるすべての項目に適用されるクリッピング領域<xref:System.Drawing.Graphics>を保持します。 クリッピング領域は、<xref:System.Drawing.Graphics.SetClip%2A>メソッドを呼び出して設定できます。  
  
 2 つの四角形の和集合を形成して、プラスの形をした領域を作成する例を次に示します。 その領域は、<xref:System.Drawing.Graphics>オブジェクトのクリッピング領域として指定されます。 次に、クリッピング領域の内部に制限された 2 本の線を描画します。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
  
' Opaque red, width 5  
Dim pen As New Pen(Color.Red, 5)  
  
' Opaque aqua  
Dim brush As New SolidBrush(Color.FromArgb(255, 180, 255, 255))  
  
' Create a plus-shaped region by forming the union of two rectangles.  
Dim [region] As New [Region](New Rectangle(50, 0, 50, 150))  
[region].Union(New Rectangle(0, 50, 150, 50))  
graphics.FillRegion(brush, [region])  
  
' Set the clipping region.  
graphics.SetClip([region], CombineMode.Replace)  
  
' Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160)  
graphics.DrawLine(pen, 40, 20, 190, 150)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
  
// Opaque red, width 5  
Pen pen = new Pen(Color.Red, 5);
  
// Opaque aqua  
SolidBrush brush = new SolidBrush(Color.FromArgb(255, 180, 255, 255));
  
// Create a plus-shaped region by forming the union of two rectangles.  
Region region = new Region(new Rectangle(50, 0, 50, 150));  
region.Union(new Rectangle(0, 50, 150, 50));  
graphics.FillRegion(brush, region);  
  
// Set the clipping region.  
graphics.SetClip(region, CombineMode.Replace);  
  
// Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160);  
graphics.DrawLine(pen, 40, 20, 190, 150);  
```  
  
 次の図は、クリップされた線を示しています。  
  
 ![制限されたクリップ領域を示す図。](./media/managing-the-state-of-a-graphics-object/set-clipping-region-setclip-method.png)  
  
## <a name="see-also"></a>関連項目

- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [入れ子になっているグラフィックス コンテナーの使用](using-nested-graphics-containers.md)
