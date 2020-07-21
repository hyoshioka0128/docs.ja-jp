---
title: '方法: 要素をキャッシュしてレンダリングのパフォーマンスを向上させる'
ms.date: 03/30/2017
helpviewer_keywords:
- rendering performance [WPF], caching an element
- BitmapCache [WPF], improving rendering performance
- CacheMode [WPF], improving rendering performance
- performance [WPF], caching an element
- UIElement [WPF], caching
ms.assetid: 4739c1fc-60ba-4c46-aba6-f6c1a2688f19
ms.openlocfilehash: 118e8b0cca52c44788c9d5b291d710f765e7af2a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947278"
---
# <a name="how-to-improve-rendering-performance-by-caching-an-element"></a>方法: 要素をキャッシュしてレンダリングのパフォーマンスを向上させる
<xref:System.Windows.Media.BitmapCache> クラスを使用すると、複雑な <xref:System.Windows.UIElement> のレンダリング パフォーマンスを向上させることができます。 要素をキャッシュするには、<xref:System.Windows.Media.BitmapCache> クラスの新しいインスタンスを作成し、それを要素の <xref:System.Windows.UIElement.CacheMode%2A> プロパティに割り当てます。 <xref:System.Windows.Media.BitmapCache>は、<xref:System.Windows.Media.BitmapCacheBrush> で効率的に再利用できます。  
  
## <a name="example"></a>例  
 次のコード例では、複合要素を作成し、それをビットマップとしてキャッシュして、要素をアニメーション化するときにパフォーマンスを向上させる方法を示します。 この要素は、頂点が多数ある形状ジオメトリを保持するキャンバスです。 既定値の <xref:System.Windows.Media.BitmapCache> がキャンバスの <xref:System.Windows.UIElement.CacheMode%2A> に割り当てられ、キャッシュされたビットマップはアニメーションでスムーズにスケーリングされます。  
  
 [!code-xaml[System.Windows.Media.BitmapCache#_BitmapCacheXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcache/cs/window1.xaml#_bitmapcachexaml)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.BitmapCache>
- <xref:System.Windows.Media.BitmapCacheBrush>
- <xref:System.Windows.UIElement.CacheMode%2A>
- [方法: キャッシュされた要素をブラシとして使用する](how-to-use-a-cached-element-as-a-brush.md)
