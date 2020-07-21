---
title: シーケンスのすべての要素が条件を満たしているかどうかの確認
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 339ec145-826c-46d2-8cf2-3acd252cd072
ms.openlocfilehash: 7de65579cb41641aded0b9a320fac59804959ff5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782232"
---
# <a name="determine-if-any-or-all-elements-in-a-sequence-satisfy-a-condition"></a>シーケンスのすべての要素が条件を満たしているかどうかの確認
<xref:System.Linq.Enumerable.All%2A> 演算子は、シーケンスのすべての要素が条件を満たす場合に `true` を返します。  
  
 <xref:System.Linq.Queryable.Any%2A> 演算子は、シーケンスの要素が 1 つでも条件を満たす場合に `true` を返します。  
  
## <a name="example"></a>例  
 次の例では、最低 1 件の注文がある顧客のシーケンスを返します。 `Where`/`where` 句は、指定した `Customer` に `Order` がある場合に `true` と評価されます。  
  
 [!code-csharp[DLinqQueryExamples#37](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#37)]
 [!code-vb[DLinqQueryExamples#37](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#37)]  
  
## <a name="example"></a>例  
 次の Visual Basic コードでは、注文がない顧客のリストを調べ、リストに記載されている顧客に連絡先名があることを確認します。  
  
 [!code-vb[DLinqQueryExamples#37v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#37v)]  
  
## <a name="example"></a>例  
 次の C# コードでは、注文の `ShipCity` が "C" で始まる顧客のシーケンスを返します。 注文のない顧客も結果に含まれます。 (<xref:System.Linq.Queryable.All%2A> 演算子はシーケンスが空の場合に `true` を返すように設計されています)。注文のない顧客を削除してコンソールに出力するには、`Count` 演算子を使用します。  
  
 [!code-csharp[DLinqQueryExamples#38](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#38)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
