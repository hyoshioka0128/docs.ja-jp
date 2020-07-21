---
title: NAVIGATE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: f107f29d-005f-4e39-a898-17f163abb1d0
ms.openlocfilehash: 09128a367a02e1f9b206a9cc068987166c76381b
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319553"
---
# <a name="navigate-entity-sql"></a>NAVIGATE (Entity SQL)

エンティティ間で確立されたリレーションシップをナビゲートします。

## <a name="syntax"></a>構文

```sql
navigate(instance-expression, [relationship-type], [to-end [, from-end] ])
```

## <a name="arguments"></a>引数

`instance-expression` エンティティのインスタンス。

`relationship-type` 概念スキーマ定義言語 (CSDL) ファイルで指定されたリレーションシップの種類の名前。 `relationship-type` は \<名前空間>.\<リレーションシップ種類名> として修飾されます。

`to` リレーションシップの終端。

`from` リレーションシップの開始。

## <a name="return-value"></a>戻り値

終端のカーディナリティが 1 の場合、戻り値は `Ref<T>` になります。 終端のカーディナリティが n の場合、戻り値は `Collection<Ref<T>>` になります。

## <a name="remarks"></a>Remarks

リレーションシップは、Entity Data Model (EDM) における最上位のコンストラクトです。 リレーションシップは、複数のエンティティ型の間で確立され、ユーザーはエンティティ間のリレーションシップをナビゲートできます。 `from` と `to` は、リレーションシップ内の名前解決があいまいでない場合の条件付きのオプションです。

NAVIGATE は、O および C 空間で有効です。

ナビゲーション構造の一般的な形式は次のようになります。

navigate(`instance-expression`, `relationship-type`, [ `to-end` [, `from-end` ] ] )

次に例を示します。

```sql
Select o.Id, navigate(o, OrderCustomer, Customer, Order)
From LOB.Orders as o
```

ここで、OrderCustomer は `relationship`であり、Customer と Order はリレーションシップの `to-end` (顧客) と `from-end` (注文) です。 OrderCustomer が n:1 リレーションシップの場合、ナビゲーション式の結果型は Ref\<Customer> となります。

この式をより簡略化すると、次のようになります。

```sql
Select o.Id, navigate(o, OrderCustomer)
From LOB.Orders as o
```

同様に、次の形式のクエリでは、ナビゲーション式は Collection<Ref\<Order>> のようになります。

```sql
Select c.Id, navigate(c, OrderCustomer, Order, Customer)
From LOB.Customers as c
```

インスタンス式は、エンティティ/参照型になる必要があります。

## <a name="example"></a>例

次の Entity SQL クエリでは、NAVIGATE 演算子を使用して、Address エンティティ型と SalesOrderHeader エンティティ型間で確立されたリレーションシップをナビゲートします。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。

1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。

2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。

 [!code-sql[DP EntityServices Concepts#NAVIGATE](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#navigate)]

## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [方法: Navigate 演算子でリレーションシップをナビゲートする](navigate-entity-sql.md)
