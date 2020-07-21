---
title: インク入力コントロールの作成
ms.date: 03/30/2017
helpviewer_keywords:
- ink strokes [WPF], managing
- managing ink strokes [WPF]
- ink input control [WPF]
- input from mouse [WPF], accepting
- mouse input [WPF], accepting
- ink [WPF], rendering
- ink strokes [WPF], collecting
- rendering ink [WPF]
- collecting ink strokes [WPF]
- DynamicRenderer objects [WPF]
- StylusPlugIn objects [WPF]
ms.assetid: c31f3a67-cb3f-4ded-af9e-ed21f6575b26
ms.openlocfilehash: 394318488b0afb8e043389e0abc3f51dce8604c0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186292"
---
# <a name="creating-an-ink-input-control"></a>インク入力コントロールの作成
インクを動的および静的にレンダリングするカスタム コントロールを作成できます。 つまり、ユーザーがストロークを描画するのに合わせてインクをレンダリングすることで、インクがタブレット ペンから "流れ出している" ように見えます。また、タブレット ペンの使用、クリップボードからの貼り付け、またはファイルからの読み込みにより、インクがコントロールに追加された後で、インクを表示します。 インクを動的にレンダリングするには、コントロールで <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を使用する必要があります。 インクを静的にレンダリングするには、スタイラス イベント メソッド (<xref:System.Windows.UIElement.OnStylusDown%2A>、<xref:System.Windows.UIElement.OnStylusMove%2A>、<xref:System.Windows.UIElement.OnStylusUp%2A>) をオーバーライドして、<xref:System.Windows.Input.StylusPoint> データを収集し、ストロークを作成して、それらを <xref:System.Windows.Controls.InkPresenter> (コントロールのインクをレンダリングします) に追加する必要があります。  
  
 このトピックは、次の内容で構成されています。  
  
