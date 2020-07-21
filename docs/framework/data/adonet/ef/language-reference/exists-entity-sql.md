---
title: EXISTS (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d28ead43-4afb-4bdc-af64-efd2e05005d7
ms.openlocfilehash: 44f128a292b013fd3a3a80efdd2d10a63e3cfb07
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833836"
---
# <a name="exists-entity-sql"></a>EXISTS (Entity SQL)
コレクションが空かどうかを調べます。  
  
## <a name="syntax"></a>構文  
  
```sql  
[NOT] EXISTS ( expression )  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 コレクションを返す任意の有効な式。  
  
 NOT  
 EXISTS の結果を否定することを指定します。  
  
## <a name="return-value"></a>戻り値  
 コレクションが空でない場合は `true`、それ以外の場合は `false` です。  
  
## <a name="remarks"></a>Remarks  
 EXISTS は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の 1 つです。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] のすべての集合演算子は左から右に評価されます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の優先順位に関する情報については、「[EXCEPT](except-entity-sql.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、EXISTS 演算子を使用して、コレクションが空かどうかを調べます。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#EXISTS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#exists)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
