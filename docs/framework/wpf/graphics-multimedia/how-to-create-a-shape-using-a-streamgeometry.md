---
title: '方法: StreamGeometry を使用して図形を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], shapes
- shapes [WPF], creating with StreamGeometry class
ms.assetid: 08f7c8ce-074b-49cd-9aba-cc9592d4ee51
ms.openlocfilehash: ce2097568349ad376540163f5fe05d6a3e5b0643
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348026"
---
# <a name="how-to-create-a-shape-using-a-streamgeometry"></a>方法: StreamGeometry を使用して図形を作成する
<xref:System.Windows.Media.StreamGeometry> は、幾何学図形を作成するための <xref:System.Windows.Media.PathGeometry> に代わる軽量の手段です。 複雑なジオメトリを記述する必要があるが、データ バインディング、アニメーション、または変更をサポートするオーバーヘッドが望ましくない場合は、<xref:System.Windows.Media.StreamGeometry> を使用します。 たとえば、<xref:System.Windows.Media.StreamGeometry> クラスは効率的であるため、装飾の記述に適しています。  
  
## <a name="example"></a>例  
 次の例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で属性構文の使用によって三角形の <xref:System.Windows.Media.StreamGeometry> が作成されます。  
  
 [!code-xaml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 <xref:System.Windows.Media.StreamGeometry> 属性構文の詳細については、「[パス マークアップ構文](path-markup-syntax.md)」ページを参照してください。  
  
## <a name="example"></a>例  
 次の例では、コードで <xref:System.Windows.Media.StreamGeometry> を使用して三角形が定義されます。 この例ではまず、<xref:System.Windows.Media.StreamGeometry> が作成され、次に <xref:System.Windows.Media.StreamGeometryContext> が取得され、それを使用して三角形が記述されます。  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryTriangleExample.cs#streamgeometrytriangleexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometrytriangleexample.vb#streamgeometrytriangleexamplewholepage)]  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.StreamGeometry> と <xref:System.Windows.Media.StreamGeometryContext> を使用するメソッドが作成され、指定されたパラメーターに基づいて幾何学図形が定義されます。  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryExample.cs#streamgeometryexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometryexample.vb#streamgeometryexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Media.StreamGeometry>
- <xref:System.Windows.Media.StreamGeometryContext>
- [PathGeometry を使用して図形を作成する](how-to-create-a-shape-by-using-a-pathgeometry.md)
- [ジオメトリの概要](geometry-overview.md)
