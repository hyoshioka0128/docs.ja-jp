---
title: '方法 : パス グラデーションを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- path gradients [Windows Forms], creating
- gradients [Windows Forms], creating path
- graphics paths [Windows Forms], creating gradient
ms.assetid: 1948e834-e104-481c-b71d-d8aa9e4d106e
ms.openlocfilehash: cf4dc558c008fb8adfc327a6a894a428e985df03
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182642"
---
# <a name="how-to-create-a-path-gradient"></a>方法 : パス グラデーションを作成する
この<xref:System.Drawing.Drawing2D.PathGradientBrush>クラスでは、徐々に変化する色で図形を塗りつぶす方法をカスタマイズできます。 たとえば、パスの中心に 1 色、パスの境界に別の色を指定できます。 パスの境界に沿った複数の点ごとに、個別の色を指定することもできます。  
  
> [!NOTE]
> GDI+ では、パスはオブジェクトによって維持される一連の直線と曲線<xref:System.Drawing.Drawing2D.GraphicsPath>です。 GDI+ パスの詳細については[、「GDI+ のグラフィックス パス](graphics-paths-in-gdi.md)」および「[パスの作成と描画](constructing-and-drawing-paths.md)」を参照してください。  

この記事の例は、コントロールのイベント ハンドラーから呼び出<xref:System.Windows.Forms.Control.Paint>されるメソッドです。  

### <a name="to-fill-an-ellipse-with-a-path-gradient"></a>楕円をパス グラデーションで塗りつぶすには  
  
