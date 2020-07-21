---
title: クエリ式の構文例:順序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: bcbc9625-7cf7-476e-85d2-058f12682f54
ms.openlocfilehash: 73000b16b29238dfb60596060733ecf8d7caa45b
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398435"
---
# <a name="query-expression-syntax-examples-ordering"></a>クエリ式の構文例:順序
このトピックでは、クエリ式構文で、`OrderBy` メソッドおよび `OrderByDescending` メソッドを使用して、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を照会する例を取り上げます。 これらの例で使用されている、AdventureWorks Sales Model は、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルから作成されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="orderby"></a>OrderBy  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Enumerable.OrderBy%2A> を使用して、姓の順に並べ替えられた連絡先の一覧を返します。  
  
 [!code-csharp[DP L2E Examples#OrderBySimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbysimple1)]
 [!code-vb[DP L2E Examples#OrderBySimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbysimple1)]  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Enumerable.OrderBy%2A> を使用して、連絡先の一覧を姓の長さの順に並べ替えます。  
  
 [!code-csharp[DP L2E Examples#OrderBySimple2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbysimple2)]
 [!code-vb[DP L2E Examples#OrderBySimple2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbysimple2)]  
  
## <a name="orderbydescending"></a>OrderByDescending  
  
### <a name="example"></a>例  
 次の例では、`orderby… descending` メソッドと同等の `Order By … Descending` (Visual Basic の場合は <xref:System.Linq.Enumerable.OrderByDescending%2A>) を使用して、価格の一覧を高いものから低い順に並べ替えます。  
  
 [!code-csharp[DP L2E Examples#OrderByDescendingSimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbydescendingsimple1)]
 [!code-vb[DP L2E Examples#OrderByDescendingSimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbydescendingsimple1)]  
  
## <a name="thenby"></a>ThenBy  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Queryable.OrderBy%2A> と <xref:System.Linq.Queryable.ThenBy%2A> を使用して、姓の順、次に名の順に並べ替えられた連絡先の一覧を返します。  
  
 [!code-csharp[DP L2E Examples#OrderByThenBy](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbythenby)]
 [!code-vb[DP L2E Examples#OrderByThenBy](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbythenby)]  
  
## <a name="thenbydescending"></a>ThenByDescending  
  
### <a name="example"></a>例  
 次の例では、`OrderBy… Descending` メソッドと同等の <xref:System.Linq.Enumerable.ThenByDescending%2A> を使用して、製品の一覧を、名前順に、次に表示価格の高いものから低い順に並べ替えます。  
  
 [!code-csharp[DP L2E Examples#ThenByDescendingSimple](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#thenbydescendingsimple)]
 [!code-vb[DP L2E Examples#ThenByDescendingSimple](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#thenbydescendingsimple)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
