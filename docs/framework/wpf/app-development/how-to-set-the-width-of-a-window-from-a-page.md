---
title: '方法: ページからウィンドウの幅を設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- width of windows [WPF], setting from a page
- windows [WPF], setting width from a page
- pages [WPF], setting window width from
ms.assetid: 31601c92-7889-472a-b07e-bf675ad21c92
ms.openlocfilehash: 1e16b75ecb85550facdf24a5b9e341cf0c061178
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940775"
---
# <a name="how-to-set-the-width-of-a-window-from-a-page"></a>方法: ページからウィンドウの幅を設定する
この例では、<xref:System.Windows.Controls.Page> からウィンドウの幅を設定する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Page> では、<xref:System.Windows.Controls.Page.WindowWidth%2A> を設定することによって、そのホスト ウィンドウの幅を設定できます。 このプロパティを使用すると、<xref:System.Windows.Controls.Page> では、それをホストするウィンドウの種類を明示的に知っていなくてもかまいません。  
  
> [!NOTE]
> <xref:System.Windows.Controls.Page.WindowWidth%2A> を使用してウィンドウの幅を設定するには、<xref:System.Windows.Controls.Page> がウィンドウの子である必要があります。  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowWidthXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowWidthPage.xaml#setpagewindowwidthxaml)]
