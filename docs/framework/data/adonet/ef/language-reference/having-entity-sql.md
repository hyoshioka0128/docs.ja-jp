---
title: HAVING (Entity SQL)
ms.date: 03/30/2017
ms.assetid: b5d52d97-8372-4335-beac-2d0b79dc3707
ms.openlocfilehash: 97ed6e06241804bf2f576c910a2235b0cb570bbb
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833730"
---
# <a name="having-entity-sql"></a>HAVING (Entity SQL)
グループまたは集計の検索条件を指定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
[ HAVING search_condition ]  
```  
  
## <a name="arguments"></a>引数  
 `search_condition`  
 グループまたは集計の検索条件を指定します。 HAVING 句を GROUP BY ALL と共に使用した場合、HAVING 句により ALL はオーバーライドされます。  
  
## <a name="remarks"></a>Remarks  
 HAVING 句は、グループ化の結果について追加的なフィルター処理条件を指定する場合に使用します。 クエリ式で GROUP BY 句が指定されていないと、暗黙的な単独セットのグループになります。  
  
> [!NOTE]
> HAVING は、[SELECT](select-entity-sql.md) ステートメントでのみ使用できます。 [GROUP BY](group-by-entity-sql.md) が使われていない場合、HAVING は WHERE 句のように動作します。  
  
GROUP BY 操作後に適用される場合を除いて、HAVING 句は WHERE 句と同様に動作します。 つまり、次の例のように、HAVING 句では別名および集計のグループ化のみを参照できます。
  
```sql  
SELECT Name, SUM(o.Price * o.Quantity) AS Total FROM orderLines AS o GROUP BY o.Product AS Name  
HAVING SUM(o.Quantity) > 1  
```  
  
 前述のグループは、複数の製品を含むグループのみに制限されています。  
  
## <a name="example"></a>例  
 次の Entity SQL のクエリでは、HAVING および GROUP BY 操作を使用して、グループまたは集計の検索条件を指定します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: PrimitiveType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-primitivetype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecutePrimitiveTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#HAVING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#having)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [クエリ式](query-expressions-entity-sql.md)
