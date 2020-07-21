---
title: '方法: ScrollBar のつまみのサイズをカスタマイズする'
ms.date: 03/30/2017
helpviewer_keywords:
- ScrollBar control [WPF]
- customizing thumb size [WPF]
- thumb size [WPF]
ms.assetid: fa32b866-5ca1-4e73-85e7-2ac64b80d194
ms.openlocfilehash: 60ae7c4e95801036c5deb0c485645297509b830c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911054"
---
# <a name="how-to-customize-the-thumb-size-on-a-scrollbar"></a>方法: ScrollBar のつまみのサイズをカスタマイズする
このトピックでは、<xref:System.Windows.Controls.Primitives.ScrollBar> の <xref:System.Windows.Controls.Primitives.Thumb> を固定サイズに設定する方法と、<xref:System.Windows.Controls.Primitives.ScrollBar> の <xref:System.Windows.Controls.Primitives.Thumb> に最小サイズを指定する方法について説明します。  
  
## <a name="example"></a>例  
  
## <a name="description"></a>説明  
 次の例では、<xref:System.Windows.Controls.Primitives.Thumb> が固定サイズの <xref:System.Windows.Controls.Primitives.ScrollBar> が作成されます。 この例では、<xref:System.Windows.Controls.Primitives.Thumb> の <xref:System.Windows.Controls.Primitives.Track.ViewportSize%2A> プロパティが <xref:System.Double.NaN> に設定され、高さ <xref:System.Windows.Controls.Primitives.Thumb> が設定されています。  <xref:System.Windows.Controls.Primitives.Thumb> の幅を固定して水平 <xref:System.Windows.Controls.Primitives.ScrollBar> を作成するには、幅 <xref:System.Windows.Controls.Primitives.Thumb> を設定します。  
  
## <a name="code"></a>コード  
 [!code-xaml[ScrollBarCustomThumbSize#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#1)]  
  
## <a name="description"></a>説明  
 次の例では、<xref:System.Windows.Controls.Primitives.Thumb> が最小サイズの <xref:System.Windows.Controls.Primitives.ScrollBar> が作成されます。 この例では、値 <xref:System.Windows.SystemParameters.VerticalScrollBarButtonHeightKey%2A> が設定されています。 <xref:System.Windows.Controls.Primitives.Thumb> の幅を最小にして水平 <xref:System.Windows.Controls.Primitives.ScrollBar> を作成するには、<xref:System.Windows.SystemParameters.HorizontalScrollBarButtonWidthKey%2A> を設定します。  
  
## <a name="code"></a>コード  
 [!code-xaml[ScrollBarCustomThumbSize#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#2)]  
  
## <a name="see-also"></a>関連項目

- [ScrollBar のスタイルとテンプレート](scrollbar-styles-and-templates.md)
