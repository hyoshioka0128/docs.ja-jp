---
title: シーケンスの最初の要素の取得
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ccdc3777-b2c2-44e3-a627-abef8d79a555
ms.openlocfilehash: 9faeed754942d7b176872484ac776c1df592bbd8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792712"
---
# <a name="return-the-first-element-in-a-sequence"></a>シーケンスの最初の要素の取得
<xref:System.Linq.Enumerable.First%2A> 演算子を使用すると、シーケンスの内最初の要素を返すことができます。 <xref:System.Linq.Enumerable.First%2A> を使用するクエリは直ちに実行されます。  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は <xref:System.Linq.Enumerable.Last%2A> 演算子をサポートしません。  
  
## <a name="example"></a>例  
 次のコードは、テーブル内の最初の `Shipper` を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行すると、結果は次のようになります。  
  
 `ID = 1, Company = Speedy Express`。  
  
 [!code-csharp[DLinqQueryExamples#14](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#14)]
 [!code-vb[DLinqQueryExamples#14](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#14)]  
  
## <a name="example"></a>例  
 次のコードは、`Customer` が BONAP の単一の `CustomerID` を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行すると、結果は `ID = BONAP, Contact = Laurence Lebihan` になります。  
  
 [!code-csharp[DLinqQueryExamples#15](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#15)]
 [!code-vb[DLinqQueryExamples#15](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#15)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
