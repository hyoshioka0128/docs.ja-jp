---
title: '方法: ページを更新する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], refreshing
- refreshing pages [WPF]
ms.assetid: 06dd1bbd-81c4-40ad-ac0d-7a5b326b1465
ms.openlocfilehash: 71a71c91384a8905413358d023531afec23f2d41
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947669"
---
# <a name="how-to-refresh-a-page"></a>方法: ページを更新する
この例では、<xref:System.Windows.Navigation.NavigationWindow.Refresh%2A> メソッドを呼び出して、<xref:System.Windows.Navigation.NavigationWindow> の現在の内容を更新する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Navigation.NavigationWindow.Refresh%2A> では、<xref:System.Windows.Navigation.NavigationWindow> の現在の内容が、ソースから再度読み込まれて更新されます。  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateRefreshCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigaterefreshcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateRefreshCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigaterefreshcode)]
