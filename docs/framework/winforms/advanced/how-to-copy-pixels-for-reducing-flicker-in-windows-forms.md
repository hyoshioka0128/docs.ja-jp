---
title: '方法: フリッカを減らすためにピクセルをコピーする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bitblt
- graphics [Windows Forms], copying
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing flicker
- pixels [Windows Forms], copying
- flicker
- bit-block transfer
ms.assetid: 33b76910-13a3-4521-be98-5c097341ae3b
ms.openlocfilehash: a25295532d7123d92bcacc6828d3e8cfcc839d6e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182583"
---
# <a name="how-to-copy-pixels-for-reducing-flicker-in-windows-forms"></a>方法 :ピクセルをコピーして Windows フォームのちらつきを低減する
単純なグラフィックをアニメーション化すると、ユーザーがちらつきやその他の望ましくない視覚効果を見つめてしまうことがあります。 この問題を制限する 1 つの方法は、グラフィック上で "bitblt" プロセスを使用することです。 Bitblt は、ピクセルの元の四角形からピクセルのターゲット矩形へのカラーデータの「ビットブロック転送」です。  
  
 Windows フォームでは、クラスのメソッドを<xref:System.Drawing.Graphics.CopyFromScreen%2A>使用して bitblt が実行されます。 <xref:System.Drawing.Graphics> メソッドのパラメータでは、ソースとコピー先 (ポイント)、コピーする領域のサイズ、および新しい図形の描画に使用するグラフィックス オブジェクトを指定します。  
  
 次の例では、フォーム上のイベント ハンドラーで図形が<xref:System.Windows.Forms.Control.Paint>描画されます。 次に、<xref:System.Drawing.Graphics.CopyFromScreen%2A>このメソッドを使用して図形を複製します。  
  
> [!NOTE]
> フォームの<xref:System.Windows.Forms.Control.DoubleBuffered%2A>プロパティを設定すると`true`、イベント内のグラフィックス ベースの<xref:System.Windows.Forms.Control.Paint>コードがダブル バッファリングされます。 以下のコードを使用する場合、この方法でパフォーマンスが向上するわけではありませんが、より複雑なグラフィックス操作コードを使用する場合は、注意が必要です。  
  
## <a name="example"></a>例  
  
```vb  
Private Sub Form1_Paint(ByVal sender As Object, ByVal e As _  
    System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint  
    ' Draw a circle with a bar on top.  
        e.Graphics.FillEllipse(Brushes.DarkBlue, New Rectangle _  
             (10, 10, 60, 60))  
        e.Graphics.FillRectangle(Brushes.Khaki, New Rectangle _  
             (20, 30, 60, 10))  
    ' Copy the graphic to a new location.  
        e.Graphics.CopyFromScreen(New Point(10, 10), New Point _  
             (100, 100), New Size(70, 70))  
End Sub  
```  
  
```csharp  
private void Form1_Paint(System.Object sender,  
    System.Windows.Forms.PaintEventArgs e)  
        {  
        e.Graphics.FillEllipse(Brushes.DarkBlue, new  
            Rectangle(10,10,60,60));  
        e.Graphics.FillRectangle(Brushes.Khaki, new  
            Rectangle(20,30,60,10));  
        e.Graphics.CopyFromScreen(new Point(10, 10), new Point(100, 100),
            new Size(70, 70));  
}  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記のコードはフォームの<xref:System.Windows.Forms.Control.Paint>イベント ハンドラで実行されるため、フォームが再描画されたときにグラフィックスが保持されます。 そのため、フォームのサイズが変更されたり、別のフォーム<xref:System.Windows.Forms.Form.Load>によって隠されたりしても描画されたコンテンツは再描画されないため、イベント ハンドラでグラフィックス関連のメソッドを呼び出しません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.CopyPixelOperation>
- <xref:System.Drawing.Graphics.FillRectangle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.OnPaint%2A?displayProperty=nameWithType>
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [ペンを使用した直線と図形の描画](using-a-pen-to-draw-lines-and-shapes.md)
