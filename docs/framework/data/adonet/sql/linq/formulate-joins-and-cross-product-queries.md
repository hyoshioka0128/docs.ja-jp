---
title: 結合およびクロス積クエリの作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d8072ede-0521-4670-9bec-1778ceeb875b
ms.openlocfilehash: 002a644ff5d48b25351228dcd74330707491d6c8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782096"
---
# <a name="formulate-joins-and-cross-product-queries"></a>結合およびクロス積クエリの作成
次の例は、複数のテーブルからの結果を組み合わせる方法を示しています。  
  
## <a name="example"></a>例  
 次の例では、Visual Basic の `From` 句 (C# の `from` 句) で外部キー ナビゲーションを使用して、London の顧客の注文をすべて選択します。  
  
 [!code-csharp[DLinqQueryExamples#47](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#47)]
 [!code-vb[DLinqQueryExamples#47](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#47)]  
  
## <a name="example"></a>例  
 次の例では、Visual Basic の `Where` 句 (C# の `where` 句) で外部キー ナビゲーションを使用して、`Supplier` が米国にあり、在庫切れになっている `Products` をフィルター処理します。  
  
 [!code-csharp[DLinqQueryExamples#48](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#48)]
 [!code-vb[DLinqQueryExamples#48](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#48)]  
  
## <a name="example"></a>例  
 次の例では、Visual Basic の `From` 句 (C# の `from` 句) で外部キー ナビゲーションを使用して、シアトルの従業員をフィルター処理し、その担当区域を表示します。  
  
 [!code-csharp[DLinqQueryExamples#49](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#49)]  
  
## <a name="example"></a>例  
 次の例では、Visual Basic の `Select` 句 (C# の `select` 句) で外部キー ナビゲーションを使用して、上司と部下の関係にあり、同じ `City` 出身の 2 人の従業員の組み合わせをフィルター処理します。  
  
 [!code-csharp[DLinqQueryExamples#50](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#50)]
 [!code-vb[DLinqQueryExamples#50](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50)]  
  
## <a name="example"></a>例  
 次の Visual Basic の例では、すべての顧客と注文を調べ、注文と顧客が一致すること、およびリスト内のすべての顧客に連絡先名が指定されていることを確認します。  
  
 [!code-vb[DLinqQueryExamples#50v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50v)]  
  
## <a name="example"></a>例  
 次の例は、2 つのテーブルを明示的に結合し、両方のテーブルからの結果を投影します。  
  
 [!code-csharp[DLinqQueryExamples#51](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#51)]
 [!code-vb[DLinqQueryExamples#51](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#51)]  
  
## <a name="example"></a>例  
 次の例は、3 つのテーブルを明示的に結合し、各テーブルからの結果を投影します。  
  
 [!code-csharp[DLinqQueryExamples#52](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#52)]
 [!code-vb[DLinqQueryExamples#52](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#52)]  
  
## <a name="example"></a>例  
 次の例は、`LEFT OUTER JOIN` を使用して、`DefaultIfEmpty()` を実現する方法を示しています。 `DefaultIfEmpty()` に `Order` がない場合は、`Employee` メソッドから null が返されます。  
  
 [!code-csharp[DLinqQueryExamples#53](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#53)]
 [!code-vb[DLinqQueryExamples#53](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#53)]  
  
## <a name="example"></a>例  
 次の例は、結合の結果の `let` 式を投影します。  
  
 [!code-csharp[DLinqQueryExamples#54](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#54)]
 [!code-vb[DLinqQueryExamples#54](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#54)]  
  
## <a name="example"></a>例  
 次の例は、複合キーを使用する `join` を示しています。  
  
 [!code-csharp[DLinqQueryExamples#55](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#55)]
 [!code-vb[DLinqQueryExamples#55](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#55)]  
  
## <a name="example"></a>例  
 次の例は、一方が null 許容で他方がそうでない `join` の作成方法を示しています。  
  
 [!code-csharp[DLinqQueryExamples#56](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#56)]
 [!code-vb[DLinqQueryExamples#56](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#56)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
