---
title: '方法: ストーリーボード アニメーション間で HandoffBehavior を指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- Storyboards [WPF], handoff behavior between animations
- animation [WPF], handoff behavior between
ms.assetid: 97bd6842-929b-49d9-813e-46553ae46472
ms.openlocfilehash: d7129d6a48bdf31dc4953bb450267ad3b38fdd17
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651039"
---
# <a name="how-to-specify-handoffbehavior-between-storyboard-animations"></a>方法: ストーリーボード アニメーション間で HandoffBehavior を指定する
この例は、ストーリーボード アニメーション間でハンドオフ動作を指定する方法を示します。 <xref:System.Windows.Media.Animation.BeginStoryboard> の <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> プロパティは、既にプロパティに適用されている既存のアニメーションと新しいアニメーションが相互作用する方法を指定します。  
  
## <a name="example"></a>例  
 次の例では、マウス カーソルを合わせると拡大し、カーソルを離すと縮小する 2 つのボタンを作成しています。 ボタンにマウスを合わせてからカーソルをすぐに離すと、最初のアニメーションが終了する前に 2 番目のアニメーションが適用されます。 このように 2 つのアニメーションが重なり、<xref:System.Windows.Media.Animation.HandoffBehavior.Compose> と <xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace> の <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> の値の違いを確認できます。 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> の値を重複するアニメーションと組み合わされると、アニメーション間でのスムーズな画面切り替え効果が生まれます。一方、<xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace> の値を指定すると、新しいアニメーションが、前に重なっていたアニメーションを直ちに置き換えます。  
  
 [!code-xaml[timingbehaviors_snip#HandoffBehaviorWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/HandoffBehaviorExample.xaml#handoffbehaviorwholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.BeginStoryboard>
- <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>
- [アニメーションの概要](animation-overview.md)
- [アニメーションおよびタイミングに関する「方法」トピック](animation-and-timing-how-to-topics.md)