- 次の例では、楕円をパス グラデーション ブラシで塗りつぶします。 中心の色は青に設定され、境界カラーは水色に設定されます。 塗りつぶされた楕円を次の図に示します。  
  
     ![グラデーションパスは楕円を塗りつぶします。](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse.png)  
  
     デフォルトでは、パスグラデーションブラシはパスの境界の外側に伸びません。 パス グラデーション ブラシを使用して、パスの境界を越えた図形を塗りつぶすと、パスの外側にある画面の領域は塗りつぶされません。  
  
     次の図は、次のコードの呼<xref:System.Drawing.Graphics.FillEllipse%2A?displayProperty=nameWithType>び出しをに変更`e.Graphics.FillRectangle(pthGrBrush, 0, 10, 200, 40)`した場合の動作を示しています。  
  
     ![パスの境界を越えて拡張されたグラデーション パス。](./media/how-to-create-a-path-gradient/gradient-path-extended-beyond-boundary.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#11)]
     [!code-vb[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#11)]  
  
     上記のコード例は Windows フォームで使用するように設計されており<xref:System.Windows.Forms.PaintEventArgs>、e を必要とします。 <xref:System.Windows.Forms.PaintEventHandler>  
  
### <a name="to-specify-points-on-the-boundary"></a>境界上の点を指定するには  
  
- 次の例では、星型のパスからパス グラデーション ブラシを作成します。 このコードでは、<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterColor%2A>星の中心の色を赤に設定するプロパティを設定します。 次に、配列内<xref:System.Drawing.Drawing2D.PathGradientBrush.SurroundColors%2A>の個々のポイントでさまざまな色 (`colors`配列に格納されている) を指定`points`するプロパティを設定します。 最後のコード ステートメントは、星形のパスをパス グラデーション ブラシで塗りつぶします。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#12)]
     [!code-vb[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#12)]  
  
- コード内にオブジェクトを含まないパス<xref:System.Drawing.Drawing2D.GraphicsPath>グラデーションを描画する例を次に示します。 この例<xref:System.Drawing.Drawing2D.PathGradientBrush.%23ctor%2A>の特定のコンストラクターは、ポイントの配列を受け取りますが<xref:System.Drawing.Drawing2D.GraphicsPath>、オブジェクトは必要ありません。 また、 は<xref:System.Drawing.Drawing2D.PathGradientBrush>パスではなく四角形を塗りつぶすために使用されます。 この四角形はブラシの定義に使用した閉じたパスよりも大きいので、一部の矩形はブラシで描画されません。 次の図は、四角形 (点線) と、パス グラデーション ブラシで描画された四角形の部分を示しています。
  
     ![パスグラデーションブラシで塗りつぶされたグラデーション部分。](./media/how-to-create-a-path-gradient/gradient-painted-path-gradient-brush.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#13)]
     [!code-vb[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#13)]  
  
### <a name="to-customize-a-path-gradient"></a>パスグラデーションをカスタマイズするには  
  
- パス グラデーション ブラシをカスタマイズする方法の 1<xref:System.Drawing.Drawing2D.PathGradientBrush.FocusScales%2A>つは、そのプロパティを設定することです。 フォーカススケールは、メインパスの内側にある内側のパスを指定します。 中心点だけでなく、その内側のパス内のどこにでも中心の色が表示されます。  
  
     次の例では、楕円パスに基づいてパス グラデーション ブラシを作成します。 このコードでは、境界の色を青に設定し、中心カラーを水色に設定し、次にパス グラデーション ブラシを使用して楕円パスを塗りつぶします。  
  
     次に、パス グラデーション ブラシのフォーカス スケールを設定します。 x フォーカススケールは 0.3 に設定され、y フォーカススケールは 0.8 に設定されます。 このコードはオブジェクト<xref:System.Drawing.Graphics.TranslateTransform%2A>のメソッドを<xref:System.Drawing.Graphics>呼び出して、後続の<xref:System.Drawing.Graphics.FillPath%2A>呼び出しで最初の楕円の右側にある楕円を塗りつぶします。  
  
     フォーカススケールの効果を確認するには、中心をメインの楕円と共有する小さな楕円を想像します。 小さな楕円は、中心を中心にして、0.3 倍、垂直方向に 0.8 倍の倍率でスケーリングされた主な楕円です。 外側の楕円の境界から内側の楕円の境界に移動すると、色が青から水色に徐々に変化します。 内側の楕円の境界から共有の中心に移動しても、色はアクアのままです。  
  
     以下のコードの出力を次の図に示します。 左側の楕円は、中心点でのみ水上です。 右側の楕円は、内側のパスの内側の至る所にアクアです。  
  
 ![フォーカススケールのグラデーション効果](./media/how-to-create-a-path-gradient/focus-scales-aqua-inner-outer-ellipse.png)  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#14)]  
  
### <a name="to-customize-with-interpolation"></a>補間を使用してカスタマイズするには  
  
- パス グラデーション ブラシをカスタマイズするもう 1 つの方法は、補間色の配列と補間位置の配列を指定することです。  
  
     次の例では、三角形に基づいてパス グラデーション ブラシを作成します。 このコードでは、<xref:System.Drawing.Drawing2D.PathGradientBrush.InterpolationColors%2A>パス グラデーション ブラシのプロパティを設定して、補間色 (濃い緑、アクア、青) の配列と補間位置 (0, 0.25, 1) の配列を指定します。 三角形の境界から中心点に移動すると、色は濃い緑色から水色に、次に水色から青に徐々に変化します。 濃い緑からアクアへの変化は、濃い緑から青までの距離の25%で起こります。  
  
     次の図は、カスタム パス グラデーション ブラシで塗りつぶされた三角形を示しています。  
  
     ![カスタム パス グラデーション ブラシで塗りつぶされた三角形。](./media/how-to-create-a-path-gradient/gradient-brush-filled-triangle.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#15)]
     [!code-vb[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#15)]  
  
### <a name="to-set-the-center-point"></a>中心点を設定するには  
  
- デフォルトでは、パスグラデーションブラシの中心点は、ブラシの構築に使用されるパスの重心にあります。 中心点の位置は、クラスのプロパティを<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A>設定することによって変更できます。 <xref:System.Drawing.Drawing2D.PathGradientBrush>  
  
     次の例では、楕円に基づいてパス グラデーション ブラシを作成します。 楕円の中心は (70, 35) ですが、パスグラデーションブラシの中心点は (120, 40) に設定されています。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#16)]
     [!code-vb[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#16)]  
  
     次の図は、塗りつぶされた楕円とパス グラデーション ブラシの中心点を示しています。  
  
     ![塗りつぶされた楕円と中心点を持つグラデーションパス。](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse-center-point.png)  
  
- パス グラデーション ブラシの中心点を、ブラシの構築に使用したパスの外側の位置に設定できます。 次の例では、上記のコードで<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A>プロパティを設定する呼び出しを置き換えます。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#17)]
     [!code-vb[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#17)]  
  
     次の図は、この変更の出力を示しています。  
  
     ![パスの外側に中心点があるグラデーションパス。](./media/how-to-create-a-path-gradient/gradient-path-center-point-outside.png)  
  
     上の図では、楕円の右端の点は純粋な青ではありません (ただし、非常に近い点です)。 グラデーションの色は、塗りつぶしが純粋な青 (0, 0, 255) になる点 (145, 35) に達したかのように配置されます。 しかし、パスグラデーションブラシはパスの内側にのみ描画されるため、塗りつぶしが決して (145, 35) に達することはありません。  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記の例は Windows フォームで使用するように設計されており、<xref:System.Windows.Forms.PaintEventArgs>`e`<xref:System.Windows.Forms.Control.Paint>イベント ハンドラーのパラメーターである が必要です。  
  
## <a name="see-also"></a>関連項目

- [グラデーション ブラシを使用した図形の塗りつぶし](using-a-gradient-brush-to-fill-shapes.md)
