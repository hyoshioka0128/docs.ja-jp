---
title: '方法: 移動履歴の前後への移動'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- history [WPF], navigating forward
- navigation [WPF], through navigation history (forward)
ms.assetid: 5939d574-5f53-469e-85f5-1f2b13607caa
ms.openlocfilehash: 76a78debdce14123cc465ac9abf4db906fe0a2df
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961352"
---
# <a name="how-to-navigate-forward-or-back-through-navigation-history"></a>方法: 移動履歴の前後への移動
この例では、ナビゲーション履歴内のエントリ間を前方または後方に移動する方法を示します。  
  
## <a name="example"></a>例  
 次のホストのコンテンツから実行されたコードでは、ナビゲーション履歴内を、一度に 1 エントリずつ、前方または後方に移動できます。  
  
- <xref:System.Windows.Navigation.NavigationService> を使用する <xref:System.Windows.Navigation.NavigationWindow>  
  
- <xref:System.Windows.Navigation.NavigationService> を使用する <xref:System.Windows.Controls.Frame>  
  
- Internet Explorer  
  
 1 つ前方のエントリに移動するには、その前にまず、**CanGoForward** プロパティを調べて、ナビゲーション履歴で前方にエントリがあることを確認する必要があります。 1 つ前方のエントリに移動するには、**GoForward** メソッドを呼び出します。 これを次の例に示します。  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateForwardCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigateforwardcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateForwardCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigateforwardcode)]  
  
 1 つ後方のエントリに移動するには、その前にまず、**CanGoBack** プロパティを調べて、ナビゲーション履歴で後方にエントリがあることを確認する必要があります。 1 つ後方のエントリに移動するには、**GoBack** メソッドを呼び出します。 これを次の例に示します。  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoForward**、**GoForward**、**CanGoBack**、**GoBack** は、<xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Controls.Frame>、<xref:System.Windows.Navigation.NavigationService> によって実装されています。  
  
> [!NOTE]
> **GoForward** を呼び出して、ナビゲーション履歴の前方にエントリがない場合、または **GoBack** を呼び出して、ナビゲーション履歴の後方にエントリがない場合は、<xref:System.InvalidOperationException> がスローされます。
