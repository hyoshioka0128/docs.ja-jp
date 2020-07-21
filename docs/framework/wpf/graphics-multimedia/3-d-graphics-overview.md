---
title: 3D グラフィックスの概要
description: Windows Presentation Foundation (WPF) の 3D グラフィックスを使用する、マークアップと手続き型コードの両方での 3D グラフィックスの描画、変換、およびアニメーション化について理解を深めます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 3D graphics [WPF]
- graphics [WPF], 3D
ms.assetid: 67f31ed4-e36b-4b02-9889-dcce245d7afc
ms.openlocfilehash: 51da6a1ed6d5e98b99c64ee23be52f7b2385897f
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853875"
---
# <a name="3d-graphics-overview"></a>3D グラフィックスの概要
<a name="introduction"></a>[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の 3D 機能を使用すると、開発者は、マークアップと手続き型コードの両方で 3D グラフィックスを描画、変換、およびアニメーション化できます。 開発者は 2D と 3D グラフィックスを組み合わせて、リッチなコントロールを作成したり、データの複雑なイラストを提供したり、アプリケーションのインターフェイスのユーザー エクスペリエンスを拡張したりすることができます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での 3D のサポートは、フル機能のゲーム開発プラットフォームを提供するようには設計されていません。 このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] グラフィックス システムでの 3D 機能の概要について説明します。  

<a name="threed_in_2d"></a>
## <a name="3d-in-a-2d-container"></a>2D コンテナーでの 3D  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での 3D グラフィックス コンテンツは <xref:System.Windows.Controls.Viewport3D> 要素にカプセル化されており、2 次元要素の構造体に含めることができます。 グラフィックス システムは、<xref:System.Windows.Controls.Viewport3D> を、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内の他の多くの要素と同様に 2 次元のビジュアル要素として処理します。 <xref:System.Windows.Controls.Viewport3D> は、3 次元シーンのウィンドウ (ビューポート) として機能します。 より正確には、3D シーンが投影されるサーフェイスです。  
  
 従来の 2D アプリケーションでは、グリッドやキャンバスのような別のコンテナー要素と同じように <xref:System.Windows.Controls.Viewport3D> を使用します。  同じシーン グラフ内で他の 2D 描画オブジェクトと共に <xref:System.Windows.Controls.Viewport3D> を使用できますが、<xref:System.Windows.Controls.Viewport3D> 内の 2D と 3D オブジェクトを相互に貫通させることはできません。  このトピックでは、<xref:System.Windows.Controls.Viewport3D> の内部に 3D グラフィックスを描画する方法について説明します。  
  
<a name="coord_space"></a>
## <a name="3d-coordinate-space"></a>3D 座標空間  
 2D グラフィックス用の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 座標系の原点は、レンダリング領域 (通常は画面) の左上にあります。 2D システムでは、x 軸の正の値は右に向かって大きくなり、y 軸の正の値は下に向かって大きくなります。  一方、3D 座標系では、原点はレンダリング領域の中央にあり、x 軸の正の値は右に向かって大きくなりますが、y 軸の正の値は上に向かって大きくなり、z 軸の正の値は原点から手前に向かって大きくなります。  
  
 ![座標系](./media/coordsystem-1.png "CoordSystem-1")  
従来の 2D および 3D 座標系の表現  
  
 これらの軸によって定義される空間は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内の 3D オブジェクトのための静止した基準枠です。 この空間内にモデルを構築し、それらを表示するためのライトとカメラを作成するときは、この静止した基準枠 ("ワールド空間") と、モデルに変換を適用するときにモデルごとに作成するローカルな基準枠を区別することをお勧めします。 また、ワールド空間内のオブジェクトは、ライトとカメラの設定により、まったく違って見えたり、またはまったく見えなくなることがありますが、カメラの位置によってワールド空間内のオブジェクトの場所が変化することはないことに注意してください。  
  
