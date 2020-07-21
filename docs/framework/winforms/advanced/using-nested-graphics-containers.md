---
title: 入れ子になっているグラフィックス コンテナーの使用
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [Windows Forms], nested containers
- graphics [Windows Forms], clipping
- graphics [Windows Forms], transformations in nested objects
ms.assetid: a0d9f178-43a4-4323-bb5a-d3e3f77ae6c1
ms.openlocfilehash: 460ebb37ee62691a1e282f756840121fd378ebd8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182461"
---
# <a name="using-nested-graphics-containers"></a>入れ子になっているグラフィックス コンテナーの使用
GDI+ には、オブジェクト内の状態の一部を一時的に置換または拡張するために<xref:System.Drawing.Graphics>使用できるコンテナーが用意されています。 オブジェクトの<xref:System.Drawing.Graphics.BeginContainer%2A>メソッドを呼び出してコンテナーを<xref:System.Drawing.Graphics>作成します。 ネストされたコンテナー<xref:System.Drawing.Graphics.BeginContainer%2A>を形成するために、繰り返し呼び出すことができます。 の<xref:System.Drawing.Graphics.BeginContainer%2A>各呼び出しは、 への<xref:System.Drawing.Graphics.EndContainer%2A>呼び出しと対にする必要があります。  
  
## <a name="transformations-in-nested-containers"></a>入れ子になったコンテナーの変換  
 次の例では、<xref:System.Drawing.Graphics>そのオブジェクト内にオブジェクトと<xref:System.Drawing.Graphics>コンテナーを作成します。 オブジェクトの<xref:System.Drawing.Graphics>ワールド変換は、x 方向の変換 100 単位、y 方向の 80 単位です。 コンテナのワールド変換は30度回転です。 コードは 2`DrawRectangle(pen, -60, -30, 120, 60)`回呼び出しを行います。 最初の<xref:System.Drawing.Graphics.DrawRectangle%2A>呼び出しはコンテナー内にあります。つまり、呼び出しは と の<xref:System.Drawing.Graphics.BeginContainer%2A>呼<xref:System.Drawing.Graphics.EndContainer%2A>び出しの間にあります。 2 番目の<xref:System.Drawing.Graphics.DrawRectangle%2A>呼び出しは<xref:System.Drawing.Graphics.EndContainer%2A>、 への呼び出しの後です。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.MiscLegacyTopics#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#61)]  
  
 上記のコードでは、コンテナー内から描画された四角形は、最初にコンテナーのワールド変換 (回転) によって変換され、次にオブジェクトのワールド<xref:System.Drawing.Graphics>変換 (移動) によって変換されます。 コンテナの外側から描画される四角形は、<xref:System.Drawing.Graphics>オブジェクトのワールド変換 (変換) によってのみ変換されます。 次の図は、2 つの四角形を示しています。
  
 ![入れ子になったコンテナーを示す図。](./media/using-nested-graphics-containers/nested-containers-illustration.png)  
  
