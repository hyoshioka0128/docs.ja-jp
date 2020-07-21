---
title: '方法: UIElement を左右または上下に反転させる'
ms.date: 03/30/2017
helpviewer_keywords:
- flipping UIElements [WPF]
- UIElements [WPF], flipping
ms.assetid: 02c6730f-65c0-40d5-a553-4cb663721882
ms.openlocfilehash: 6b3da322493d17e4f8e36a35b9a0e40fdc9dc685
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61767054"
---
# <a name="how-to-flip-a-uielement-horizontally-or-vertically"></a>方法: UIElement を左右または上下に反転させる
この例からは、<xref:System.Windows.Media.ScaleTransform> を使用し、<xref:System.Windows.UIElement> を左右または上下に反転させる方法がわかります。 この例では、<xref:System.Windows.Media.ScaleTransform> をその <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに適用することで <xref:System.Windows.Controls.Button> コントロール (<xref:System.Windows.UIElement> 型) が反転します。  
  
## <a name="example"></a>例  
 反転するボタンを以下で図解します。  
  
 ![変換のないボタン](./media/graphicsmm-buttonflipbeforeflip.gif "graphicsmm_buttonflipbeforeflip")  
反転する UIElement  
  
 次のコードではボタンが作成されます。  
  
 [!code-xaml[Transforms_snip#GraphicsMMButtonWithoutFlip](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmbuttonwithoutflip)]  
  
## <a name="example"></a>例  
 ボタンを左右に反転させるには、<xref:System.Windows.Media.ScaleTransform> を作成し、その <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> プロパティを -1 に設定します。 ボタンの <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.ScaleTransform> を適用します。  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample1)]  
  
 ![ボタンが &#40;0,0&#41; あたりで左右に反転しました](./media/graphicsmm-buttonfliphorizontalflip-displaced.gif "graphicsmm_buttonfliphorizontalflip_displaced")  
ScaleTransform 適用後のボタン  
  
## <a name="example"></a>例  
 上の画像からわかるように、反転したボタンは移動もしています。 これはボタンがその左上隅から反転されたためです。 ボタンを定位置で反転させるには、<xref:System.Windows.Media.ScaleTransform> をその隅ではなくその中心に適用します。 <xref:System.Windows.Media.ScaleTransform> をボタンの中心に適用する簡単な方法は、ボタンの <xref:System.Windows.UIElement.RenderTransformOrigin%2A> プロパティを 0.5, 0.5 に設定することです。  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample2)]  
  
 ![ボタンがその中心あたりで左右に反転しました](./media/graphicsmm-buttonfliphorizontalflip-inplace.gif "graphicsmm_buttonfliphorizontalflip_inplace")  
RenderTransformOrigin が 0.5, 0.5 のボタン  
  
## <a name="example"></a>例  
 ボタンを上下に反転させるには、<xref:System.Windows.Media.ScaleTransform> オブジェクトの <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> プロパティをその <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> プロパティの代わりに設定します。  
  
 [!code-xaml[Transforms_snip#GraphicsMMVerticalFlipButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmverticalflipbuttonexample2)]  
  
 ![ボタンがその中心あたりで上下に反転しました](./media/graphicsmm-buttonflipverticalflip-inplace.gif "graphicsmm_buttonflipverticalflip_inplace")  
上下に反転したボタン  
  
## <a name="see-also"></a>関連項目

- [変換の概要](../graphics-multimedia/transforms-overview.md)
