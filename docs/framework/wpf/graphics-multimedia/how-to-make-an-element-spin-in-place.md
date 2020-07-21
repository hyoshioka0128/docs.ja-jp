---
title: '方法: 要素のスピンを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], spinning elements
- spinning elements [WPF]
ms.assetid: 1f011976-8b07-4c31-9faf-019e0ddaa24c
ms.openlocfilehash: a1b515822391de08ec8ed8ff0ff1f0086874dc02
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112077"
---
# <a name="how-to-make-an-element-spin-in-place"></a>方法: 要素のスピンを設定する
この例では、<xref:System.Windows.Media.RotateTransform> と <xref:System.Windows.Media.Animation.DoubleAnimation> を使用して要素をスピンさせる方法を示します。  
  
 次の例では、要素の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.RotateTransform> を適用します。 この例では、<xref:System.Windows.Media.Animation.DoubleAnimation> を使用して <xref:System.Windows.Media.RotateTransform> の <xref:System.Windows.Media.RotateTransform.Angle%2A> をアニメーション化します。 要素を定位置でスピンさせるために、この例では要素の <xref:System.Windows.UIElement.RenderTransformOrigin%2A> プロパティを点 (0.5, 0.5) に設定しています。  
  
## <a name="example"></a>例  
 [!code-xaml[transformanimations_snip#11](~/samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/RotateAboutCenterExample.xaml#11)]  
  
 その他の変換の例を含むサンプル全体については、「[2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [変換の概要](transforms-overview.md)
