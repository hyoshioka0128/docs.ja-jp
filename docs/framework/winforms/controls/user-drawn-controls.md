---
title: ユーザー描画コントロール
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], user-drawn
- OnPaint method [Windows Forms]
- user-drawn controls [Windows Forms]
ms.assetid: 034af4b5-457f-4160-a937-22891817faa8
ms.openlocfilehash: c68c8c88376cfe7295962264c466030115f2f3db
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182006"
---
# <a name="user-drawn-controls"></a>ユーザー描画コントロール
.NET Framework では、独自のコントロールを簡単に開発できます。 コードによってバインドされた一連の標準コントロールであるユーザー コントロールを作成することも、独自のコントロールを一からデザインすることもできます。 継承を使用して、既存のコントロールから継承するコントロールを作成し、その固有の機能を追加することもできます。 どのような方法を使用しても、.NET Framework には、作成するコントロールのカスタム グラフィカル インターフェイスを描画する機能が用意されています。  
  
 コントロールの描画は、コントロールの<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドでコードを実行することによって行われます。 <xref:System.Windows.Forms.Control.OnPaint%2A>メソッドの単一の引数は、<xref:System.Windows.Forms.PaintEventArgs>コントロールのレンダリングに必要なすべての情報と機能を提供するオブジェクトです。 では<xref:System.Windows.Forms.PaintEventArgs>、コントロールのレンダリングで使用される 2 つの主要なオブジェクトをプロパティとして提供します。  
  
- <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>object : 描画されるコントロールの一部を表す四角形。 これは、コントロール全体、またはコントロールの描画方法に応じてコントロールの一部にすることができます。  
  
- <xref:System.Drawing.Graphics>object - コントロールの描画に必要な機能を提供する、いくつかのグラフィックス指向のオブジェクトとメソッドをカプセル化します。  
  
 オブジェクトの<xref:System.Drawing.Graphics>詳細と使用方法については、「[方法: 図面用のグラフィックス オブジェクトを作成する](../advanced/how-to-create-graphics-objects-for-drawing.md)」を参照してください。  
  
 この<xref:System.Windows.Forms.Control.OnPaint%2A>イベントは、コントロールが画面に描画または更新され、<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>オブジェクトが描画が行われる四角形を表すたびに発生します。 コントロール全体を更新する必要がある場合は<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>、 はコントロール全体のサイズを表します。 ただし、コントロールの一部だけを更新する必要がある場合、<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>オブジェクトは再描画が必要な領域のみを表します。 このような場合の例としては、ユーザー インターフェイスの別のコントロールまたはフォームによってコントロールが部分的に隠されていた場合があります。  
  
 <xref:System.Windows.Forms.Control>クラスから継承する場合は、メソッドをオーバーライドし<xref:System.Windows.Forms.Control.OnPaint%2A>、グラフィックス レンダリング コードを内部に提供する必要があります。 ユーザー コントロールまたは継承されたコントロールにカスタム グラフィカル インターフェイスを提供する場合は、<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドをオーバーライドして提供することもできます。 例を次に示します。  
  
```vb  
Protected Overrides Sub OnPaint(ByVal e As PaintEventArgs)  
   ' Call the OnPaint method of the base class.  
   MyBase.OnPaint(e)  
  
   ' Declare and instantiate a drawing pen.  
   Using myPen As System.Drawing.Pen = New System.Drawing.Pen(Color.Aqua)  
      ' Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, New Rectangle(Me.Location, Me.Size))  
   End Using
End Sub  
```  
  
```csharp  
protected override void OnPaint(PaintEventArgs e)  
{  
   // Call the OnPaint method of the base class.  
   base.OnPaint(e);  
  
   // Declare and instantiate a new pen.  
   using (System.Drawing.Pen myPen = new System.Drawing.Pen(Color.Aqua))  
   {
      // Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, new Rectangle(this.Location,
         this.Size));  
   }
}  
```  
  
 前の例では、非常に単純なグラフィカル表現でコントロールをレンダリングする方法を示します。 このメソッドは<xref:System.Windows.Forms.Control.OnPaint%2A>、基本クラスのメソッドを呼び出<xref:System.Drawing.Pen>し、描画に使用するオブジェクトを作成し、最後に<xref:System.Windows.Forms.Control.Location%2A>、コントロールの で<xref:System.Windows.Forms.Control.Size%2A>決定された四角形に楕円を描画します。 ほとんどのレンダリング コードはこれよりかなり複雑になりますが、この例では、オブジェクト内に含まれる<xref:System.Drawing.Graphics>オブジェクトの使用方法を<xref:System.Windows.Forms.PaintEventArgs>示します。 または<xref:System.Windows.Forms.UserControl><xref:System.Windows.Forms.Button>などのグラフィカル表現を既に持っているクラスから継承していて、その表現をレンダリングに組み込まない場合は、基本クラスの<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドを呼び出すべきではありません。  
  
 コントロールの<xref:System.Windows.Forms.Control.OnPaint%2A>メソッドのコードは、コントロールが最初に描画されたとき、および更新されるたびに実行されます。 コントロールのサイズを変更するたびにコントロールが再描画されるようにするには、コントロールのコンストラクターに次の行を追加します。  
  
```vb  
SetStyle(ControlStyles.ResizeRedraw, True)  
```  
  
```csharp  
SetStyle(ControlStyles.ResizeRedraw, true);  
```  
  
> [!NOTE]
> プロパティを<xref:System.Windows.Forms.Control.Region%2A?displayProperty=nameWithType>使用して、四角形以外のコントロールを実装します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Control.Region%2A>
- <xref:System.Windows.Forms.ControlStyles>
- <xref:System.Drawing.Graphics>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- <xref:System.Windows.Forms.PaintEventArgs>
- [方法 : 描画する Graphics オブジェクトを作成する](../advanced/how-to-create-graphics-objects-for-drawing.md)
- [内在コントロール](constituent-controls.md)
- [さまざまなカスタム コントロール](varieties-of-custom-controls.md)
