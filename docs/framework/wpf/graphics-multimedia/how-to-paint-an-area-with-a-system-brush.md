---
title: '方法: システム ブラシで領域を塗りつぶす'
ms.date: 03/30/2017
helpviewer_keywords:
- system brushes [WPF], painting with
- painting [WPF], with system brushes
- brushes [WPF], painting with system brushes [WPF]
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
ms.openlocfilehash: 26511c577bf06b016dfc69cedc7fce2bafb35f32
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645376"
---
# <a name="how-to-paint-an-area-with-a-system-brush"></a>方法: システム ブラシで領域を塗りつぶす
<xref:System.Windows.SystemColors> クラスを使用すると、<xref:System.Windows.SystemColors.ControlBrush%2A>、<xref:System.Windows.SystemColors.ControlBrushKey%2A>、<xref:System.Windows.SystemColors.DesktopBrush%2A> などのシステム ブラシと色を利用できます。 システム ブラシは、指定したシステム カラーで領域を塗りつぶす <xref:System.Windows.Media.SolidColorBrush> オブジェクトです。 システム ブラシは、常に純色の塗りつぶしを生成します。グラデーションを作成するために使用することはできません。  
  
 システム ブラシは、静的なリソースとしても、動的なリソースとしても使用できます。 アプリケーションの実行中にユーザーがシステム ブラシを変更したときにブラシを自動的に更新する場合は、動的なリソースを使用します。それ以外の場合は、静的なリソースを使用します。 SystemColors クラスには、厳密な名前付け規則に従うさまざまな静的プロパティが含まれます。  
  
- *\<SystemColor>* Brush  
  
     指定したシステム カラーの <xref:System.Windows.Media.SolidColorBrush> への静的な参照が取得されます。  
  
- *\<SystemColor>* BrushKey  
  
     指定したシステム カラーの <xref:System.Windows.Media.SolidColorBrush> への動的な参照が取得されます。  
  
- *\<SystemColor>* Color  
  
     指定したシステム カラーの <xref:System.Windows.Media.Color> 構造体への静的な参照が取得されます。  
  
- *\<SystemColor>* ColorKey  
  
     指定したシステム カラーの <xref:System.Windows.Media.Color> 構造体への動的な参照が取得されます。  
  
 システム カラーは <xref:System.Windows.Media.Color> 構造体であり、ブラシの構成に使用できます。 たとえば、<xref:System.Windows.Media.LinearGradientBrush> オブジェクトのグラデーションの終了位置の <xref:System.Windows.Media.GradientStop.Color%2A> プロパティにシステム カラーを設定することで、システム カラーを使用してグラデーションを作成できます。 例については、「[グラデーションでシステム カラーを使用する](how-to-use-system-colors-in-a-gradient.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、動的なシステム ブラシの参照を使用して、ボタンの背景を設定します。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 次の例では、静的なシステム ブラシの参照を使用して、ボタンの背景を設定します。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 グラデーションでのシステム カラーの使用方法を示す例については、「[グラデーションでシステム カラーを使用する](how-to-use-system-colors-in-a-gradient.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [グラデーションでシステム カラーを使用する](how-to-use-system-colors-in-a-gradient.md)
- [純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)
