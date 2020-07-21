---
title: 一連の数値の中の最小値の検出
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 78203093-f242-4572-9b31-9495b10926aa
ms.openlocfilehash: d8aee43f13ec92f649b4df20505ac56c336fe07a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793836"
---
# <a name="find-the-minimum-value-in-a-numeric-sequence"></a>一連の数値の中の最小値の検出
一連の数値の中から最小値を返すには、<xref:System.Linq.Enumerable.Min%2A> 演算子を使用します。  
  
## <a name="example"></a>例  
 次の例では、製品の最低単価を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行した場合の出力は、`2.5000` です。  
  
 [!code-csharp[DLinqQueryExamples#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#9)]
 [!code-vb[DLinqQueryExamples#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#9)]  
  
## <a name="example"></a>例  
 次の例では、注文の最低配送料を見つけます。  
  
 Northwind サンプル データベースに対してこのクエリを実行した場合の出力は、`0.0200` です。  
  
 [!code-csharp[DLinqQueryExamples#10](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#10)]
 [!code-vb[DLinqQueryExamples#10](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#10)]  
  
## <a name="example"></a>例  
 次の例では、Min を使用して、各カテゴリ内で単価が最も安い `Products` を見つけます。 出力はカテゴリごとに行われます。  
  
 [!code-csharp[DLinqQueryExamples#11](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#11)]
 [!code-vb[DLinqQueryExamples#11](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#11)]  
  
 Northwind サンプル データベースに対してこのクエリを実行すると、結果は次のようになります。  
  
 `1`  
  
 `Guaraná Fantástica`  
  
 `2`  
  
 `Aniseed Syrup`  
  
 `3`  
  
 `Teatime Chocolate Biscuits`  
  
 `4`  
  
 `Geitost`  
  
 `5`  
  
 `Filo Mix`  
  
 `6`  
  
 `Tourtière`  
  
 `7`  
  
 `Longlife Tofu`  
  
 `8`  
  
 `Konbu`  
  
## <a name="see-also"></a>関連項目

- [集計クエリ](aggregate-queries.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