<a name="cameras"></a>
## <a name="cameras-and-projections"></a>カメラと投影  
 2D で作業する開発者は、2 次元の画面に描画プリミティブを配置することに慣れています。 3D シーンを作成するときは、実際には 3D オブジェクトの 2D 表現を作成しているということを忘れないようにすることが重要です。 3D シーンは観察者の視点によって見え方が異なるので、その視点を指定する必要があります。 <xref:System.Windows.Media.Media3D.Camera> クラスを使用して、3D シーンに対するこの視点を指定できます。  
  
 3D シーンが 2D サーフェイス上でどのように表現されるかを理解するもう 1 つの方法は、表示サーフェイスへの投影としてシーンを記述することです。 <xref:System.Windows.Media.Media3D.ProjectionCamera> を使用すると、異なる投影とそのプロパティを指定して、観察者に対する 3D モデルの見え方を変更できます。 <xref:System.Windows.Media.Media3D.PerspectiveCamera> は、シーンを短縮遠近法で描画する投影を指定します。  つまり、<xref:System.Windows.Media.Media3D.PerspectiveCamera> は消失点透視投影を提供します。  シーンの座標空間内でのカメラの位置、カメラの方向と視野、およびシーン内での "上" の方向を定義するベクトルを指定できます。 次の図は、<xref:System.Windows.Media.Media3D.PerspectiveCamera> の投影を示したものです。  
  
 <xref:System.Windows.Media.Media3D.ProjectionCamera> の <xref:System.Windows.Media.Media3D.ProjectionCamera.NearPlaneDistance%2A> と <xref:System.Windows.Media.Media3D.ProjectionCamera.FarPlaneDistance%2A> プロパティは、カメラの投影の範囲を制限します。 カメラはシーン内の任意の場所に配置できるため、カメラをモデルの内部またはモデルの非常に近くに実際に配置することができ、オブジェクトを正しく識別するのが困難になる場合があります。  <xref:System.Windows.Media.Media3D.ProjectionCamera.NearPlaneDistance%2A> では、それより近くにはオブジェクトを描画できないカメラからの最小距離を指定できます。  逆に、<xref:System.Windows.Media.Media3D.ProjectionCamera.FarPlaneDistance%2A> では、それより遠くにはオブジェクトが描画されないカメラからの距離を指定でき、遠すぎて識別できないオブジェクトがシーンに含まれないようにすることができます。  
  
 ![カメラの設定](./media/coordsystem-6.png "CoordSystem-6")  
カメラの位置  
  
 <xref:System.Windows.Media.Media3D.OrthographicCamera> は、2D ビジュアル サーフェイスへの 3D モデルの正投影を指定します。 他のカメラと同じように、位置、視線方向、および "上" の向きを指定します。 ただし、<xref:System.Windows.Media.Media3D.PerspectiveCamera> とは異なり、<xref:System.Windows.Media.Media3D.OrthographicCamera> によって記述されるのは遠近法を含まない投影です。 つまり、<xref:System.Windows.Media.Media3D.OrthographicCamera> は、辺がカメラの位置で一致する描画ボックスではなく、辺が平行な描画ボックスを記述します。 次の図は、同じモデルを <xref:System.Windows.Media.Media3D.PerspectiveCamera> と <xref:System.Windows.Media.Media3D.OrthographicCamera> を使用して表示したものです。  
  
 ![正投影と透視投影](./media/camera-projections4.png "Camera_projections4")  
