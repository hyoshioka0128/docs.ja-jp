---
title: クエリ式の構文例:順序付け (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 653a4a97-1e4a-4b2d-8d24-7dbe1f2a5c84
ms.openlocfilehash: 932f5e4f6073844a951d06dabec45e5ff3e743bf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782996"
---
# <a name="query-expression-syntax-examples-ordering-linq-to-dataset"></a>クエリ式の構文例:順序付け (LINQ to DataSet)
このトピックでは、<xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.OrderByDescending%2A>、<xref:System.Linq.Enumerable.Reverse%2A>、および <xref:System.Linq.Enumerable.ThenByDescending%2A> の各メソッドで、クエリ構文を使って <xref:System.Data.DataSet> に対するクエリを実行し、その結果を並べ替える例を紹介しています。  
  
 これらの例で使用されている `FillDataSet` メソッドの指定については、「[DataSet へのデータの読み込み](loading-data-into-a-dataset.md)」を参照してください。  
  
 このトピックの例には、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルが使用されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 詳細については、[Visual Studio で LINQ to DataSet プロジェクトを作成する](how-to-create-a-linq-to-dataset-project-in-vs.md)」を参照してください。  
  
## <a name="orderby"></a>OrderBy  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.OrderBy%2A> を使用して、姓の順に並べ替えられた連絡先の一覧を返します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderBySimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbysimple1)]
 [!code-vb[DP LINQ to DataSet Examples#OrderBySimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbysimple1)]  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.OrderBy%2A> を使用して、連絡先の一覧を名の長さの順に並べ替えます。  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderBySimple2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbysimple2)]
 [!code-vb[DP LINQ to DataSet Examples#OrderBySimple2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbysimple2)]  
  
## <a name="orderbydescending"></a>OrderByDescending  
  
### <a name="example"></a>例  
 この例では、`orderby… descending` メソッドと同等の `Order By … Descending` (<xref:System.Linq.Enumerable.OrderByDescending%2A>) を使用して、価格の一覧を高いものから低い順に並べ替えます。  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderByDescendingSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbydescendingsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#OrderByDescendingSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbydescendingsimple1)]  
  
## <a name="reverse"></a>Reverse  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.Reverse%2A> を使用して、`OrderDate` が 2002 年 2 月 20 日よりも前の日付である注文の一覧を作成します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#reverse)]
 [!code-vb[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#reverse)]  
  
## <a name="thenbydescending"></a>ThenByDescending  
  
### <a name="example"></a>例  
 この例では、`OrderBy… Descending` メソッドと同等の <xref:System.Linq.Enumerable.ThenByDescending%2A> を使用して、製品の一覧を、名前順に、次に表示価格の高いものから低い順に並べ替えます。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ThenByDescendingSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#thenbydescendingsimple)]
 [!code-vb[DP LINQ to DataSet Examples#ThenByDescendingSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#thenbydescendingsimple)]  
  
## <a name="see-also"></a>関連項目

- [DataSet へのデータの読み込み](loading-data-into-a-dataset.md)
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
- [標準クエリ演算子の概要 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [標準クエリ演算子の概要 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
