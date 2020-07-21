---
title: 3D パフォーマンスの最大化
ms.date: 03/30/2017
helpviewer_keywords:
- 3D graphics [WPF]
ms.assetid: 4bcf949d-d92f-4d8d-8a9b-1e4c61b25bf6
ms.openlocfilehash: 3825ea8e57c6863e2ee654072efda623db21c2a8
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111999"
---
# <a name="maximize-wpf-3d-performance"></a>WPF の 3D パフォーマンスの最大化
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] を使用して 3D コントロールを作成し、アプリケーションに 3D シーンを含めるときに、パフォーマンスの最適化を考慮することが重要です。 このトピックでは、アプリケーションのパフォーマンスに影響を与える 3D クラスとプロパティの一覧を示し、それらを使用するときにパフォーマンスを最適化するための推奨事項も併せて説明します。  
  
 このトピックは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 3D 機能について詳しく理解していることを前提としています。 このドキュメントの提案は、"レンダリング層 2" (おおまかに言うと、ピクセル シェーダー バージョン 2.0 と頂点シェーダー バージョン 2.0 をサポートするハードウェアとして定義されています) に適用されます。 詳細については、「[グラフィックスの描画層](../advanced/graphics-rendering-tiers.md)」を参照してください。  
  
## <a name="performance-impact-high"></a>パフォーマンスへの影響:High  
  
|プロパティ|推奨事項|  
|-|-|  
|<xref:System.Windows.Media.Brush>|ブラシの速度 (最速から低速):<br /><br /> <xref:System.Windows.Media.SolidColorBrush><br /><br /> <xref:System.Windows.Media.LinearGradientBrush><br /><br /> <xref:System.Windows.Media.ImageBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush> (キャッシュ済み)<br /><br /> <xref:System.Windows.Media.VisualBrush> (キャッシュ済み)<br /><br /> <xref:System.Windows.Media.RadialGradientBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush> (キャッシュされていない)<br /><br /> <xref:System.Windows.Media.VisualBrush> (キャッシュされていない)|  
|<xref:System.Windows.UIElement.ClipToBoundsProperty>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で <xref:System.Windows.Controls.Viewport3D> のコンテンツを Viewport3D の四角形に明示的にクリップする必要がない場合は常に、`Viewport3D.ClipToBounds` を false に設定します。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のアンチエイリアスされたクリッピングは非常に遅くなる可能性があり、<xref:System.Windows.Controls.Viewport3D> で `ClipToBounds` は既定で有効 (低速) になっています。|  
|<xref:System.Windows.UIElement.IsHitTestVisible%2A>|マウス ヒット テストの実行時に、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で <xref:System.Windows.Controls.Viewport3D> のコンテンツを考慮する必要がない場合は常に、`Viewport3D.IsHitTestVisible` を false に設定します。  3D コンテンツのヒット テストは、ソフトウェアで実行され、メッシュが大きいと速度が低下する場合があります。 <xref:System.Windows.Controls.Viewport3D> で <xref:System.Windows.UIElement.IsHitTestVisible%2A> は既定で有効 (低速) になっています。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D>|異なる素材または変換が必要な場合にのみ、異なるモデルを作成します。  それ以外の場合は、同じ素材と変換を含む多数の <xref:System.Windows.Media.Media3D.GeometryModel3D> インスタンスを、少数のより大きな <xref:System.Windows.Media.Media3D.GeometryModel3D> および <xref:System.Windows.Media.Media3D.MeshGeometry3D> インスタンスに結合しようとします。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|メッシュ アニメーション (フレームごとにメッシュの個々の頂点を変更すること) は、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では常に効率的であるとは限りません。  各頂点が変更されたときの変更通知のパフォーマンスへの影響を最小限に抑えるには、頂点ごとの変更を実行する前に、ビジュアル ツリーからメッシュを切り離します。  メッシュが変更されたら、それをビジュアル ツリーに再接続します。  また、この方法でアニメーション化されるメッシュのサイズを最小限にしてみます。|  
|3D アンチエイリアシング|レンダリングの速度を上げるには、添付プロパティ <xref:System.Windows.Media.RenderOptions.EdgeMode%2A> を `Aliased` に設定して、<xref:System.Windows.Controls.Viewport3D> でのマルチサンプリングを無効にします。  Windows では、ピクセルあたり 4 サンプルの 3D アンチエイリアシングが既定で有効になっています。|  
|テキスト|3D シーンのライブ テキスト (<xref:System.Windows.Media.DrawingBrush> または <xref:System.Windows.Media.VisualBrush> 内にあるためライブである) が低速になることがあります。 テキストが変更されない場合は、代わりに (<xref:System.Windows.Media.Imaging.RenderTargetBitmap> によって) テキストのイメージを使用してみてください。|  
|<xref:System.Windows.Media.TileBrush>|ブラシのコンテンツが静的でないために 3D シーンで <xref:System.Windows.Media.VisualBrush> または <xref:System.Windows.Media.DrawingBrush> を使用する必要がある場合は、ブラシのキャッシュを試します (添付プロパティ <xref:System.Windows.Media.RenderOptions.CachingHint%2A> を `Cache` に設定します)。  必要な品質レベルを維持したまま、キャッシュされたブラシがあまり頻繁に再生成されないように、(添付プロパティ <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> および <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> を使用して) 最小および最大のスケール無効化しきい値を設定します。  既定では、<xref:System.Windows.Media.DrawingBrush> と <xref:System.Windows.Media.VisualBrush> はキャッシュされません。つまり、ブラシで塗りつぶされたものを再レンダリングする必要があるたびに、まずブラシのコンテンツ全体を中間の面に再レンダリングする必要があります。|  
|<xref:System.Windows.Media.Effects.BitmapEffect>|<xref:System.Windows.Media.Effects.BitmapEffect> を使用すると、影響を受けるすべてのコンテンツがハードウェアの高速化なしで強制的にレンダリングされます。  パフォーマンスを最大限高めるには、<xref:System.Windows.Media.Effects.BitmapEffect> を使用しないでください。|  
  
