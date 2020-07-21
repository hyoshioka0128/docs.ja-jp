---
title: '方法: ストーリーボードを使用してアニメーション化した後にプロパティを設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], changing property values after
ms.assetid: 79466556-4dbf-40bd-9c1e-a77613b07077
ms.openlocfilehash: 593d3fcefe3bb81518d0886afde82f9a172874ba
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912386"
---
# <a name="how-to-set-a-property-after-animating-it-with-a-storyboard"></a>方法: ストーリーボードを使用してアニメーション化した後にプロパティを設定する
プロパティをアニメーション化した後に、その値を変更できないように見える場合があります。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.Animation.Storyboard> は <xref:System.Windows.Media.SolidColorBrush> の色をアニメーション化するために使用されます。 ボタンをクリックすると、ストーリーボードがトリガーされます。 <xref:System.Windows.Media.Animation.Timeline.Completed> イベントは、<xref:System.Windows.Media.Animation.ColorAnimation> が完了したときにプログラムに通知されるように処理されます。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton1Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton1declaration)]  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.ColorAnimation> が完了すると、プログラムはブラシの色を青色に変更しようとします。  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton1handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton1handler)]  
  
 前のコードは、何も実行しないように見えます。つまり、ブラシは、ブラシをアニメーション化した <xref:System.Windows.Media.Animation.ColorAnimation> によって指定された値である黄色のままです。 実際には、基になるプロパティ値 (基準値) は青色に変更されます。 しかし、有効な値または現在の値は黄色のままです。これは、<xref:System.Windows.Media.Animation.ColorAnimation> がまだ基準値をオーバーライドしているためです。 基準値が再度有効な値になるようにするには、アニメーションがプロパティに影響しないようにする必要があります。 ストーリーボード アニメーションでこれを行うには、次の 3 つの方法があります。  
  
- アニメーションの <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティを <xref:System.Windows.Media.Animation.FillBehavior.Stop> に設定します。  
  
- ストーリーボード全体を削除します。  
  
- アニメーションを個々のプロパティから削除します。  
  
## <a name="set-the-animations-fillbehavior-property-to-stop"></a>アニメーションの FillBehavior プロパティを Stop に設定する  
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> を <xref:System.Windows.Media.Animation.FillBehavior.Stop> に設定して、有効期間の終了に達した後はターゲット プロパティへの影響を停止するようにアニメーションに指示します。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton2Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton2declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton2handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton2handler)]  
  
## <a name="remove-the-entire-storyboard"></a>ストーリーボード全体を削除する  
 <xref:System.Windows.Media.Animation.RemoveStoryboard> トリガーまたは <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType> メソッドを使用して、ターゲット プロパティへの影響を停止するようにストーリーボード アニメーションに指示します。 この方法と <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティの設定との違いは、ストーリーボードをいつでも削除できることにあります。一方、<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティは、アニメーションが有効期間の終了に達したときにのみ効果があります。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton3Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton3declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton3handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton3handler)]  
  
## <a name="remove-an-animation-from-an-individual-property"></a>アニメーションを個々のプロパティから削除する  
 アニメーションがプロパティに影響しないようにするもう 1 つの手法は、アニメーション化されるオブジェクトの <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> メソッドを使用することです。 アニメーション化するプロパティを最初のパラメーターとして指定し、`null` を 2 番目のパラメーターとして指定します。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton4Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton4declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton4handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton4handler)]  
  
 この手法は、非ストーリーボード アニメーションにも使用できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>
- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Media.Animation.RemoveStoryboard>
- [アニメーションの概要](animation-overview.md)
- [プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)
