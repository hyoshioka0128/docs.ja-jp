---
title: 日付と時刻の正規関数
ms.date: 03/30/2017
ms.assetid: 9628b74f-1585-436a-b385-8b02ed0cdd63
ms.openlocfilehash: 3dd6c0da3f9851df7bb9725d9d6c08fef5a0d3d3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251097"
---
# <a name="date-and-time-canonical-functions"></a>日付と時刻の正規関数
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] には、日付および時刻の正規関数が含まれます。  
  
## <a name="remarks"></a>Remarks  
 次の表に、日付と時刻の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数を示します。 `datetime` は <xref:System.DateTime> 値です。  
  
|関数|説明|  
|--------------|-----------------|  
|`AddNanoseconds(expression,number)`|指定されたナノ秒数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddMicroseconds(expression,number)`|指定されたマイクロ秒数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddMilliseconds(expression,number)`|指定されたミリ秒数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddSeconds(expression,number)`|指定された秒数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddMinutes(expression,number)`|指定された分数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddHours(expression,number)`|指定された時間数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`、`DateTime`、`DateTimeOffset`、または `Time`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddDays(expression,number)`|指定された日数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`: `DateTime` または `DateTimeOffset`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddMonths(expression,number)`|指定された月数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`: `DateTime` または `DateTimeOffset`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`AddYears(expression,number)`|指定された年数を表す `number` を `expression` に追加します。<br /><br /> **引数**<br /><br /> `expression`: `DateTime` または `DateTimeOffset`。<br /><br /> `number`: `Int32`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`CreateDateTime(year,month,day,hour,minute,second)`|サーバーのタイム ゾーンでのサーバーの現在の日時として新しい `DateTime` 値を返します。<br /><br /> **引数**<br /><br /> `year`、`month`、`day`、`hour`、`minute`: `Int16` および `Int32`。<br /><br /> `second`: `Double`。<br /><br /> **戻り値**<br /><br /> `DateTime`。|  
|`CreateDateTimeOffset(year,month,day,hour,minute,second,tzoffset)`|世界協定時刻 (UTC) を基準としたサーバーの現在の日時として新しい `DateTimeOffset` 値を返します。<br /><br /> **引数**<br /><br /> `year`、`month`、`day`、`hour`、`minute`、`tzoffset`: `Int32`。<br /><br /> `second`: `Double`。<br /><br /> **戻り値**<br /><br /> `DateTimeOffset`。|  
|`CreateTime(hour,minute,second)`|現在の時刻として新しい `Time` 値を返します。<br /><br /> **引数**<br /><br /> `hour` および `minute`: `Int32`。<br /><br /> `second`: `Double`。<br /><br /> **戻り値**<br /><br /> `Time`。|  
|`CurrentDateTime()`|サーバーのタイム ゾーンでのサーバーの現在の日時として `DateTime` 値を返します。<br /><br /> **戻り値**<br /><br /> `DateTime`。|  
|`CurrentDateTimeOffset()`|現在の日付、時刻、およびオフセットを `DateTimeOffset` として返します。<br /><br /> **戻り値**<br /><br /> `DateTimeOffset`。|  
|`CurrentUtcDateTime()`|UTS タイム ゾーンでのサーバーの現在の日時として <xref:System.DateTime> 値を返します。<br /><br /> **戻り値**<br /><br /> `DateTime`。|  
|`Day(expression)`|1 ～ 31 の間の `expression` として `Int32` の日付の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime` および `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。<br /><br /> **例**<br /><br /> `-- The following example returns 12.`<br /><br /> `Day(cast('03/12/1998' as DateTime))`|  
|`DayOfYear(expression)`|`expression` の日付の部分を 1 ～ 366 の間の `Int32` として返します。366 はうるう年の最後の日に対して返されます。<br /><br /> **引数**<br /><br /> `DateTime` または `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffNanoseconds(startExpression,endExpression)`|`startExpression` と `endExpression` の差をナノ秒単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffMilliseconds(startExpression,endExpression)`|`startExpression` と `endExpression` の差をミリ秒単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffMicroseconds(startExpression,endExpression)`|`startExpression` と `endExpression` の差をマイクロ秒単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffSeconds(startExpression,endExpression)`|`startExpression` と `endExpression` の差を秒単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffMinutes(startExpression,endExpression)`|`startExpression` と `endExpression` の差を分単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffHours(startExpression,endExpression)`|`startExpression` と `endExpression` の差を時間単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime`、`DateTimeOffset`、または `Time`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffDays(startExpression,endExpression)`|`startExpression` と `endExpression` の差を日単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime` または `DateTimeOffset`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffMonths(startExpression,endExpression)`|`startExpression` と `endExpression` の差を月単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime` または `DateTimeOffset`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`DiffYears(startExpression,endExpression)`|`startExpression` と `endExpression` の差を年単位で返します。<br /><br /> **引数**<br /><br /> `startExpression`、`endExpression`: `DateTime` または `DateTimeOffset`。 **注:** `startExpression` と `endExpression` は、同じ型である必要があります。 <br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`GetTotalOffsetMinutes(datetimeoffset)`|GMT からのオフセット `datetimeoffset` (分数) を返します。 この値は通常、+780 ～ -780 (+ 13 時間～ - 13 時間) の間になります。 **注:** この関数は、SQL Server 2008 でのみサポートされます。 <br /><br /> **引数**<br /><br /> `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`Hour(expression)`|0 ～ 23 の間の `expression` として `Int32` の時間の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime, Time` および `DateTimeOffset`。<br /><br /> **例**<br /><br /> `-- The following example returns 22.`<br /><br /> `Hour(cast('22:35:5' as DateTime))`|  
|`Millisecond(expression)`|0 ～ 999 の間の `expression` として `Int32` のミリ秒の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime, Time` および `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。|  
|`Minute(expression)`|0 ～ 59 の間の `expression` として `Int32` の分の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime, Time` または `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。<br /><br /> **例**<br /><br /> `-- The following example returns 35`<br /><br /> `Minute(cast('22:35:5' as DateTime))`|  
|`Month(expression)`|1 ～ 12 の間の `expression` として `Int32` の月の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime` または `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。<br /><br /> **例**<br /><br /> `-- The following example returns 3.`<br /><br /> `Month(cast('03/12/1998' as DateTime))`|  
|`Second(expression)`|0 ～ 59 の間の `expression` として `Int32` の秒の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime, Time` および `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。<br /><br /> **例**<br /><br /> `-- The following example returns 5`<br /><br /> `Second(cast('22:35:5' as DateTime))`|  
|`TruncateTime(expression)`|時間の値が切り捨てられた `expression` を返します。<br /><br /> **引数**<br /><br /> `DateTime` または `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `expression` の型。|  
|`Year(expression)`|`Int32` `YYYY` として `expression` の年の部分を返します。<br /><br /> **引数**<br /><br /> `DateTime` および `DateTimeOffset`。<br /><br /> **戻り値**<br /><br /> `Int32`。<br /><br /> **例**<br /><br /> `-- The following example returns 1998.`<br /><br /> `Year(cast('03/12/1998' as DateTime))`|  
  
 `null` が入力された場合、これらの関数は `null` を返します。  
  
 同等の機能は、Microsoft SQL クライアント マネージド プロバイダーでも利用できます。 詳細については、「[Entity Framework 用 SqlClient 関数](../sqlclient-for-ef-functions.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [正規関数](canonical-functions.md)
