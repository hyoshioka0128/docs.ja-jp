---
title: '方法: ListBox のスクロール速度を向上させる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListBox control [WPF], reusing item containers
- ListBox control [WPF], improving scrolling performance
ms.assetid: 1e2bf8f3-c8ce-47f7-a400-a7fe11d1a848
ms.openlocfilehash: a9d1ca1d8ac2ef830984408f3052eb0ed0987c5d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770865"
---
# <a name="how-to-improve-the-scrolling-performance-of-a-listbox"></a>方法: ListBox のスクロール速度を向上させる
<xref:System.Windows.Controls.ListBox> に含まれる項目が多い場合、ユーザーがマウス ホイールを使用したり、スクロール バーのつまみをドラッグしたりして <xref:System.Windows.Controls.ListBox> をスクロールするときに、ユーザー インターフェイスの応答が遅くなることがあります。 `VirtualizingStackPanel.VirtualizationMode` 添付プロパティを <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> に設定することで、ユーザーがスクロールしたときの <xref:System.Windows.Controls.ListBox> のパフォーマンスを向上させることができます。  
  
## <a name="example"></a>例  
  
## <a name="description"></a>説明  
次の例では、<xref:System.Windows.Controls.ListBox> を作成し、`VirtualizingStackPanel.VirtualizationMode` 添付プロパティを <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> に設定して、スクロール中のパフォーマンスを向上させます。  
  
## <a name="code"></a>コード  
 [!code-xaml[RecycleItemContainerShippets#VirtualizationMode](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizationmode)]  
  
 次の例は、前の例で使用するデータを示しています。  
  
 [!code-csharp[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#listboxdata)]
 [!code-vb[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#listboxdata)]
