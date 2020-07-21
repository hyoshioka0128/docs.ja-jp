---
title: '方法: アクティブな期間の末尾に到達したタイムラインの FillBehavior を指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- FillBehavior property for inactive timelines [WPF]
- Timelines [WPF], FillBehavior property
ms.assetid: db805f59-d513-4dac-af15-47005dae3199
ms.openlocfilehash: 1f54f2c1bb49bb7a0301f112a109194ab1a8658e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141174"
---
# <a name="how-to-specify-the-fillbehavior-for-a-timeline-that-has-reached-the-end-of-its-active-period"></a>方法: アクティブな期間の末尾に到達したタイムラインの FillBehavior を指定する
この例では、アニメーション化対象のプロパティの非アクティブな <xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> を指定する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> プロパティは、アニメーション化対象のプロパティの値がアニメーション化されていないとき、つまり、<xref:System.Windows.Media.Animation.Timeline> は非アクティブであるが、その親 <xref:System.Windows.Media.Animation.Timeline> がアクティブな期間つまり保持期間内のときに、その値がどのように処理されるかを決定します。 たとえば、アニメーション化対象のプロパティが、アニメーションの終了後にその終了値のままになるか、アニメーションが開始される前の値に戻るかなどです。  
  
 次の例では、<xref:System.Windows.Media.Animation.DoubleAnimation> を使用して、2 つの四角形の <xref:System.Windows.FrameworkElement.Width%2A> をアニメーション化します。 それぞれの四角形は、別個の <xref:System.Windows.Media.Animation.Timeline> オブジェクトを使用します。  
  
 一方の <xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> は <xref:System.Windows.Media.Animation.FillBehavior.Stop> に設定されています。これにより、<xref:System.Windows.Media.Animation.Timeline> の終了時に四角形の幅がアニメーション化されていない値に戻ります。 もう一方の <xref:System.Windows.Media.Animation.Timeline> の <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> は <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd> であり、<xref:System.Windows.Media.Animation.Timeline> の終了時に幅が終了値のままになります。  
  
 [!code-xaml[timingbehaviors_snip#FillBehaviorWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/FillBehaviorExample.xaml#fillbehaviorwholepage)]  
  
 サンプル全体については、「[アニメーション サンプル ギャラリー](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationExamples)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.DoubleAnimation>
- <xref:System.Windows.FrameworkElement.Width%2A>
- <xref:System.Windows.Media.Animation.Timeline>
- <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>
- <xref:System.Windows.Media.Animation.FillBehavior.Stop>
- <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>
- [アニメーションの概要](animation-overview.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
