---
title: '方法: ビジュアル内のジオメトリのヒット テストを実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [WPF], on visual objects comprising Geometry objects [WPF]
- visual objects [WPF], hit tests on
- Geometry objects [WPF], visual objects comprising
ms.assetid: 8bf2643f-d7f9-4cb4-9ea6-5b893c23200d
ms.openlocfilehash: 52b9b99b0af38d797e4a3c98dc0979211c930c1f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923378"
---
# <a name="how-to-hit-test-geometry-in-a-visual"></a>方法: ビジュアル内のジオメトリのヒット テストを実行する
この例では、1 つ以上の <xref:System.Windows.Media.Geometry> オブジェクトで構成されるビジュアル オブジェクトに対してヒット テストを実行する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> メソッドを使用するビジュアル オブジェクトから <xref:System.Windows.Media.DrawingGroup> を取得する方法を示しています。 次に、<xref:System.Windows.Media.DrawingGroup> の各描画のレンダリングされたコンテンツに対してヒット テストを実行し、ヒットしたジオメトリを確認します。  
  
> [!NOTE]
> 通常、ポイントがビジュアルの描画されたコンテンツと交差するかどうかを判定するには、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドを使用します。  
  
 [!code-csharp[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#visualsoverviewsnippet4)]
 [!code-vb[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#visualsoverviewsnippet4)]  
  
 <xref:System.Windows.Media.Geometry.FillContains%2A> メソッドは、指定した <xref:System.Windows.Point> または <xref:System.Windows.Media.Geometry> を使用してヒット テストを実行できるようにする、オーバーロードされたメソッドです。 ジオメトリに線が付いている場合は、塗りつぶしの境界の外側までストロークを拡張できます。 この場合、<xref:System.Windows.Media.Geometry.FillContains%2A> に加えて <xref:System.Windows.Media.Geometry.StrokeContains%2A> を呼び出す必要があります。  
  
 また、ベジエ平坦化に使用する <xref:System.Windows.Media.ToleranceType> を指定することもできます。  
  
> [!NOTE]
> このサンプルでは、ジオメトリに適用される可能性のある変換やクリッピングは考慮していません。 また、スタイルが設定されたコントロールには直接関連付けられた描画がないので、このサンプルはスタイルが設定されたコントロールに対しては機能しません。  
  
## <a name="see-also"></a>関連項目

- [ビジュアル層でのヒット テスト](hit-testing-in-the-visual-layer.md)
- [パラメーターとしてジオメトリを使用してヒット テストを実行する](how-to-hit-test-using-geometry-as-a-parameter.md)
