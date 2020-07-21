---
title: '方法: 移動履歴を遡る'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- history [WPF], navigating back
- navigation [WPF], through navigation history (back)
ms.assetid: 9343234b-d864-441d-b8a7-d895cba80a87
ms.openlocfilehash: 53b32e145390d7052262042c7a793699c163b373
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969350"
---
# <a name="how-to-navigate-back-through-navigation-history"></a>方法: 移動履歴を遡る
この例では、ナビゲーション履歴の後方のエントリに移動する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Navigation.NavigationService> を使用する <xref:System.Windows.Controls.Frame>、または Internet Explorer でホストされているコンテンツから実行されているコードでは、一度に 1 エントリずつ、ナビゲーション履歴内を後方に移動できます。  
  
 **GoBack** メソッドを呼び出すことによって 1 つ後方のエントリに移動する前に、**CanGoBack** プロパティを調べて、ナビゲーション履歴の後方にエントリがあることを確認する必要があります。 これを次の例に示します。  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoBack** と **GoBack** は、<xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Controls.Frame>、<xref:System.Windows.Navigation.NavigationService> によって実装されています。  
  
> [!NOTE]
> **GoBack** を呼び出して、ナビゲーション履歴の後方にエントリがない場合は、<xref:System.InvalidOperationException> が発生します。
