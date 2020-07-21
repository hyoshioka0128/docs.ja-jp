---
title: クエリ式 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c36f327b-e230-48d4-bbd5-78dc6478c447
ms.openlocfilehash: 4428286890f41573a02daf31a4593d0c8f9ad34b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249272"
---
# <a name="query-expressions-entity-sql"></a>クエリ式 (Entity SQL)
クエリ式とは、さまざまなクエリ演算子を組み合わせて 1 つの構文にしたものです。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] には、[リテラル](literals-entity-sql.md)、[パラメーター](parameters-entity-sql.md)、[変数](variables-entity-sql.md)、演算子、[関数](functions-entity-sql.md)、集合演算子などのさまざまな種類の式が用意されています。 詳細については、「[Entity SQL リファレンス](entity-sql-reference.md)」をご覧ください。  
  
## <a name="clauses"></a>句  
 クエリ式は、オブジェクトのコレクションに連続した操作を適用する一連の句で構成されます。 これらは、標準の SQL select ステートメントと同じ句に基づいています:[SELECT](select-entity-sql.md)、[FROM](from-entity-sql.md)、[WHERE](where-entity-sql.md)、[GROUP BY](group-by-entity-sql.md)、[HAVING](having-entity-sql.md)、および [ORDER BY](order-by-entity-sql.md)。  
  
## <a name="scope"></a>スコープ  
 FROM 句で定義された名前は、出現順 (左から右の順) に FROM スコープに導入されます。 JOIN リストでは、式は既にリストで定義されている名前を参照できます。 FROM 句で指定された要素のパブリック プロパティは FROM スコープに追加されません。それらは常に、別名で修飾された名前を使用して参照する必要があります。 通常は、SELECT 式のすべての部分が FROM スコープに含まれると見なされます。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
