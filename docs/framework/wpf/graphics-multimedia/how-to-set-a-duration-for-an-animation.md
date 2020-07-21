---
title: '方法: アニメーションの継続時間を設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], duration
- Timelines [WPF], description
- duration of animations [WPF]
ms.assetid: 155034ef-7d00-4416-a73c-b1713992d2eb
ms.openlocfilehash: bdae1689ffeb8c54d756b9debbd26d57a052892d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651156"
---
# <a name="how-to-set-a-duration-for-an-animation"></a>方法: アニメーションの継続時間を設定する
<xref:System.Windows.Media.Animation.Timeline> は、時間のセグメントを表し、そのセグメントの長さはタイムラインの <xref:System.Windows.Duration> によって決定されます。 <xref:System.Windows.Media.Animation.Timeline> は、継続時間の最後に到達すると、再生を停止します。 <xref:System.Windows.Media.Animation.Timeline> に子タイムラインがある場合は、子も再生を停止します。 アニメーションの場合、<xref:System.Windows.Duration> は、アニメーションが開始値から終了値まで切り替わるのに要する時間を指定します。  
  
 <xref:System.Windows.Duration> には、特定の有限の時間、または特殊な値 <xref:System.Windows.Duration.Automatic%2A> または <xref:System.Windows.Duration.Forever%2A> を指定できます。 アニメーションには常に有限の長さを定義する必要があるため、アニメーションの継続時間は常に時間の値にする必要があります。そうしないと、アニメーションはターゲット値の間の切り替え方法を認識できません。 <xref:System.Windows.Media.Animation.Storyboard> や <xref:System.Windows.Media.Animation.ParallelTimeline> などのコンテナー タイムライン (<xref:System.Windows.Media.Animation.TimelineGroup> オブジェクト) の既定の継続時間は <xref:System.Windows.Duration.Automatic%2A> で、最後の子が再生を停止すると自動的に終了します。  
  
 次の例では、<xref:System.Windows.Shapes.Rectangle> の幅、高さ、塗りつぶしの色がアニメーション化されています。 継続時間はアニメーションとコンテナーのタイムラインに設定されるため、アニメーションの認識速度の制御や、コンテナー タイムラインの継続時間が設定された子タイムラインの継続時間のオーバーライドなどのアニメーション効果に影響します。  
  
## <a name="example"></a>例  
 [!code-xaml[timingbehaviors_snip#DurationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/DurationExample.xaml#durationexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Duration>
- [アニメーションの概要](animation-overview.md)
