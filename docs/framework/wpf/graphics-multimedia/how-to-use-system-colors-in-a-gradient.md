---
title: '方法: グラデーションでシステム カラーを使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- gradients [WPF], system colors in
- system colors in gradients [WPF]
ms.assetid: 11942e7e-6300-4b50-8ed1-f50e8d20e7d2
ms.openlocfilehash: 55c99640907a0c372f8c7bbc50b9b45c9f15ef3c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769240"
---
# <a name="how-to-use-system-colors-in-a-gradient"></a>方法: グラデーションでシステム カラーを使用する
グラデーションでシステム カラーを使用するには、<xref:System.Windows.SystemColors> クラスの *\<SystemColor>* Color と *\<SystemColor>* ColorKey の静的プロパティを使用して、カラーの参照を取得します。ここで、 *\<SystemColor>* は、目的のシステム カラーの名前です。 システム テーマが変更されたときに自動的に更新される動的参照を作成する場合は、 *\<SystemColor>* ColorKey プロパティを使用します。 それ以外の場合は、 *\<SystemColor>* Color プロパティを使用します。  
  
## <a name="example"></a>例  
 次の例では、動的なシステム カラー リソースを使用して、グラデーションを作成します。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemColorExample.xaml#graphicsmmdynamicsystemcolorgradientexamplewholepage)]  
  
 次の例では、静的なシステム カラー リソースを使用して、グラデーションを作成します。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemColorExample.xaml#graphicsmmstaticsystemcolorgradientexamplewholepage)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.SystemColors>
- [システム ブラシで領域を塗りつぶす](how-to-paint-an-area-with-a-system-brush.md)
- [純色およびグラデーションによる塗りつぶしの概要](painting-with-solid-colors-and-gradients-overview.md)
