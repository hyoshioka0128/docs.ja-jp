---
title: 入れ子になった Entity SQL クエリの作成
ms.date: 03/30/2017
ms.assetid: 685d4cd3-2c1f-419f-bb46-c9d97a351eeb
ms.openlocfilehash: 6b2fc9a32fc30d205b9c33257bf98781cfa07499
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150390"
---
# <a name="composing-nested-entity-sql-queries"></a>入れ子になった Entity SQL クエリの作成
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、機能の豊富な関数言語です。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の構成要素は式です。 従来の SQL と異なり、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では結果セットは表形式に限定されません。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、リテラル、パラメーター、入れ子になった式などが含まれた複雑な式を作成できます。 式の値は、パラメーター化されている場合、つまり他の式で構成される場合があります。  
  
## <a name="nested-expressions"></a>入れ子になった式  
 入れ子になった式は、その式によって返される型の値が受け入れられる場所であればどこにでも配置できます。 次に例を示します。  
  
```sql  
-- Returns a hierarchical collection of three elements at top-level.
-- x must be passed in the parameter collection.  
ROW(@x, {@x}, {@x, 4, 5}, {@x, 7, 8, 9})  
  
-- Returns a hierarchical collection of one element at top-level.  
-- x must be passed in the parameter collection.  
{{{@x}}};  
```  
  
 入れ子になったクエリは、projection 句に配置できます。 次に例を示します。  
  
```sql  
-- Returns a collection of rows where each row contains an Address entity.  
-- and a collection of references to its corresponding SalesOrderHeader entities.  
SELECT address, (SELECT DEREF(soh)
                    FROM NAVIGATE(address, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS soh)
                    AS salesOrderHeader FROM AdventureWorksEntities.Address AS address  
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、入れ子になったクエリを次のようにかっこで囲む必要があります。  
  
```sql  
-- Pseudo-Entity SQL  
( SELECT …  
FROM … )  
UNION ALL  
( SELECT …  
FROM … );  
```  
  
 次の例では、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] で式を正しく入れ子にする方法を示します。[方法:2 つのクエリの結合を並べ替える](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896299(v=vs.100))。  
  
## <a name="nested-queries-in-projection"></a>投影内の入れ子になったクエリ  
 project 句内の入れ子になったクエリは、サーバーでデカルト積に変換されないことがあります。 SQL Server などの一部のバックエンド サーバーでは、これによって TempDB テーブルのサイズが非常に大きくなり、サーバーのパフォーマンスに悪影響を及ぼす場合があります。  
  
 以下は、このようなクエリの例です。  
  
```sql  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## <a name="ordering-nested-queries"></a>入れ子になったクエリの順序  
 Entity Framework では、入れ子になった式をクエリ内の任意の場所に配置できます。 Entity SQL ではクエリを柔軟に作成できるので、入れ子になったクエリの順序を含むクエリを記述できます。 ただし、入れ子になったクエリの順序は維持されません。  
  
```sql  
-- The following query will order the results by last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```sql  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
