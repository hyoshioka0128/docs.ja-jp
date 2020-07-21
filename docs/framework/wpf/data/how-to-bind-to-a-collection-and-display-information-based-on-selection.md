---
title: '方法: コレクションにバインドして選択に基づく情報を表示する'
description: 次の例に従って、Windows Presentation Foundation (WPF) でコレクションにバインドし、選択に基づいて情報を表示する方法を確認します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data collections [WPF], selecting data for views
- data binding [WPF], creating views of data collections
- data binding [WPF], selecting data for views
- data binding [WPF], binding to collections
ms.assetid: 952a7d76-dd29-49e5-86f5-32c4530e70eb
ms.openlocfilehash: fb8757ee6818a2812308a0a132fa9d06951ad52e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619612"
---
# <a name="how-to-bind-to-a-collection-and-display-information-based-on-selection"></a>方法: コレクションにバインドして選択に基づく情報を表示する
簡単なマスター詳細シナリオでは、<xref:System.Windows.Controls.ListBox> などのデータ バインドされた <xref:System.Windows.Controls.ItemsControl> があります。 ユーザーの選択に基づいて、選択された項目に関する詳細情報を表示します。 この例では、このシナリオを実装する方法を示します。  
  
## <a name="example"></a>例  
 この例の `People` は、`Person` クラスの <xref:System.Collections.ObjectModel.ObservableCollection%601> です。 この `Person` クラスには `FirstName`、`LastName`、`HomeTown` の 3 つのプロパティが含まれ、すべて `string` 型です。  
  
 [!code-xaml[CollectionBinding#Source](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#source)]  
[!code-xaml[CollectionBinding#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#ui)]  
  
 <xref:System.Windows.Controls.ContentControl> では、`Person` の情報の表示方法を定義する次の <xref:System.Windows.DataTemplate> が使用されます。  
  
 [!code-xaml[CollectionBinding#DetailTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#detailtemplate)]  
  
 次に、この例で生成される内容のスクリーンショットを示します。 <xref:System.Windows.Controls.ContentControl> には、選択されたユーザーの他のプロパティが表示されます。  
  
 ![コレクションへのバインディング](./media/databinding-collectionbindingsample.png "DataBinding_CollectionBindingSample")  
  
 この例では、次の 2 つの点に注意してください。  
  
1. <xref:System.Windows.Controls.ListBox> と <xref:System.Windows.Controls.ContentControl> は同じソースにバインドされます。 どちらのコントロールもコレクション オブジェクト全体にバインドされるため、両方のバインディングの <xref:System.Windows.Data.Binding.Path%2A> プロパティは指定されません。  
  
2. これを機能させるには、<xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> プロパティを `true` に設定する必要があります。 このプロパティを設定すると、選択された項目が常に <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A> として設定されます。 または、<xref:System.Windows.Controls.ListBox> で <xref:System.Windows.Data.CollectionViewSource> からデータが取得される場合は、選択と通貨が自動的に同期されます。  
  
 `Person` クラスでは、次のように `ToString` メソッドがオーバーライドされていることに注意してください。 既定では、<xref:System.Windows.Controls.ListBox> によって `ToString` が呼び出され、バインドされたコレクション内の各オブジェクトの文字列形式が表示されます。 そのため、各 `Person` が <xref:System.Windows.Controls.ListBox> の名として表示されます。  
  
 [!code-csharp[CollectionBinding#ToString](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Data.cs#tostring)]
 [!code-vb[CollectionBinding#ToString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionBinding/VisualBasic/Person.vb#tostring)]  
  
## <a name="see-also"></a>関連項目

- [階層データでマスター詳細パターンを使用する](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)
- [階層 XML データでマスター詳細パターンを使用する](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [データ テンプレートの概要](data-templating-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
