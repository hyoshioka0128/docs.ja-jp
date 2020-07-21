---
title: LIMIT (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c22ffede-0a52-44d1-99b9-4a91e651e1b9
ms.openlocfilehash: 275b22686c6c932b2a9e4b20973ac07e99d47e14
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319631"
---
# <a name="limit-entity-sql"></a>LIMIT (Entity SQL)
物理的なページングは、ORDER BY 句の LIMIT サブ句を使用して実行できます。 LIMIT は ORDER BY 句と切り離して使用することはできません。  
  
## <a name="syntax"></a>構文  
  
```sql  
[ LIMIT n ]  
```  
  
## <a name="arguments"></a>引数  
 `n`  
 選択する項目の数。  
  
 LIMIT 式のサブ句が ORDER BY 句に存在する場合、クエリは並べ替え順序に従って並べ替えられ、結果の行数は LIMIT 式によって制限されます。 たとえば、LIMIT 5 は、結果セットを 5 つのインスタンスまたは行に制限します。 LIMIT は機能的に TOP と等価ですが、LIMIT では ORDER BY 句が存在する必要がある点が異なります。 SKIP および LIMIT は ORDER BY 句と共に別々に使用できます。  
  
> [!NOTE]
> TOP 修飾子と SKIP サブ句が同じクエリ式内に存在する場合には、Entity Sql クエリは無効と見なされます。 TOP 式を LIMIT 式に変更してクエリを記述し直す必要があります。  
  
## <a name="example"></a>例  
 次の Entity SQL クエリでは、SELECT ステートメントで返されたオブジェクトの並べ替え順序の指定に ORDER BY 演算子を LIMIT と共に使用します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#LIMIT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#limit)]  
  
## <a name="see-also"></a>関連項目

- [ORDER BY](order-by-entity-sql.md)
- [方法: クエリの結果をページングする](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [ページング](paging-entity-sql.md)
- [TOP](top-entity-sql.md)
