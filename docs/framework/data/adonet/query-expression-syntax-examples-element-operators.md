---
title: クエリ式の構文例:要素演算子 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ca392dda-16e3-45c7-8d87-12d8d4ee0578
ms.openlocfilehash: ae29ed3d61489b9da24a34e2e99ee32bd67c6d5c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783036"
---
# <a name="query-expression-syntax-examples-element-operators-linq-to-dataset"></a>クエリ式の構文例:要素演算子 (LINQ to DataSet)
このトピックでは、<xref:System.Linq.Enumerable.First%2A> メソッドおよび <xref:System.Linq.Enumerable.ElementAt%2A> メソッドを使用し、クエリ式の構文を使って <xref:System.Data.DataRow> から <xref:System.Data.DataSet> 要素を取得する例を紹介しています。  
  
 これらの例で使用されている `FillDataSet` メソッドの指定については、「[DataSet へのデータの読み込み](loading-data-into-a-dataset.md)」を参照してください。  
  
 このトピックの例には、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルが使用されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 詳細については、[Visual Studio で LINQ to DataSet プロジェクトを作成する](how-to-create-a-linq-to-dataset-project-in-vs.md)」を参照してください。  
  
## <a name="elementat"></a>ElementAt  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.ElementAt%2A> メソッドを使用し、`PostalCode` == "M4B 1V7" の条件に該当する 5 番目の住所を取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ElementAt](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#elementat)]
 [!code-vb[DP LINQ to DataSet Examples#ElementAt](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#elementat)]  
  
## <a name="first"></a>First  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.First%2A> メソッドを使用して、名が 'Brooke' である最初の連絡先を取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#FirstSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#firstsimple)]
 [!code-vb[DP LINQ to DataSet Examples#FirstSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#firstsimple)]  
  
## <a name="see-also"></a>関連項目

- [DataSet へのデータの読み込み](loading-data-into-a-dataset.md)
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
- [標準クエリ演算子の概要 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [標準クエリ演算子の概要 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
