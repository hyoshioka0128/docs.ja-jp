---
title: カスタム レンダリング インク
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom-rendering ink
- ink [WPF], custom-rendering
- classes [WPF], InkCanvas
ms.assetid: 65c978a7-0ee0-454f-ac7f-b1bd2efecac5
ms.openlocfilehash: 0ceb831057a9a92aa7319d2004f04d7cf5ac820e
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111830"
---
# <a name="custom-rendering-ink"></a>カスタム レンダリング インク
ストロークの <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> プロパティでは、ストロークのサイズ、色、形状などの外観を指定できますが、<xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> で許可されている以上の外観のカスタマイズをしたい場合があります。 エアブラシ、油絵、およびその他の多くの効果の外観でレンダリングすることで、インクの外観をカスタマイズしたい場合もあります。 Windows Presentation Foundation (WPF) では、カスタムの <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> と <xref:System.Windows.Ink.Stroke> オブジェクトを実装することで、インクをカスタム レンダリングできます。  
  
 このトピックは、次の内容で構成されています。  
  
- [アーキテクチャ](#Architecture)  
  
- [動的なレンダラーの実装](#ImplementingADynamicRenderer)  
  
- [カスタム ストロークの実装](#ImplementingCustomStrokes)  
  
- [カスタム InkCanvas の実装](#ImplementingACustomInkCanvas)  
  
- [まとめ](#Conclusion)  
  
<a name="Architecture"></a>
## <a name="architecture"></a>アーキテクチャ  
 インク レンダリングは 2 回発生します。ユーザーがインクを手描き入力サーフェイスに書き込む時と、ストロークが手書き対応のサーフェスに追加された後です。 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> では、ユーザーがデジタイザー上でタブレット ペンを移動すると、インクがレンダリングされ、<xref:System.Windows.Ink.Stroke> が要素に追加されると、それ自体がレンダリングされます。  
  
 インクを動的にレンダリングするときに実装する 3 つのクラスがあります。  
  
1. **DynamicRenderer**: <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> から派生するクラスを実装します。 このクラスは、描画されたとおりにストロークがレンダリングされる特殊な <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> です。 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> では別のスレッドでレンダリングが行われるため、アプリケーション ユーザー インターフェイス (UI) スレッドがブロックされている場合でも、インクを収集するための手描き入力サーフェスが表示されます。 スレッド処理モデルの詳細については、「[インク スレッド モデル](the-ink-threading-model.md)」を参照してください。 ストロークの動的なレンダリングをカスタマイズするには、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> メソッドをオーバーライドします。  
  
2. **Stroke**: <xref:System.Windows.Ink.Stroke> から派生するクラスを実装します。 このクラスでは、<xref:System.Windows.Input.StylusPoint> データが <xref:System.Windows.Ink.Stroke> オブジェクトに変換された後のデータの静的なレンダリングが行われます。 ストロークの静的なレンダリングを動的レンダリングと一致させるには、<xref:System.Windows.Ink.Stroke.DrawCore%2A> メソッドをオーバーライドします。  
  
3. **InkCanvas:** <xref:System.Windows.Controls.InkCanvas> から派生するクラスを実装します。 カスタマイズされた <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> プロパティに割り当てます。 <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> メソッドをオーバーライドし、カスタム ストロークを <xref:System.Windows.Controls.InkCanvas.Strokes%2A> プロパティに追加します。 これにより、インクの外観に一貫性を確保します。  
  
<a name="ImplementingADynamicRenderer"></a>
## <a name="implementing-a-dynamic-renderer"></a>動的なレンダラーの実装  
 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> クラスは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の標準部分ですが、より特殊なレンダリングを実行するには、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> から派生した動的レンダラーをカスタマイズし、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> メソッドをオーバーライドする必要があります。  
  
 次の例では、線状グラデーション ブラシの効果を使用してインクを描画するカスタマイズされた <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#1](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#1)]
[!code-vb[AdvancedInkTopicsSamples#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#1)]  
  
<a name="ImplementingCustomStrokes"></a>
## <a name="implementing-custom-strokes"></a>カスタム ストロークの実装  
 <xref:System.Windows.Ink.Stroke> から派生するクラスを実装します。 このクラスでは、<xref:System.Windows.Ink.Stroke> オブジェクトに変換された後の <xref:System.Windows.Input.StylusPoint> データがレンダリングされます。 実際の描画を行うには、<xref:System.Windows.Ink.Stroke.DrawCore%2A> クラスをオーバーライドします。  
  
 Stroke クラスでは、<xref:System.Windows.Ink.Stroke.AddPropertyData%2A> メソッドを使用することで、カスタム データを格納することもできます。 このデータは、保持されるときにストローク データと共に格納されます。  
  
 <xref:System.Windows.Ink.Stroke> クラスでは、ヒット テストも実行できます。 また、現在のクラスで <xref:System.Windows.Ink.Stroke.HitTest%2A> メソッドをオーバーライドすることにより、独自のヒット テスト アルゴリズムを実装することもできます。  
  
 次の C# コードでは、<xref:System.Windows.Input.StylusPoint> データを 3D ストロークとしてレンダリングするカスタム <xref:System.Windows.Ink.Stroke> クラスを示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#2](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#2)]
[!code-vb[AdvancedInkTopicsSamples#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#2)]  
  
<a name="ImplementingACustomInkCanvas"></a>
## <a name="implementing-a-custom-inkcanvas"></a>カスタム InkCanvas の実装  
 カスタマイズした<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> とストロークを使用する最も簡単な方法は、<xref:System.Windows.Controls.InkCanvas> の派生クラスを実装し、これらのクラスを使用することです。 <xref:System.Windows.Controls.InkCanvas> には、ユーザーが描画するときにストロークをレンダリングする方法を指定する <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> プロパティがあります。  
  
 <xref:System.Windows.Controls.InkCanvas> でストロークをカスタム レンダリングするには、次のようにします。  
  
- <xref:System.Windows.Controls.InkCanvas> から派生するクラスを作成します。  
  
- カスタマイズした <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A?displayProperty=nameWithType> プロパティに割り当てます。  
  
- <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> メソッドをオーバーライドします。 このメソッドで、InkCanvas に追加された元のストロークを削除します。 次に、カスタム ストロークを作成し、それを <xref:System.Windows.Controls.InkCanvas.Strokes%2A> プロパティに追加して、そのカスタム ストロークを含む新しい <xref:System.Windows.Controls.InkCanvasStrokeCollectedEventArgs> で基底クラスを呼び出します。  
  
 次の C# コードでは、カスタマイズした <xref:System.Windows.Controls.InkCanvas> を使用してカスタム ストロークを収集するカスタムの <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> クラスを示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#9](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#9)]  
  
 <xref:System.Windows.Controls.InkCanvas> では複数の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を使用できます。 複数の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> オブジェクトを <xref:System.Windows.UIElement.StylusPlugIns%2A> プロパティに追加することで、<xref:System.Windows.Controls.InkCanvas> に追加できます。  
  
<a name="Conclusion"></a>
## <a name="conclusion"></a>まとめ  
 独自の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> クラス、<xref:System.Windows.Ink.Stroke> クラス、<xref:System.Windows.Controls.InkCanvas> クラスを派生させることで、インクの外観をカスタマイズできます。 これらのクラスを合わせて、ユーザーがストロークを描画し、その後ストロークが収集される際に、ストロークの外観を一致させます。  
  
## <a name="see-also"></a>関連項目

- [高度なインク処理](advanced-ink-handling.md)
