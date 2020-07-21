---
title: + (文字列連結) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 580130fa-6c7c-4f76-a47d-d22c27ccadf6
ms.openlocfilehash: 9c078e193eeecd4d331c5e3c04c66dee2c4a1daa
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319308"
---
# <a name="-string-concatenation-entity-sql"></a>+ (文字列連結) (Entity SQL)
2 つの文字列を連結します。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression + expression  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 EDM.String データ型の任意の有効な式。 両方の式は、同じデータ型でなければなりません。または、一方の式をもう一方の式のデータ型に暗黙的に変換できる必要があります。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数の暗黙の型の昇格の結果であるデータ型。 暗黙の型の昇格について詳しくは、「[型システム](type-system-entity-sql.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、+ 演算子を使用して、2 つの文字列を連結します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: PrimitiveType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-primitivetype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecutePrimitiveTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#CONCAT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#concat)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [概念モデルの型 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)