## <a name="performance-impact-medium"></a>パフォーマンスへの影響:Medium  
  
|プロパティ|推奨事項|  
|-|-|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|メッシュが、共有頂点を持つ隣接した三角形として定義され、それらの頂点の位置、法線、およびテクスチャ座標が同じである場合は、各共有頂点を 1 回だけ定義し、<xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> を使用して指標によってそれらの三角形を定義します。|  
|<xref:System.Windows.Media.ImageBrush>|テクスチャのサイズを明示的に制御している場合 (<xref:System.Windows.Media.Imaging.RenderTargetBitmap> と <xref:System.Windows.Media.ImageBrush> のどちらか一方または両方を使用している場合) は、そのサイズを最小限にしてみます。  解像度テクスチャが低くなると、画質が低下する可能性があるので、品質とパフォーマンスの適切なバランスを探してください。|  
|Opacity|半透明の 3D コンテンツ (反射など) をレンダリングする場合は、`Viewport3D.Opacity` を 1 未満の値に設定することで別の半透明の <xref:System.Windows.Controls.Viewport3D> を作成するのではなく、(<xref:System.Windows.Media.Brush.Opacity%2A> または <xref:System.Windows.Media.Media3D.DiffuseMaterial.Color%2A> によって) ブラシまたは素材の不透明度プロパティを使用します。|  
|<xref:System.Windows.Controls.Viewport3D>|シーンで使用している <xref:System.Windows.Controls.Viewport3D> オブジェクトの数を最小限に抑えます。  モデルごとに個別の Viewport3D インスタンスを作成するのではなく、同じ Viewport3D に複数の 3D モデルを配置します。|  
|<xref:System.Windows.Freezable>|通常は、<xref:System.Windows.Media.Media3D.MeshGeometry3D>、<xref:System.Windows.Media.Media3D.GeometryModel3D>、ブラシ、素材を再利用すると便利です。  すべて `Freezable` から派生しているため、マルチペアレントにできます。|  
|<xref:System.Windows.Freezable>|アプリケーションでプロパティが変更されないままになる場合は、Freezable に対して <xref:System.Windows.Freezable.Freeze%2A> メソッドを呼び出します。  固定すると、ワーキング セットを減らして速度を上げることができます。|  
|<xref:System.Windows.Media.Brush>|ブラシのコンテンツが変更されない場合は、<xref:System.Windows.Media.VisualBrush> や <xref:System.Windows.Media.DrawingBrush> ではなく <xref:System.Windows.Media.ImageBrush> を使用します。  2D コンテンツは、<xref:System.Windows.Media.Imaging.RenderTargetBitmap> によって <xref:System.Windows.Controls.Image> に変換され、その後 <xref:System.Windows.Media.ImageBrush> で使用できます。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>|実際に <xref:System.Windows.Media.Media3D.GeometryModel3D> の背面を表示する必要がある場合を除き、<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> は使用しないでください。|  
|<xref:System.Windows.Media.Media3D.Light>|ライトの速度 (最速から低速):<br /><br /> <xref:System.Windows.Media.Media3D.AmbientLight><br /><br /> <xref:System.Windows.Media.Media3D.DirectionalLight><br /><br /> <xref:System.Windows.Media.Media3D.PointLight><br /><br /> <xref:System.Windows.Media.Media3D.SpotLight>|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|次の制限の下でメッシュ サイズを維持するようにしてください。<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>:20,001 個の <xref:System.Windows.Media.Media3D.Point3D> インスタンス<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>:60,003 個の <xref:System.Int32> インスタンス|  
|<xref:System.Windows.Media.Media3D.Material>|素材の速度 (最速から低速):<br /><br /> <xref:System.Windows.Media.Media3D.EmissiveMaterial><br /><br /> <xref:System.Windows.Media.Media3D.DiffuseMaterial><br /><br /> <xref:System.Windows.Media.Media3D.SpecularMaterial>|  
|<xref:System.Windows.Media.Brush>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 3D は、一貫した方法で非表示のブラシ (黒のアンビエント ブラシ、クリア ブラシなど) をオプトアウトしません。  これらをシーンに入れないことを検討してください。|  
|<xref:System.Windows.Media.Media3D.MaterialGroup>|<xref:System.Windows.Media.Media3D.MaterialGroup> 内の各 <xref:System.Windows.Media.Media3D.Material> で別のレンダリング パスが生成されます。そのため、単純な素材でも多くの素材を含めると、GPU で塗りつぶしの要求が大幅に増加する可能性があります。  <xref:System.Windows.Media.Media3D.MaterialGroup> 内の素材の数は最小限に抑えてください。|  
  
