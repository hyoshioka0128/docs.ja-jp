---
title: クエリ式の構文例:パーティション分割
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e41aed0-3be9-4f75-98de-860a85552a3c
ms.openlocfilehash: b845564c02b55b8729efc893d7eecc48bd60f710
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398547"
---
# <a name="query-expression-syntax-examples-partitioning"></a>クエリ式の構文例:パーティション分割
このトピックでは、クエリ式構文で、<xref:System.Linq.Enumerable.Skip%2A> メソッドおよび <xref:System.Linq.Enumerable.Take%2A> メソッドを使用して、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を照会する例を取り上げます。 これらの例で使用されている、AdventureWorks Sales Model は、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルから作成されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="skip"></a>Skip  
  
### <a name="example"></a>例  
 次の例では、Seattle から最初の 2 つを除くすべての住所を、<xref:System.Linq.Enumerable.Skip%2A> メソッドを使って取得します。  
  
 [!code-csharp[DP L2E Examples#SkipNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP L2E Examples#SkipNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#skipnested)]  
  
## <a name="take"></a>Take  
  
### <a name="example"></a>例  
 次の例では、Seattle から最初の 3 つの住所を、<xref:System.Linq.Enumerable.Take%2A> メソッドを使って取得します。  
  
 [!code-csharp[DP L2E Examples#TakeNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#takenested)]
 [!code-vb[DP L2E Examples#TakeNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#takenested)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
