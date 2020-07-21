---
title: '方法: イベントの発生時に要素に変換を適用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], transformations as event responses
- properties [WPF], LayoutTransform
- transformations as event responses [WPF]
- properties [WPF], RenderTransform
- LayoutTransform property [WPF]
ms.assetid: 71e4327e-ca57-444c-a3cf-09fb381491a0
ms.openlocfilehash: 8f04db274432c0e89c6839bef825976c8a2f853c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64630753"
---
# <a name="how-to-apply-a-transform-to-an-element-when-an-event-occurs"></a>方法: イベントの発生時に要素に変換を適用する
この例では、イベントが発生したときに <xref:System.Windows.Media.ScaleTransform> を適用する方法を示します。 ここで示される概念は、他の種類の変換を適用する場合に使用するものと同じです。 使用可能な変換の種類の詳細については、「<xref:System.Windows.Media.Transform> クラス」または「[変換の概要](transforms-overview.md)」を参照してください。  
  
 要素に変換を適用するには、次の 2 つの方法があります。  
  
- 変換がレイアウトに影響 "*しない*" ようにする場合は、要素の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティを使用します。  
  
- 変換がレイアウトに影響するようにする場合は、要素の <xref:System.Windows.FrameworkElement.LayoutTransform%2A> プロパティを使用します。  
  
 次の例では、ボタンの <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.ScaleTransform> を適用します。 マウスをボタンの上に移動すると、<xref:System.Windows.Media.ScaleTransform> の <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> プロパティと <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> プロパティが `2` に設定され、ボタンが大きくなります。 マウスがボタンから離れると、<xref:System.Windows.Media.ScaleTransform.ScaleX%2A> と <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> が `1` に設定され、ボタンは元のサイズに戻ります。  
  
## <a name="example"></a>例  
 [!code-xaml[ButtonTransform#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml#1)]  
  
 [!code-csharp[ButtonTransform#1cb](~/samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml.cs#1cb)]
 [!code-vb[ButtonTransform#1cb](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ButtonTransform/VisualBasic/ButtonTransformExample.xaml.vb#1cb)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.ScaleTransform>
- [変換の概要](transforms-overview.md)
- [方法トピック](transformations-how-to-topics.md)
- [ルーティング イベントの概要](../advanced/routed-events-overview.md)
