---
title: '方法: 子タイムラインを使用してアニメーションを簡素化する'
ms.date: 03/30/2017
helpviewer_keywords:
- simplifying animations by child timelines [WPF]
- animation [WPF], simplifying by child timelines
- child timelines [WPF]
ms.assetid: 8335d770-d13d-42bd-8dfa-63f92c0327e2
ms.openlocfilehash: 21a297208be045eea79d6f5ca6c8eac016d26345
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61804014"
---
# <a name="how-to-simplify-animations-by-using-child-timelines"></a>方法: 子タイムラインを使用してアニメーションを簡素化する
この例では、子 <xref:System.Windows.Media.Animation.ParallelTimeline> オブジェクトを使用して、アニメーションを単純化する方法を示しています。 <xref:System.Windows.Media.Animation.Storyboard> は、それに含まれているタイムラインのターゲット情報を指定する <xref:System.Windows.Media.Animation.Timeline> の一種です。 <xref:System.Windows.Media.Animation.Storyboard> を使用すると、オブジェクトとプロパティ情報を含むタイムラインのターゲット情報を指定することができます。  
  
 アニメーションを開始するには、<xref:System.Windows.Media.Animation.Storyboard>に子要素として、<xref:System.Windows.Media.Animation.ParallelTimeline> オブジェクトを 1 つ以上入れ子にします。 これらの <xref:System.Windows.Media.Animation.ParallelTimeline> オブジェクトには他のアニメーションも含めることができるため、複雑なアニメーションでタイミング シーケンスをより上手にカプセル化できます。 たとえば、<xref:System.Windows.Controls.TextBlock> と複数の図形を同じ <xref:System.Windows.Media.Animation.Storyboard>内にアニメーション化する場合は、<xref:System.Windows.Controls.TextBlock> と図形のアニメーションを別々の <xref:System.Windows.Media.Animation.ParallelTimeline> に分けることができます。 各 <xref:System.Windows.Media.Animation.ParallelTimeline> にはそれぞれ <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> があり、<xref:System.Windows.Media.Animation.ParallelTimeline> のすべての子要素がこの <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> を基準として開始されるため、タイミングをより適切にカプセル化できます。  
  
 次の例では、同じ <xref:System.Windows.Media.Animation.Storyboard>内の 2 つのテキスト (<xref:System.Windows.Controls.TextBlock> オブジェクト) をアニメーション化します。 <xref:System.Windows.Media.Animation.ParallelTimeline> では、<xref:System.Windows.Controls.TextBlock> オブジェクトのアニメーションを 1 つカプセル化します。  
  
 **パフォーマンスに関するメモ:** <xref:System.Windows.Media.Animation.Storyboard> のタイムラインは互いに入れ子にできますが、オーバーヘッドが少ない <xref:System.Windows.Media.Animation.ParallelTimeline> の方が入れ子には適しています。 (<xref:System.Windows.Media.Animation.Storyboard> クラスは <xref:System.Windows.Media.Animation.ParallelTimeline> クラスを継承します。)  
  
## <a name="example"></a>例  
 [!code-xaml[Timelines_snip#ParallelTimelineWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Timelines_snip/CS/ParallelTimelineExample.xaml#paralleltimelinewholepage)]  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [ストーリーボード アニメーション間で HandoffBehavior を指定する](how-to-specify-handoffbehavior-between-storyboard-animations.md)
