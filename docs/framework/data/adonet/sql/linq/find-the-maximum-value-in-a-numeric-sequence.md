---
title: 一連の数値の中の最大値の検出
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 70d7c058-0280-4815-a008-6f290093591a
ms.openlocfilehash: ebef8cb373da4021fd68fd7ce38de8cb06eb81ec
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782172"
---
# <a name="find-the-maximum-value-in-a-numeric-sequence"></a>一連の数値の中の最大値の検出
一連の数値の中の最大値を見つけるには、<xref:System.Linq.Enumerable.Max%2A> 演算子を使用します。  
  
## <a name="example"></a>例  
 次の例では、従業員の最新の入社日を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行した場合の出力は、`11/15/1994 12:00:00 AM` です。  
  
 [!code-csharp[DLinqQueryExamples#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#6)]
 [!code-vb[DLinqQueryExamples#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#6)]  
  
## <a name="example"></a>例  
 次の例では、製品の最大在庫数を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行した場合の出力は、`125` です。  
  
 [!code-csharp[DLinqQueryExamples#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#7)]
 [!code-vb[DLinqQueryExamples#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#7)]  
  
## <a name="example"></a>例  
 次の例では、Max を使用して、各カテゴリ内で単価が最も高い `Products` を見つけます。 出力では、カテゴリごとに結果の一覧が示されます。  
  
 [!code-csharp[DLinqQueryExamples#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#8)]
 [!code-vb[DLinqQueryExamples#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#8)]  
  
 Northwind サンプル データベースに対してこのクエリを実行すると、結果は次のようになります。  
  
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

- [集計クエリ](aggregate-queries.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