## <a name="clipping-in-nested-containers"></a>ネストされたコンテナでのクリッピング  
 入れ子になったコンテナーがクリッピング領域を処理する方法を次の例に示します。 コードは、その<xref:System.Drawing.Graphics>オブジェクト内にオブジェクトとコンテナー<xref:System.Drawing.Graphics>を作成します。 <xref:System.Drawing.Graphics>オブジェクトのクリッピング領域は長方形で、コンテナのクリッピング領域は楕円です。 コードは、メソッドに 2<xref:System.Drawing.Graphics.DrawLine%2A>つの呼び出しを行います。 最初の呼び<xref:System.Drawing.Graphics.DrawLine%2A>出しはコンテナー内にあり、2 番目<xref:System.Drawing.Graphics.DrawLine%2A>の呼び出しはコンテナーの外側<xref:System.Drawing.Graphics.EndContainer%2A>にあります (呼び出し後)。 最初の線は、2 つのクリップ領域の交点によってクリップされます。 2 番目の線は、オブジェクトの四角形のクリップ領域によってのみ<xref:System.Drawing.Graphics>クリップされます。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#62](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#62)]
 [!code-vb[System.Drawing.MiscLegacyTopics#62](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#62)]  
  
 次の図は、2 つのクリップされた線を示しています。
  
 ![線が切り取られた入れ子になったコンテナーを示す図。](./media/using-nested-graphics-containers/nested-container-clipped-lines.png)  
  
 前の 2 つの例が示すように、変換とクリッピング領域は、入れ子になったコンテナーで累積されます。 コンテナと<xref:System.Drawing.Graphics>オブジェクトのワールド変換を設定すると、両方の変換がコンテナ内から描画される項目に適用されます。 コンテナの変換が最初に適用され、オブジェクトの変換が 2<xref:System.Drawing.Graphics>番目に適用されます。 コンテナと<xref:System.Drawing.Graphics>オブジェクトのクリッピング領域を設定すると、コンテナ内部から描画された項目は、2 つのクリッピング領域の交点によってクリップされます。  
  
## <a name="quality-settings-in-nested-containers"></a>入れ子になったコンテナーの品質設定  
 入れ子<xref:System.Drawing.Graphics.SmoothingMode%2A>になった<xref:System.Drawing.Graphics.TextRenderingHint%2A>コンテナーの品質設定 ( 、、など ) は累積されません。むしろ、コンテナの品質設定は<xref:System.Drawing.Graphics>、オブジェクトの品質設定を一時的に置き換えます。 新しいコンテナーを作成すると、そのコンテナーの品質設定が既定値に設定されます。 たとえば、スムージング モード<xref:System.Drawing.Graphics>が<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>のオブジェクトがあるとします。 コンテナを作成する場合、コンテナ内部のスムージング モードが既定のスムージング モードになります。 コンテナのスムージング モードは自由に設定でき、コンテナ内から描画される項目は、設定したモードに従って描画されます。 呼<xref:System.Drawing.Graphics.EndContainer%2A>び出しの後に描画された項目は、 への呼び<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>出しの前に設定されていたスムー<xref:System.Drawing.Graphics.BeginContainer%2A>ジング モード ( ) に従って描画されます。  
  
## <a name="several-layers-of-nested-containers"></a>ネストされたコンテナの複数の層  
 <xref:System.Drawing.Graphics>オブジェクト内の 1 つのコンテナに制限はありません。 前のコンテナでネストされたコンテナのシーケンスを作成し、ネストされた各コンテナのワールド変換、クリッピング領域、および品質設定を指定できます。 最も内側のコンテナーの内部から描画メソッドを呼び出すと、変換は最も内側のコンテナーから始まり、最も外側のコンテナーで終わる順に適用されます。 最も内側のコンテナーの内側から描画された項目は、すべてのクリッピング領域の交差部分によってクリップされます。  
  
 次の例では、<xref:System.Drawing.Graphics>オブジェクトを作成し、テキストレンダリングヒント<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>をに設定します。 このコードは、2 つのコンテナーを作成し、もう 1 つは入れ子にします。 外側のコンテナーのテキスト レンダリング ヒントが<xref:System.Drawing.Text.TextRenderingHint.SingleBitPerPixel>に設定され、内部コンテナーのテキスト レンダリング ヒントが<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>に設定されます。 このコードは、内部コンテナーから 1 つ、外側のコンテナーから 1 つ、オブジェクト<xref:System.Drawing.Graphics>自体から 1 つずつ、3 つの文字列を描画します。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#63](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#63)]
 [!code-vb[System.Drawing.MiscLegacyTopics#63](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#63)]  
  
 次の図は、3 つの文字列を示しています。 内部コンテナーと<xref:System.Drawing.Graphics>オブジェクトから描画される文字列は、アンチエイリアシングによってスムージングされます。 <xref:System.Drawing.Graphics.TextRenderingHint%2A>プロパティが に設定されているため、外側のコンテナーから描画された文字列は、アンチエイリアシングによって<xref:System.Drawing.Text.TextRenderingHint.SingleBitPerPixel>スムージングされません。  
  
 ![入れ子になったコンテナーから描画された文字列を示す図。](./media/using-nested-graphics-containers/nested-containers-three-strings.png)  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Graphics>
- [Graphics オブジェクトの状態の管理](managing-the-state-of-a-graphics-object.md)
