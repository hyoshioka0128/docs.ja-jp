---
title: UNION (Entity SQL)
ms.date: 03/30/2017
ms.assetid: df98a4db-b00d-4c8b-bd74-0d285f27e1df
ms.openlocfilehash: a5a20beb0ab55dcbaf2dbbb75801b50ab9ef6722
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319219"
---
# <a name="union-entity-sql"></a>UNION (Entity SQL)
複数のクエリの結果を 1 つのコレクションに結合します。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression  
UNION [ ALL ]  
expression  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 コレクションと結合するコレクションを返す任意の有効なクエリ式。すべての式は、 `expression`と同じ型であるか、共通の基本データ型または派生型である必要があります。  
  
 UNION  
 複数のコレクションを結合し、1 つのコレクションとして返すことを指定します。  
  
 ALL  
 複数のコレクションを結合し、重複も含めて 1 つのコレクションとして返すことを指定します。 指定しない場合、重複は結果コレクションから削除されます。  
  
## <a name="return-value"></a>戻り値  
 `expression`と同じ型であるか、共通の基本データ型または派生型であるコレクション。  
  
## <a name="remarks"></a>Remarks  
 UNION は、 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の 1 つです。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] のすべての集合演算子は左から右に評価されます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の集合演算子の優先順位に関する情報については、「[EXCEPT](except-entity-sql.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、UNION ALL 演算子を使用して、2 つのクエリの結果を 1 つのコレクションに結合します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#UNION](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#union)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
