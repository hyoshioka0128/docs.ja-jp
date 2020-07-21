---
title: 複数テーブルにまたがるクエリ (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6819a16f-8656-41af-a54d-dfec0cb66366
ms.openlocfilehash: 8f9a538482580134fa876866dfe394c3dfc7de2a
ms.sourcegitcommit: 7bc6887ab658550baa78f1520ea735838249345e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75634886"
---
# <a name="cross-table-queries-linq-to-dataset"></a>複数テーブルにまたがるクエリ (LINQ to DataSet)
LINQ to DataSet では、1 つのテーブルを対象とするクエリに加え、複数テーブルにまたがるクエリを実行できます。 これは、"*結合*" を使用することで実現されます。 結合とは、あるデータ ソース内のオブジェクトを、他方のデータ ソース内で共通の属性 (たとえば製品や連絡先 ID) を持つオブジェクトと関連付けることです。 オブジェクト指向プログラミングでは、それぞれのオブジェクトは別のオブジェクトを参照するメンバーを持つため、オブジェクト間のリレーションシップのナビゲーションは比較的簡単です。 ただし、外部データベース テーブル内でのリレーションシップのナビゲーションは単純ではありません。 データベース テーブルは、組み込みのリレーションシップを持ちません。 このようなケースでは、結合操作を使用して、互いのソースの要素を対応付けることができます。 たとえば、製品情報と売上情報が 2 つのテーブルに格納されている場合、結合操作を使用して、同じ販売注文の売上情報と製品を対応付けることができます。  
  
 LINQ (統合言語クエリ) フレームワークには、<xref:System.Linq.Enumerable.Join%2A> と <xref:System.Linq.Enumerable.GroupJoin%2A> の 2 つの結合演算子が用意されています。 これらの演算子では、キーが等しいときにだけ 2 つのデータ ソースを一致させる結合方法である "*等結合*" が実行されます。 (これに対し、Transact-SQL では、`equals` 以外に `less than` 演算子などの結合演算子がサポートされています)。  
  
 リレーショナル データベース用語では、<xref:System.Linq.Enumerable.Join%2A> は内部結合を実行します。 内部結合とは、対応するデータセット内で一致するオブジェクトがあるオブジェクトのみが返される結合です。  
  
 リレーショナル データベースの用語で <xref:System.Linq.Enumerable.GroupJoin%2A> 演算子に直接相当するものはありません。これらの演算子では、内部結合と左外部結合のスーパーセットが実装されています。 左外部結合とは、最初 (左側) のコレクションの各要素が返される結合であり、第 2 のコレクションに相関する要素がない場合でも返されます。  
  
 結合について詳しくは、「[結合演算](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397908(v=vs.120))」をご覧ください。  
  
## <a name="example"></a>例  
 次の例では、AdventureWorks サンプル データベースの `SalesOrderHeader` テーブルと `SalesOrderDetail` テーブルを従来の方法で結合し、8 月以降のオンラインでの注文を取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#join)]
 [!code-vb[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#join)]  
  
## <a name="see-also"></a>関連項目

- [DataSet のクエリ](querying-datasets-linq-to-dataset.md)
- [単一テーブルのクエリ](single-table-queries-linq-to-dataset.md)
- [型指定された DataSet のクエリ](querying-typed-datasets.md)
- [結合演算](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397908(v=vs.120))
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
