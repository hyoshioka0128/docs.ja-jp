---
title: '方法: DataContext レベルでフィルター処理する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 15505cd7-0df2-427a-9f86-e0f96f60ee2e
ms.openlocfilehash: 0ef5ba8e975cb1c59720c96b214ae2696cc6356e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781945"
---
# <a name="how-to-filter-at-the-datacontext-level"></a>方法: DataContext レベルでフィルター処理する
`EntitySets` を `DataContext` レベルでフィルター処理できます。 このフィルター処理は、対象の <xref:System.Data.Linq.DataContext> インスタンスを使って実行されたすべてのクエリに適用されます。  
  
## <a name="example"></a>例  
 次の例では、あらかじめ読み込まれた顧客からの注文を <xref:System.Data.Linq.DataLoadOptions.AssociateWith%28System.Linq.Expressions.LambdaExpression%29?displayProperty=nameWithType> に基づいてフィルター処理するために `ShippedDate` が使用されます。  
  
 [!code-csharp[DLinqQueryConcepts#10](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#10)]
 [!code-vb[DLinqQueryConcepts#10](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#10)]  
  
## <a name="see-also"></a>関連項目

- [クエリの概念](query-concepts.md)
