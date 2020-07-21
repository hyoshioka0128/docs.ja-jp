---
title: '方法: データ CollectionView のオブジェクト間を移動する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CollectionView [WPF], navigating through objects
- data binding [WPF], navigating through objects in data CollectionView
- navigating through objects in data CollectionView [WPF]
ms.assetid: fcd37590-bce1-4ac9-8b74-3b96c7458b8a
ms.openlocfilehash: 5ca386db89dcaa66d364d2ed7169c67393cebead
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459709"
---
# <a name="how-to-navigate-through-the-objects-in-a-data-collectionview"></a>方法: データ CollectionView のオブジェクト間を移動する
ビューでは、並べ替え、フィルター処理、グループ化に応じて、同じデータ コレクションを異なる方法で表示できます。 ビューでは、現在のレコード ポインターの概念が提供され、ポインターを移動できます。 この例では、<xref:System.Windows.Data.CollectionView> クラスで提供されている機能を使用して、現在のオブジェクトを取得する方法と、データ コレクション内のオブジェクト間を移動する方法を示します。  
  
## <a name="example"></a>例  
 この例では、`myCollectionView` は、バインドされたコレクションに対するビューである <xref:System.Windows.Data.CollectionView> オブジェクトです。  
  
 次の例では、`OnButton` はアプリケーションの `Previous` ボタンと `Next` ボタンのイベント ハンドラーであり、これらのボタンを使用してユーザーはデータ コレクション内を移動できます。 <xref:System.Windows.Data.CollectionView.IsCurrentBeforeFirst%2A> プロパティと <xref:System.Windows.Data.CollectionView.IsCurrentAfterLast%2A> プロパティによって、<xref:System.Windows.Data.CollectionView.MoveCurrentToFirst%2A> と <xref:System.Windows.Data.CollectionView.MoveCurrentToLast%2A> を適切に呼び出すことができるように、現在のレコード ポインターがリストのそれぞれ先頭および末尾にあるかどうかが報告されることに注意してください。  
  
 ビューの <xref:System.Windows.Data.CollectionView.CurrentItem%2A> プロパティは、コレクション内の現在の注文項目を返すために、`Order` としてキャストされます。  
  
 [!code-csharp[CollectionView#OnButton](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#onbutton)]
 [!code-vb[CollectionView#OnButton](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#onbutton)]  
  
## <a name="see-also"></a>関連項目

- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [ビュー内のデータの並べ替え](how-to-sort-data-in-a-view.md)
- [ビュー内のデータをフィルター処理する](how-to-filter-data-in-a-view.md)
- [XAML でビューを使用してデータの並べ替えおよびグループ化を行う](how-to-sort-and-group-data-using-a-view-in-xaml.md)
- [方法トピック](data-binding-how-to-topics.md)
