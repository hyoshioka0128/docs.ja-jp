---
title: サポートされていない式 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
dev_langs:
- sql
ms.openlocfilehash: 956fe117eb0c59392c3999046bc70deaed268ac6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248781"
---
# <a name="unsupported-expressions"></a>サポートされていない式

このトピックでは、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] でサポートされていない Transact-SQL 式について説明します。 詳細については、「[Entity SQL と Transact-SQL の相違点](how-entity-sql-differs-from-transact-sql.md)」を参照してください。

## <a name="quantified-predicates"></a>定量化された述語

Transact-SQL では、次の形式のコンストラクターを使用できます。

```sql
sal > all (select salary from employees)
sal > any (select salary from employees)
```

ただし、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、このようなコンストラクターがサポートされていません。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、これに相当する式を次のように記述できます。

```sql
not exists(select 0 from employees as e where sal <= e.salary)
exists(select 0 from employees as e where sal > e.salary)
```

## <a name="-operator"></a>* 演算子

Transact-SQL では、すべての列を投影する必要があることを示すために、SELECT 句で * 演算子を使用できます。これは [!INCLUDE[esql](../../../../../../includes/esql-md.md)] でサポートされていません。

## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
- [Entity SQL と Transact-SQL の相違点](how-entity-sql-differs-from-transact-sql.md)
