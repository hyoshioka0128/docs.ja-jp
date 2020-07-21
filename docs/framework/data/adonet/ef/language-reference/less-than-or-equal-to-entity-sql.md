---
title: <= (以下) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 7c46da5c-fa09-4d90-adcc-c7e1b769d8e6
ms.openlocfilehash: b3c8fef47b06b9fdd0a1619a9e56d3d916d9dd2d
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319634"
---
# <a name="-less-than-or-equal-to-entity-sql"></a>\<= (以下) (Entity SQL)
2 つの式を比較して、左の式の値が右の式の値以下であるかどうかを判別します。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression <= expression  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 任意の有効な式。 両方の式とも、暗黙的に変換可能なデータ型でなければなりません。  
  
## <a name="result-types"></a>戻り値の型  
 左の式の値が右の式の値以下である場合は`true` 、そうでない場合は `false`。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリは「<=」比較演算子を使用して 2 つの式を比較し、左の式の値が右の式の値以下であるかどうかを判別します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#LESS_OR_EQUALS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#less_or_equals)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
