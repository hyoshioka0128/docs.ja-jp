---
title: '方法: AnimationClock を使用してプロパティをアニメーション化する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], properties [WPF], with AnimationClocks
- AnimationClocks [WPF]
ms.assetid: e6542021-714c-4675-9567-04f1c7380834
ms.openlocfilehash: 13d91e8589c40d84ba374ffc613388e24407796a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591287"
---
# <a name="how-to-animate-a-property-by-using-an-animationclock"></a>方法: AnimationClock を使用してプロパティをアニメーション化する
この例からは、<xref:System.Windows.Media.Animation.Clock> オブジェクトを使用してプロパティをアニメーション化する方法がわかります。  
  
 依存関係プロパティをアニメーション化するには次の 3 つの方法があります。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline> を作成し、それを <xref:System.Windows.Media.Animation.Storyboard> を使用してプロパティと関連付けます。  
  
- オブジェクトの <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用して、ターゲット プロパティに 1 つの <xref:System.Windows.Media.Animation.AnimationTimeline> を適用します。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline> から <xref:System.Windows.Media.Animation.AnimationClock> を作成して、それをプロパティに適用します。  
  
 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトと <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> メソッドを使用すると、クロックを直接作成して配布しなくても、プロパティをアニメーション化できます (例については、「[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)」と「[ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)」を参照してください)。つまり、クロックは自動的に作成されて配布されます。  
  
## <a name="example"></a>例  
 次の例は、<xref:System.Windows.Media.Animation.AnimationClock> を作成して、それを 2 つの類似したプロパティに適用する方法を示します。  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 <xref:System.Windows.Media.Animation.Clock> の開始後にこれを対話的に制御する方法の例については、「[クロックを対話的に制御する](how-to-interactively-control-a-clock.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)
- [ストーリーボードを使用せずにプロパティをアニメーション化する](how-to-animate-a-property-without-using-a-storyboard.md)
- [プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)