- [方法: スタイラス ポイント データを収集してインク ストロークを作成する](#CollectingStylusPointDataAndCreatingInkStrokes)  
  
- [方法: コントロールがマウスからの入力を受け入れられるようにする](#EnablingYourControlToAcceptInputTromTheMouse)  
  
- [組み合わせる](#PuttingItTogether)  
  
- [追加のプラグインと DynamicRenderers を使用する](#UsingAdditionalPluginsAndDynamicRenderers)  
  
- [まとめ](#AdvancedInkHandling_Conclusion)  
  
<a name="CollectingStylusPointDataAndCreatingInkStrokes"></a>
## <a name="how-to-collect-stylus-point-data-and-create-ink-strokes"></a>方法: スタイラス ポイント データを収集してインク ストロークを作成する  
 インクストロークを収集して管理するコントロールを作成するには、次のようにします。  
  
1. <xref:System.Windows.Controls.Control> または <xref:System.Windows.Controls.Control> の派生クラスのいずれか (<xref:System.Windows.Controls.Label> など) からクラスを派生します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
    [!code-csharp[AdvancedInkTopicsSamples#14](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#14)]  
    [!code-csharp[AdvancedInkTopicsSamples#15](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#15)]  
  
2. クラスに <xref:System.Windows.Controls.InkPresenter> を追加し、<xref:System.Windows.Controls.ContentControl.Content%2A> プロパティに新しい <xref:System.Windows.Controls.InkPresenter> を設定します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#16](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#16)]  
  
3. <xref:System.Windows.Controls.InkPresenter.AttachVisuals%2A> メソッドを呼び出すことによって <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> を <xref:System.Windows.Controls.InkPresenter> にアタッチし、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> を <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに追加します。 これにより、コントロールによってスタイラス ポイント データが収集されたら、<xref:System.Windows.Controls.InkPresenter> でインクを表示できるようになります。  
  
     [!code-csharp[AdvancedInkTopicsSamples#17](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#17)]  
    [!code-csharp[AdvancedInkTopicsSamples#18](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#18)]  
  
4. <xref:System.Windows.UIElement.OnStylusDown%2A> メソッドをオーバーライドします。  このメソッドでは、<xref:System.Windows.Input.Stylus.Capture%2A> を呼び出してスタイラスをキャプチャします。 スタイラスをキャプチャすることにより、スタイラスがコントロールの境界から出た場合でも、コントロールは <xref:System.Windows.UIElement.StylusMove> イベントと <xref:System.Windows.UIElement.StylusUp> イベントを引き続き受け取ります。 これは絶対に必要なわけではありませんが、優れたユーザー エクスペリエンスを実現するためにほとんどの場合に必要です。 新しい <xref:System.Windows.Input.StylusPointCollection> を作成して <xref:System.Windows.Input.StylusPoint> データを収集します。 最後に、<xref:System.Windows.Input.StylusPoint> データの初期セットを <xref:System.Windows.Input.StylusPointCollection> に追加します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#7](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#7)]  
  
5. <xref:System.Windows.UIElement.OnStylusMove%2A> メソッドをオーバーライドし、前に作成した <xref:System.Windows.Input.StylusPointCollection> オブジェクトに <xref:System.Windows.Input.StylusPoint> データを追加します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#8](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#8)]  
  
6. <xref:System.Windows.UIElement.OnStylusUp%2A> メソッドをオーバーライドし、<xref:System.Windows.Input.StylusPointCollection> データを使用して新しい <xref:System.Windows.Ink.Stroke> を作成します。 作成した新しい <xref:System.Windows.Ink.Stroke> を <xref:System.Windows.Controls.InkPresenter> の <xref:System.Windows.Controls.InkPresenter.Strokes%2A> コレクションに追加し、スタイラスのキャプチャを解放します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#10](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#10)]  
  
<a name="EnablingYourControlToAcceptInputTromTheMouse"></a>
## <a name="how-to-enable-your-control-to-accept-input-from-the-mouse"></a>方法: コントロールがマウスからの入力を受け入れられるようにする  
 前に示したコントロールをアプリケーションに追加して実行し、マウスを入力デバイスとして使用した場合、ストロークが永続化されないことがわかります。 入力デバイスとしてマウスを使用したときにストロークを保持するには、次のようにします。  
  
1. <xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A> をオーバーライドして、新しい <xref:System.Windows.Input.StylusPointCollection> 作成します。イベントが発生したときのマウスの位置を取得し、ポイント データを使用して <xref:System.Windows.Input.StylusPoint> を作成し、<xref:System.Windows.Input.StylusPoint> を <xref:System.Windows.Input.StylusPointCollection> に追加します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#11](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#11)]  
  
2. <xref:System.Windows.UIElement.OnMouseMove%2A> メソッドをオーバーライドします。 イベントが発生したときのマウスの位置を取得し、ポイント データを使用して <xref:System.Windows.Input.StylusPoint> を作成します。  前に作成した <xref:System.Windows.Input.StylusPointCollection> オブジェクトに <xref:System.Windows.Input.StylusPoint> を追加します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#12](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#12)]  
  
3. <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> メソッドをオーバーライドします。  <xref:System.Windows.Input.StylusPointCollection> データを使用して新しい <xref:System.Windows.Ink.Stroke> を作成し、作成した新しい <xref:System.Windows.Ink.Stroke> を <xref:System.Windows.Controls.InkPresenter> の <xref:System.Windows.Controls.InkPresenter.Strokes%2A> コレクションに追加します。  
  
     [!code-csharp[AdvancedInkTopicsSamples#13](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#13)]  
  
<a name="PuttingItTogether"></a>
## <a name="putting-it-together"></a>組み合わせる  
 次の例は、ユーザーがマウスまたはペンを使用したときにインクを収集するカスタム コントロールです。  
  
 [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
[!code-csharp[AdvancedInkTopicsSamples#6](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#6)]  
  
<a name="UsingAdditionalPluginsAndDynamicRenderers"></a>
## <a name="using-additional-plug-ins-and-dynamicrenderers"></a>追加のプラグインと DynamicRenderers を使用する  
 InkCanvas と同様に、カスタム コントロールでは、カスタム <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> オブジェクトと追加の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> オブジェクトを使用できます。 これらを <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに追加します。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 内の <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> オブジェクトの順序は、レンダリング時のインクの外観に影響します。 `dynamicRenderer` という名前の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> と、タブレット ペンからのインクをオフセットする `translatePlugin` という名前のカスタム <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> があるとします。 `translatePlugin` が <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 内の最初の <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> であり、`dynamicRenderer` が 2 番目の場合は、ユーザーがペンを動かすと、"流れ出す" インクはオフセットされます。 `dynamicRenderer` が最初で、`translatePlugin` が 2 番目の場合は、ユーザーがペンを持ち上げるまでインクはオフセットされません。  
  
<a name="AdvancedInkHandling_Conclusion"></a>
## <a name="conclusion"></a>まとめ  
 スタイラス イベント メソッドをオーバーライドすることにより、インクを収集してレンダリングするコントロールを作成できます。 独自のコントロールを作成し、独自の <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> クラスを派生させ、それを <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> に挿入することにより、デジタル インクで想像できるほとんどどのような動作でも実装できます。 生成された <xref:System.Windows.Input.StylusPoint> データにアクセスできるため、<xref:System.Windows.Input.Stylus> の入力をカスタマイズし、アプリケーションに適した方法で画面にレンダリングする機会があります。 そのように低いレベルで <xref:System.Windows.Input.StylusPoint> のデータにアクセスできるため、アプリケーションに最適なパフォーマンスでインクのコレクションとレンダリングを実装できます。  
  
## <a name="see-also"></a>関連項目

- [高度なインク処理](advanced-ink-handling.md)
- [ペン入力へのアクセスとその操作](https://docs.microsoft.com/previous-versions/ms818317(v=msdn.10))
