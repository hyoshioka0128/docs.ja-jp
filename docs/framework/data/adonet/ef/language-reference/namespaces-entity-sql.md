---
title: 名前空間 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 83991c21-60db-4af9-aca3-b416f6cae98e
ms.openlocfilehash: 7f05067c4bdb859f3661f775c2502852b6658522
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319554"
---
# <a name="namespaces-entity-sql"></a>名前空間 (Entity SQL)
型名、エンティティ セット、関数など、グローバル識別子の名前の競合を防ぐために、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] には名前空間が採用されています。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] での名前空間のサポートは、.NET Framework での名前空間のサポートと似ています。  
  
 次の例のように、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、2 とおりの形式で USING 句を指定できます。1 つは略称的な別名を指定する修飾名前空間、もう 1 つは別名を指定しない非修飾名前空間です。  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## <a name="name-resolution-rules"></a>名前解決ルール  
 識別子がローカル スコープ内で解決できない場合、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではグローバル スコープ (名前空間) で名前が探索されます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、まず識別子 (プレフィックス) と修飾名前空間の 1 つを照合します。 一致が見つかった場合は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] により、指定された名前空間で、その識別子の残りの部分の解決が試みられます。 一致が見つからなかった場合は、例外がスローされます。  
  
 次に、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] により、すべての (プロローグで指定された) 非修飾名前空間で識別子の検索が試みられます。 その識別子が属している名前空間を一意に特定できた場合は、その場所が返されます。 同じ識別子に対して複数の名前空間が見つかった場合は、例外がスローされます。 識別子に対応する名前空間を特定できなかった場合、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、次の例のように、名前が 1 つ外側のスコープ (<xref:System.Data.Common.DbCommand> オブジェクトまたは <xref:System.Data.Common.DbConnection> オブジェクト) に渡されます。  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## <a name="differences-from-the-net-framework"></a>.NET Framework との違い  
 .NET Framework では、部分修飾名前空間を使用できます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では使用できません。  
  
## <a name="adonet-usage"></a>ADO.NET の使用法  
 クエリは、ADO.NET の <xref:System.Data.Common.DbCommand> オブジェクトを使用して表されます。 <xref:System.Data.Common.DbCommand> オブジェクトは、<xref:System.Data.Common.DbConnection> オブジェクトに対して構築できます。 名前空間を <xref:System.Data.Common.DbCommand> オブジェクトや <xref:System.Data.Common.DbConnection> オブジェクトの一部として指定することもできます。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] によってクエリ自体の内部で識別子を解決できなかった場合は、同様のルールに従って、外側の名前空間が調査されます。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [Entity SQL の概要](entity-sql-overview.md)
