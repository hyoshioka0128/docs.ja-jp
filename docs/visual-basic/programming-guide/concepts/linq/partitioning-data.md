---
title: データのパーティション分割
ms.date: 07/20/2015
ms.assetid: 69c59379-b66e-422c-b324-5b5c07760ef7
ms.openlocfilehash: 34749f9d7b137bade66b6103650871246c3cc532
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406847"
---
# <a name="partitioning-data-visual-basic"></a>データのパーティション分割 (Visual Basic)
LINQ におけるパーティション分割とは、要素を並べ替えずに入力シーケンスを 2 つのセクションに分割し、それらのセクションの 1 つを返す操作を指します。  
  
 次の図は、文字のシーケンスに対して 3 つの異なるパーティション分割操作を実行した結果を示しています。 最初の操作では、シーケンスの最初の 3 つの要素が返されます。 2 番目の操作では、最初の 3 つの要素がスキップされ、残りの要素が返されます。 3 番目の操作では、シーケンスの最初の 2 つの要素がスキップされ、次の 3 つの要素が返されます。  
  
 ![LINQ のパーティション操作を示す図。](./media/partitioning-data/linq-partitioning-operations.png)  
  
 次のセクションに、シーケンスのパーティション分割を実行する標準クエリ演算子メソッドの一覧を示します。  
  
## <a name="operators"></a>演算子  
  
|演算子名|説明|Visual Basic のクエリ式の構文|説明|  
|-------------------|-----------------|------------------------------------------|----------------------|  
|Skip|シーケンス内の指定した位置まで要素をスキップします。|`Skip`|<xref:System.Linq.Enumerable.Skip%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Skip%2A?displayProperty=nameWithType>|  
|SkipWhile|述語関数に基づき、条件を満たさない要素が出現する位置まで要素をスキップします。|`Skip While`|<xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=nameWithType>|  
|Take|シーケンス内の指定した位置までの要素を取得します。|`Take`|<xref:System.Linq.Enumerable.Take%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Take%2A?displayProperty=nameWithType>|  
|TakeWhile|述語関数に基づき、条件を満たさない要素が出現する位置までの要素を取得します。|`Take While`|<xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>クエリ式の構文例  
  
### <a name="skip"></a>Skip  
 次のコード例は、Visual Basic の `Skip` 句を使用し、文字列配列に格納されている最初の 4 つの文字列をスキップして残りの文字列を返します。  
  
 [!code-vb[CsLINQPartitioning#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#1)]  
  
### <a name="skipwhile"></a>SkipWhile  
 次のコード例は、Visual Basic の `Skip While` 句を使用し、配列内の文字列のうち、先頭文字が "a" である文字列をスキップします。 配列に格納されている残りの文字列が返されます。  
  
 [!code-vb[CsLINQPartitioning#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#2)]  
  
### <a name="take"></a>Take  
 次のコード例は、Visual Basic の `Take` 句を使用して、文字列配列内の最初の 2 つの文字列を返します。  
  
 [!code-vb[CsLINQPartitioning#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#3)]  
  
### <a name="takewhile"></a>TakeWhile  
 次のコード例は、Visual Basic の `Take While` 句を使用し、配列から長さが 5 以下である文字列を返します。  
  
 [!code-vb[CsLINQPartitioning#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#4)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [Skip 句](../../../language-reference/queries/skip-clause.md)
- [Skip While 句](../../../language-reference/queries/skip-while-clause.md)
- [Take 句](../../../language-reference/queries/take-clause.md)
- [Take While 句](../../../language-reference/queries/take-while-clause.md)
