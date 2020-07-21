---
title: 装飾の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], about adorners
ms.assetid: 33d4c5c2-2daf-4e45-ba9a-5b673e2b8280
ms.openlocfilehash: b41c1f10f7e1b7c1799fd27270a3eeb9899ceeb6
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111180"
---
# <a name="adorners-overview"></a>装飾の概要

装飾は特別な種類の <xref:System.Windows.FrameworkElement> で、ユーザーに視覚的手掛かりを提供するために使用されます。 装飾は、要素への機能ハンドル追加やコントロールに関する状態情報の提供など、さまざまな用途に使用できます。

## <a name="about-adorners"></a>装飾について

<xref:System.Windows.Documents.Adorner> は、<xref:System.Windows.UIElement> にバインドされるカスタム <xref:System.Windows.FrameworkElement> です。 装飾は、<xref:System.Windows.Documents.AdornerLayer> に描画されます。これは、常に装飾対象の要素またはそのコレクションの最上層に位置するレンダリング面です。 装飾のレンダリングは、装飾がバインドされる <xref:System.Windows.UIElement> のレンダリングとは独立しています。 通常、装飾は、装飾対象の要素の左上に位置する標準の 2 次元座標の原点を使用して、バインド先の要素に対して相対的な位置に配置されます。

装飾の一般的な用途は、次のとおりです。

- ユーザーが要素を操作 (サイズ変更、回転、位置の変更など) するための機能ハンドルを <xref:System.Windows.UIElement> に追加する。
- 視覚的なフィードバックによって、さまざまな状態を表示し、各種のイベントに応答する。
- <xref:System.Windows.UIElement> に視覚的装飾をオーバーレイする。
- <xref:System.Windows.UIElement> の一部または全部を視覚的にマスクするか、オーバーライドする。

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、視覚的要素を装飾する基本的なフレームワークを提供します。 次の表に示すのは、オブジェクトの装飾に使用する主な種類と、その用途の一覧です。 その後に、使用例をいくつか示します。

|||
|-|-|
|<xref:System.Windows.Documents.Adorner>|具体的な装飾の実装すべての継承元になる抽象基本クラス。|
|<xref:System.Windows.Documents.AdornerLayer>|装飾される 1 つ以上の要素に対する、装飾のレンダリング層を表すクラス。|
|<xref:System.Windows.Documents.AdornerDecorator>|1 つの装飾層を要素のコレクションに関連付けることを可能にするクラス。|

## <a name="implementing-a-custom-adorner"></a>カスタム装飾の実装

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] が提供する装飾フレームワークは、カスタム装飾の作成をサポートすることを主な目的としています。 カスタム装飾は、抽象クラス <xref:System.Windows.Documents.Adorner> から継承されるクラスを実装することによって作成されます。

> [!NOTE]
> <xref:System.Windows.Documents.Adorner> の親は、装飾される要素ではなく、<xref:System.Windows.Documents.Adorner> をレンダリングする <xref:System.Windows.Documents.AdornerLayer> です。

次の例では、簡単な装飾を実装するクラスを示します。 この例の装飾では、<xref:System.Windows.UIElement> の四隅が円で装飾されるだけです。

[!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
[!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]
  
次の図に示すのは、<xref:System.Windows.Controls.TextBox> に適用された SimpleCircleAdorner です。

![装飾されたテキスト ボックスを示すスクリーンショット。](./media/adorners-overview/simplecircleadorner-textbox.png)

## <a name="rendering-behavior-for-adorners"></a>装飾のレンダリング動作

装飾自体にはレンダリング動作が備わっていないので、装飾のレンダリングは装飾の実装側の責任で行う必要がある点に、注意が必要です。 レンダリング動作を実装する一般的な方法は、(この例で示すように) <xref:System.Windows.UIElement.OnRender%2A> メソッドをオーバーライドし、1 つまたは複数の <xref:System.Windows.Media.DrawingContext> オブジェクトを使用して、必要に応じて装飾のビジュアルをレンダリングすることです。

> [!NOTE]
> 装飾層に配置されているすべてのものは、設定した他のすべてのスタイルの上に描画されます。 つまり、装飾は常に視覚的に最上位にあり、z オーダーを使用してオーバーライドすることはできません。

## <a name="events-and-hit-testing"></a>イベントおよびヒット テスト

他のすべての <xref:System.Windows.FrameworkElement> と同様に、装飾は入力イベントを受け取ります。  装飾は、それが装飾する要素よりも常に高い z オーダーを持つため、下位にある装飾対象の要素に向けられた入力イベント (<xref:System.Windows.UIElement.Drop> または <xref:System.Windows.UIElement.MouseMove> など) であっても受け取ります。  装飾は、特定の入力イベントをリッスンし、それらのイベントを再度発生させることによって、下位にある装飾対象の要素に渡すことができます。

装飾の下にある要素に対するヒット テストをパススルーするには、その装飾でヒット テストの <xref:System.Windows.UIElement.IsHitTestVisible%2A> プロパティを **false** に設定します。  ヒット テストの詳細については、「[ビジュアル層でのヒット テスト](../graphics-multimedia/hit-testing-in-the-visual-layer.md)」を参照してください。

## <a name="adorning-a-single-uielement"></a>単一の UIElement の装飾

特定の <xref:System.Windows.UIElement> に装飾をバインドするには、次の手順を行います。

1. 静的メソッド <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> を呼び出して、装飾対象の <xref:System.Windows.UIElement> の <xref:System.Windows.Documents.AdornerLayer> オブジェクトを取得します。 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> では、指定した <xref:System.Windows.UIElement> を起点としてビジュアル ツリーが上方に探索され、最初に見つかった装飾層が返されます。 (装飾層が見つからない場合、メソッドにより null が返されます)。

2. <xref:System.Windows.Documents.AdornerLayer.Add%2A> メソッドを呼び出し、装飾を対象の <xref:System.Windows.UIElement> にバインドします。

 次の例では、SimpleCircleAdorner (上図参照) を *myTextBox* という名前の <xref:System.Windows.Controls.TextBox> にバインドします。

 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]

> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して、装飾を別の要素にバインドする方法は、現在サポートされていません。

## <a name="adorning-the-children-of-a-panel"></a>パネルの子の装飾

<xref:System.Windows.Controls.Panel> の子に装飾をバインドするには、次の手順を行います。

1. `static` メソッド <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> を呼び出し、子が装飾対象となる要素の装飾層を検出します。

2. 親要素の子を列挙し、<xref:System.Windows.Documents.AdornerLayer.Add%2A> メソッドを呼び出して、装飾を各子要素にバインドします。

次の例では、SimpleCircleAdorner (上図参照) を *myStackPanel* という名前の <xref:System.Windows.Controls.StackPanel> の子にバインドします。

[!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
[!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.AdornerHitTestResult>
- [WPF での図形と基本描画の概要](../graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)
- [イメージ、描画、およびビジュアルによる塗りつぶし](../graphics-multimedia/painting-with-images-drawings-and-visuals.md)
- [Drawing オブジェクトの概要](../graphics-multimedia/drawing-objects-overview.md)
- [方法トピック](adorners-how-to-topics.md)
