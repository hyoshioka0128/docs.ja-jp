---
title: 内在コントロール
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], constituent controls
- constituent controls [Windows Forms]
- user controls [Windows Forms], constituent controls
ms.assetid: 5565e720-198b-4bbd-a2bd-c447ba641798
ms.openlocfilehash: 2865a3d85bd56151038ee90c18d199d3a584b5d4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182411"
---
# <a name="constituent-controls"></a>内在コントロール
ユーザー コントロールを構成するコントロール ("*内在コントロール*" と呼ばれます) は、カスタム グラフィックスのレンダリングに関してはそれほど柔軟ではありません。 すべての Windows フォーム コントロールは、独自の<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドを使用して独自のレンダリングを処理します。 このメソッドは保護されているため、開発者はアクセスできず、したがってコントロールが描画されるときに実行を防ぐことはできません。 ただし、これは、内在コントロールの外観に影響を与えるコードを追加できないという意味ではありません。 イベント ハンドラーを追加することで、追加のレンダリングを実現できます。 たとえば、 という名前<xref:System.Windows.Forms.UserControl>`MyButton`のボタンを使用して を作成したとします。 によって<xref:System.Web.UI.WebControls.Button>提供される以上の追加のレンダリングを必要とする場合は、次のようなコードをユーザー コントロールに追加します。  
  
```vb  
Public Sub MyPaint(ByVal sender as Object, e as PaintEventArgs) Handles _  
   MyButton.Paint  
   'Additional rendering code goes here  
End Sub  
```  
  
```csharp  
// Add the event handler to the button's Paint event.  
MyButton.Paint +=
   new System.Windows.Forms.PaintEventHandler (this.MyPaint);  
// Create the custom painting method.  
protected void MyPaint (object sender,
System.Windows.Forms.PaintEventArgs e)  
{  
   // Additional rendering code goes here.  
}  
```  
  
> [!NOTE]
> などの<xref:System.Windows.Forms.TextBox>Windows フォーム コントロールの一部は、Windows によって直接描画されます。 これらの場合、<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドは呼び出されないため、上記の例は呼び出されることはありません。  
  
 この例は、`MyButton.Paint` イベントが実行されるたびに実行するメソッドを作成し、それによって追加のグラフィカル表示をコントロールに追加します。 これにより `MyButton.OnPaint` の実行は妨げられないので、カスタム描画に加えて、ボタンによって通常実行されるすべての描画が実行されることに注意してください。 GDI+ テクノロジとカスタム レンダリングについて詳しくは、「[Creating Graphical Images with GDI+](../advanced/how-to-create-graphics-objects-for-drawing.md)」 (GDI+ でのグラフィカル イメージの作成) をご覧ください。 コントロールの表示を独自のものにしたい場合の最善の方法は、継承コントロールを作成し、カスタム レンダリング コードをそこに記述するというものです。 詳しくは、「[ユーザー描画コントロール](user-drawn-controls.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- [ユーザー描画コントロール](user-drawn-controls.md)
- [方法 : 描画する Graphics オブジェクトを作成する](../advanced/how-to-create-graphics-objects-for-drawing.md)
- [さまざまなカスタム コントロール](varieties-of-custom-controls.md)
