---
title: '方法: TileBrush の水平方向および垂直方向の配置を設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF], alignment of
- vertical alignment of TileBrushes [WPF]
- aligning [WPF], TileBrushes
- horizontal alignment of Tilebrushes [WPF]
ms.assetid: 65ae89bd-9246-4c9e-bde4-2fb991d4060d
ms.openlocfilehash: e3bfb2b209e40c435c3a321c874dfbd7a9a2fd50
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912368"
---
# <a name="how-to-set-the-horizontal-and-vertical-alignment-of-a-tilebrush"></a>方法: TileBrush の水平方向および垂直方向の配置を設定する
この例は、タイル内の内容の水平方向および垂直の配置を制御する方法を示します。 <xref:System.Windows.Media.TileBrush> の水平方向と垂直方向の配置を制御するには、その <xref:System.Windows.Media.TileBrush.AlignmentX%2A> と <xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティを使用します。  
  
 <xref:System.Windows.Media.TileBrush> の <xref:System.Windows.Media.TileBrush.AlignmentX%2A> と <xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティは、次のいずれかの条件が該当する場合に使用されます。  
  
- <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティが <xref:System.Windows.Media.Stretch.Uniform> または <xref:System.Windows.Media.Stretch.UniformToFill> であり、<xref:System.Windows.Media.TileBrush.Viewbox%2A> および <xref:System.Windows.Media.TileBrush.Viewport%2A> の縦横比が異なる。  
  
- <xref:System.Windows.Media.TileBrush.Stretch%2A> プロパティが <xref:System.Windows.Media.Stretch.None> であり、<xref:System.Windows.Media.TileBrush.Viewbox%2A> と <xref:System.Windows.Media.TileBrush.Viewport%2A> のサイズが異なる。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.TileBrush> の型である <xref:System.Windows.Media.DrawingBrush> の内容が、タイルの左上隅に配置されます。 この例では内容を配置するため、<xref:System.Windows.Media.DrawingBrush> の <xref:System.Windows.Media.TileBrush.AlignmentX%2A> プロパティが <xref:System.Windows.Media.AlignmentX.Left> に、<xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティが <xref:System.Windows.Media.AlignmentY.Top> に設定されます。 この例を実行すると、次の出力が生成されます。  
  
 ![左上に配置された TileBrush](./media/graphicsmm-tilebrushalignmentexampletopleft.png "graphicsmm_TileBrushAlignmentExampleTopLeft")  
内容が左上隅に配置された TileBrush  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushtopleftalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushtopleftalignmentinline)]
 [!code-xaml[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushtopleftalignmentinline)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> プロパティを <xref:System.Windows.Media.AlignmentX.Right> に設定し、<xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティを <xref:System.Windows.Media.AlignmentY.Bottom> に設定することにより、<xref:System.Windows.Media.DrawingBrush> の内容がタイルの右下隅に配置されます。 この例では次の出力が生成されます。  
  
 ![右下に配置された TileBrush](./media/graphicsmm-tilebrushalignmentexamplebottomright.png "graphicsmm_TileBrushAlignmentExampleBottomRight")  
内容が右下隅に配置された TileBrush  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushbottomrightalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushbottomrightalignmentinline)]
 [!code-xaml[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushbottomrightalignmentinline)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> プロパティを <xref:System.Windows.Media.AlignmentX.Left> に設定し、<xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティを <xref:System.Windows.Media.AlignmentY.Top> に設定することにより、<xref:System.Windows.Media.DrawingBrush> の内容がタイルの左上隅に配置されます。 また、<xref:System.Windows.Media.DrawingBrush> の <xref:System.Windows.Media.TileBrush.Viewport%2A> と <xref:System.Windows.Media.TileBrush.TileMode%2A> を設定することで、タイル パターンが生成されます。 この例では次の出力が生成されます。  
  
 ![左上に配置されたタイル化された TileBrush](./media/graphicsmm-tilebrushalignmentexampletoplefttiled.png "graphicsmm_TileBrushAlignmentExampleTopLeftTiled")  
基本タイルの左上に内容が配置されたタイル パターン  
  
 図では、内容がどのように配置されているかをわかりやすくするために、基本タイルが強調されています。 <xref:System.Windows.Media.DrawingBrush> の内容で基本タイルが水平方向にいっぱいに並べて配置されているため、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> の設定は効果がないことに注意してください。  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushtopleftalignmenttiledinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushtopleftalignmenttiledinline)]
 [!code-xaml[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushtopleftalignmenttiledinline)]  
  
## <a name="example"></a>例  
 最後の例では、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> プロパティを <xref:System.Windows.Media.AlignmentX.Right> に設定し、<xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティを <xref:System.Windows.Media.AlignmentY.Bottom> に設定することにより、タイル化された <xref:System.Windows.Media.DrawingBrush> の内容がその基本タイルの右下に配置されます。 この例では次の出力が生成されます。  
  
 ![右下に配置されたタイル化された TileBrush](./media/graphicsmm-tilebrushalignmentexamplebottomrighttiled.png "graphicsmm_TileBrushAlignmentExampleBottomRightTiled")  
基本タイルの右上に内容が配置されたタイル パターン  
  
 ここでも、<xref:System.Windows.Media.DrawingBrush> の内容で基本タイルが水平方向にいっぱいに並べて配置されているため、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> の設定は効果がありません。  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushbottomrightalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushbottomrightalignmentinline)]
 [!code-xaml[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushbottomrightalignmentinline)]  
  
 これらの例では、<xref:System.Windows.Media.TileBrush.AlignmentX%2A> と <xref:System.Windows.Media.TileBrush.AlignmentY%2A> プロパティがどのように使用されるのかを示すために、<xref:System.Windows.Media.DrawingBrush> オブジェクトが使用されています。 これらのプロパティは、すべてのタイル ブラシ (<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.ImageBrush>、および <xref:System.Windows.Media.VisualBrush>) で同じように動作します。 タイル ブラシの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.VisualBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
