---
title: 集計関数 (Entity Framework 用 SqlClient)
ms.date: 03/30/2017
ms.assetid: 03303f01-b591-4efc-9875-f9c608edff0b
ms.openlocfilehash: 1fad25f2229b4fa810cf82a96dcb8c50a9de3070
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150650"
---
# <a name="aggregate-functions-sqlclient-for-entity-framework"></a>集計関数 (Entity Framework 用 SqlClient)
.NET Framework Data Provider for SQL Server (SqlClient) には、集計関数が用意されています。 集計関数は、一連の入力値に対して計算を実行し、値を返します。 これらの関数は、SqlClient の SqlServer 名前空間に存在します。 Entity Framework は、プロバイダーの名前空間プロパティを使用することにより、型や関数など、特定のコンストラクターに対してこのプロバイダーによってどのプレフィックスが使用されているかを特定できます。  
  
 以下は、SqlClient の集計関数です。  

## <a name="avgexpression"></a>AVG(expression)

コレクション内の値の平均値を返します。 NULL 値は無視されます。

**引数**

`Int32`、`Int64`、`Double`、および `Decimal`。

**戻り値**

`expression` の型。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_AVG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_avg)]

## <a name="checksum_aggcollection"></a>CHECKSUM_AGG(collection)

 コレクション内にある値のチェックサムを返します。 NULL 値は無視されます。

 **引数**

 Collection(`Int32`)。

 **戻り値**

 `Int32`。

 **例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_CHECKSUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_checksum)]

## <a name="countexpression"></a>COUNT(expression)

コレクション内のアイテムの数を `Int32` 型の値として返します。

**引数**

Collection\<T>。T は次のいずれかの型です。

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`|`Guid` (SQL Server 2000 では返されません)|

**戻り値**

`Int32`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_COUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_count)]

## <a name="count_bigexpression"></a>COUNT_BIG(expression)

コレクション内のアイテムの数を `bigint` 型の値として返します。

 **引数**

 Collection(T)。T は次のいずれかの型です。

 |   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`|`Guid` (SQL Server 2000 では返されません)|

**戻り値**

`Int64`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_COUNTBIG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_countbig)]

## <a name="maxexpression"></a>MAX(expression)

コレクション内の最大値を返します。

**引数**

Collection(T)。T は次のいずれかの型です。

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`||

**戻り値**

`expression` の型。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_MAX](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_max)]

## <a name="minexpression"></a>MIN(expression)

コレクション内の最小値を返します。

**引数**

Collection(T)。T は次のいずれかの型です。

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`||

**戻り値**

`expression` の型。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_MIN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_min)]

## <a name="stdevexpression"></a>STDEV(expression)

指定された式のすべての値の統計的標準偏差を返します。

**引数**

Collection(`Double`)。

**戻り値**

`Double`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_STDEV](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdev)]

## <a name="stdevpexpression"></a>STDEVP(expression)

指定された式のすべての値を母集団として統計的標準偏差を返します。

**引数**

Collection(`Double`)。

**戻り値**

`Double`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_STDEVP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdevp)]

## <a name="sumexpression"></a>SUM(expression)

コレクション内のすべての値の合計を返します。

**引数**

Collection(T)。T は次のいずれかの型です: `Int32`、`Int64`、`Double`、`Decimal`。

**戻り値**

`expression` の型。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_SUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_sum)]

## <a name="varexpression"></a>VAR(expression)

指定された式のすべての値の統計的分散を返します。

**引数**

Collection(`Double`)。

**戻り値**

`Double`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_VAR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_var)]

## <a name="varpexpression"></a>VARP(expression)

指定した式のすべての値について、母集団に対する統計的変位を返します。

**引数**

Collection(`Double`)。

**戻り値**

`Double`。

**例**

[!code-sql[DP EntityServices Concepts#SQLSERVER_VARP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_varp)]
  
## <a name="see-also"></a>関連項目

- [集計関数 (Transact-SQL)](/sql/t-sql/functions/aggregate-functions-transact-sql)
- [Entity SQL 言語](./language-reference/entity-sql-language.md)
- [集計正規関数](./language-reference/aggregate-canonical-functions.md)
