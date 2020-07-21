---
title: '方法: DataTemplate によって生成された要素を検索する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- finding DataTemplate elements [WPF]
- DataTemplate [WPF]
ms.assetid: bfcd564e-5e9e-451e-8641-a9b5c3cfac90
ms.openlocfilehash: 3b222880aa4eda32502e3dcece2fa5c0b57b7a51
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646433"
---
# <a name="how-to-find-datatemplate-generated-elements"></a>方法: DataTemplate によって生成された要素を検索する
この例では、<xref:System.Windows.DataTemplate> によって生成された要素を検索する方法を示します。  
  
## <a name="example"></a>例  
 この例では、いくつかの XML データにバインドされている <xref:System.Windows.Controls.ListBox> があります。  
  
 [!code-xaml[FindGeneratedItems#LB](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#lb)]  
  
 <xref:System.Windows.Controls.ListBox> では、次の <xref:System.Windows.DataTemplate> が使用されます。  
  
 [!code-xaml[FindGeneratedItems#DT](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#dt)]  
  
 特定の <xref:System.Windows.Controls.ListBoxItem> の <xref:System.Windows.DataTemplate> によって生成された <xref:System.Windows.Controls.TextBlock> 要素を取得する場合は、<xref:System.Windows.Controls.ListBoxItem> を取得し、その <xref:System.Windows.Controls.ListBoxItem> 内の <xref:System.Windows.Controls.ContentPresenter> を見つけて、その <xref:System.Windows.Controls.ContentPresenter> に設定されている <xref:System.Windows.DataTemplate> 上で <xref:System.Windows.FrameworkTemplate.FindName%2A> を呼び出す必要があります。 これらの手順を実行する方法を次の例に示します。 デモンストレーションを目的として、この例では、<xref:System.Windows.DataTemplate> で生成されたテキスト ブロックのテキストの内容を示すメッセージ ボックスを作成します。  
  
 [!code-csharp[FindGeneratedItems#DTFindElement](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#dtfindelement)]
 [!code-vb[FindGeneratedItems#DTFindElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#dtfindelement)]  
  
 <xref:System.Windows.Media.VisualTreeHelper> メソッドを使用する `FindVisualChild` の実装を次に示します。  
  
 [!code-csharp[FindGeneratedItems#FVC](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#fvc)]
 [!code-vb[FindGeneratedItems#FVC](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#fvc)]  
  
## <a name="see-also"></a>関連項目

- [方法: ControlTemplate によって生成された要素を検索する](../controls/how-to-find-controltemplate-generated-elements.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [WPF XAML 名前スコープ](../advanced/wpf-xaml-namescopes.md)
- [WPF のツリー](../advanced/trees-in-wpf.md)
