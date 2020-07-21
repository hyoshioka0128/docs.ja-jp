---
title: '方法: ビュー内のデータの並べ替え'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], sorting data in views
- data binding [WPF], grouping data in views
- grouping data in views [WPF]
- views [WPF], sorting data
- views [WPF], grouping data
- sorting data in views [WPF]
ms.assetid: f4c43578-01b7-4774-a953-acb95a13b94a
ms.openlocfilehash: 14314ed019f9194a657787bd767ae68615e94ac7
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73454831"
---
# <a name="how-to-sort-data-in-a-view"></a>方法: ビュー内のデータの並べ替え
この例では、ビュー内のデータを並べ替える方法について説明します。  
  
## <a name="example"></a>例  
 次の例では、簡単な <xref:System.Windows.Controls.ListBox> と <xref:System.Windows.Controls.Button> を作成します。  
  
 [!code-xaml[ListBoxSort_snip#HowTo](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml#howto)]  
  
 ボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーには、<xref:System.Windows.Controls.ListBox> 内の項目を降順で並べ替えるためのロジックが含まれています。 この方法で <xref:System.Windows.Controls.ListBox> に項目を追加すると、<xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemCollection> に項目が追加され、<xref:System.Windows.Controls.ItemCollection> は <xref:System.Windows.Data.CollectionView> クラスから派生しているため、これを行うことができます。 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティを使用して <xref:System.Windows.Controls.ListBox> をコレクションにバインドしている場合は、同じ手法を使用して並べ替えることができます。  
  
 [!code-csharp[ListBoxSort_snip#HowToCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml.cs#howtocode)]
 [!code-vb[ListBoxSort_snip#HowToCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxSort_snip/visualbasic/window1.xaml.vb#howtocode)]  
  
 ビュー オブジェクトへの参照がある限り、同じ手法を使用して、他のコレクション ビューの内容を並べ替えることができます。 ビューを取得する方法の例については、「[データ コレクションの既定のビューを取得する](how-to-get-the-default-view-of-a-data-collection.md)」を参照してください。 別の例については、「[ヘッダーがクリックされたときに GridView 列を並べ替える](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)」を参照してください。 ビューについて詳しくは、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」の「コレクションへのバインド」をご覧ください。  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で並べ替えロジックを適用する方法の例については、「[XAML でビューを使用してデータの並べ替えおよびグループ化を行う](how-to-sort-and-group-data-using-a-view-in-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.ListCollectionView.CustomSort%2A>
- [ヘッダーがクリックされたときに GridView 列を並べ替える](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [ビュー内のデータをフィルター処理する](how-to-filter-data-in-a-view.md)
- [方法トピック](data-binding-how-to-topics.md)
