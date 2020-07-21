---
title: 数値演算正規関数
ms.date: 03/30/2017
ms.assetid: 6f6cddc6-b561-4ebe-84b6-841ef5b4113b
ms.openlocfilehash: 9417ff9836912017c9d88bb24a18849aaac2836a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250310"
---
# <a name="math-canonical-functions"></a>数値演算正規関数

Entity SQL には、次の数値演算正規関数が含まれています。
  
## <a name="absvalue"></a>Abs(value)

`value` の絶対値を返します。

**引数**

`Int16`、`Int32`、`Int64`、`Byte`、`Single`、`Double`、および `Decimal`。

**戻り値**

`value` の型。

**例**

`Abs(-2)`

## <a name="ceilingvalue"></a>Ceiling(value)

`value` 以上で最小の整数値を返します。

**引数**

`Single`、`Double`、および `Decimal`。

**戻り値**

`value` の型。

**例**

[!code-csharp[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_ceiling)]
[!code-sql[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_ceiling)]

## <a name="floorvalue"></a>Floor(value)

`value` 以下で最大の整数値を返します。

**引数**

`Single`、`Double`、および `Decimal`。

**戻り値**

`value` の型。

**例**

[!code-csharp[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_floor)]
[!code-sql[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_floor)]

## <a name="powervalue-exponent"></a>Power(value, exponent)

指定された `value` を指定された `exponent` でべき乗した結果を返します。

**引数**

|  |  |
|--|--|
|`value` | `Int32, Int64, Double`、または `Decimal`。 |
|`exponent` | `Int64`、`Double`、または `Decimal`。 |

**戻り値**

`value` の型。

**例**

`Power(748.58,2)`

## <a name="roundvalue"></a>Round(value)

最も近い整数に丸められた `value` の整数部分を返します。

**引数**

`Single`、`Double`、および `Decimal`。

**戻り値**

`value` の型。

**例**

`Round(748.58)`

## <a name="roundvalue-digits"></a>Round(value, digits)

`value` を指定された最も近い `digits` に丸めて返します。

**引数**

|  |  |
|--|--|
|`value`|`Double` または `Decimal`。|
|`digits`|`Int16` または `Int32`。|

**戻り値**

`value` の型。

**例**

`Round(748.58,1)`

## <a name="truncatevalue-digits"></a>Truncate(value, digits)

`value` を指定された最も近い `digits` に切り詰めて返します。

**引数**

|  |  |
|--|--|
|`value`|`Double` または `Decimal`。|
|`digits`|`Int16` または `Int32`。|

**戻り値**

`value` の型。

**例**

`Truncate(748.58,1)`  
  
 `null` が入力された場合、これらの関数は `null` を返します。  
  
 同等の機能は、Microsoft SQL クライアント マネージド プロバイダーでも利用できます。 詳細については、「[Entity Framework 用 SqlClient 関数](../sqlclient-for-ef-functions.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [正規関数](canonical-functions.md)
