---
title: '方法 : 色を傾斜する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], transforming with color matrices
- colors [Windows Forms], shearing
ms.assetid: 0a424171-5b8b-45c4-afef-e9720a6c3e22
ms.openlocfilehash: 825e5a90ebb0d9df3b894ce7bd353e917b676939
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142395"
---
# <a name="how-to-shear-colors"></a>方法 : 色を傾斜する
せん断は、カラー成分を別の色成分に比例する量だけ増減します。 たとえば、赤の成分が青成分の半分の値増加する変換を考えてみます。 このような変換では、色(0.2、0.5、1)は(0.7、0.5、1)になります。 新しい赤の成分は 0.2 + (1/2)(1) = 0.7 です。  
  
## <a name="example"></a>例  
 次の例では、ColorBars4.bmp ファイルから<xref:System.Drawing.Image>オブジェクトを作成します。 次に、前の段落で説明したせん断変換をイメージ内の各ピクセルに適用します。  
  
 次の図は、左側に元のイメージを、右にせよげイメージを示しています。
  
 ![原画とシレ画像を並べて色付きストライプを持つ2つの正方形。](./media/how-to-shear-colors/original-image-sheared-image.png)  
  
 次の表は、せん断変換の前後の 4 つのバーのカラー ベクトルを示しています。  
  
|変更元|せん断|  
|--------------|-------------|  
|(0, 0, 1, 1)|(0.5, 0, 1, 1)|  
|(0.5, 1, 0.5, 1)|(0.75, 1, 0.5, 1)|  
|(1, 1, 0, 1)|(1, 1, 0, 1)|  
|(0.4, 0.4, 0.4, 1)|(0.6, 0.4, 0.4, 1)|  
  
 [!code-csharp[System.Drawing.Misc3#9](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Misc3/CS/Form1.cs#9)]
 [!code-vb[System.Drawing.Misc3#9](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Misc3/VB/Form1.vb#9)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記の例は Windows フォームで使用するように設計されており、<xref:System.Windows.Forms.PaintEventArgs>`e`<xref:System.Windows.Forms.Control.Paint>イベント ハンドラーのパラメーターである が必要です。 システム`ColorBars.bmp`で有効なイメージ名とパスで置き換えます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [イメージの色の変更](recoloring-images.md)
