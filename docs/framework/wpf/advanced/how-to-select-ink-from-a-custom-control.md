---
title: '方法: カスタム コントロールからインクを選択する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ink selection
- ink [WPF], selecting from custom control
- custom controls [WPF], ink selection
ms.assetid: 5f3a45c6-6d40-4017-9b47-933f134ceba3
ms.openlocfilehash: 5c9b2f3d64e4cbb309772d6a1d9fa88f589df84c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768412"
---
# <a name="how-to-select-ink-from-a-custom-control"></a>方法: カスタム コントロールからインクを選択する
カスタム コントロールに <xref:System.Windows.Ink.IncrementalLassoHitTester> を追加すると、<xref:System.Windows.Controls.InkCanvas> でなげなわを使ってインクを選択する場合と同様に、ユーザーがなげなわツールを使ってインクを選択できるようにコントロールを有効にすることができます。  
  
 この例では、インクを有効にしたカスタム コントロールの作成に慣れていることを前提としています。  インク入力を受け入れるカスタム コントロールを作成するには、「[インク入力コントロールの作成](creating-an-ink-input-control.md)」を参照してください。  
  
## <a name="example"></a>例  
 ユーザーがなげなわを描画すると、ユーザーがなげなわを完了した後に、<xref:System.Windows.Ink.IncrementalLassoHitTester> によってなげなわパスの境界内にあるストロークが予測されます。  なげなわパスの境界内にあると判断されたストロークは、選択対象と考えることができます。  選択されたストロークを選択解除することもできます。  たとえば、なげなわを描画しているときにユーザーが方向を反転させると、<xref:System.Windows.Ink.IncrementalLassoHitTester> によって一部のストロークの選択が解除されることがあります。  
  
 <xref:System.Windows.Ink.IncrementalLassoHitTester> によって <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> イベントが発生します。これにより、ユーザーがなげなわを描画している間にカスタム コントロールが応答できるようになります。  たとえば、ユーザーがストロークを選択または選択解除するときに、ストロークの外観を変更できます。  
  