## <a name="performance-impact-low"></a>パフォーマンスへの影響:Low  
  
|プロパティ|推奨事項|  
|-|-|  
|<xref:System.Windows.Media.Media3D.Transform3DGroup>|アニメーションまたはデータ バインディングが不要な場合は、複数の変換を含む変換グループを使用するのではなく、1 つの <xref:System.Windows.Media.Media3D.MatrixTransform3D> を使用して、それを、使用しなければ変換グループに個別に存在する変換すべての結果に設定します。|  
|<xref:System.Windows.Media.Media3D.Light>|シーンのライト数を最小限に抑えます。 シーン内のライトが多すぎると、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] が強制的にソフトウェア レンダリングにフォールバックされます。  上限は、約 110 個の <xref:System.Windows.Media.Media3D.DirectionalLight> オブジェクト、70 個の <xref:System.Windows.Media.Media3D.PointLight> オブジェクト、または 40 個の<xref:System.Windows.Media.Media3D.SpotLight> オブジェクトです。|  
|<xref:System.Windows.Media.Media3D.ModelVisual3D>|静的オブジェクトを別の <xref:System.Windows.Media.Media3D.ModelVisual3D> インスタンスに配置することで、移動するオブジェクトとそれらを区別します。  ModelVisual3D は、変換された境界をキャッシュするので、<xref:System.Windows.Media.Media3D.GeometryModel3D> よりも "重い" です。  GeometryModel3D はモデルとして最適化され、ModelVisual3D はシーン ノードとして最適化されています。  GeometryModel3D の共有インスタンスをシーンに配置するには、ModelVisual3D を使用します。|  
|<xref:System.Windows.Media.Media3D.Light>|シーンのライト数を変更する回数を最小限に抑えます。  ライト数を変更するたびにシェーダーの再生成と再コンパイルが強制されます。ただし、その構成が以前に存在していた (そのため、そのシェーダーがキャッシュされていた) 場合を除きます。|  
|淡色|黒のライトは表示されませんが、レンダリング時間に追加されます。除外することを検討してください。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で MeshGeometry3D の <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>、<xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A>、<xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A>、<xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> などの大きなコレクションの構築時間を最小限に抑えるには、値の作成前にコレクションのサイズを事前に設定します。 可能であれば、コレクションのコンストラクターに、配列やリストなどの事前に作成されたデータ構造を渡します。|  
  
## <a name="see-also"></a>関連項目

- [3D グラフィックスの概要](3-d-graphics-overview.md)
