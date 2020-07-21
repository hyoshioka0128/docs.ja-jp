---
title: クエリ式の構文例:射影
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 079926c5-e6b5-4fb9-b4cf-9c63886dd626
ms.openlocfilehash: b5139cc310689eb05833ead8d35c03d02eb2fc58
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398415"
---
# <a name="query-expression-syntax-examples-projection"></a>クエリ式の構文例:射影
このトピックでは、クエリ式の構文で、`Select` メソッドおよび `From … From …` キーワードを使用して、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を照会する例を取り上げます。 `From … From …` は、メソッドは、`SelectMany` メソッドのクエリ ベース版に相当します。 これらの例で使用されている、AdventureWorks Sales Model は、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルから作成されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="select"></a>選択  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Enumerable.Select%2A> メソッドを使用して `Product` テーブルからすべての行を取得し、製品名を表示しています。  
  
 [!code-csharp[DP L2E Examples#SelectSimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP L2E Examples#SelectSimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectsimple1)]  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Enumerable.Select%2A> を使用して、一連の製品名だけを取得しています。  
  
 [!code-csharp[DP L2E Examples#SelectSimple2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectsimple2)]
 [!code-vb[DP L2E Examples#SelectSimple2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectsimple2)]  
  
### <a name="example"></a>例  
 次の例では、<xref:System.Linq.Queryable.Select%2A> メソッドを使用して、`Product.Name` プロパティおよび `Product.ProductID` プロパティを一連の匿名型に射影します。  
  
 [!code-csharp[DP L2E Examples#SelectAnonymousTypes](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectanonymoustypes)]
 [!code-vb[DP L2E Examples#SelectAnonymousTypes](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectanonymoustypes)]  
  
## <a name="from--from--selectmany"></a>From … From … (SelectMany)  
  
### <a name="example"></a>例  
 次の例では、`From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> メソッドと等価) を使用して、`TotalDue` が 500.00 に満たないすべての注文を選択します。  
  
 [!code-csharp[DP L2E Examples#SelectManyCompoundFrom](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanycompoundfrom)]
 [!code-vb[DP L2E Examples#SelectManyCompoundFrom](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanycompoundfrom)]  
  
### <a name="example"></a>例  
 次の例では、`From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> メソッドと等価) を使用して、2002 年 10 月 1 日以降に受けたすべての注文を選択します。  
  
 [!code-csharp[DP L2E Examples#SelectManyCompoundFrom2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanycompoundfrom2)]
 [!code-vb[DP L2E Examples#SelectManyCompoundFrom2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanycompoundfrom2)]  
  
### <a name="example"></a>例  
 次の例では、`From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> メソッドと等価) を使用して、注文の合計が 10000.00 を超えるすべての注文を選択します。このとき、`From` 割り当てを使用して、合計を 2 回要求しないようにしています。  
  
 [!code-csharp[DP L2E Examples#SelectManyFromAssignment](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanyfromassignment)]
 [!code-vb[DP L2E Examples#SelectManyFromAssignment](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanyfromassignment)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
