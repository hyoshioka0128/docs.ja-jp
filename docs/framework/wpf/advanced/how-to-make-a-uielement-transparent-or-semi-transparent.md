---
title: '方法: UIElement を透明または半透明にする'
ms.date: 03/30/2017
helpviewer_keywords:
- UIElements [WPF], transparency
- opacity [WPF], of UIElements
- transparency of UIElements [WPF]
- UIElements [WPF], opacity
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
ms.openlocfilehash: 1de9a7e11fee241ecb71242e9808e77b7e5e63b0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942871"
---
# <a name="how-to-make-a-uielement-transparent-or-semi-transparent"></a>方法: UIElement を透明または半透明にする
この例では、<xref:System.Windows.UIElement> を透明または半透明にする方法を示します。 要素を透明または半透明にするには、その <xref:System.Windows.UIElement.Opacity%2A> プロパティを設定します。 値に `0.0` を指定すると要素は完全に透明になり、値に `1.0` を指定すると要素は完全に不透明になります。 値に `0.5` を指定すると、要素の不透明度は 50% などになります。 要素の <xref:System.Windows.UIElement.Opacity%2A> は、既定で `1.0` に設定されています。  
  
## <a name="example"></a>例  
 次の例では、ボタンの <xref:System.Windows.UIElement.Opacity%2A> を `0.25` に設定し、それとそのコンテンツ (この場合はボタンのテキスト) を 25% 不透明にします。  
  
 [!code-xaml[brushsamples_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 要素のコンテンツに独自の <xref:System.Windows.UIElement.Opacity%2A> 設定がある場合、それらの値は、含まれる要素 <xref:System.Windows.UIElement.Opacity%2A> に乗算されます。  
  
 次の例では、ボタンの <xref:System.Windows.UIElement.Opacity%2A> を `0.25` に設定し、ボタンに含まれる <xref:System.Windows.Controls.Image> コントロールの <xref:System.Windows.UIElement.Opacity%2A> を `0.5` に設定します。 その結果、イメージは次に従って 12.5% 不透明になります。0.25 * 0.5 = 0.125。  
  
 [!code-xaml[brushsamples_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 要素の不透明度を制御するもう 1 つの方法は、要素を塗りつぶす <xref:System.Windows.Media.Brush> の不透明度を設定する方法です。 この方法により、要素の一部を選択的に不透明に変更でき、要素の <xref:System.Windows.UIElement.Opacity%2A> プロパティを使用するよりもパフォーマンスが向上します。 次の例では、ボタンの <xref:System.Windows.Controls.Control.Background%2A> の塗りつぶしに使用される <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.Brush.Opacity%2A> を `0.25` に設定します。 その結果、このブラシの背景は 25% 不透明になりますが、そのコンテンツ (ボタンのテキスト) は、100% 不透明のままです。  
  
 [!code-xaml[brushsamples_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 また、ブラシ内の個々の色の不透明度を制御することもできます。 色とブラシの詳細については、「[単色とグラデーションによる塗りつぶしの概要](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)」を参照してください。 要素の不透明度をアニメーション化する方法の例については、「[要素またはブラシの不透明度をアニメーション化する](../graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md)」を参照してください。
