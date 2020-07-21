---
title: スタイル内でアニメーション化する方法
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], properties [WPF], within styles
- styles [WPF], animating properties within
ms.assetid: 6a791f3d-6b1f-4972-a2f9-35880bcfd954
ms.openlocfilehash: 0b29648bf15f0046adcdee610f9565f7deb24972
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76744879"
---
# <a name="how-to-animate-in-a-style"></a>スタイル内でアニメーション化する方法

この例では、スタイル内でプロパティをアニメーション化する方法を示します。 スタイル内でアニメーション化する場合、スタイルが定義されているフレームワーク要素のみを直接ターゲットにできます。 Freezable オブジェクトをターゲットにするには、スタイルが設定されている要素のプロパティから "ドット ダウン" する必要があります。

次の例では、いくつかのアニメーションがスタイル内に定義されており、<xref:System.Windows.Controls.Button> に適用されています。 ユーザーがボタンの上にマウスを移動すると、ボタンは不透明から部分的に半透明になって元に戻ることを繰り返します。 ユーザーがマウスをボタンから移動すると、ボタンは完全に不透明になります。 ボタンをクリックすると、ボタンの背景色がオレンジから白に変わり、元に戻ります。 ボタンの描画に使用される <xref:System.Windows.Media.SolidColorBrush> を直接ターゲットにすることはできないため、ボタンの <xref:System.Windows.Controls.Control.Background%2A> プロパティからドット ダウンしてアクセスします。

## <a name="example"></a>例

[!code-xaml[timingbehaviors_snip#21](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StyleStoryboardsExample.xaml#21)]

スタイル内でアニメーション化するときに、存在しないオブジェクトをターゲットにすることができる点に注意してください。 たとえば、スタイルで <xref:System.Windows.Media.SolidColorBrush> を使用してボタンの背景プロパティを設定していたが、ある時点でそのスタイルがオーバーライドされて、<xref:System.Windows.Media.LinearGradientBrush> を使用してボタンの背景が設定されたとします。  <xref:System.Windows.Media.SolidColorBrush> をアニメーション化しても例外はスローされません。アニメーションは、単に警告なしで失敗します。

ストーリーボードのターゲット設定構文の詳細については、「[ストーリーボードの概要](storyboards-overview.md)」を参照してください。 アニメーション化の詳細については、「[アニメーションの概要](animation-overview.md)」を参照してください。 スタイルの詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。
