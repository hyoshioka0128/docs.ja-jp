---
title: インク スレッド モデル
ms.date: 03/30/2017
helpviewer_keywords:
- application user interface thread [WPF]
- stylus plug-in
- ink threading model [WPF]
- ink [WPF], rendering
- pen thread [WPF]
- threading model [WPF]
- rendering ink [WPF]
- dynamic rendering thread [WPF]
- ink collection plug-in
- plug-ins [WPF], for ink
ms.assetid: c85fcad1-cb50-4431-847c-ac4145a35c89
ms.openlocfilehash: b753fcffbdaa1cc9ba960a774077457dd0263e0a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64621371"
---
# <a name="the-ink-threading-model"></a>インク スレッド モデル
タブレット PC のインクの利点の 1 つが、通常のペンを使って紙に書く感覚に非常に似ていることです。  これを実現するために、タブレット ペンでは、マウスよりもはるかに高速に入力データが収集され、ユーザーが書くときに、インクがレンダリングされます。  アプリケーションのユーザー インターフェイス (UI) スレッドは、ペン データを収集してインクをレンダリングするのに十分ではありません。ブロックされる可能性があるためです。  これを解決するには、ユーザーがインクを書き込むときに、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションで、2 つの追加のスレッドを使用します。  
  
 次の一覧は、デジタル インクの収集とレンダリングに参加するスレッドを示しています。  
  
- ペン スレッド - スタイラスからの入力を受け取るスレッド  (実際には、これはスレッド プールですが、このトピックではペン スレッドと呼びます)。  
  
- アプリケーション ユーザー インターフェイス スレッド - アプリケーションのユーザー インターフェイスを制御するスレッド。  
  
- 動的レンダリング スレッド - ユーザーがストロークを描画している間、インクをレンダリングするスレッド。 動的レンダリング スレッドは、Window Presentation Foundation [スレッド モデル](threading-model.md)に説明されているように、アプリケーションの他の UI 要素をレンダリングするスレッドとは別です。  
  
 アプリケーションで使用されるのが、<xref:System.Windows.Controls.InkCanvas> でも、[インク入力コントロール作成](creating-an-ink-input-control.md)時のものに似たカスタム コントロールでも、インク モデルは同じです。  このトピックでは、スレッドについて <xref:System.Windows.Controls.InkCanvas> の観点から説明しますが、カスタム コントロールを作成する場合も同じ概念が適用されます。  
  
## <a name="threading-overview"></a>スレッドの概要  
 次の図は、ユーザーがストロークを描画するときのスレッド モデルを示しています。  
  
 ![ストローク描画中のスレッド モデル。](./media/inkthreading-drawingink.png "InkThreading_DrawingInk")  
  
1. ユーザーがストロークを描画している間発生するアクション  
  
    1. ユーザーがストロークを描画すると、スタイラス ポイントがペン スレッドに送られます。  ペン スレッドで、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> などのスタイラス プラグインにより、スタイラス ポイントが受け入れられ、<xref:System.Windows.Controls.InkCanvas> によって受け取られる前に変更することができます。  
  
    2. 動的レンダリング スレッドで、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> により、スタイラス ポイントがレンダリングされます。 これは、前のステップと同時に発生します。  
  
    3. UI スレッドで、<xref:System.Windows.Controls.InkCanvas> により、スタイラス ポイントが受け取られます。  
  
2. ユーザーがストロークを終了した後に発生するアクション  
  
    1. ユーザーがストロークの描画を終了すると、<xref:System.Windows.Controls.InkCanvas> により <xref:System.Windows.Ink.Stroke> オブジェクトが作成され、<xref:System.Windows.Controls.InkPresenter> に追加されます。これにより、静的にレンダリングされます。  
  
    2. UI スレッドにより、ストロークが静的にレンダリングされたことが <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> に警告され、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、ストロークの視覚表示が削除されます。  
  