透視投影と正投影  
  
 次のコードでは、カメラの一般的な設定を示します。  
  
 [!code-csharp[3dgallery_procedural_snip#Basic3DShapeCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Basic3DShapeExample.cs#basic3dshapecodeexampleinline1)]
 [!code-vb[3dgallery_procedural_snip#Basic3DShapeCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/basic3dshapeexample.vb#basic3dshapecodeexampleinline1)]  
  
<a name="models_meshes"></a>
## <a name="model-and-mesh-primitives"></a>モデルとメッシュ プリミティブ  
  
 <xref:System.Windows.Media.Media3D.Model3D> は、ジェネリック型の 3D オブジェクトを表す抽象基底クラスです。 3D シーンを構築するには、表示するオブジェクトと、<xref:System.Windows.Media.Media3D.Model3D> から派生するシーン グラフを構成するオブジェクトが必要です。 現在、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は <xref:System.Windows.Media.Media3D.GeometryModel3D> でモデリング ジオメトリをサポートしています。 このモデルの <xref:System.Windows.Media.Media3D.GeometryModel3D.Geometry%2A> プロパティは、メッシュ プリミティブを受け取ります。  
  
 モデルを構築するには、最初にプリミティブ (メッシュ) を作成します。 3D のプリミティブは、1 つの 3D エンティティを形成する頂点の集合です。 ほとんどの 3D システムでは、最も簡単な閉じた図形 (3 つの頂点で定義された三角形) でモデル化されたプリミティブが提供されます。  三角形の 3 つの頂点は同一平面上にあるため、三角形の追加を続けて、メッシュと呼ばれる複雑な図形をモデル化できます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 3D システムで現在提供されている <xref:System.Windows.Media.Media3D.MeshGeometry3D> クラスを使用すると、ジオメトリを指定できます。球や立方体のような定義済みの 3D プリミティブは現在サポートされていません。 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> プロパティとして三角形の頂点のリストを指定することにより、<xref:System.Windows.Media.Media3D.MeshGeometry3D> の作成を開始します。 各頂点を <xref:System.Windows.Media.Media3D.Point3D> として指定します。  ([!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、各頂点の座標を表す 3 組の数値のリストとして、このプロパティを指定します)。ジオメトリによっては、メッシュが多くの三角形で構成され、その一部が同じ角 (頂点) を共有する可能性があります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でメッシュを正しく描画するには、どの頂点がどの三角形によって共有されているのかということに関する情報が必要です。 この情報は、<xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> プロパティで三角形の頂点のリストを指定することにより提供します。 このリストでは、<xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> のリストで指定されている点が三角形を決定する順序を指定します。  
  
 [!code-xaml[basic3d#Basic3DXAML3DN3](~/samples/snippets/xaml/VS_Snippets_Wpf/Basic3D/XAML/Window1.xaml#basic3dxaml3dn3)]  
  
 上の例の <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> のリストでは、立方体の形状をしたメッシュを定義する 8 個の頂点が指定されています。 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> プロパティでは、3 つの頂点の 12 個のグループのリストが指定されています。  リストの各数値は、<xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> のリストへのオフセットを示します。  たとえば、<xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> のリストで指定されている最初の 3 つの頂点は、(1,1,0)、(0,1,0)、(0,0,0) です。 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> のリストで指定されている最初の 3 つの頂点は 0、2、1 であり、これは <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> のリストの 1 番目、3 番目、2 番目の点に対応します。 つまり、この立方体モデルを構成する最初の三角形は、(1,1,0)、(0,1,0)、(0,0,0) から作成されます。残りの 11 個の三角形も同じようにして決定されます。  
  
 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A> および <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> プロパティの値を指定することで、モデルの定義を続けることができます。  グラフィックス システムがモデルのサーフェイスをレンダリングするには、特定の三角形において面が向いている方向に関する情報が必要です。 この情報を使って、モデルの照明の計算が行われます。光源に正対しているサーフェイスは、光源に対して角度のあるサーフェスより明るくなります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]は位置座標を使って既定の法線ベクトルを決定できますが、曲面の外観を近似する別の法線ベクトルを指定することもできます。  
  
 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> プロパティは、メッシュの頂点に対するテクスチャの描画方法を決定する座標のマップ方法をグラフィックス システムに指示する <xref:System.Windows.Point> のコレクションを指定します。 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> は 0 から 1 (この値を含む) の範囲の値で指定します。  <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A> プロパティと同様に、グラフィックス システムは既定のテクスチャ座標を計算できますが、異なるテクスチャ座標を設定して、たとえば繰り返しパターンの一部を含むテクスチャのマッピングを制御できます。 テクスチャ座標について詳しくは、マネージド Direct3D SDK の後続のトピックをご覧ください。  
  
 次の例では、手続き型コードで立方体モデルの 1 つの面を作成する方法を示します。 立方体全体を単一の GeometryModel3D として描画できます。この例では、後で各面に異なるテクスチャを適用するため、個別のモデルとして立方体の面を描画します。  
  
 [!code-csharp[3doverview#3DOverview3DN6](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn6)]
 [!code-vb[3doverview#3DOverview3DN6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn6)]  
  
 [!code-csharp[3doverview#3DOverview3DN7](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn7)]
 [!code-vb[3doverview#3DOverview3DN7](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn7)]  
  
<a name="materials"></a>'
## <a name="applying-materials-to-the-model"></a>モデルへのマテリアルの適用  
  
 メッシュが 3 次元のオブジェクトのように見えるには、頂点と三角形によって定義されたサーフェイスをカバーするようにテクスチャを適用し、カメラで照明および投影できるようにする必要があります。 2D では、色、パターン、グラデーション、その他のビジュアル コンテンツを画面の領域に適用するには、<xref:System.Windows.Media.Brush> クラスを使用します。  ただし、3D オブジェクトの見た目は、オブジェクトに適用された色またはパターンだけでなく、照明モデルの関数になります。 現実世界のオブジェクトは、サーフェイスの質によって光の反射が異なります。光沢のあるサーフェイスの見た目は荒くて艶のないサーフェイスとは異なり、光を吸収するオブジェクトや反射するオブジェクトがあります。 2D オブジェクトに適用できるものと同じすべてのブラシを 3D オブジェクトにも適用できますが、直接適用することはできません。  
  
 モデルのサーフェイスの特性を定義するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で<xref:System.Windows.Media.Media3D.Material> 抽象クラスを使用します。 Material の具象サブクラスでは、モデルのサーフェイスの一部の外観特性が決まり、SolidColorBrush、TileBrush、または VisualBrush を渡すことができる Brush プロパティも提供されます。  
  
- <xref:System.Windows.Media.Media3D.DiffuseMaterial> は、そのモデルがディフューズ光で照らされているかのように、モデルにブラシが適用されることを指定します。 DiffuseMaterial を使用することは、2D モデルにブラシを直接使うことと最もよく似ています。モデルのサーフェイスは光沢があるようにはライトを反射しません。  
  
- <xref:System.Windows.Media.Media3D.SpecularMaterial> は、モデルのサーフェイスが硬いか光沢があり、ハイライトを反射するように、モデルにブラシを適用するよう指定します。 <xref:System.Windows.Media.Media3D.SpecularMaterial.SpecularPower%2A> プロパティの値を指定することにより、テクスチャがこの反射品質 ("光沢") を示唆するレベルを設定できます。  
  
- <xref:System.Windows.Media.Media3D.EmissiveMaterial> を使用すると、モデルがブラシの色と同じライトを放射しているように、テクスチャを適用するよう指定できます。 これによってモデルが明るくなることはありませんが、DiffuseMaterial または SpecularMaterial のテクスチャとは異なるシャドウになります。  
  
 パフォーマンスを向上させるには、<xref:System.Windows.Media.Media3D.GeometryModel3D> の背面 (カメラとは反対側にあるために見ることができないモデルの面) をシーンから除去できます。  平面など、モデルの背面に適用する <xref:System.Windows.Media.Media3D.Material> を指定するには、モデルの <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> プロパティを設定します。  
  
 光彩効果や反射効果など、ある種のサーフェイス品質を実現するには、複数の異なるブラシを連続してモデルに適用することが必要な場合があります。 <xref:System.Windows.Media.Media3D.MaterialGroup> クラスを使用することで、複数の Material を適用および再利用できます。 MaterialGroup の子は、複数のレンダリング パスの最初から最後まで適用されます。  
  
 次のコード例では、単色と描画をブラシとして 3D モデルに適用する方法を示します。  
  
 [!code-xaml[basic3d#Basic3DXAML3DN5](~/samples/snippets/xaml/VS_Snippets_Wpf/Basic3D/XAML/Window1.xaml#basic3dxaml3dn5)]  
  ' [!code-xaml[3doverview#3DOverview3DN9](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/app.xaml#3doverview3dn9)]  
 ' [!code-csharp[3doverview#3DOverview3DN8](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn8)]
  [!code-vb[3doverview#3DOverview3DN8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn8)]  
  
<a name="lights"></a>
## <a name="illuminating-the-scene"></a>シーンの照明  
 3D グラフィックスのライトは、現実でのライトと同じように働いて、サーフェイスを見えるようにします。 さらに重要なことは、ライトによって投影に含まれるシーンの部分が決まります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の Light オブジェクトは、さまざまなライト効果とシャドウ効果を作成し、現実世界のさまざまな照明の動作に従ってモデル化されます。 シーンには少なくとも 1 つのライトを含めます。そうしないとモデルは見えません。  
  
 基底クラス <xref:System.Windows.Media.Media3D.Light> からは次のライトが派生します。  
  
- <xref:System.Windows.Media.Media3D.AmbientLight>:位置や方向に関係なくすべてのオブジェクトを一様に照らす環境光を提供します。  
  
- <xref:System.Windows.Media.Media3D.DirectionalLight>:光源が遠くにあるように照らします。  指向性ライトでは <xref:System.Windows.Media.Media3D.DirectionalLight.Direction%2A> を Vector3D として指定しますが、位置は指定しません。  
  
- <xref:System.Windows.Media.Media3D.PointLight>:光源が近くにあるように照らします。 PointLight には位置があり、その位置から光を投射します。 シーン内のオブジェクトは、その位置および光源からの距離に応じて照らされます。 <xref:System.Windows.Media.Media3D.PointLightBase> の <xref:System.Windows.Media.Media3D.PointLightBase.Range%2A> プロパティでは、モデルがライトによって照らされなくなる最も遠い距離を指定します。 また、PointLight には減衰プロパティもあり、距離によって光の強度がどの程度低下するかを指定します。 光の減衰には、一定、線形、または 2 次補間を指定できます。  
  
- <xref:System.Windows.Media.Media3D.SpotLight>:<xref:System.Windows.Media.Media3D.PointLight>から継承します。 SpotLight は PointLight と同じように照らし、位置と方向の両方を持ちます。 <xref:System.Windows.Media.Media3D.SpotLight.InnerConeAngle%2A> と <xref:System.Windows.Media.Media3D.SpotLight.OuterConeAngle%2A> プロパティで角度によって指定される円錐状の領域に、光を照射します。  
  
 Light は <xref:System.Windows.Media.Media3D.Model3D> オブジェクトであるため、位置、色、方向、範囲などのライトのプロパティを、変換およびアニメーション化できます。  
  
 [!code-xaml[hittest3d#HitTest3D3DN6](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml#hittest3d3dn6)]  
  
 [!code-csharp[basic3d#Basic3D3DN11](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn11)]
 [!code-vb[basic3d#Basic3D3DN11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn11)]  
  
 [!code-csharp[basic3d#Basic3D3DN12](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn12)]
 [!code-vb[basic3d#Basic3D3DN12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn12)]  
  
 [!code-csharp[basic3d#Basic3D3DN13](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn13)]
 [!code-vb[basic3d#Basic3D3DN13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn13)]  
  
<a name="transforms"></a>
## <a name="transforming-models"></a>モデルの変換  
 モデルを作成するとき、モデルにはシーン内で特定の位置があります。 モデルをシーン内で移動したり、回転したり、そのサイズを変更したりするのに、モデル自体を定義する頂点を変更するのは実用的ではありません。  そのような場合は、2D と同じように、モデルに変換を適用します。  
  
 各モデル オブジェクトが備える <xref:System.Windows.Media.Media3D.Model3D.Transform%2A> プロパティを使用して、モデルの移動、回転、サイズ変更を行うことができます。  変換を適用するときは、ベクトルにより、または変換で指定する値により、モデルのすべてのポイントをオフセットします。 つまり、モデルが定義されている座標空間 ("モデル空間") を変換するのであって、シーン全体の座標系 ("ワールド空間") 内でモデルのジオメトリを構成する値を変更するのではありません。  
  
 モデルの変換について詳しくは、「[3D 変換の概要](3-d-transformations-overview.md)」をご覧ください。  
  
<a name="animations"></a>
## <a name="animating-models"></a>モデルのアニメーション化  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の 3D の実装は、2D グラフィックスと同じタイミングおよびアニメーション システムに参加しています。 つまり、3D シーンをアニメーション化するには、そのモデルのプロパティをアニメーション化します。 プリミティブのプロパティを直接アニメーション化することもできますが、通常は、モデルの位置や外観を変更する変換をアニメーション化する方が簡単です。 変換は <xref:System.Windows.Media.Media3D.Model3DGroup> オブジェクトおよび個別のモデルに適用できるため、あるアニメーション セットを Model3Dgroup の子に適用し、別のアニメーション セットを子オブジェクトのグループに適用するといったことが可能です。 また、シーンの照明のプロパティをアニメーション化することにより、さまざまな視覚効果を実現できます。 最後に、カメラの位置または視野をアニメーション化することで、投影自体をアニメーション化することもできます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のタイミングおよびアニメーション システムの背景情報については、「[アニメーションの概要](animation-overview.md)」、「[ストーリーボードの概要](storyboards-overview.md)」、および「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」の各トピックをご覧ください。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のオブジェクトをアニメーション化するには、タイムラインを作成し、アニメーションを定義して (時間経過と共に一部のプロパティの値を実際に変更します)、アニメーションを適用するプロパティを指定します。 3D シーンのすべてのオブジェクトは <xref:System.Windows.Controls.Viewport3D> の子であるため、シーンに適用するアニメーションの対象となるプロパティは、Viewport3D のプロパティです。  
  
 その場で揺れるように見えるモデルを作成したいものとします。 そのためには、<xref:System.Windows.Media.Media3D.RotateTransform3D> をモデルに適用し、回転軸をあるベクトルから別のベクトルにアニメーション化します。 次のコード例では、RotateTransform3D が TransformGroup でモデルに適用される複数の変換の 1 つであるものとして、変換の Rotation3D の Axis プロパティに Vector3DAnimation を適用する方法を示します。  
  
 [!code-csharp[3doverview#3DOverview3DN1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn1)]
 [!code-vb[3doverview#3DOverview3DN1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn1)]  
  
 [!code-csharp[3doverview#3DOverview3DN3](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn3)]
 [!code-vb[3doverview#3DOverview3DN3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn3)]  
  
 [!code-csharp[3doverview#3DOverview3DN4](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn4)]
 [!code-vb[3doverview#3DOverview3DN4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn4)]  
  
 [!code-csharp[3doverview#3DOverview3DN5](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn5)]
 [!code-vb[3doverview#3DOverview3DN5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn5)]  
  
<a name="animations1"></a>
## <a name="add-3d-content-to-the-window"></a>ウィンドウへの 3D コンテンツの追加  
 シーンをレンダリングするには、モデルとライトを <xref:System.Windows.Media.Media3D.Model3DGroup> に追加した後、<xref:System.Windows.Media.Media3D.Model3DGroup> を <xref:System.Windows.Media.Media3D.ModelVisual3D> の <xref:System.Windows.Media.Media3D.ModelVisual3D.Content%2A> として設定します。 <xref:System.Windows.Media.Media3D.ModelVisual3D> を <xref:System.Windows.Controls.Viewport3D> の <xref:System.Windows.Controls.Viewport3D.Children%2A> コレクションに追加します。 <xref:System.Windows.Controls.Viewport3D.Camera%2A> プロパティを設定することにより、カメラを <xref:System.Windows.Controls.Viewport3D> に追加します。  
  
 最後に、<xref:System.Windows.Controls.Viewport3D> をウィンドウに追加します。 <xref:System.Windows.Controls.Viewport3D> がキャンバスなどのレイアウト要素のコンテンツとして含まれるときは、<xref:System.Windows.FrameworkElement.Height%2A> と <xref:System.Windows.FrameworkElement.Width%2A> プロパティ (<xref:System.Windows.FrameworkElement> から継承されます) を設定することによって、Viewport3D のサイズを指定します。  
  
 [!code-xaml[hostingwpfusercontrolinwf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Viewport3D>
- <xref:System.Windows.Media.Media3D.PerspectiveCamera>
- <xref:System.Windows.Media.Media3D.DirectionalLight>
- <xref:System.Windows.Media.Media3D.Material>
- [3D 変換の概要](3-d-transformations-overview.md)
- [WPF の 3D パフォーマンスの最大化](maximize-wpf-3d-performance.md)
- [方法トピック](3-d-graphics-how-to-topics.md)
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
