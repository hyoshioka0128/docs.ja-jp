---
title: '方法: アニメーションを加速または減速させる'
ms.date: 03/30/2017
helpviewer_keywords:
- decelerating animation [WPF]
- accelerating animation [WPF]
- animation [WPF], accelerating
- animation [WPF], decelerating
ms.assetid: 4f383b2c-f94d-4a4e-9a06-f56f5dae95f9
ms.openlocfilehash: 7ab55ba44b866a992b9021284f170858f0108d15
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81243012"
---
# <a name="how-to-accelerate-or-decelerate-an-animation"></a>方法: アニメーションを加速または減速させる

この例では、時間の経過と共にアニメーションを加速および減速させる方法を示します。 次の例では、<xref:System.Windows.Media.Animation.Timeline.AccelerationRatio%2A> と <xref:System.Windows.Media.Animation.Timeline.DecelerationRatio%2A> の異なる設定を使用したアニメーションによって複数の四角形がアニメーション化されます。  
  
## <a name="example"></a>例  
 [!code-xaml[timingbehaviors_snip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AccelDecelExample.xaml#1)]  
  
 この例では、コードは省略されています。 詳しいコードについては、[アニメーションのタイミング動作 (C#)](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp) または[アニメーションのタイミング動作 (Visual Basic)](https://github.com/dotnet/docs/tree/master/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic) に関する記事を参照してください。
