---
title: 集計関数 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: acfd3149-f519-4c6e-8fe1-b21d243a0e58
ms.openlocfilehash: c79071e73763b56c0dde906499f3eef1d296ce0c
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251345"
---
# <a name="aggregate-functions-entity-sql"></a>集計関数 (Entity SQL)
集計は、コレクションをグループ操作の一部としてスカラーに圧縮する言語構成要素です。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 集計には次の 2 つの形式があります。  
  
- 式内のあらゆる位置で使用できる [!INCLUDE[esql](../../../../../../includes/esql-md.md)] コレクション関数。 これには、コレクションに対して作用するプロジェクションおよび述語での集計関数の使用が含まれます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] で集計を指定するには、コレクション関数を使用することをお勧めします。  
  
- GROUP BY 句を含むクエリ式内のグループ集計。 Transact-SQL と同様に、グループ集計では集計の入力に対する修飾子として DISTINCT と ALL を受け入れます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、まず式をコレクション関数として解釈しようとしますが、SELECT 式のコンテキストにある式はグループ集計として解釈されます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、[GROUPPARTITION](grouppartition-entity-sql.md) という特殊な集計演算子が定義されます。 この演算子を使用すると、グループ化された入力セットへの参照を取得できます。 これにより、GROUP BY 句の結果をグループ集計関数やコレクション関数以外の場所で使用できる高度なグループ化クエリが可能になります。  
  
## <a name="collection-functions"></a>コレクション関数  
 コレクション関数はコレクションに対して実行され、スカラー値を返します。 たとえば、`orders` がすべての `orders` のコレクションである場合、次の式を使用して、最も早い出荷日を計算できます。  
  
 `min(select value o.ShipDate from LOB.Orders as o)`  
  
## <a name="group-aggregates"></a>グループ集計  
 グループ集計では、GROUP BY 句によって定義されたグループ結果ごとに計算が実行されます。 GROUP BY 句により、データがグループに分けられます。 分けられた各グループに集計関数が適用され、それぞれのグループ内の要素を集計計算の入力として使用して、各集計が計算されます。 SELECT 式で GROUP BY 句を使用した場合、プロジェクション、HAVING、または ORDER BY 句で使用できるのは、グループ化式の名前、集計式、または定数式だけです。  
  
 次の例では、製品ごとの平均発注数量を計算しています。  
  
 `select p, avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `group by ol.Product as p`  
  
 SELECT 式に明示的な GROUP BY 句を指定せずに、グループ集計を行うこともできます。 すべての要素が 1 つのグループとして処理されます。これは定数に基づくグループ化を指定する場合と同じです。  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol group by 1`  
  
 GROUP BY 句で使用される式は、WHERE 句式から参照できる同じ名前解決スコープを使用して評価されます。  
  
## <a name="see-also"></a>関連項目

- [関数](functions-entity-sql.md)
