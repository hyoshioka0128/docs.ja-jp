---
title: '方法: 結合したジオメトリを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- combining geometries [WPF]
- graphics [WPF], combining geometries
- geometries [WPF], combining
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
ms.openlocfilehash: c5ebe87abd4c2cf70f8fa17f1fcc773293f3ad27
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910095"
---
# <a name="how-to-create-a-combined-geometry"></a>方法: 結合したジオメトリを作成する
この例は、ジオメトリを結合する方法を示しています。 2 つのジオメトリを結合するには、<xref:System.Windows.Media.CombinedGeometry> オブジェクトを使用します。 結合する 2 つのジオメトリでその <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> プロパティと <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> プロパティを設定します。また、ジオメトリの結合方法を決定する <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> プロパティを `Union`、`Intersect`、`Exclude`、または `Xor` に設定します。  
  
 2 つ以上のジオメトリから複合ジオメトリを作成するには、<xref:System.Windows.Media.GeometryGroup> を使用します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.CombinedGeometry> が `Exclude` のジオメトリ結合モードで定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#21](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![除外組み合わせモードの結果](./media/mil-task-combined-geometry-exclude.PNG "mil_task_combined_geometry_exclude")  
結合したジオメトリの除外  
  
 次のマークアップでは、<xref:System.Windows.Media.CombinedGeometry> が `Intersect` の結合モードを指定して定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#22](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![交差組み合わせモードの結果](./media/mil-task-combined-geometry-intersect.PNG "mil_task_combined_geometry_intersect")  
結合したジオメトリの交差  
  
 次のマークアップでは、<xref:System.Windows.Media.CombinedGeometry> が `Union` の結合モードで定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#23](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![和集合結合モードの結果](./media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
結合したジオメトリの和集合  
  
 次のマークアップでは、<xref:System.Windows.Media.CombinedGeometry> が `Xor` の結合モードで定義されています。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> と <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> は両方とも同じ半径の円として定義されますが、中心は 50 オフセットされています。  
  
 [!code-xaml[GeometrySample#24](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 結合モードの結果](./media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_xor")  
結合したジオメトリの Xor
