---
title: クエリ式の例 (LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: f743fbc7-faff-45e5-af1e-61577d87f0cc
ms.openlocfilehash: 4dd078c99d545397a032586d6814e0232a7641cc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783025"
---
# <a name="query-expression-examples-linq-to-dataset"></a>クエリ式の例 (LINQ to DataSet)
このセクションでは、標準クエリ演算子を使用する LINQ to DataSet プログラミングの例を、クエリ式の構文を中心に説明します。 これらの例で使用されている <xref:System.Data.DataSet> は、`FillDataSet` メソッド (「[DataSet へのデータの読み込み](loading-data-into-a-dataset.md)」を参照) を使用して設定します。 詳しくは、「[標準クエリ演算子の概要 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)」または「[標準クエリ演算子の概要 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [射影](query-expression-syntax-examples-projection-linq-to-dataset.md)  
 このトピックでは、<xref:System.Linq.Enumerable.Select%2A> メソッドおよび <xref:System.Linq.Enumerable.SelectMany%2A> メソッドを使って <xref:System.Data.DataSet> を照会する例を取り上げます。  
  
 [制限](query-expression-syntax-examples-restriction-linq-to-dataset.md)  
 このトピックでは、<xref:System.Linq.Enumerable.Where%2A> メソッドを使って <xref:System.Data.DataSet> を照会する例を取り上げます。  
  
 [パーティション分割](query-expression-syntax-examples-partitioning.md)  
 このトピックでは、<xref:System.Linq.Enumerable.Skip%2A> メソッドおよび <xref:System.Linq.Enumerable.Take%2A> メソッドを使って <xref:System.Data.DataSet> を照会し、結果をパーティション分割する例を取り上げます。  
  
 [順序付け](query-expression-syntax-examples-ordering-linq-to-dataset.md)  
 このトピックでは、<xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.OrderByDescending%2A>、<xref:System.Linq.Enumerable.Reverse%2A>、<xref:System.Linq.Enumerable.ThenByDescending%2A> の各メソッドを使って <xref:System.Data.DataSet> を照会し、結果を並べ替える例を取り上げます。  
  
 [要素演算子](query-expression-syntax-examples-element-operators.md)  
 このトピックでは、<xref:System.Linq.Enumerable.First%2A> メソッドおよび <xref:System.Linq.Enumerable.ElementAt%2A> メソッドを使用して <xref:System.Data.DataRow> から <xref:System.Data.DataSet> 要素を取得する例を取り上げます。  
  
 [集計演算子](query-expression-syntax-examples-aggregate-operators.md)  
 このトピックでは、<xref:System.Linq.Enumerable.Average%2A>、<xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Min%2A>、<xref:System.Linq.Enumerable.Sum%2A> の各メソッドを使って <xref:System.Data.DataSet> を照会し、データを集計する例を取り上げます。  
  
 [結合演算子](query-expression-syntax-examples-join-operators.md)  
 このトピックでは、<xref:System.Linq.Enumerable.GroupJoin%2A> メソッドおよび <xref:System.Linq.Enumerable.Join%2A> メソッドを使って <xref:System.Data.DataSet> を照会する例を取り上げます。  
  
## <a name="see-also"></a>関連項目

- [メソッド ベースのクエリ例](method-based-query-examples-linq-to-dataset.md)
- [DataSet 固有の演算子の例](dataset-specific-operator-examples-linq-to-dataset.md)
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
