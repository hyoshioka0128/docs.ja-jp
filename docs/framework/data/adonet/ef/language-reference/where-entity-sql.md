---
title: WHERE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: a8e1061e-0028-4a6f-8f19-b9f48e96c4b8
ms.openlocfilehash: b551d15d7de2cf07afc7455b7fd0a0faf6436ccf
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319183"
---
# <a name="where-entity-sql"></a>WHERE (Entity SQL)
WHERE 句は、[FROM](from-entity-sql.md) 句の直後に適用されます。  
  
## <a name="syntax"></a>構文  
  
```sql  
[ WHERE expression ]  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 ブール型です。  
  
## <a name="remarks"></a>Remarks  
 WHERE 句のセマンティクスは、Transact-SQL で記述する場合と同じです。 ソース コレクションの要素を条件を満たすものに制限することで、クエリ式によって生成されるオブジェクトを制限します。  
  
```sql  
select c from cs as c where e  
```  
  
 式 `e` には Boolean 型が含まれる必要があります。  
  
 WHERE 句は、FROM 句の直後、およびグループ化、順序付け、または投影が実行される前に適用されます。 FROM 句で定義されたすべての要素名は、WHERE 句の式に対して表示されます。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [クエリ式](query-expressions-entity-sql.md)
