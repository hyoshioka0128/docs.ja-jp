---
title: '方法: ページからウィンドウのタイトルを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- windows [WPF], setting title from a page
- title of window [WPF], setting from a page
- pages [WPF], setting window title from
ms.assetid: fecf0d19-3eb6-4f8c-a44f-ff1b6f2b34b3
ms.openlocfilehash: 0f618af89965822b0df96a264997dabd9cae7608
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940787"
---
# <a name="how-to-set-the-title-of-a-window-from-a-page"></a>方法: ページからウィンドウのタイトルを設定する
この例では、<xref:System.Windows.Controls.Page> がホストされているウィンドウのタイトルを設定する方法を示します。  
  
## <a name="example"></a>例  
 ページでは、次のように <xref:System.Windows.Controls.Page.WindowTitle%2A> プロパティを設定することにより、そのページをホストしているウィンドウのタイトルを変更できます。  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowTitleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowTitlePage.xaml#setpagewindowtitlexaml)]  
  
> [!NOTE]
> ページの <xref:System.Windows.Controls.Page.Title%2A> プロパティを設定しても、ウィンドウのタイトルの値は変更されません。 <xref:System.Windows.Controls.Page.Title%2A> で指定されているのは、ナビゲーション履歴でのページ エントリの名前です。
