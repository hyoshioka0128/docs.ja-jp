---
title: '方法: CompositionTarget を使用したフレームの間隔ごとの描画'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CompositionTarget objects [WPF], rendering per frame
- rendering per frame using CompositionTarget objects [WPF]
ms.assetid: 701246cd-66b7-4d69-ada9-17b3b433d95d
ms.openlocfilehash: 8864204ccdd1e860cc910dfe8baa2f25edfb2fcc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956980"
---
# <a name="how-to-render-on-a-per-frame-interval-using-compositiontarget"></a>方法: CompositionTarget を使用したフレームの間隔ごとの描画
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション エンジンには、フレームベースのアニメーションを作成するためのさまざまな機能が用意されています。 ただし、フレームベースの描画をさらにきめ細かく制御することが必要となるアプリケーション シナリオがあります。 <xref:System.Windows.Media.CompositionTarget> オブジェクトを使用すると、フレームごとのコールバックに基づいて、カスタム アニメーションを作成できます。  
  
 <xref:System.Windows.Media.CompositionTarget> は、アプリケーションが描画される表示サーフェイスを表す静的クラスです。 アプリケーションのシーンが描画されるたびに <xref:System.Windows.Media.CompositionTarget.Rendering> イベントが発生します。 レンダリング フレーム レートは、1 秒あたりのシーンの描画回数です。  
  
> [!NOTE]
> <xref:System.Windows.Media.CompositionTarget> を使用したコード サンプル全体については、[CompositionTarget サンプルの使用](https://go.microsoft.com/fwlink/?LinkID=160045)に関する記事を参照してください。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.CompositionTarget.Rendering> イベントは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のレンダリング プロセス中に発生します。 次の例では、<xref:System.Windows.Media.CompositionTarget> の静的な <xref:System.Windows.Media.CompositionTarget.Rendering> メソッドに <xref:System.EventHandler> デリゲートを登録する方法を示しています。  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget1](~/samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget1)]
 [!code-vb[CompositionTargetSample#CompositionTarget1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget1)]  
  
 独自の描画イベント ハンドラー メソッドを使用して、描画のカスタム コンテンツを作成できます。 このイベント ハンドラー メソッドは、フレームごとに 1 回呼び出されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] がビジュアル ツリーの永続化されたレンダリング データを合成シーン グラフにマーシャリングするたびに、イベント ハンドラー メソッドが呼び出されます。 さらに、ビジュアル ツリーに対する変更によって合成シーン グラフが強制的に更新される場合も、イベント ハンドラー メソッドが呼び出されます。 イベント ハンドラー メソッドは、レイアウトが計算された後に呼び出されます。 ただし、イベント ハンドラー メソッド内でレイアウトを変更できます。つまり、そのレイアウトは、描画する前にもう一度計算されることになります。  
  
 次の例は、<xref:System.Windows.Media.CompositionTarget> イベント ハンドラー メソッドでカスタム描画を指定する方法を示します。 この場合、<xref:System.Windows.Controls.Canvas> の背景色は、マウスの座標位置に基づくカラー値で描画されます。 <xref:System.Windows.Controls.Canvas> 内でマウスを移動すると、その背景色が変わります。 また、現在の経過時間および描画されたフレームの合計数に基づいて、平均フレーム レートが計算されます。  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget2](~/samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget2)]
 [!code-vb[CompositionTargetSample#CompositionTarget2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget2)]  
  
 カスタム描画は、コンピューターごとに異なる速度で実行される場合があります。 これは、カスタム描画がフレーム レートに依存するためです。 実行しているシステムとそのシステムの負荷に応じて、<xref:System.Windows.Media.CompositionTarget.Rendering> イベントが 1 秒あたりに呼び出される回数が異なる場合があります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションを実行するデバイスのグラフィックス ハードウェアの機能およびパフォーマンスの決定については、「[グラフィックスの描画層](../advanced/graphics-rendering-tiers.md)」を参照してください。  
  
 イベントの発生中の描画 <xref:System.EventHandler> デリゲートの追加または削除は、イベントが終了するまで遅延します。 これは、<xref:System.MulticastDelegate> ベースのイベントが共通言語ランタイム (CLR) で処理される方法と一貫しています。 また、描画イベントが特定の順序で呼び出されるかどうかは保証されません。 特定の順序に依存する複数の <xref:System.EventHandler> デリゲートがある場合、単一の <xref:System.Windows.Media.CompositionTarget.Rendering> イベントを登録し、手動でデリゲートを正しい順序で多重化する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.CompositionTarget>
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
