---
title: ビジュアル層でのヒット テスト
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit testing functionality [WPF]
- visual layer [WPF], hit testing functionality
ms.assetid: b1a64b61-14be-4d75-b89a-5c67bebb2c7b
ms.openlocfilehash: d4d304353e91147c57297dcc4525759ff1474b4f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186400"
---
# <a name="hit-testing-in-the-visual-layer"></a>ビジュアル層でのヒット テスト
ここでは、ビジュアル層で提供されるヒット テスト機能の概要について説明します。 ヒット テストのサポートにより、ジオメトリまたはポイント値が <xref:System.Windows.Media.Visual> のレンダリングされたコンテンツ内にあるかどうかを判断でき、複数のオブジェクトを選択するための選択四角形などのユーザー インターフェイスの動作を実装できます。  

<a name="hit_testing_scenarios"></a>
## <a name="hit-testing-scenarios"></a>ヒット テストのシナリオ  
 <xref:System.Windows.UIElement> クラスは、指定された座標値を使用して要素に対してヒット テストを実行できるようにする <xref:System.Windows.UIElement.InputHitTest%2A> メソッドを提供します。 多くの場合、<xref:System.Windows.UIElement.InputHitTest%2A> メソッドは、要素のヒット テストを実装するために必要な機能を提供します。 ただし、ビジュアル層でのヒット テストを実装する必要があるシナリオもいくつか存在します。  
  
- <xref:System.Windows.UIElement> 以外のオブジェクトに対するヒット テスト: これは、<xref:System.Windows.Media.DrawingVisual> やグラフィックス オブジェクトなど、<xref:System.Windows.UIElement> 以外のオブジェクトのヒット テストを行う場合に適用されます。  
  
- ジオメトリを使用したヒット テスト: これは、ポイントの座標値ではなくジオメトリ オブジェクトを使用してヒット テストを行う必要がある場合に適用されます。  
  
- 複数のオブジェクトに対するヒット テスト: 重なっているオブジェクトなどの複数のオブジェクトに対してヒット テストを行う必要がある場合に適用されます。 最初のビジュアルだけでなく、ジオメトリまたはポイントと交差するすべてのビジュアルの結果を取得できます。  
  
- <xref:System.Windows.UIElement> ヒット テスト ポリシーの無視: これは、要素が無効化されているか、または非表示になっているかなどの要因を考慮する <xref:System.Windows.UIElement> ヒット テスト ポリシーを無視する必要がある場合に適用されます。  
  
> [!NOTE]
> ビジュアル層でのテスト ヒットを示すコード サンプル全体については、「[DrawingVisuals を使用したヒット テストのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Visual%20Layer/DrawingVisual)」と「[Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)」を参照してください。  
  
<a name="hit_testing_support"></a>
## <a name="hit-testing-support"></a>ヒット テストのサポート  
 <xref:System.Windows.Media.VisualTreeHelper> クラスの <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドの目的は、ジオメトリまたはポイントの座標値が、特定のオブジェクト (コントロールやグラフィック要素など) のレンダリングされたコンテンツ内にあるかどうかを確認することです。 たとえば、ヒット テストを使用することで、オブジェクトの外接する四角形内でのマウス クリックが、円のジオメトリ内にあるかどうかを確認できます。 また、ヒット テストの既定の実装をオーバーライドして、独自のカスタム ヒット テスト計算を実行することもできます。  
  
 四角形以外のオブジェクトの領域と外接する四角形の関係を次の図に示します。  
  
 ![有効なヒット テスト領域のダイアグラム](./media/wcpsdk-mmgraphics-visuals-hittest-1.png "wcpsdk_mmgraphics_visuals_hittest_1")  
有効なヒット テスト領域のダイアグラム  
  
