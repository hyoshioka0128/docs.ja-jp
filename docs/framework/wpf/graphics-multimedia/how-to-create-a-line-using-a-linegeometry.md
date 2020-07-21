---
title: '方法: LineGeometry を使用して線を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], lines
ms.assetid: 41231b22-1f74-4c26-a8e7-a55b29f8f6bd
ms.openlocfilehash: f8c334a54f78aec7af91064a447fd18f23dcfbdc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61905204"
---
# <a name="how-to-create-a-line-using-a-linegeometry"></a>方法: LineGeometry を使用して線を作成する
この例では、<xref:System.Windows.Media.LineGeometry> クラスを使用して線を表す方法を示します。 <xref:System.Windows.Media.LineGeometry> は開始点と終了点によって定義されます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.LineGeometry> を作成してレンダリングする方法を示します。  <xref:System.Windows.Shapes.Path> 要素は、線をレンダリングする目的で使用されています。  線には領域がないため、<xref:System.Windows.Shapes.Path> オブジェクトの <xref:System.Windows.Shapes.Shape.Fill%2A> は指定されていません。その代わり、<xref:System.Windows.Shapes.Shape.Stroke%2A> プロパティと <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> プロパティが使用されています。  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
(10,20) から (100,130) まで描画された LineGeometry  
  
 その他の単純なジオメトリ クラスには <xref:System.Windows.Media.LineGeometry> と <xref:System.Windows.Media.EllipseGeometry> が含まれています。 これらのジオメトリも、もっと複雑なジオメトリも、<xref:System.Windows.Media.PathGeometry> または <xref:System.Windows.Media.StreamGeometry> を利用して作成できます。 詳細については、「[ジオメトリの概要](geometry-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ジオメトリの概要](geometry-overview.md)
- [複合図形を作成する](how-to-create-a-composite-shape.md)
- [PathGeometry を使用して図形を作成する](how-to-create-a-shape-by-using-a-pathgeometry.md)
