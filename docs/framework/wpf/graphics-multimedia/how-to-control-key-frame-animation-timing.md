---
title: '方法: キー フレーム アニメーションのタイミングを制御する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], timing
- timing key-frame animation
ms.assetid: b059216f-7d4b-4ca8-a019-bc287ee7bf16
ms.openlocfilehash: 8cfd2be0bbc526ed92a5fb1b558a5a41dc9c3113
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344736"
---
# <a name="how-to-control-key-frame-animation-timing"></a>方法: キー フレーム アニメーションのタイミングを制御する

この例では、キー フレーム アニメーション内のキー フレームのタイミングを制御する方法を示します。 他のアニメーションと同様に、キー フレーム アニメーションには <xref:System.Windows.Media.Animation.Timeline.Duration%2A> プロパティがあります。 アニメーションの継続時間を指定するだけでなく、その継続時間のどの部分を各キー フレームに割り当てるかを指定する必要があります。 時間を割り当てるには、アニメーションの各キーフ レームに <xref:System.Windows.Media.Animation.KeyTime> を指定します。

各キー フレームの <xref:System.Windows.Media.Animation.KeyTime> では、キーフ レームの終了時点を指定します (キー フレームの再生時間の長さを指定するわけではありません)。 <xref:System.Windows.Media.Animation.KeyTime> は、<xref:System.TimeSpan> 値として、パーセントとして、<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> または <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 特殊値として指定できます。

## <a name="example"></a>例

次の例では、<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> を使用して画面全体で四角形をアニメーション化します。 キー フレームのキー時間は <xref:System.TimeSpan> 値で設定します。

[!code-csharp[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimestimespanexample)]
[!code-vb[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimestimespanexample)]
[!code-xaml[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimestimespanexample)]

次の図は、各キー フレームの値に到達したことを示しています。

![キー値は 3 秒、4 秒、10 秒です](./media/graphicsmm-keyframe-keytime1-timespan.png "graphicsmm_keyframe_keytime1_timespan")

次の例は同一のアニメーションを示していますが、キー フレームのキー時間にパーセント値が設定されている点が異なります。

[!code-csharp[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespercentageexample)]
[!code-vb[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespercentageexample)]
[!code-xaml[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespercentageexample)]

次の図は、各キー フレームの値に到達したことを示しています。

![キー値は 3 秒、4 秒、10 秒です](./media/graphicsmm-keyframe-keytime2-percentage.png "graphicsmm_keyframe_keytime2_percentage")

次の例では <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> キー時間値を使用しています。

[!code-csharp[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimesuniformexample)]
[!code-vb[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimesuniformexample)]
[!code-xaml[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimesuniformexample)]

次の図は、各キー フレームの値に到達したことを示しています。

![キー値は 3.3 秒、6.6 秒、9.9 秒です](./media/graphicsmm-keyframe-keytime3-uniform.png "graphicsmm_keyframe_keytime3_uniform")

最後の例では <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> キー時間値を使用しています。

[!code-csharp[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespacedexample)]
[!code-vb[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespacedexample)]
[!code-xaml[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespacedexample)]

次の図は、各キー フレームの値に到達したことを示しています。

![キー値は 0 秒、5 秒、10 秒です](./media/graphicsmm-keyframe-keytime4-paced.png "graphicsmm_keyframe_keytime4_paced")

わかりやすくするために、この例のコード バージョンではストーリーボードではなくローカル アニメーションを使用しています。1 つのプロパティに適用されるのが 1 つのアニメーションだけであるためです。ただし、この例は、代わりにストーリーボードを使用するように変更できます。 コードでストーリーボードを宣言する方法を示す例については、「[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)」を参照してください。

サンプル全体については、「[キーフレーム アニメーションのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Animation/KeyFrameAnimation)」を参照してください。 キー フレーム アニメーションの詳細については、「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [アニメーションの概要](animation-overview.md)
- [方法トピック](animation-and-timing-how-to-topics.md)