<a name="hit_testing_and_z-order"></a>
## <a name="hit-testing-and-z-order"></a>ヒット テストと z オーダー  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のビジュアル層は、最上位のオブジェクトだけでなく、ポイントまたはジオメトリの下にあるすべてのオブジェクトに対するヒット テストをサポートします。 結果は z オーダーで返されます。 ただし、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドにパラメーターとして渡すビジュアル オブジェクトによって、ビジュアル ツリーのどの部分がヒット テストの対象となるかが決まります。 ヒット テストは、ビジュアル ツリー全体またはその一部に対して実行できます。  
  
 次の図では、四角形と三角形の両方のオブジェクト上に円オブジェクトがあります。 z オーダーの値が最上位のビジュアル オブジェクトのヒット テストのみに関心がある場合は、<xref:System.Windows.Media.HitTestResultCallback> から <xref:System.Windows.Media.HitTestResultBehavior.Stop> を返すようにビジュアル ヒット テストの列挙体を設定して、最初の項目の後にヒット テストの走査を停止することができます。  
  
 ![ビジュアル ツリーの z オーダーのダイアグラム](./media/wcpsdk-mmgraphics-visuals-hittest-2.png "wcpsdk_mmgraphics_visuals_hittest_2")  
ビジュアル ツリーの z オーダーのダイアグラム  
  
 特定のポイントまたはジオメトリの下にあるすべてのビジュアル オブジェクトを列挙する場合は、<xref:System.Windows.Media.HitTestResultCallback> から <xref:System.Windows.Media.HitTestResultBehavior.Continue> を返します。 つまり、完全に隠されているものも含めて、他のオブジェクトの下にあるすべてのビジュアル オブジェクトに対してヒット テストを行うことができます。 詳細については、「ヒット テスト結果のコールバックの使用」のサンプル コードを参照してください。  
  
> [!NOTE]
> 透明なビジュアル オブジェクトのヒット テストも実行できます。  
  
<a name="using_default_hit_testing"></a>
## <a name="using-default-hit-testing"></a>既定のヒット テストの使用  
 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドを使用して、テストを実行するビジュアル オブジェクトとポイントの座標値を指定することにより、ビジュアル オブジェクトのジオメトリ内にポイントがあるかどうかを識別できます。 ビジュアル オブジェクトのパラメーターは、ヒット テストの検索のためのビジュアル ツリー内の開始点を識別します。 ビジュアル オブジェクトは、ジオメトリに座標が含まれているビジュアル ツリー内に存在する場合は、<xref:System.Windows.Media.HitTestResult> オブジェクトの <xref:System.Windows.Media.HitTestResult.VisualHit%2A> プロパティに設定されます。 その後、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドから <xref:System.Windows.Media.HitTestResult> が返されます。 ヒット テストを行っているビジュアル サブツリーにポイントが含まれていない場合、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> は `null` を返します。  
  
