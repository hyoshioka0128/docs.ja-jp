---
title: メソッド ベースのクエリ構文例:結合演算子
description: これらの例を活用することにより、Join メソッドと GroupJoin メソッドを使用して、LINQ to Entities のメソッドベースのクエリ構文でモデルに対してクエリを実行する方法を学習できます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d00f0efa-9084-4c17-843f-54904fcb4204
ms.openlocfilehash: 3b1445b39bdcd9a9b4d0672be0598233319cb85d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286832"
---
# <a name="method-based-query-syntax-examples-join-operators"></a>メソッド ベースのクエリ構文例:結合演算子
このトピックでは、メソッド ベースのクエリ構文で、<xref:System.Linq.Enumerable.Join%2A> メソッドと <xref:System.Linq.Enumerable.GroupJoin%2A> メソッドを使用して、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を照会する例を取り上げます。 これらの例で使用されている、AdventureWorks Sales Model は、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルから作成されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="groupjoin"></a>GroupJoin  
  
### <a name="example"></a>例  
 次の例では、SalesOrderHeader テーブルおよび SalesOrderDetail テーブルに対して <xref:System.Linq.Enumerable.GroupJoin%2A> を実行することによって、顧客ごとの注文数を調べます。 GroupJoin は、左外部結合に相当します。つまり、1 つ目 (左側) のデータ ソースに存在するすべての要素は、関連する要素がもう一方のデータ ソースに存在するかどうかに関係なく返されます。  
  
 [!code-csharp[DP L2E Examples#GroupJoin2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupjoin2_mq)]
 [!code-vb[DP L2E Examples#GroupJoin2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupjoin2_mq)]  
  
### <a name="example"></a>例  
 次の例では、Contact テーブルおよび SalesOrderHeader テーブルに対して <xref:System.Linq.Enumerable.GroupJoin%2A> を実行して、連絡先ごとの注文数を調べます。 各連絡先の注文数と ID が表示されます。  
  
 [!code-csharp[DP L2E Examples#GroupJoin_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupjoin_mq)]
 [!code-vb[DP L2E Examples#GroupJoin_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupjoin_mq)]  
  
## <a name="join"></a>Join  
  
### <a name="example"></a>例  
 次の例では、Contact テーブルと SalesOrderHeader テーブルの結合を実行します。  
  
 [!code-csharp[DP L2E Examples#JoinSimple_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#joinsimple_mq)]
 [!code-vb[DP L2E Examples#JoinSimple_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#joinsimple_mq)]  
  
### <a name="example"></a>例  
 次の例では、Contact テーブルと SalesOrderHeader テーブルを結合し、結果を連絡先 ID でグループ化します。  
  
 [!code-csharp[DP L2E Examples#JoinWithGroupedResults_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#joinwithgroupedresults_mq)]
 [!code-vb[DP L2E Examples#JoinWithGroupedResults_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#joinwithgroupedresults_mq)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
