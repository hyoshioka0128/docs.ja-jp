---
title: '方法: Windows フォームに直線を描画する'
description: 描画イベントを処理してフォーム上に線を描画し、PaintEventArgs の Graphics プロパティを使用して描画を実行する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- Graphics.DrawLine
helpviewer_keywords:
- examples [Windows Forms], drawing lines on forms
- drawing [Windows Forms], lines
- lines [Windows Forms], drawing
- drawing lines
ms.assetid: 55c1dbeb-75d0-430c-9814-a24b8971ad8c
ms.openlocfilehash: c8e92dc265c63413275561d0e2e3aa820eaec724
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621627"
---
# <a name="how-to-draw-a-line-on-a-windows-form"></a>方法: Windows フォームに直線を描画する
この例では、フォーム上に線を描画します。 通常、フォームで描画する場合は、フォームのイベントを処理 <xref:System.Windows.Forms.Control.Paint> し、のプロパティを使用して描画を実行します。 <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> <xref:System.Windows.Forms.PaintEventArgs> 次に例を示します。  
  
## <a name="example"></a>例  
 [!code-csharp[System.Drawing.UsingAPen#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 前の例は、Windows フォームで使用するために設計されていて、<xref:System.Windows.Forms.PaintEventArgs> イベント ハンドラーのパラメーターである `e`<xref:System.Windows.Forms.Control.Paint> を必要とします。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 <xref:System.IDisposable.Dispose%2A>オブジェクトなどのシステムリソースを消費するオブジェクトに対しては、常にを呼び出す必要があり <xref:System.Drawing.Pen> ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Graphics.DrawLine%2A>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- [グラフィックス プログラミングについて](getting-started-with-graphics-programming.md)
- [ペンを使用した直線と図形の描画](using-a-pen-to-draw-lines-and-shapes.md)
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
