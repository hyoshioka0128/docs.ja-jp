---
title: SELECT (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 9a33bd0d-ded1-41e7-ba3c-305502755e3b
ms.openlocfilehash: de6c497e7d781d705c68092e4a13ee07b727b2b7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149910"
---
# <a name="select-entity-sql"></a>SELECT (Entity SQL)
クエリで返される要素を指定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
SELECT [ ALL | DISTINCT ] [ topSubclause ] aliasedExpr
      [{ , aliasedExpr }] FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause ]  
-- or  
SELECT VALUE [ ALL | DISTINCT ] [ topSubclause ] expr FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause  
```  
  
## <a name="arguments"></a>引数  
 ALL  
 結果セットに重複を含むことを指定します。 ALL は既定値です。  
  
 DISTINCT  
 結果セットに一意な結果のみを含むことを指定します。  
  
 VALUE  
 1 つの項目のみを指定でき、row ラッパーを追加しません。  
  
 `topSubclause`  
 `top(expr)`の形式で、クエリから返す最初の結果数を指定する有効な式。  
  
 [ORDER BY](order-by-entity-sql.md) 演算子の LIMIT パラメーターにより、結果セットの最初の n 項目を選ぶこともできます。  
  
 `aliasedExpr`  
 次の形式の式。  
  
 `expr` as `identifier` &#124; `expr`  
  
 `expr`  
 リテラルまたは式。  
  
## <a name="remarks"></a>Remarks  
 [FROM](from-entity-sql.md)、[GROUP BY](group-by-entity-sql.md)、[HAVING](having-entity-sql.md) 句が評価された後で、SELECT 句が評価されます。 SELECT 句は、FROM 句または外側のスコープから現在スコープ内にある項目のみを参照できます。 GROUP BY 句を指定した場合、SELECT 句は GROUP BY キーの別名のみを参照できます。 FROM 句の項目への参照は、集計関数でのみ実行できます。  
  
 SELECT キーワードの後に続く 1 つまたは複数のクエリ式の一覧は、選択リスト (旧称、投影) と呼びます。 投影のより一般的な形式は、単一クエリ式です。 次の例に示すように、コレクション `member1` からメンバー `collection1`を選択すると、 `member1` の各オブジェクトに対応するすべての `collection1`値の新しいコレクションが生成されます。  
  
```sql  
SELECT collection1.member1 FROM collection1  
```  
  
 たとえば、 `customers` が、タイプ `Customer` のコレクションで、このコレクションに、タイプ `Name` であるプロパティ `string`が含まれる場合、 `Name` から `customers` を選択すると、文字列のコレクションが返されます。  
  
```sql  
SELECT customers.Name FROM customers AS c  
```  
  
 JOIN 構文 (FULL、INNER、LEFT、OUTER、ON、および RIGHT) を使用することもできます。 内部結合に対しては ON が必要ですが、クロス結合に対しては ON を使用できません。  
  
## <a name="row-and-value-select-clauses"></a>ROW 句および VALUE SELECT 句  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、SELECT 句の 2 つのバリアントをサポートします。 最初のバリアント、row select は、SELECT キーワードによって識別され、このバリアントを使用して、投影する必要がある 1 つまたは複数の値を指定できます。row ラッパーは、返された値の前後に暗黙的に追加されるため、クエリ式の結果は常に、行のマルチセットになります。  
  
 row select の各クエリ式は、別名を指定する必要があります。 別名を指定しないと、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] は別名生成規則を使用して別名の生成を試みます。  
  
 SELECT 句のもう 1 つのバリアント、value select は SELECT VALUE キーワードによって識別されます。 このバリアントは、1 つの値のみを指定でき、row ラッパーを追加しません。  
  
 次の例に示すように、row select は常に VALUE SELECT として表現できます。  
  
```sql  
SELECT 1 AS a, "abc" AS b FROM C  
SELECT VALUE ROW(1 AS a, "abc" AS b) FROM C
```  
  
## <a name="all-and-distinct-modifiers"></a>ALL 修飾子および DISTINCT 修飾子  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の SELECT のどちらのバリアントも ALL 修飾子または DISTINCT 修飾子を指定できます。 DISTINCT 修飾子を指定した場合、SELECT 句まで (SELECT 句を含めて) のクエリ式によって生成されたコレクションから重複が除外されます。 ALL 修飾子が指定された場合、重複は除外されません。ALL 修飾子は既定値です。  
  
## <a name="differences-from-transact-sql"></a>Transact-SQL との違い  
 Transact-SQL とは異なり、 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では SELECT 句で * 引数を使用できません。  代わりに、 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、次の例に示すように、FROM 句からコレクションの別名を参照して、レコード全体にクエリを投影できます。  
  
```sql  
SELECT * FROM T1, T2  
```  
  
 上の Transact-SQL クエリ式は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では次のように表されます。  
  
```sql  
SELECT a1, a2 FROM T1 AS a1, T2 AS a2  
```  
  
## <a name="example"></a>例  
 次の Entity SQL クエリは、SELECT 演算子を使用して、クエリによって返される要素を指定します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#LESS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#less)]  
  
## <a name="see-also"></a>関連項目

- [クエリ式](query-expressions-entity-sql.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
- [TOP](top-entity-sql.md)
