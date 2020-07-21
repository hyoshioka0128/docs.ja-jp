---
title: '方法: 多くのオブジェクトを一度に取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 18aff4d8-bde8-461b-9960-ccabb24e9d22
ms.openlocfilehash: 48cdb47bec35b5315e03629d3a01657136bf7ed2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781677"
---
# <a name="how-to-retrieve-many-objects-at-once"></a>方法: 多くのオブジェクトを一度に取得する
多くのオブジェクトを 1 つのクエリで取得するには、<xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> を使用します。  
  
## <a name="example"></a>例  
 <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> メソッドを使用して、`Customer` と `Order` の両方を取得するコードの例を次に示します。  
  
 [!code-csharp[DLinqQueryConcepts#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#9)]
 [!code-vb[DLinqQueryConcepts#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#9)]  
  
## <a name="see-also"></a>関連項目

- [クエリの概念](query-concepts.md)
