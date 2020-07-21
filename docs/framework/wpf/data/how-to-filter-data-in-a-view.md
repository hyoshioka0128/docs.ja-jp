---
title: '方法: ビュー内のデータをフィルター処理する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- views [WPF], filtering data
- filtering data in views [WPF]
- data binding [WPF], filtering data in views
ms.assetid: c76e8606-4cc4-45a8-9110-e2ec66dc6afd
ms.openlocfilehash: f15bcfd1e3c4175f8b4b97244f120d5edbdec9b8
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77453079"
---
# <a name="how-to-filter-data-in-a-view"></a>方法: ビュー内のデータをフィルター処理する
この例では、ビュー内のデータをフィルター処理する方法を示します。  
  
## <a name="example"></a>例  
 フィルターを作成するには、フィルター処理ロジックを提供するメソッドを定義します。 メソッドは、コールバックとして使用され、`object` 型のパラメーターを受け取ります。 次のメソッドでは、`filled` プロパティが "No" に設定されているすべての `Order` オブジェクトが返され、残りのオブジェクトはフィルターで除外されます。  
  
 [!code-csharp[SortFilter#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#2)]
 [!code-vb[SortFilter#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#2)]  
  
 次の例で示すように、フィルターを適用できます。 この例では、`myCollectionView` は <xref:System.Windows.Data.ListCollectionView> オブジェクトです。  
  
 [!code-csharp[SortFilter#Filter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#filter)]
 [!code-vb[SortFilter#Filter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#filter)]  
  
 フィルター処理を元に戻すには、<xref:System.Windows.Data.CollectionView.Filter%2A> プロパティを `null` に設定します。  
  
 [!code-csharp[SortFilter#Unfilter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#unfilter)]
 [!code-vb[SortFilter#Unfilter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#unfilter)]  
  
 ビューを作成または取得する方法については、「[データ コレクションの既定のビューを取得する](how-to-get-the-default-view-of-a-data-collection.md)」を参照してください。 完全な例については、「[ビュー サンプルの項目の並べ替えとフィルター処理](https://github.com/Microsoft/WPF-Samples/tree/master/Data%20Binding/SortFilter)」を参照してください。  
  
 ビュー オブジェクトの元が <xref:System.Windows.Data.CollectionViewSource> オブジェクトの場合は、<xref:System.Windows.Data.CollectionViewSource.Filter> イベントのイベント ハンドラーを設定することによって、フィルター処理ロジックを適用します。 次の例では、`listingDataView` は <xref:System.Windows.Data.CollectionViewSource> のインスタンスです。  
  
 [!code-csharp[DataBindingLab#10](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 次に示すのは、`ShowOnlyBargainsFilter` フィルター イベント ハンドラーの例の実装です。 このイベント ハンドラーでは、<xref:System.Windows.Data.FilterEventArgs.Accepted%2A> プロパティを使用して、`CurrentPrice` が $25 以上である `AuctionItem` オブジェクトを除外します。  
  
 [!code-csharp[DataBindingLab#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.CollectionView.CanFilter%2A>
- <xref:System.Windows.Data.BindingListCollectionView.CustomFilter%2A>
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [ビュー内のデータの並べ替え](how-to-sort-data-in-a-view.md)
- [方法トピック](data-binding-how-to-topics.md)
