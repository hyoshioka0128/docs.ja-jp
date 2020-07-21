---
title: '方法: ListBoxItem を取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListBox controls [WPF], getting a ListBoxItem
- ListBoxItem [WPF]
ms.assetid: da877c6f-5fd8-40cb-8909-225cbfd99aa5
ms.openlocfilehash: 27a435feb4a941c77af221ab25bd63ea98b16e92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910326"
---
# <a name="how-to-get-a-listboxitem"></a>方法: ListBoxItem を取得する
<xref:System.Windows.Controls.ListBox> 内の特定のインデックスで特定の <xref:System.Windows.Controls.ListBoxItem> を取得する必要がある場合、<xref:System.Windows.Controls.ItemContainerGenerator> を利用できます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.ListBox> とその項目を示します。  
  
 [!code-xaml[ListBoxItems#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml#1)]  
  
 次の例では、<xref:System.Windows.Controls.ItemContainerGenerator> の <xref:System.Windows.Controls.ItemContainerGenerator.ContainerFromIndex%2A> プロパティに項目のインデックスを指定することで項目を取得する方法を示します。  
  
 [!code-csharp[ListBoxItems#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ListBoxItems#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#2)]  
  
 リスト ボックス項目を取得すると、次の例のように、項目のコンテンツを表示できます。  
  
 [!code-csharp[ListBoxItems#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#3)]
 [!code-vb[ListBoxItems#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#3)]
