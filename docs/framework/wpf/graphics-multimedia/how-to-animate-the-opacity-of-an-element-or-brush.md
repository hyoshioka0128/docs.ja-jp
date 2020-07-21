---
title: '方法: 要素またはブラシの不透明度をアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- opacity [WPF], animating
- animation [WPF], Opacity property
ms.assetid: 572af23b-39dd-48d1-9db5-4bca56a4b3d3
ms.openlocfilehash: 2f18861eb18f81b631245d1d933b7acb1b3e0e42
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950515"
---
# <a name="how-to-animate-the-opacity-of-an-element-or-brush"></a>方法: 要素またはブラシの不透明度をアニメーション化する
フレームワーク要素のビューをフェードインおよびフェードアウトさせるには、その <xref:System.Windows.UIElement.Opacity%2A> プロパティをアニメーション化するか、描画に使用する <xref:System.Windows.Media.Brush> (またはブラシ) の <xref:System.Windows.Media.Brush.Opacity%2A> プロパティをアニメーション化します。 要素の不透明度をアニメーション化すると、要素とその子のビューがフェードインおよびフェードアウトしますが、要素を描画するために使用するブラシをアニメーション化すると、要素のどの部分をフェードさせるかをより細かく選択できるようになります。 たとえば、ボタンの背景を描画するために使用するブラシの不透明度をアニメーション化することができます。 これを行うと、ボタンの背景のビューがフェードインおよびフェードアウトして、テキストは完全に不透明のままになります。  
  
> [!NOTE]
> <xref:System.Windows.Media.Brush> の <xref:System.Windows.Media.Brush.Opacity%2A> をアニメーション化すると、要素の <xref:System.Windows.UIElement.Opacity%2A> プロパティをアニメーション化するよりもパフォーマンスが向上します。  
  
 次の例では、2 つのボタンをアニメーション化して、それらのビューがフェードインおよびフェードアウトするようにします。 最初の <xref:System.Windows.Controls.Button> の不透明度は、`1.0` から `0.0` まで、5 秒間の <xref:System.Windows.Media.Animation.Timeline.Duration%2A> でアニメーション化されます。 2 番目のボタンもアニメーション化されますが、ボタン全体の不透明度ではなく、その <xref:System.Windows.Controls.Control.Background%2A> を描画するために使用する SolidColorBrush の不透明度がアニメーション化されます。 この例を実行すると、最初のボタンのビューは完全にフェードインおよびフェードアウトしますが、2 番目のボタンは、背景のビューのみがフェードインおよびフェードアウトします。 テキストと枠線は、完全に不透明なままです。  
  
## <a name="example"></a>例  
 [!code-xaml[timingbehaviors_snip#10](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/OpacityAnimationExample.xaml#10)]  
  
 この例では、コードは省略されています。 完全なサンプルでは、<xref:System.Windows.Media.LinearGradientBrush> 内の <xref:System.Windows.Media.Color> の不透明度をアニメーション化する方法も示しています。  完全なサンプルについては、「[Animating the Opacity of an Element Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/OpacityAnimation)」 (要素サンプルの不透明度をアニメーション化する) を参照してください。
