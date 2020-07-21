---
title: '方法: 要素を変換する'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], translations
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
ms.openlocfilehash: addff0e22fb3f27ea924887809c0635aeb3ad67d
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111973"
---
# <a name="how-to-translate-an-element"></a>方法: 要素を変換する
この例では、<xref:System.Windows.Media.TranslateTransform> を使用して要素を平行移動 (移動) する方法を示します。  
  
 <xref:System.Windows.Media.TranslateTransform> クラスは、絶対配置をサポートしていないパネル内の要素を移動する場合に特に役立ちます。 たとえば、<xref:System.Windows.Media.TranslateTransform> を要素の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに適用することで、<xref:System.Windows.Controls.StackPanel> または <xref:System.Windows.Controls.DockPanel> 内の要素を移動できます。  
  
 要素を x 軸に沿って移動させる分量をピクセル単位で指定するには、<xref:System.Windows.Media.TranslateTransform> の <xref:System.Windows.Media.TranslateTransform.X%2A> プロパティを使用します。 要素を y 軸に沿って移動させる分量をピクセル単位で指定するには、<xref:System.Windows.Media.TranslateTransform.Y%2A> プロパティを使用します。 最後に、<xref:System.Windows.Media.TranslateTransform> を要素の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに適用します。  
  
 次の例では、<xref:System.Windows.Media.TranslateTransform> を使用して、要素を右方向に 50 ピクセル、下方向に 50 ピクセル移動します。  
  
## <a name="example"></a>例  
 [!code-xaml[transformsSample#53](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 サンプル全体については、「[2D 変換のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [変換の概要](transforms-overview.md)
