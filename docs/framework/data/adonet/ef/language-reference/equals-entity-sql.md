---
title: = (等しい) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 948eb588-7080-4046-bb48-633b007393bf
ms.openlocfilehash: 101dccd40e9197c7cf0795ccb80ded367676842d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150313"
---
# <a name="-equals-entity-sql"></a>= (等しい) (Entity SQL)
2 つの式の等価性を比較します。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression = expression  
-- or
expression == expression  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 任意の有効な式。 両方の式とも、暗黙的に変換可能なデータ型でなければなりません。  
  
## <a name="result-types"></a>戻り値の型  
 左の式が右の式と等しい場合は`true` 、等しくない場合は `false`。  
  
## <a name="remarks"></a>Remarks  
 == 演算子は = 演算子と同じです。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、= 比較演算子を使用して 2 つの式の等価性を比較します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#EQUALS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#equals)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
