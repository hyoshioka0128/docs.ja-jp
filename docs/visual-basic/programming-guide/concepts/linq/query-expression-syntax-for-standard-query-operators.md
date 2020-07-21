---
title: 標準クエリ演算子のクエリ式構文
ms.date: 07/20/2015
ms.assetid: eb978d86-d3b5-497b-95ce-a054bea8f510
ms.openlocfilehash: 69bb50007c04bf8d1ee1553a37aca542afbffab0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396286"
---
# <a name="query-expression-syntax-for-standard-query-operators-visual-basic"></a>標準クエリ演算子のクエリ式構文 (Visual Basic)
頻繁に使用される標準クエリ演算子の中には、Visual Basic 言語専用のキーワード構文が使用されているものがあります。こうした構文では、標準クエリ演算子を、"*クエリ式*" の一部として呼び出すことができます。 クエリ式は*メソッド ベース*の方法とは異なり、より読み取りやすいクエリの表現形式です。 クエリ式の句は、コンパイル時にクエリ メソッドへの呼び出しに変換されます。  
  
## <a name="query-expression-syntax-table"></a>クエリ式の構文表  
 次の表は、同等なクエリ式の句がある標準クエリ演算子の一覧です。  
  
|メソッド|Visual Basic のクエリ式の構文|  
|------------|------------------------------------------|  
|<xref:System.Linq.Enumerable.All%2A>|`Aggregate … In … Into All(…)`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Any%2A>|`Aggregate … In … Into Any()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Average%2A>|`Aggregate … In … Into Average()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Cast%2A>|`From … As …`<br /><br /> (詳細については「[from 句](../../../language-reference/queries/from-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Count%2A>|`Aggregate … In … Into Count()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Distinct%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|`Distinct`<br /><br /> (詳細については、「[Distinct 句](../../../language-reference/queries/distinct-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`Group … By … Into …`<br /><br /> (詳細については、「[Group By 句](../../../language-reference/queries/group-by-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`Group Join … In … On …`<br /><br /> (詳細については、「[Group Join 句](../../../language-reference/queries/group-join-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`From x In …, y In … Where x.a = b.a`<br /><br /> \- または -<br /><br /> `Join … [As …]In … On …`<br /><br /> (詳細については、「[Join 句](../../../language-reference/queries/join-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.LongCount%2A>|`Aggregate … In … Into LongCount()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Max%2A>|`Aggregate … In … Into Max()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Min%2A>|`Aggregate … In … Into Min()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By`<br /><br /> (詳細については、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By … Descending`<br /><br /> (詳細については、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Select%2A>|`Select`<br /><br /> (詳細については、「[Select 句](../../../language-reference/queries/select-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|複数の `From` 句<br /><br /> (詳細については「[from 句](../../../language-reference/queries/from-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Skip%2A>|`Skip`<br /><br /> (詳細については「[Skip 句](../../../language-reference/queries/skip-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|`Skip While`<br /><br /> (詳細については「[Skip While 句](../../../language-reference/queries/skip-while-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Sum%2A>|`Aggregate … In … Into Sum()`<br /><br /> (詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Take%2A>|`Take`<br /><br /> (詳細については、「[Take 句](../../../language-reference/queries/take-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.TakeWhile%2A>|`Take While`<br /><br /> (詳細については、「[Take While 句](../../../language-reference/queries/take-while-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, …`<br /><br /> (詳細については、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, … Descending`<br /><br /> (詳細については、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。)|  
|<xref:System.Linq.Enumerable.Where%2A>|`Where`<br /><br /> (詳細については、「[Where 句](../../../language-reference/queries/where-clause.md)」を参照してください。)|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [実行方法による標準クエリ演算子の分類 (Visual Basic)](classification-of-standard-query-operators-by-manner-of-execution.md)
