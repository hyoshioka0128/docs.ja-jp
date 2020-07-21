---
title: '方法: ポップアップをアニメーション化する'
ms.date: 03/30/2017
helpviewer_keywords:
- Popup control [WPF], animating
- animation [WPF], Popup controls
ms.assetid: acaa2a0a-6137-4efd-9cd1-75ece222e390
ms.openlocfilehash: b70d9c4cb1bca26a6c77d3a7c50add517ca8ef92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911288"
---
# <a name="how-to-animate-a-popup"></a>方法: ポップアップをアニメーション化する
この例では、<xref:System.Windows.Controls.Primitives.Popup> コントロールをアニメーション化する 2 つの方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.Primitives.PopupAnimation> プロパティが値 <xref:System.Windows.Controls.Primitives.PopupAnimation.Slide> に設定されています。それにより、<xref:System.Windows.Controls.Primitives.Popup> は表示時、"スライドイン" します。  
  
 <xref:System.Windows.Controls.Primitives.Popup> を回転させるため、この例では、<xref:System.Windows.Controls.Primitives.Popup> の子要素である <xref:System.Windows.Controls.Canvas> で <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.RotateTransform> が割り当てられています。  
  
 変換を正しく機能させるため、この例では、<xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> プロパティを `true` に設定する必要があります。 また、<xref:System.Windows.Controls.Primitives.Popup> が回転するために十分な空間を <xref:System.Windows.Controls.Canvas> の <xref:System.Windows.FrameworkElement.Margin%2A> で指定する必要があります。  
  
 [!code-xaml[AnimatedPopup#RotateTransform2](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform2)]  
  
 次の例では、<xref:System.Windows.Controls.Button> のクリック時に発生する <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントによって、アニメーションを開始する <xref:System.Windows.Media.Animation.Storyboard> がトリガーされるしくみを示します。  
  
 [!code-xaml[AnimatedPopup#RotateTransform1](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.UIElement.RenderTransform%2A>
- <xref:System.Windows.Controls.Primitives.BulletDecorator>
- <xref:System.Windows.Media.RotateTransform>
- <xref:System.Windows.Media.Animation.Storyboard>
- <xref:System.Windows.Controls.Primitives.Popup>
- [方法トピック](popup-how-to-topics.md)
- [ポップアップの概要](popup-overview.md)
