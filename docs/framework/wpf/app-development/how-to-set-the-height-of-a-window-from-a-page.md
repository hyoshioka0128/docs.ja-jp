---
title: '方法: ページからウィンドウの高さを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- windows [WPF], setting height from a page
- pages [WPF], setting window height from
- height of window [WPF], setting from a page
ms.assetid: 4e4488ff-ab5c-4ee9-81a4-e1addb55c5cc
ms.openlocfilehash: c1041af88241011b51c96d7b61423344a32b25ca
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940800"
---
# <a name="how-to-set-the-height-of-a-window-from-a-page"></a>方法: ページからウィンドウの高さを設定する
この例では、<xref:System.Windows.Controls.Page> からウィンドウの高さを設定する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Page> では、<xref:System.Windows.Controls.Page.WindowHeight%2A> を設定することによって、そのホスト ウィンドウの高さを設定できます。 このプロパティを使用すると、<xref:System.Windows.Controls.Page> では、それをホストするウィンドウの種類を明示的に知っていなくてもかまいません。  
  
> [!NOTE]
> <xref:System.Windows.Controls.Page.WindowHeight%2A> を使用してウィンドウの高さを設定するには、<xref:System.Windows.Controls.Page> がウィンドウの子である必要があります。  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowHeightXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowHeightPage.xaml#setpagewindowheightxaml)]