> [!NOTE]
> 既定のヒット テストでは、常に z オーダーで最上位のオブジェクトが返されます。 部分的または完全に隠されているものも含めて、すべてのビジュアル オブジェクトを識別するには、ヒット テストの結果のコールバックを使用します。  
  
 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドのポイント パラメーターとして渡す座標値は、ヒット テストの対象であるビジュアル オブジェクトの座標空間に対して相対的である必要があります。 たとえば、入れ子になったビジュアル オブジェクトが親の座標空間の (100, 100) に定義されている場合、(0, 0) での子のビジュアルのヒット テストは、親の座標空間の (100, 100) でのヒット テストと同じになります。  
  
 次のコードでは、ヒット テストに使用するイベントをキャプチャするために使用される <xref:System.Windows.UIElement> オブジェクトにマウス イベント ハンドラーを設定する方法を示します。  
  
 [!code-csharp[HitTestingOverview#100](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[HitTestingOverview#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#100)]  
  
### <a name="how-the-visual-tree-affects-hit-testing"></a>ヒット テストに対するビジュアル ツリーの影響  
 ビジュアル ツリー内の開始点によって、ヒット テストによるオブジェクトの列挙時に返されるオブジェクトが決定されます。 ヒット テストの対象となるオブジェクトが複数存在する場合、ビジュアル ツリー内の開始点として使用されるビジュアル オブジェクトは、対象となるすべてのオブジェクトの共通の先祖である必要があります。 たとえば、次の図のボタン要素と描画ビジュアルの両方のヒット テストを行う場合、ビジュアル ツリー内の開始点を、その両方の共通の先祖に設定する必要があります。 この場合、キャンバス要素がボタン要素と描画ビジュアルの両方の共通の先祖になります。  
  
 ![ビジュアル ツリー階層のダイアグラム](./media/wcpsdk-mmgraphics-visuals-overview-01.gif "wcpsdk_mmgraphics_visuals_overview_01")  
ビジュアル ツリー階層のダイアグラム  
  
> [!NOTE]
> <xref:System.Windows.UIElement.IsHitTestVisible%2A> プロパティは、レンダリングされたコンテンツの一部からヒット テストの結果として <xref:System.Windows.UIElement> 派生オブジェクトが返される可能性があるかどうかを宣言する値を取得または設定します。 これにより、ビジュアル ツリーを選択的に変更し、ヒット テストの対象となるビジュアル オブジェクトを決定することができます。  
  
<a name="using_a_hit_test_result_callback"></a>
## <a name="using-a-hit-test-result-callback"></a>ヒット テスト結果のコールバックの使用  
 ジオメトリに指定した座標値が含まれるビジュアル ツリーのすべてのビジュアル オブジェクトを列挙できます。 これにより、他のビジュアル オブジェクトによって部分的または完全に隠されているものも含めて、すべてのビジュアル オブジェクトを識別することができます。 ビジュアル ツリー内のビジュアル オブジェクトを列挙するには、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドとヒット テスト コールバック関数を使用します。 ヒット テスト コールバック関数は、指定した座標値がビジュアル オブジェクトに含まれている場合にシステムによって呼び出されます。  
  
 ヒット テストの結果の列挙時には、ビジュアル ツリーを変更する操作を実行しないでください。 走査中のビジュアル ツリーに対してオブジェクトの追加または削除を行うと、予測不可能な動作を招く可能性があります。 ビジュアル ツリーは、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドが返された後で、安全に変更できます。 <xref:System.Collections.ArrayList> などのデータ構造体を提供して、ヒット テストの結果の列挙時に値を格納することもできます。  
  
 [!code-csharp[HitTestingOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[HitTestingOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#101)]  
  
 ヒット テストのコールバック メソッドは、ビジュアル ツリーの特定のビジュアル オブジェクトでヒット テストが識別されたときに、ユーザーが実行するアクションを定義します。 アクションを実行したら、その他のビジュアル オブジェクトの列挙を続行するかどうかを決定する <xref:System.Windows.Media.HitTestResultBehavior> 値を返します。  
  
 [!code-csharp[HitTestingOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[HitTestingOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#102)]  
  
> [!NOTE]
> ヒットしたビジュアル オブジェクトの列挙の順序は、z オーダー順です。 z オーダーの最上位のビジュアル オブジェクトが最初に列挙されます。 その他のビジュアル オブジェクトは、z オーダーの上位から順に列挙されます。 この列挙の順序は、ビジュアルの描画順序に対応します。  
  
 <xref:System.Windows.Media.HitTestResultBehavior.Stop> を返すことによって、ヒット テスト コールバック関数の任意の時点でビジュアル オブジェクトの列挙を停止できます。  
  
 [!code-csharp[HitTestingOverview#103](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#103)]
 [!code-vb[HitTestingOverview#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#103)]  
  
<a name="using_a_hit_test_filter_callback"></a>
## <a name="using-a-hit-test-filter-callback"></a>ヒット テスト フィルターのコールバックの使用  
 オプションのヒット テスト フィルターを使用して、ヒット テストの結果に渡されるオブジェクトを制限できます。 これにより、ヒット テストの結果でビジュアル ツリーの一部を処理する必要がない場合、その部分を無視できます。 ヒット テスト フィルターを実装するには、ヒット テスト フィルターのコールバック関数を定義して、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドを呼び出すときにパラメーター値として渡します。  
  
 [!code-csharp[HitTestingOverview#104](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#104)]
 [!code-vb[HitTestingOverview#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#104)]  
  
 オプションのヒット テスト フィルターのコールバック関数を指定しない場合は、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドのパラメーターとして `null` 値を渡します。  
  
 [!code-csharp[HitTestingOverview#105](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#105)]
 [!code-vb[HitTestingOverview#105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#105)]  
  
 ![ヒット テスト フィルターを使用したビジュアル ツリーの簡略化](./media/filteredvisualtree-01.png "FilteredVisualTree_01")  
ビジュアル ツリーの簡略化  
  
 ヒット テスト フィルターのコールバック関数を使用すると、描画されるコンテンツに指定した座標が含まれるすべてのビジュアルを列挙できます。 ただし、ヒット テストの結果のコールバック関数で、ビジュアル ツリーの一部の分岐を処理する必要がない場合、これらの分岐を無視できます。 ヒット テスト フィルターのコールバック関数の戻り値によって、ビジュアル オブジェクトの列挙体が実行するアクションの種類が決定されます。 たとえば、値 <xref:System.Windows.Media.HitTestFilterBehavior.ContinueSkipSelfAndChildren> を返した場合、ヒット テストの結果の列挙体から現在のビジュアル オブジェクトとその子を削除できます。 つまり、ヒット テストの結果のコールバック関数は、列挙体でこれらのオブジェクトを認識しなくなります。 オブジェクトのビジュアル ツリーから余分なものを取り除くと、ヒット テストの結果の列挙体が渡されるときの処理を減らすことができます。 次のコード例では、フィルターはラベルとその子孫をスキップし、他のすべてのヒット テストを行います。  
  
 [!code-csharp[HitTestingOverview#106](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#106)]
 [!code-vb[HitTestingOverview#106](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#106)]  
  
> [!NOTE]
> ヒット テスト フィルターのコールバックは、ヒット テストの結果のコールバックが呼び出されない場合に呼び出されることがあります。  
  
<a name="overriding_default_hit_testing"></a>
## <a name="overriding-default-hit-testing"></a>既定のヒット テストのオーバーライド  
 <xref:System.Windows.Media.Visual.HitTestCore%2A> メソッドをオーバーライドすることにより、ビジュアル オブジェクトの既定のヒット テスト サポートをオーバーライドできます。 これは、<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドを呼び出すと、<xref:System.Windows.Media.Visual.HitTestCore%2A> のオーバーライドされた実装が呼び出されることを意味します。 座標がビジュアル オブジェクトの描画されるコンテンツの外側にあっても、ビジュアル オブジェクトの外接する四角形内でヒット テストが実行されると、オーバーライドされたメソッドが呼び出されます。  
  
 [!code-csharp[HitTestingOverview#107](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#107)]
 [!code-vb[HitTestingOverview#107](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#107)]  
  
 ビジュアル オブジェクトの外接する四角形と描画されるコンテンツの両方に対してヒット テストを行う必要が生じる場合もあります。 オーバーライドされた <xref:System.Windows.Media.Visual.HitTestCore%2A> メソッドの `PointHitTestParameters` パラメーター値を基本メソッド <xref:System.Windows.Media.Visual.HitTestCore%2A> のパラメーターとして使用すると、ビジュアル オブジェクトの外接する四角形のヒットに基づいてアクションを実行し、ビジュアル オブジェクトのレンダリングされたコンテンツに対して 2 番目のヒット テストを実行できます。  
  
 [!code-csharp[HitTestingOverview#108](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#108)]
 [!code-vb[HitTestingOverview#108](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#108)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>
- <xref:System.Windows.Media.HitTestResult>
- <xref:System.Windows.Media.HitTestResultCallback>
- <xref:System.Windows.Media.HitTestFilterCallback>
- <xref:System.Windows.UIElement.IsHitTestVisible%2A>
- [DrawingVisuals を使用したヒット テストのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Visual%20Layer/DrawingVisual)
- [Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)
- [ビジュアル内のジオメトリのヒット テストを実行する](how-to-hit-test-geometry-in-a-visual.md)
- [Win32 ホスト コンテナーを使用してヒット テストを実行する](how-to-hit-test-using-a-win32-host-container.md)