## <a name="managing-the-ink-mode"></a>インク モードの管理  
 なげなわをコントロールのインクとは異なる外観にすると、ユーザーにとって便利です。 これを実現するには、ユーザーがインクを書き込んでいるか、選択しているかをカスタム コントロールで追跡する必要があります。 これを行う最も簡単な方法は、2 つの値を使用して列挙型を宣言することです。1 つはユーザーがインクを書き込んでいることを示すものと、もう 1 つはユーザーがインクを選択していることを示すものです。  
  
 [!code-csharp[HowToSelectInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#2)]
 [!code-vb[HowToSelectInk#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#2)]  
  
 次に、2 つの <xref:System.Windows.Ink.DrawingAttributes> をクラスに追加します。1 つはユーザーがインクを書き込むときに使用するもの、もう 1 つはユーザーがインクを選択するときに使用するものです。  コンストラクターで <xref:System.Windows.Ink.DrawingAttributes> を初期化し、両方の <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> イベントを同じイベント ハンドラーにアタッチします。 次に、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> プロパティをインク <xref:System.Windows.Ink.DrawingAttributes> に設定します。  
  
 [!code-csharp[HowToSelectInk#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#3)]
 [!code-vb[HowToSelectInk#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#3)]  
[!code-csharp[HowToSelectInk#4](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#4)]
[!code-vb[HowToSelectInk#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#4)]  
  
 選択モードを公開するプロパティを追加します。 ユーザーが選択モードを変更したら、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> の <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> プロパティを適切な <xref:System.Windows.Ink.DrawingAttributes> オブジェクトに設定してから、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> プロパティを <xref:System.Windows.Controls.InkPresenter> に再アタッチします。  
  
 [!code-csharp[HowToSelectInk#5](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#5)]
 [!code-vb[HowToSelectInk#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#5)]  
  
 アプリケーションによってインク ストロークと選択ストロークの外観を決定できるように、<xref:System.Windows.Ink.DrawingAttributes> をプロパティとして公開します。  
  
 [!code-csharp[HowToSelectInk#6](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#6)]
 [!code-vb[HowToSelectInk#6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#6)]  
  
 <xref:System.Windows.Ink.DrawingAttributes> オブジェクトのプロパティが変更された場合、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> を <xref:System.Windows.Controls.InkPresenter> に再アタッチする必要があります。  <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> イベントのイベント ハンドラーで、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> を <xref:System.Windows.Controls.InkPresenter> に再アタッチします。  
  
 [!code-csharp[HowToSelectInk#7](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#7)]
 [!code-vb[HowToSelectInk#7](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#7)]  
  
## <a name="using-the-incrementallassohittester"></a>IncrementalLassoHitTester の使用  
 選択したストロークを含む <xref:System.Windows.Ink.StrokeCollection> を作成して初期化します。  
  
 [!code-csharp[HowToSelectInk#8](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#8)]
 [!code-vb[HowToSelectInk#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#8)]  
  
 ユーザーがインクまたはなげなわでストロークを描画し始めたら、選択したストロークの選択を解除します。 次に、ユーザーがなげなわを描画している場合は、<xref:System.Windows.Ink.StrokeCollection.GetIncrementalLassoHitTester%2A> を呼び出して <xref:System.Windows.Ink.IncrementalLassoHitTester> を作成し、<xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> イベントを登録して、<xref:System.Windows.Ink.IncrementalHitTester.AddPoints%2A> を呼び出します。 このコードを個別のメソッドにして、<xref:System.Windows.UIElement.OnStylusDown%2A> および <xref:System.Windows.UIElement.OnMouseDown%2A> メソッドから呼び出すことができます。  
  
 [!code-csharp[HowToSelectInk#9](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#9)]
 [!code-vb[HowToSelectInk#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#9)]  
  
 ユーザーがなげなわを描画している間に、スタイラス ポイントを <xref:System.Windows.Ink.IncrementalLassoHitTester> に追加します。  <xref:System.Windows.UIElement.OnStylusMove%2A>、<xref:System.Windows.UIElement.OnStylusUp%2A>、<xref:System.Windows.UIElement.OnMouseMove%2A>、<xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> メソッドから次のメソッドを呼び出します。  
  
 [!code-csharp[HowToSelectInk#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#10)]
 [!code-vb[HowToSelectInk#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#10)]  
  
 ユーザーがストロークを選択または選択解除したときに応答するように <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged?displayProperty=nameWithType> イベントを処理します。  <xref:System.Windows.Ink.LassoSelectionChangedEventArgs> クラスには、選択されたストロークと選択解除されたストロークをそれぞれ取得する <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.SelectedStrokes%2A> プロパティと <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.DeselectedStrokes%2A> プロパティがあります。  
  
 [!code-csharp[HowToSelectInk#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#11)]
 [!code-vb[HowToSelectInk#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#11)]  
  
 ユーザーがなげなわの描画を完了したら、<xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> イベントの登録を解除して <xref:System.Windows.Ink.IncrementalHitTester.EndHitTesting%2A> を呼び出します。  
  
 [!code-csharp[HowToSelectInk#12](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#12)]
 [!code-vb[HowToSelectInk#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#12)]  
  
## <a name="putting-it-all-together"></a>すべてを組み合わせると次のようになります。  
 次の例は、ユーザーがなげなわでインクを選択できるようにするカスタム コントロールです。  
  
 [!code-csharp[HowToSelectInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#1)]
 [!code-vb[HowToSelectInk#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Ink.IncrementalLassoHitTester>
- <xref:System.Windows.Ink.StrokeCollection>
- <xref:System.Windows.Input.StylusPointCollection>
- [インク入力コントロールの作成](creating-an-ink-input-control.md)
