---
title: 汎用 IEnumerable への型の変換
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 64774fb5-7447-4296-ad3b-8a94346f99a1
ms.openlocfilehash: c92f65c22fe4b4128a171c757bb9e9c0ccbc3fee
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247727"
---
# <a name="convert-a-type-to-a-generic-ienumerable"></a>汎用 IEnumerable への型の変換
汎用 <xref:System.Linq.Enumerable.AsEnumerable%2A> として型指定された引数を返すには、`IEnumerable` を使用します。  
  
## <a name="example"></a>例  
 この例では、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (既定の汎用 `Query` を使用) は、クエリを SQL に変換し、サーバー上での実行を試みます。 しかし、`where` 句が、SQL に変換できない、ユーザー定義のクライアント側メソッド (`isValidProduct`) を参照しています。  
  
 これを解決するには、クライアント側の汎用 <xref:System.Collections.Generic.IEnumerable%601> 実装の `where` を指定し、汎用 <xref:System.Linq.IQueryable%601> を置き換えます。 <xref:System.Linq.Enumerable.AsEnumerable%2A> 演算子を呼び出すことによって、これを行います。  
  
 [!code-csharp[DLinqQueryExamples#46](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#46)]
 [!code-vb[DLinqQueryExamples#46](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#46)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
