---
title: シーケンスの要素の並べ替え
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d59b93a9-50c8-4770-a114-d902f6a0ea76
ms.openlocfilehash: 21fa2f9e1dc2f255fe94f2420ba90a809ab5b05e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792666"
---
# <a name="sort-elements-in-a-sequence"></a>シーケンスの要素の並べ替え
1 つ以上のキーに従ってシーケンスを並べ替えるには、<xref:System.Linq.Enumerable.OrderBy%2A> 演算子を使用します。  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、`string` や `int` などの単純で基本的なデータ型による順序付けをサポートするように設計されています。 匿名型のように複数の値を持つ複雑なクラスでの順序付けはサポートされていません。 また、`byte` データ型もサポートされていません。  
  
## <a name="example"></a>例  
 次の例は、`Employees` を入社日の順に並べ替えます。  
  
 [!code-csharp[DLinqQueryExamples#20](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#20)]
 [!code-vb[DLinqQueryExamples#20](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#20)]  
  
## <a name="example"></a>例  
 次の例は、`where` を使用して、`Orders` に出荷された `London` を運送料の順に並べ替えます。  
  
 [!code-csharp[DLinqQueryExamples#21](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#21)]
 [!code-vb[DLinqQueryExamples#21](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#21)]  
  
## <a name="example"></a>例  
 次の例は、`Products` を単価の高い順に並べ替えます。  
  
 [!code-csharp[DLinqQueryExamples#22](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#22)]
 [!code-vb[DLinqQueryExamples#22](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#22)]  
  
## <a name="example"></a>例  
 次の例は、`OrderBy` で複数のフィールドを使用して、`Customers` を最初に都市の順に、次に連絡先の順に並べ替えます。  
  
 [!code-csharp[DLinqQueryExamples#24](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#24)]
 [!code-vb[DLinqQueryExamples#24](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#24)]  
  
## <a name="example"></a>例  
 次の例では、`EmployeeID 1` からの注文が、最初に `ShipCountry` の順に、次に運送料の高い順に並べ替えられます。  
  
 [!code-csharp[DLinqQueryExamples#25](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#25)]
 [!code-vb[DLinqQueryExamples#25](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#25)]  
  
## <a name="example"></a>例  
 次の例は、<xref:System.Linq.Enumerable.OrderBy%2A> 演算子、<xref:System.Linq.Enumerable.Max%2A> 演算子、および <xref:System.Linq.Enumerable.GroupBy%2A> 演算子を組み合わせて、各カテゴリで単価の最も高い `Products` を特定し、そのグループをカテゴリ ID の順に並べ替えます。  
  
 [!code-csharp[DLinqQueryExamples#26](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#26)]
 [!code-vb[DLinqQueryExamples#26](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#26)]  
  
 Northwind サンプル データベースに対して前のクエリを実行すると、結果は次のようになります。  
  
 `1`  
  
 `Côte de Blaye`  
  
 `2`  
  
 `Vegie-spread`  
  
 `3`  
  
 `Sir Rodney's Marmalade`  
  
 `4`  
  
 `Raclette Courdavault`  
  
 `5`  
  
 `Gnocchi di nonna Alice`  
  
 `6`  
  
 `Thüringer Rostbratwurst`  
  
 `7`  
  
 `Manjimup Dried Apples`  
  
 `8`  
  
 `Carnarvon Tigers`  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
