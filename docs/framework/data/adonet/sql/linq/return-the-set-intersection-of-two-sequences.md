---
title: 2 つのシーケンスの積集合の取得
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d09c344e-3548-4944-a3ed-051880e3f5b8
ms.openlocfilehash: 944d0b2efe1e74f901a493d1c3202d0f180d599d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792707"
---
# <a name="return-the-set-intersection-of-two-sequences"></a>2 つのシーケンスの積集合の取得
2 つのシーケンスの積集合を返すには、<xref:System.Linq.Queryable.Intersect%2A> 演算子を使用します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Linq.Queryable.Intersect%2A> を使用して、`Customers` と `Employees` の両方が居住しているすべての国や地域のシーケンスが返されます。  
  
 [!code-csharp[DLinqQueryExamples#42](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#42)]
 [!code-vb[DLinqQueryExamples#42](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#42)]  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、<xref:System.Linq.Queryable.Intersect%2A> 演算は集合でのみ適切に定義されます。 マルチセットのセマンティクスは未定義です。  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
- [標準クエリ演算子の変換](standard-query-operator-translation.md)
