---
title: メソッド ベースのクエリ構文例:パーティション分割 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a582c53f-f203-44ae-a797-d7f169a4fbb5
ms.openlocfilehash: 7e01bd9702ae267f80ecf24de0c0cc90d638a84c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783588"
---
# <a name="method-based-query-syntax-examples-partitioning-linq"></a>メソッド ベースのクエリ構文例:パーティション分割 (LINQ to DataSet)
このトピックでは、<xref:System.Linq.Enumerable.Skip%2A>、<xref:System.Linq.Enumerable.SkipWhile%2A>、<xref:System.Linq.Enumerable.Take%2A>、<xref:System.Linq.Enumerable.TakeWhile%2A> の各メソッドで、クエリ式の構文を使って <xref:System.Data.DataSet> に対するクエリを実行する例を紹介しています。  
  
 これらの例で使用されている `FillDataSet` メソッドは、「[DataSet へのデータの読み込み](loading-data-into-a-dataset.md)」で指定されています。  
  
 このトピックの例には、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルが使用されています。  
  
 このトピックの例には、次の `using`/`Imports` ステートメントが使用されています。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 詳細については、[Visual Studio で LINQ to DataSet プロジェクトを作成する](how-to-create-a-linq-to-dataset-project-in-vs.md)」を参照してください。  
  
## <a name="skip"></a>Skip  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.Skip%2A> テーブルから最初の 5 つを除くすべての連絡先を、`Contact` メソッドを使って取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipsimple)]
 [!code-vb[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipsimple)]  
  
### <a name="example"></a>例  
 この例では、Seattle から最初の 2 つを除くすべての住所を、<xref:System.Linq.Enumerable.Skip%2A> メソッドを使って取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipnested)]  
  
## <a name="skipwhile"></a>SkipWhile  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.OrderBy%2A> メソッドおよび <xref:System.Linq.Enumerable.SkipWhile%2A> メソッドを使用し、表示価格が 300.00 を超える製品を `Product` テーブルから取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipwhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipwhilesimple_mq)]  
  
## <a name="take"></a>Take  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.Take%2A> テーブルから最初の 5 つの連絡先だけを、`Contact` メソッドを使って取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takesimple)]
 [!code-vb[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takesimple)]  
  
### <a name="example"></a>例  
 この例では、Seattle から最初の 3 つの住所を、<xref:System.Linq.Enumerable.Take%2A> メソッドを使って取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takenested)]
 [!code-vb[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takenested)]  
  
## <a name="takewhile"></a>TakeWhile  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.OrderBy%2A> メソッドおよび <xref:System.Linq.Enumerable.TakeWhile%2A> メソッドを使用し、表示価格が 300.00 未満の製品を `Product` テーブルから取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takewhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takewhilesimple_mq)]  
  
## <a name="see-also"></a>関連項目

- [DataSet へのデータの読み込み](loading-data-into-a-dataset.md)
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
- [標準クエリ演算子の概要 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [標準クエリ演算子の概要 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
