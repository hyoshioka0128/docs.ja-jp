---
title: '方法: PathGeometry 内に複数のサブパスを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- multiple subpaths [WPF]
- graphics [WPF], subpaths
- subpaths [WPF]
ms.assetid: 104a862c-dde2-4e62-ac87-80660dd1681c
ms.openlocfilehash: 286075448cd6a343f8a7b15b2b5005f840f68e1d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904723"
---
# <a name="how-to-create-multiple-subpaths-within-a-pathgeometry"></a>方法: PathGeometry 内に複数のサブパスを作成する
この例では、<xref:System.Windows.Media.PathGeometry> に複数のサブパスを作成する方法を示しています。 サブパスを複数作成するには、サブパスごとに <xref:System.Windows.Media.PathFigure> を作成します。  
  
## <a name="example"></a>例  
 次の例では、それぞれが三角形である 2 つのサブパスが作成されます。  
  
 [!code-xaml[GeometrySample#38](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#38)]  
  
 次の例では、<xref:System.Windows.Shapes.Path> と [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の属性構文を使用して、サブパスを複数作成する方法を示しています。 各 `M` では、新しいサブパスが作成されるので、この例では、それぞれが三角形を描画する 2 つのサブパスが作成されます。  
  
 [!code-xaml[GeometrySample#58](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#58)]  
  
 (この属性構文では、実際には <xref:System.Windows.Media.PathGeometry> の軽量バージョンである <xref:System.Windows.Media.StreamGeometry> が作成されます。) 詳細については、「[パス マークアップ構文](path-markup-syntax.md)」のページを参照してください。)  
  
## <a name="see-also"></a>関連項目

- [ジオメトリの概要](geometry-overview.md)
