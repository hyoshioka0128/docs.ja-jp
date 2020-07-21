---
title: '方法 : 色を回転させる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], rotating
- examples [Windows Forms], rotating colors
ms.assetid: e2e4c300-159c-4f4a-9b56-103b0f7cbc05
ms.openlocfilehash: 8d2717dd7b819e963126072279b361fda02188bc
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111336"
---
# <a name="how-to-rotate-colors"></a>方法 : 色を回転させる
4 次元のカラースペースでの回転は、視覚化が困難です。 色成分の 1 つを固定していくことに同意することで、回転を簡単に視覚化できます。 アルファ成分を1(完全に不透明)に固定することに同意するとします。 次の図に示すように、赤、緑、青の軸を使用して、3 次元の色空間を視覚化できます。  
  
 ![赤、緑、青の軸で回転を示す図。](./media/how-to-rotate-colors/rotation-red-green-blue-axes.gif)  
  
 色は 3D 空間の点と考えることができます。 たとえば、空間内の点 (1, 0, 0) は赤を表し、空間内の点 (0, 1, 0) は緑を表します。  
  
 次の図は、赤緑平面で 60 度の角度で色 (1, 0, 0) を回転する意味を示しています。 赤緑平面に平行な平面の回転は、青い軸を中心とした回転と考えることができます。  
  
 ![青い軸を中心とした回転を示す図。](./media/how-to-rotate-colors/rotation-about-blue-axis.gif)  
  
 次の図は、カラー マトリックスを初期化して、3 つの座標軸 (赤、緑、青) のそれぞれについて回転を実行する方法を示しています。  
  
 ![3 軸の回転を実行するようにカラー マトリックスを初期化します。](./media/how-to-rotate-colors/rotation-about-three-axes.gif)  
  
## <a name="example"></a>例  
 次の例では、1 色 (1, 0, 0.6) のイメージを取得し、青軸を中心に 60 度回転します。 回転角度は、赤緑の平面に平行な平面でスイープされます。  
  
 次の図は、左側に元のイメージを、右にカラー回転したイメージを示しています。  
  
 ![元のイメージとカラー回転したイメージを示す図。](./media/how-to-rotate-colors/original-color-rotated-images.png)  
  
 次の図は、次のコードで実行される色の回転の視覚化を示しています。
  
 ![色の回転の視覚化を示す図。](./media/how-to-rotate-colors/visualization-color-rotation.gif)  
  
 [!code-csharp[System.Drawing.RotateColors#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RotateColors/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.RotateColors#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RotateColors/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記の例は Windows フォームで使用するように設計されており、<xref:System.Windows.Forms.PaintEventArgs>`e`<xref:System.Windows.Forms.Control.Paint>イベント ハンドラーのパラメーターである が必要です。 システム`RotationInput.bmp`で有効なイメージ ファイル名とパスで置き換えます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows フォームにおけるグラフィックスと描画](graphics-and-drawing-in-windows-forms.md)
- [イメージの色の変更](recoloring-images.md)
