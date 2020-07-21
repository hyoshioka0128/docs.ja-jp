---
title: '方法: イベント ハンドラーでソース要素を検索する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- source element in event handlers [WPF]
- event handlers [WPF], finding source element in
ms.assetid: 85f71c5a-b714-4c65-9711-7d905c2bbe98
ms.openlocfilehash: 9a49878c9ad8313903df4506796998fd43e2e749
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757509"
---
# <a name="how-to-find-the-source-element-in-an-event-handler"></a>方法: イベント ハンドラーでソース要素を検索する
この例からは、イベント ハンドラーでソース要素を検索する方法がわかります。  
  
## <a name="example"></a>例  
 次の例では、分離コード ファイルで宣言されている <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーを示します。 ハンドラーが添付されているボタンをユーザーがクリックすると、ハンドラーのプロパティ値が変わります。 ハンドラー コードでは、イベント引数で報告されるルーティング イベントの <xref:System.Windows.RoutedEventArgs.Source%2A> プロパティを使用し、<xref:System.Windows.RoutedEventArgs.Source%2A> 要素の <xref:System.Windows.FrameworkElement.Width%2A> プロパティ値を変更します。  
  
 [!code-xaml[RoutedEventSource#XAMLHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml#xamlhandler)]  
  
 [!code-csharp[RoutedEventSource#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventSource#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventSource/VisualBasic/default.xaml.vb#handler)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.RoutedEventArgs>
- [ルーティング イベントの概要](routed-events-overview.md)
- [方法トピック](events-how-to-topics.md)
