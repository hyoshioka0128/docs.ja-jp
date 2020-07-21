---
title: '方法: ページに移動する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], navigating to
- navigation [WPF], to page
ms.assetid: 2a556fc0-748b-417f-a58a-0d05a7afb66f
ms.openlocfilehash: 25a0dbbc609c7b6f8f2878d2068e61e492a59c7e
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582538"
---
# <a name="how-to-navigate-to-a-page"></a>方法: ページに移動する
この例では、<xref:System.Windows.Navigation.NavigationWindow> からページに移動するいくつかの方法を示します。  
  
## <a name="example"></a>例  
 次のいずれかを使用して、<xref:System.Windows.Navigation.NavigationWindow> からページに移動できます。  
  
- <xref:System.Windows.Navigation.NavigationWindow.Source%2A> プロパティ。  
  
- <xref:System.Windows.Navigation.NavigationWindow.Navigate%2A> メソッド。  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateToPageCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigatetopagecode)]
 [!code-vb[HOWTONavigationSnippets#NavigateToPageCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigatetopagecode)]  
  
> [!NOTE]
> Uniform Resource Identifier (URI) は、相対または絶対で指定できます。 詳細については、「[WPF におけるパック URI](pack-uris-in-wpf.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Frame>
- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Navigation.NavigationService>
