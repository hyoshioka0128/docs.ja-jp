---
title: '&amp;&amp; (AND) (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: e7d24213-471d-4807-b85e-570375df89b5
ms.openlocfilehash: eccad616de287a39c42e986cea84dc22feec7f70
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150514"
---
# <a name="ampamp-and-entity-sql"></a>&amp;&amp; (AND) (Entity SQL)
両方の式が `true` の場合は `true`を返します。それ以外の場合は `false` または `NULL`を返します。  
  
## <a name="syntax"></a>構文  
  
```csharp  
boolean_expression AND boolean_expression
```

or  

```csharp
boolean_expression && boolean_expression  
```  
  
## <a name="arguments"></a>引数  
 `boolean_expression`  
 ブール値を返す任意の有効な式。  
  
## <a name="remarks"></a>Remarks  
 二重のアンパサンド (&&) は、AND 演算子と同じ効果を持ちます。  
  
 使用可能な入力値と戻り値の型を次の表に示します。  
  
||`TRUE`|`FALSE`|`NULL`|  
|-|------------|-------------|------------|  
|`TRUE`|true|false|NULL|  
|`FALSE`|false|false|false|  
|`NULL`|NULL|false|NULL|  
  
## <a name="example"></a>例  
 次の Entity SQL クエリは、AND 演算子の使い方を示しています。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-csharp[DP EntityServices Concepts 2#AND](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#and)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
