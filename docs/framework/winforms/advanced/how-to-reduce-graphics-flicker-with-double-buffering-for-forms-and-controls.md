---
title: '方法: フォームとコントロールのダブル バッファリングを行うことによってグラフィックスのちらつきを軽減する'
description: Windows フォームのダブルバッファリングを使用してグラフィックスのちらつきを軽減する方法と、コントロールを使用して描画操作に関連するちらつきの問題に対処する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing double-buffered flicker
ms.assetid: 91083d3a-653f-4f15-a467-0f37b2aa39d6
ms.openlocfilehash: f7c0425729f8a1a780124621788a1c49e06e0c4e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618130"
---
# <a name="how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls"></a>方法: フォームとコントロールのダブル バッファリングを行うことによってグラフィックスのちらつきを軽減する
ダブル バッファリングでは、メモリ バッファーを使用して、複数の描画操作に関連するちらつきの問題に対処します。 ダブル バッファリングを有効にすると、すべての描画操作が画面上の描画サーフェイスではなく、最初にメモリ バッファーに描画されます。 描画操作がすべて完了すると、メモリ バッファーが、関連付けられている描画サーフェイスに直接コピーされます。 画面上で実行されるグラフィックス操作は1つだけであるため、複雑な描画操作に関連付けられているイメージのちらつきが解消されます。ほとんどのアプリケーションでは、.NET Framework によって提供される既定のダブルバッファリングによって最適な結果が得られます。 標準 Windows フォームコントロールは、既定ではダブルバッファリングされます。 フォームと作成されたコントロールでの既定のダブルバッファリングは、次の2つの方法で有効にすることができます。 プロパティをに設定するか、 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> `true` メソッドを呼び出してフラグをに設定することができ <xref:System.Windows.Forms.Control.SetStyle%2A> <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> `true` ます。 どちらの方法でも、フォームまたはコントロールの既定のダブルバッファリングが有効になり、ちらつきなしのグラフィックスレンダリングが提供されます。 メソッドの呼び出し <xref:System.Windows.Forms.Control.SetStyle%2A> は、すべてのレンダリングコードを記述したカスタムコントロールに対してのみ推奨されます。  
  
 アニメーションや高度なメモリ管理などのより高度なダブルバッファリングシナリオでは、独自のダブルバッファリングロジックを実装できます。 詳細については、「[方法: バッファリングされたグラフィックスを手動で管理する](how-to-manually-manage-buffered-graphics.md)」を参照してください。  
  
### <a name="to-reduce-flicker"></a>ちらつきを軽減するには  
  
- <xref:System.Windows.Forms.Control.DoubleBuffered%2A> プロパティを `true`に設定します。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#31)]  
  
 \- または  
  
- メソッドを呼び出して <xref:System.Windows.Forms.Control.SetStyle%2A> 、 <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> フラグをに設定 `true` します。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#32)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#32)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Control.DoubleBuffered%2A>
- <xref:System.Windows.Forms.Control.SetStyle%2A>
- [ダブル バッファリングされたグラフィックス](double-buffered-graphics.md)
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