## <a name="ink-collection-and-stylus-plug-ins"></a>インク コレクションとスタイラス プラグイン  
 各 <xref:System.Windows.UIElement> には <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> が含まれます。  <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 内の <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> オブジェクトで、ペン スレッドのスタイラス ポイントを受け取り、変更することができます。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> オブジェクトにより、<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> の順序に従ってスタイラス ポイントを受け取られます。  
  
 次の図は、<xref:System.Windows.UIElement> の <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに `stylusPlugin1`、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>、`stylusPlugin2` がこの順序で含まれているという仮定の状況を示しています。  
  
 ![スタイラス プラグインの順序が出力に影響する。](./media/inkthreading-pluginorder.png "InkThreading_PluginOrder")  
  
 上の図では、次の動作が行われます。  
  
1. `StylusPlugin1` で、x と y の値が変更されます。  
  
2. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、変更されたスタイラス ポイントが受け取られ、動的レンダリング スレッド上にレンダリングされます。  
  
3. `StylusPlugin2` で、変更されたスタイラス ポイントが受け取られ、x と y の値がさらに変更されます。  
  
4. アプリケーションで、スタイラス ポイントが収集され、ユーザーがストロークを終了したときに、ストロークが静的にレンダリングされます。  
  
 `stylusPlugin1` で、スタイラス ポイントが四角形に制限され、`stylusPlugin2` で、スタイラス ポイントを右に移動するとします。  前のシナリオでは、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、制限付きのスタイラス ポイントを受け取りますが、移動されたスタイラス ポイントは受け取りません。  ユーザーがストロークを描画すると、ストロークは四角形の境界内にレンダリングされますが、ユーザーがペンを持ち上げるまでストロークは移動したようには見えません。  
  
### <a name="performing-operations-with-a-stylus-plug-in-on-the-ui-thread"></a>UI スレッドでスタイラス プラグインを使用して操作を実行する  
 ペン スレッドでは正確なヒットテストを実行できないため、一部の要素で、他の要素向けのスタイラス入力が受け取られることがあります。 操作を実行する前に入力が正しくルーティングされたことを確認する必要がある場合は、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusDownProcessed%2A>、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusMoveProcessed%2A>、または <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusUpProcessed%2A> メソッドをサブスクライブし、操作を実行します。 これらのメソッドは、正確なヒットテストが実行された後に、アプリケーション スレッドから呼び出されます。 これらのメソッドをサブスクライブするには、ペン スレッドで発生するメソッド内で <xref:System.Windows.Input.StylusPlugIns.RawStylusInput.NotifyWhenProcessed%2A> メソッドを呼び出します。  
  
 次の図は、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> のスタイラス イベントに関するペン スレッドと UI スレッドの関係を示しています。  
  
 ![インク スレッド モデル &#40;UI とペン&#41;](./media/inkthreading-plugincallbacks.png "InkThreading_PluginCallbacks")  
  
## <a name="rendering-ink"></a>インクのレンダリング  
 ユーザーがストロークを描画すると、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、インクが別のスレッドにレンダリングされます。これにより、UI スレッドがビジー状態の場合でも、ペンからインクが "流れている" ように見えます。  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、スタイラス ポイントが収集されるときに、動的レンダリング スレッドにビジュアル ツリーが構築されます。  ユーザーがストロークを終了すると、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> により、アプリケーションで次のレンダリング パスを実行したときに通知を受け取るように要求されます。  アプリケーションで次のレンダリング パスが完了した後、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> では、ビジュアル ツリーがクリーンアップされます。  このプロセスを説明する図を次に示します。  
  
 ![インク スレッドの図](./media/inkthreading-visualtree.png "InkThreading_VisualTree")  
  
1. ユーザーがストロークを開始します。  
  
    1. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、ビジュアル ツリーが作成されます。  
  
2. ユーザーがストロークを描画し続けています。  
  
    1. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、ビジュアル ツリーが構築されます。  
  
3. ユーザーがストロークを終了します。  
  
    1. <xref:System.Windows.Controls.InkPresenter> により、そのビジュアル ツリーにストロークが追加されます。  
  
    2. メディア統合レイヤー (MIL) により、ストロークが静的にレンダリングされます。  
  
    3. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> で、ビジュアルがクリーンアップされます。
