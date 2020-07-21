---
title: TOP (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4a4a0954-82e2-4eae-bcaf-7c4552f3532d
ms.openlocfilehash: 16be25336bac386c993eae7527c9377be1073d1e
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319274"
---
# <a name="top-entity-sql"></a>TOP (Entity SQL)

SELECT 句には、オプションの ALL/DISTINCT 修飾子に続けてオプションの TOP サブ句を指定できます。 TOP サブ句は、クエリ結果の先頭から指定した行セットだけを返すよう指定します。

## <a name="syntax"></a>構文

```sql
[ TOP (n) ]
```

## <a name="arguments"></a>引数

`n` 返す行の数を指定する数値式。 `n` は単一の数値リテラルかまたは単一のパラメーターです。

## <a name="remarks"></a>Remarks

TOP 式には、単一の数値リテラルまたは単一のパラメーターを使用してください。 定数リテラルを使用する場合は、リテラルの種類を Edm.Int64 (byte、int16、int32、int64、または Edm.Int64 に昇格可能な型にマップされる任意のプロバイダー型) に暗黙的に昇格でき、その値が 0 以上である必要があります。 それ以外の場合は、例外が発生します。 パラメーターを式として使用する場合は、パラメーター型も Edm.Int64 に暗黙的に昇格できる必要がありますが、パラメーター値は遅延バインドされるため、コンパイル時に実際のパラメーター値は検証されません。

定数 TOP 式の例を以下に示します。

```sql
select distinct top(10) c.a1, c.a2 from T as a
```

パラメーター化された TOP 式の例を以下に示します。

```sql
select distinct top(@topParam) c.a1, c.a2 from T as a
```

TOP は、クエリが並べ替えられていない限り、非決定的です。 確定的な結果が必要な場合は、 [ORDER BY](skip-entity-sql.md) 句の [SKIP](limit-entity-sql.md) サブ句および [LIMIT](order-by-entity-sql.md) サブ句を使用します。 TOP     SKIP/LIMIT

## <a name="example"></a>例

次の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリは、TOP を使用して、クエリ結果から返される 1 番上の 1 行を指定します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。

1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。

2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。

    [!code-sql[DP EntityServices Concepts#TOP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#top)]

## <a name="see-also"></a>関連項目

- [SELECT](select-entity-sql.md)
- [SKIP](skip-entity-sql.md)
- [LIMIT](limit-entity-sql.md)
- [ORDER BY](order-by-entity-sql.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
