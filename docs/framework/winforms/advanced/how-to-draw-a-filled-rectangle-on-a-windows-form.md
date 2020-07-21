---
title: '方法: Windows フォームに塗りつぶした四角形を描画する'
description: Windows フォームで塗りつぶされた四角形をプログラムで描画する方法について説明します。 また、コードをコンパイルする方法についても説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- Graphics.FillRectangle
helpviewer_keywords:
- drawing [Windows Forms], rectangles
- rectangles [Windows Forms], drawing
- drawing rectangles
ms.assetid: d656a93c-987d-4809-aafd-493fe17450f0
ms.openlocfilehash: 0ad8ec97000e29b2194a9eda713aa43d5557b44c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621640"
---
# <a name="how-to-draw-a-filled-rectangle-on-a-windows-form"></a>方法: Windows フォームに塗りつぶした四角形を描画する
この例では、フォーム上に塗りつぶされた四角形を描画します。  
  
## <a name="example"></a>例  
 [!code-cpp[System.Drawing.ConceptualHowTos#2](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#2)]
 [!code-csharp[System.Drawing.ConceptualHowTos#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#2)]
 [!code-vb[System.Drawing.ConceptualHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#2)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 イベントハンドラーでは、このメソッドを呼び出すことはできません <xref:System.Windows.Forms.Form.Load> 。 フォームのサイズが変更されたり、別の形式で隠されたりした場合、描画コンテンツは再描画されません。 コンテンツが自動的に再描画されるようにするには、メソッドをオーバーライドする必要があり <xref:System.Windows.Forms.Control.OnPaint%2A> ます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 やオブジェクトなどの <xref:System.IDisposable.Dispose%2A> システムリソースを消費するオブジェクトに対しては、常にを呼び出す必要があり <xref:System.Drawing.Brush> <xref:System.Drawing.Graphics> ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Graphics.FillRectangle%2A>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- [グラフィックス プログラミングについて](getting-started-with-graphics-programming.md)
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [ペンを使用した直線と図形の描画](using-a-pen-to-draw-lines-and-shapes.md)
- [GDI+ でのブラシと塗りつぶされた図形](brushes-and-filled-shapes-in-gdi.md)
