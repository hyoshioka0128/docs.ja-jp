---
title: シーケンスの要素のグループ化
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d50c8b4-f550-4775-bbb6-eab6e874cb43
ms.openlocfilehash: bc490b579e841a0e9b3724fe0e8789cc9411683d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782183"
---
# <a name="group-elements-in-a-sequence"></a>シーケンスの要素のグループ化
<xref:System.Linq.Enumerable.GroupBy%2A> 演算子はシーケンスの要素をグループ化します。 Northwind データベースを使用する例を次に示します。  
  
> [!NOTE]
> null 列値が <xref:System.Linq.Enumerable.GroupBy%2A> クエリに含まれると、<xref:System.InvalidOperationException> がスローされることがあります。 詳しくは、「[トラブルシューティング](troubleshooting.md)」の「GroupBy InvalidOperationException」をご覧ください。  
  
## <a name="example"></a>例  
 次の例では、`Products` を基準として `CategoryID` をグループ化しています。  
  
 [!code-csharp[DLinqQueryExamples#27](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#27)]
 [!code-vb[DLinqQueryExamples#27](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#27)]  
  
## <a name="example"></a>例  
 <xref:System.Linq.Enumerable.Max%2A> を使用して各 `CategoryID` の最も高い単価を調べる例を次に示します。  
  
 [!code-csharp[DLinqQueryExamples#28](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#28)]
 [!code-vb[DLinqQueryExamples#28](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#28)]  
  
## <a name="example"></a>例  
 Average を使用して各 `UnitPrice` の `CategoryID` の平均値を求める例を次に示します。  
  
 [!code-csharp[DLinqQueryExamples#29](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#29)]
 [!code-vb[DLinqQueryExamples#29](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#29)]  
  
## <a name="example"></a>例  
 <xref:System.Linq.Queryable.Sum%2A> を使用して各 `UnitPrice` の `CategoryID` の合計値を求める例を次に示します。  
  
 [!code-csharp[DLinqQueryExamples#30](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#30)]
 [!code-vb[DLinqQueryExamples#30](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#30)]  
  
## <a name="example"></a>例  
 <xref:System.Linq.Queryable.Count%2A> を使用して各 `Products` に含まれる生産中止の `CategoryID` の数を調べる例を次に示します。  
  
 [!code-csharp[DLinqQueryExamples#31](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#31)]
 [!code-vb[DLinqQueryExamples#31](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#31)]  
  
## <a name="example"></a>例  
 `where` 句を使用して最低 10 種類の製品が含まれるすべてのカテゴリを調べる方法を次の例に示します。  
  
 [!code-csharp[DLinqQueryExamples#32](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#32)]
 [!code-vb[DLinqQueryExamples#32](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#32)]  
  
## <a name="example"></a>例  
 `CategoryID` と `SupplierID` を使用して製品をグループ化する例を次に示します。  
  
 [!code-csharp[DLinqQueryExamples#33](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#33)]
 [!code-vb[DLinqQueryExamples#33](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#33)]  
  
## <a name="example"></a>例  
 次の例は、製品の 2 つのシーケンスを返します。 最初のシーケンスには、単価が 10 以下の製品が含まれます。 2 番目のシーケンスには、単価が 10 よりも大きい製品が含まれます。  
  
 [!code-csharp[DLinqQueryExamples#34](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#34)]
 [!code-vb[DLinqQueryExamples#34](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#34)]  
  
## <a name="example"></a>例  
 <xref:System.Linq.Queryable.GroupBy%2A> 演算子は、単一キーの引数のみを受け取ります。 複数のキーを使用してグループ化する場合は、次の例に示すように、匿名型を作成する必要があります。  
  
 [!code-csharp[DLinqQueryExamples#35](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#35)]
 [!code-vb[DLinqQueryExamples#35](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#35)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
