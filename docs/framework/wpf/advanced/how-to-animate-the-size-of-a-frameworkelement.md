---
title: '方法: FrameworkElement のサイズをアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], FrameworkElement size
- FrameworkElement [WPF], animating size of
ms.assetid: d4cd5a13-c20d-4a6f-a2ba-14f2c9ce4cef
ms.openlocfilehash: d1995deec5ab2c9bf405911af43b4d242d599119
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776910"
---
# <a name="how-to-animate-the-size-of-a-frameworkelement"></a>方法: FrameworkElement のサイズをアニメーション化する
<xref:System.Windows.FrameworkElement> のサイズをアニメーション化するには、その <xref:System.Windows.FrameworkElement.Width%2A> プロパティと <xref:System.Windows.FrameworkElement.Height%2A> プロパティをアニメーション化するか、またはアニメーション化された <xref:System.Windows.Media.ScaleTransform> を使用します。  
  
 次の例では、2 つの方法を使用して、2 つのボタンのサイズがアニメーション化されています。 1 つのボタンはその <xref:System.Windows.FrameworkElement.Width%2A> プロパティをアニメーション化してサイズ変更し、もう 1 つは、その <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに適用された <xref:System.Windows.Media.ScaleTransform> をアニメーション化してサイズ変更しています。 各ボタンには、テキストがいくつか含まれます。 初期状態では、両ボタンのテキストは同じに表示されますが、ボタンのサイズが変更されると、2 番目のボタンのテキストはゆがんで表示されます。  
  
## <a name="example"></a>例  
 [!code-xaml[transformanimations_snip#1](~/samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/AnimatingSizeExample.xaml#1)]  
  
 要素を変換すると、その要素全体とそのコンテンツが変換されます。 最初のボタンの場合のように、要素のサイズが直接変更されると、親要素のサイズにそのサイズと位置が依存していない限り、要素のコンテンツのサイズは変更されません。  
  
 要素の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティにアニメーション化された変換を適用してサイズをアニメーション化する場合、<xref:System.Windows.UIElement.RenderTransform%2A> プロパティはレイアウト パスをトリガーしないため、<xref:System.Windows.FrameworkElement.Width%2A> と <xref:System.Windows.FrameworkElement.Height%2A> を直接アニメーション化する場合よりもパフォーマンスが向上します。  
  
 プロパティのアニメーション化の詳細については、「[アニメーションの概要](../graphics-multimedia/animation-overview.md)」を参照してください。 変換の詳細については「[変換の概要](../graphics-multimedia/transforms-overview.md)」を参照してください。
