---
title: 量指定子操作
ms.date: 07/20/2015
ms.assetid: ae1a2b73-503c-4f4b-a3fd-31b5adbee67c
ms.openlocfilehash: 9a2e35e0511915cb17b99550a8bf382bd9d46526
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396312"
---
# <a name="quantifier-operations-visual-basic"></a>量指定子操作 (Visual Basic)
量指定子操作は、シーケンス内の要素の一部またはすべてが条件を満たしているかどうかを示す <xref:System.Boolean> 値を返します。  
  
 次の図は、2 つの異なるソース シーケンスに対する、2 つの異なる量指定子操作を示しています。 最初の操作では、1 つ以上の要素が文字 'A' であるかどうかを尋ねていて、その結果は `true` です。 2 番目の操作では、すべての要素が文字 'A' であるかどうかを尋ねていて、その結果は `true` です。  
  
 ![LINQ 量指定子操作](./media/quantifier-operations/linq-quantifier-operations.png)  
  
 次のセクションでは、量指定子操作を実行する標準クエリ演算子のメソッドの一覧を示します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド名|説明|Visual Basic のクエリ式の構文|説明|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|すべて|シーケンス内のすべての要素が条件を満たしているかどうかを調べます。|`Aggregate … In … Into All(…)`|<xref:System.Linq.Enumerable.All%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=nameWithType>|  
|どれでも可|シーケンス内のいずれかの要素が条件を満たしているかどうかを調べます。|`Aggregate … In … Into Any()`|<xref:System.Linq.Enumerable.Any%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=nameWithType>|  
|内容|指定した要素がシーケンスに格納されているかどうかを調べます。|該当なし。|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>クエリ式の構文例  
 これらの例では、LINQ クエリのフィルタリング条件の一部に Visual Basic の `Aggregate` 句を使用しています。  
  
 次の例では、`Aggregate` 句と <xref:System.Linq.Enumerable.All%2A> 拡張メソッドを使用して、飼っているすべてのペットが特定の年齢を超えている人をコレクションから取得します。  
  
 [!code-vb[CsLINQAnyAll#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAnyAll/VB/AnyAll.vb#1)]  
  
 次の例では、`Aggregate` 句と <xref:System.Linq.Enumerable.Any%2A> 拡張メソッドを使用して、飼っているペットの少なくとも 1 匹が特定の年齢を超えている人をコレクションから取得します。  
  
 [!code-vb[CsLINQAnyAll#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAnyAll/VB/AnyAll.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [Aggregate 句](../../../language-reference/queries/aggregate-clause.md)
- [方法: 指定された単語のセットを含む文章を照会する (LINQ) (Visual Basic)](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)
