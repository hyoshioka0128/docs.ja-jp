---
title: OnPaint メソッドのオーバーライド
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Paint event [Windows Forms], handling in Windows Forms custom control
- OnPaint method [Windows Forms], overriding in Windows Forms custom controls
ms.assetid: e9ca2723-0107-4540-bb21-4f5ffb4a9906
ms.openlocfilehash: 863726a6264f01de9f00296b4a64b9fd1bb96765
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182042"
---
# <a name="overriding-the-onpaint-method"></a>OnPaint メソッドのオーバーライド
.NET Framework で定義されているイベントをオーバーライドするための基本的な手順は同じです。  
  
#### <a name="to-override-an-inherited-event"></a>継承されたイベントをオーバーライドするには  
  
1. 保護された`On` *EventName*メソッドをオーバーライドします。  
  
2. `On`オーバーライドされた`On` *EventName*メソッドから基本クラスの*EventName*メソッドを呼び出して、登録されたデリゲートがイベントを受け取るようにします。  
  
 イベント<xref:System.Windows.Forms.Control.Paint>の詳細については、各 Windows フォーム コントロールが継承するイベント<xref:System.Windows.Forms.Control.Paint>をオーバーライドする必要があるためです<xref:System.Windows.Forms.Control>。 基本<xref:System.Windows.Forms.Control>クラスは、派生コントロールの描画方法を認識せず、メソッドに描画ロジックを<xref:System.Windows.Forms.Control.OnPaint%2A>提供しません。 登録されたイベント レシーバーにイベント<xref:System.Windows.Forms.Control.Paint>をディスパッチするメソッド。 <xref:System.Windows.Forms.Control.OnPaint%2A> <xref:System.Windows.Forms.Control>  
  
 [「方法: 単純な Windows フォーム コントロールを開発する](how-to-develop-a-simple-windows-forms-control.md)」のサンプルを使用している場合は、メソッドを<xref:System.Windows.Forms.Control.OnPaint%2A>オーバーライドする例を見てきました。 次のコードは、そのサンプルから取得されます。  
  
```vb  
Public Class FirstControl  
   Inherits Control  
  
   Public Sub New()  
   End Sub  
  
   Protected Overrides Sub OnPaint(e As PaintEventArgs)  
      ' Call the OnPaint method of the base class.  
      MyBase.OnPaint(e)  
      ' Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, New SolidBrush(ForeColor), RectangleF.op_Implicit(ClientRectangle))  
   End Sub  
End Class
```  
  
```csharp  
public class FirstControl : Control {  
   public FirstControl() {}  
   protected override void OnPaint(PaintEventArgs e) {  
      // Call the OnPaint method of the base class.  
      base.OnPaint(e);  
      // Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, new SolidBrush(ForeColor), ClientRectangle);  
   }
}
```  
  
 クラス<xref:System.Windows.Forms.PaintEventArgs>には、イベントのデータ<xref:System.Windows.Forms.Control.Paint>が含まれています。 次のコードに示すように、2 つのプロパティがあります。  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   ...  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs {  
...  
    public System.Drawing.Rectangle ClipRectangle {}  
    public System.Drawing.Graphics Graphics {}  
...  
}  
```  
  
 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>は描画される四角形で、<xref:System.Windows.Forms.PaintEventArgs.Graphics%2A>プロパティはオブジェクトを<xref:System.Drawing.Graphics>参照します。 名前空間内の<xref:System.Drawing?displayProperty=nameWithType>クラスは、GDI+ の新しい Windows グラフィックス ライブラリの機能へのアクセスを提供するマネージ クラスです。 オブジェクト<xref:System.Drawing.Graphics>には、点、文字列、線、円弧、楕円、およびその他の多くの図形を描画するメソッドがあります。  
  
 コントロールは、そのビジュアル<xref:System.Windows.Forms.Control.OnPaint%2A>表示を変更する必要がある場合に、そのメソッドを呼び出します。 このメソッドは、イベントを<xref:System.Windows.Forms.Control.Paint>発生させます。  
  
## <a name="see-also"></a>関連項目

- [Events](../../../standard/events/index.md)
- [Windows フォーム コントロールのレンダリング](rendering-a-windows-forms-control.md)
- [イベントの定義](defining-an-event-in-windows-forms-controls.md)
