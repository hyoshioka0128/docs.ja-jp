---
title: '方法: キャッシュされた要素をブラシとして使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- BitmapCache [WPF], using
- cached element [WPF], use as a brush
- BitmapCacheBrush [WPF], using
- CacheMode [WPF], using
ms.assetid: d36e944a-866e-4baf-98c4-fd6a75f6fdd0
ms.openlocfilehash: 78df242c7f00b69e36ea4ab6751f51509d9e2220
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769257"
---
# <a name="how-to-use-a-cached-element-as-a-brush"></a>方法: キャッシュされた要素をブラシとして使用する
<xref:System.Windows.Media.BitmapCacheBrush> クラスを使用し、キャッシュされた要素を効率良く再利用します。 要素をキャッシュするには、<xref:System.Windows.Media.BitmapCache> クラスの新しいインスタンスを作成し、それを要素の <xref:System.Windows.UIElement.CacheMode%2A> プロパティに割り当てます。  
  
## <a name="example"></a>例  
 キャッシュされた要素を再利用する方法を次のコード例に示します。 キャッシュされた要素は、大きな画像を表示する <xref:System.Windows.Controls.Image> コントロールです。 <xref:System.Windows.Controls.Image> コントロールは <xref:System.Windows.Media.BitmapCache> クラスを使用することでビットマップとしてキャッシュされ、それを <xref:System.Windows.Media.BitmapCacheBrush> に割り当てることでキャッシュが再利用されます。 ブラシは 25 個のボタンの背景に割り当てられ、効率的な再利用を示します。  
  
 [!code-xaml[System.Windows.Media.BitmapCacheBrush#_BitmapCacheBrushXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcachebrush/cs/window1.xaml#_bitmapcachebrushxaml)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.BitmapCache>
- <xref:System.Windows.Media.BitmapCacheBrush>
- <xref:System.Windows.UIElement.CacheMode%2A>
- [方法: 要素をキャッシュしてレンダリングのパフォーマンスを向上させる](how-to-improve-rendering-performance-by-caching-an-element.md)
