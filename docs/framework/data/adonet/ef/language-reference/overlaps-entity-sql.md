---
title: OVERLAPS (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41743e89-79cb-4d7b-8a27-355b45024b61
ms.openlocfilehash: bdee9281fd406a3d029d3a10536cbdd48d2f7a58
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319414"
---
# <a name="overlaps-entity-sql"></a>OVERLAPS (Entity SQL)
2 つのコレクションに共通の要素が存在するかどうかを調べます。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression OVERLAPS expression  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 コレクションを返す任意の有効なクエリ式。もう一方のクエリ式から返されたコレクションと比較されます。 すべての式は、 `expression`と同じ型であるか、共通の基本型または派生型である必要があります。  
  
## <a name="return-value"></a>戻り値  
 2 つのコレクションに共通の要素がある場合は`true` 、それ以外の場合は `false`。  
  
## <a name="remarks"></a>Remarks  
 OVERLAPS では、次のコードと同等の機能が提供されます。  
  
 `EXISTS ( expression INTERSECT expression )`  
  
 OVERLAPS は、 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の 1 つです。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] のすべての集合演算子は左から右に評価されます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の優先順位に関する情報については、「[EXCEPT](except-entity-sql.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、OVERLAPS 演算子を使用して、2 つのコレクションに共通の値が存在するかどうかを調べます。 このクエリは、AdventureWorks Sales Model に基づいています。 これをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#OVERLAPS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#overlaps)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
