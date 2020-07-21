---
title: '方法 : 垂直方向のテキストを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [Windows Forms], drawing vertical
- Windows Forms, drawing vertical text
- strings [Windows Forms], drawing vertical
- vertical text [Windows Forms], drawing
ms.assetid: 50c69046-4188-47d9-b949-cc2610ffd337
ms.openlocfilehash: 86401342625f593945b801f7619ef9ca9681317c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182563"
---
# <a name="how-to-create-vertical-text"></a>方法 : 垂直方向のテキストを作成する
オブジェクトを<xref:System.Drawing.StringFormat>使用して、テキストを横ではなく縦方向に描画するように指定できます。  
  
## <a name="example"></a>例  
 次の例では、オブジェクトの<xref:System.Drawing.StringFormatFlags.DirectionVertical>プロパティに<xref:System.Drawing.StringFormat.FormatFlags%2A>値を<xref:System.Drawing.StringFormat>代入します。 その<xref:System.Drawing.StringFormat>オブジェクトはクラスの<xref:System.Drawing.Graphics.DrawString%2A>メソッドに<xref:System.Drawing.Graphics>渡されます。 値<xref:System.Drawing.StringFormatFlags.DirectionVertical>は<xref:System.Drawing.StringFormatFlags>列挙体のメンバーです。  
  
 次の図は、縦書きテキストを示しています。
  
 ![縦書きフォント テキストを示すグラフィック。](./media/how-to-create-vertical-text/vertical-font-text-graphic.png)  
  
 [!code-csharp[System.Drawing.FontsAndText#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.FontsAndText#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
  
- 上記の例は Windows フォームで使用するように設計されており、<xref:System.Windows.Forms.PaintEventArgs>`e`のパラメーターである が必要<xref:System.Windows.Forms.PaintEventHandler>です。  
  
## <a name="see-also"></a>関連項目

- [方法 : GDI を使用してテキストを描画する](how-to-draw-text-with-gdi.md)
