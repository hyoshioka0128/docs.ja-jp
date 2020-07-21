---
title: '方法: 要素を名前で検索する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- elements [WPF], finding by name
ms.assetid: cfa7cf35-8aa2-4060-9454-872ed4af3f0e
ms.openlocfilehash: 7405f9ba8db5d4db0ce35ca250f13e456685f39b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757847"
---
# <a name="how-to-find-an-element-by-its-name"></a>方法: 要素を名前で検索する
この例では、<xref:System.Windows.FrameworkElement.FindName%2A> メソッドを利用し、その <xref:System.Windows.FrameworkElement.Name%2A> 値で要素を見つける方法を示します。  
  
## <a name="example"></a>例  
 この例では、その名前で特定の要素を見つけるメソッドは、ボタンのイベント ハンドラーとして記述されています。 `stackPanel` は検索されるルート <xref:System.Windows.FrameworkElement> の <xref:System.Windows.FrameworkElement.Name%2A> です。例のメソッドでは次に、それを <xref:System.Windows.Controls.TextBlock> として型変換し、<xref:System.Windows.Controls.TextBlock> の表示 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] プロパティの 1 つを変更することで、見つかった要素を視覚的に示します。  
  
 [!code-csharp[FEFindName#Find](~/samples/snippets/csharp/VS_Snippets_Wpf/FEFindName/CSharp/default.xaml.cs#find)]
 [!code-vb[FEFindName#Find](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEFindName/VisualBasic/default.xaml.vb#find)]
