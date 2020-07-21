---
title: CLR メソッドと正規関数とのマッピング
ms.date: 03/30/2017
ms.assetid: e3363261-2cb8-4b54-9555-2870be99b929
ms.openlocfilehash: 6f14ad8d9e8f919fe820447cc991b102319b38d5
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251225"
---
# <a name="clr-method-to-canonical-function-mapping"></a>CLR メソッドと正規関数とのマッピング

Entity Framework は、文字列操作、数学関数などの多くのデータベース システム間で共通の機能を実装する正規関数のセットを提供します。 この関数により、開発者は広範なデータベース システムをターゲットとして指定することができます。 LINQ to Entities などのクエリ テクノロジから呼び出されると、これらの正規関数は使用されているプロバイダーに対応した正しい格納関数に変換されます。 これにより、関数の呼び出しをデータ ソース間で共通の形式で表すことができ、データ ソース間に一貫した方法でクエリを利用できます。 オペランドが数値型である場合は、ビット単位の AND、OR、NOT、および XOR 演算子も正規関数にマップされます。 ブール型のオペランドの場合、ビット単位の AND、OR、NOT、および XOR 演算子は、それぞれのオペランドの論理 AND、OR、NOT、および XOR 演算を計算します。 詳しくは、「[正規関数](canonical-functions.md)」をご覧ください。

LINQ シナリオの場合、Entity Framework に対するクエリでは、正規関数による、基になるデータ ソース上のメソッドへの特定の CLR メソッドのマッピングも行われます。 正規関数に明示的にマップされない LINQ to Entities クエリで任意のメソッドの呼び出しが実行されると、ランタイムの <xref:System.NotSupportedException> 例外がスローされます。

## <a name="systemstring-method-static-mapping"></a>System.String メソッド (静的) のマッピング

|System.String メソッド (静的)|正規関数|
|-------------------------------------|------------------------|
|System.String Concat(String `str0`, String `str1`)|Concat(`str0`, `str1`)|
|System.String Concat(String `str0`, String `str1`, String `str2`)|Concat(Concat(`str0`, `str1`), `str2`)|
|System.String Concat(String `str0`, String `str1`, String `str2`, String `str03`)|Concat(Concat(Concat(`str0`, `str1`), `str2`), `str3`)|
|Boolean Equals(String `a`, String `b`)|= 演算子|
|Boolean IsNullOrEmpty(String `value`)|(IsNull(`value`)) OR Length(`value`) = 0|
|Boolean op_Equality(String `a`, String `b`)|= 演算子|
|Boolean op_Inequality(String `a` , String `b`)|!= 演算子|
|Microsoft.VisualBasic.Strings.Trim(String `str`)|Trim(`str`)|
|Microsoft.VisualBasic.Strings.LTrim(String `str`)|Ltrim(`str`)|
|Microsoft.VisualBasic.Strings.RTrim(String `str`)|Rtrim(`str`)|
|Microsoft.VisualBasic.Strings.Len(String `expression`)|Length(`expression`)|
|Microsoft.VisualBasic.Strings.Left(String `str`, Int32 `Length`)|Left(`str`, `Length`)|
|Microsoft.VisualBasic.Strings.Mid(String `str`, Int32 `Start`, Int32 `Length`)|Substring(`str`, `Start`, `Length`)|
|Microsoft.VisualBasic.Strings.Right(String `str`, Int32 `Length`)|Right(`str`, `Length`)|
|Microsoft.VisualBasic.Strings.UCase(String `Value`)|ToUpper(`Value`)|
|Microsoft.VisualBasic.Strings.LCase(String Value)|ToLower(`Value`)|

## <a name="systemstring-method-instance-mapping"></a>System.String メソッド (インスタンス) のマッピング

|System.String メソッド (インスタンス)|正規関数|メモ|
|---------------------------------------|------------------------|-----------|
|Boolean Contains(String `value`)|`this` LIKE '%`value`%'|`value` が定数ではない場合、IndexOf(`this`, `value`) > 0 にマップされます|
|Boolean EndsWith(String `value`)|`this` LIKE `'`%`value`'|`value` が定数ではない場合、Right(`this`, length(`value`)) = `value` にマップされます。|
|Boolean StartsWith(String `value`)|`this` LIKE '`value`%'|`value` が定数ではない場合、IndexOf(`this`, `value`) = 1 にマップされます。|
|長さ|Length(`this`)||
|Int32 IndexOf(String `value`)|IndexOf(`this`, `value`) - 1||
|System.String Insert(Int32 `startIndex`, String `value`)|Concat(Concat(Substring(`this`, 1, `startIndex`), `value`), Substring(`this`, `startIndex`+1, Length(`this`) - `startIndex`))||
|System.String Remove(Int32 `startIndex`)|Substring(`this`, 1, `startIndex`)||
|System.String Remove(Int32 `startIndex`, Int32 `count`)|Concat(Substring(`this`, 1, `startIndex`) , Substring(`this`, `startIndex` + `count` +1, Length(`this`) - (`startIndex` + `count`)))|`startIndex` が 0 以上の整数である場合、サポートされるのは Remove(`count`, `count`) だけです。|
|System.String Replace(String `oldValue`, String `newValue`)|Replace(`this`, `oldValue`, `newValue`)||
|System.String Substring(Int32 `startIndex`)|Substring(`this`, `startIndex` +1, Length(`this`) - `startIndex`)||
|System.String Substring(Int32 `startIndex`, Int32 `length`)|Substring(`this`, `startIndex` +1, `length`)||
|System.String ToLower()|ToLower(`this`)||
|System.String ToUpper()|ToUpper(`this`)||
|System.String Trim()|Trim(`this`)||
|System.String TrimEnd(Char[] `trimChars`)|RTrim(`this`)||
|System.String TrimStart(Char[]`trimChars`)|LTrim(`this`)||
|Boolean Equals(String `value`)|= 演算子||

## <a name="systemdatetime-method-static-mapping"></a>System.DateTime メソッド (静的) のマッピング

|System.DateTime メソッド (静的)|正規関数|メモ|
|---------------------------------------|------------------------|-----------|
|Boolean Equals(DateTime `t1`, DateTime `t2`)|= 演算子||
|System.DateTime.Now|CurrentDateTime()||
|System.DateTime.UtcNow|CurrentUtcDateTime()||
|Boolean op_Equality(DateTime `d1`, DateTime `d2`)|= 演算子||
|Boolean op_GreaterThan(DateTime `t1`, DateTime `t2`)|> 演算子||
|Boolean op_GreaterThanOrEqual(DateTime `t1`, DateTime `t2`)|>= 演算子||
|Boolean op_Inequality(DateTime `t1`, DateTime `t2`)|!= 演算子||
|Boolean op_LessThan(DateTime `t1`, DateTime `t2`)|< 演算子||
|Boolean op_LessThanOrEqual(DateTime `t1`, DateTime `t2`)|<= 演算子||
|Microsoft.VisualBasic.DateAndTime.DatePart( _<br /><br /> ByVal `Interval` As DateInterval, \_<br /><br /> ByVal `DateValue` As DateTime, \_<br /><br /> Optional ByVal `FirstDayOfWeekValue` As FirstDayOfWeek = VbSunday, \_<br /><br /> Optional ByVal `FirstWeekOfYearValue` As FirstWeekOfYear = VbFirstJan1 \_<br /><br /> ) As Integer||詳細については、「DatePart 関数」を参照してください。|
|Microsoft.VisualBasic.DateAndTime.Now|CurrentDateTime()||
|Microsoft.VisualBasic.DateAndTime.Year(DateTime `TimeValue`)|Year()||
|Microsoft.VisualBasic.DateAndTime.Month(DateTime `TimeValue`)|Month()||
|Microsoft.VisualBasic.DateAndTime.Day(DateTime `TimeValue`)|Day()||
|Microsoft.VisualBasic.DateAndTime.Hour(DateTime `TimeValue`)|Hour()||
|Microsoft.VisualBasic.DateAndTime.Minute(DateTime `TimeValue`)|Minute()||
|Microsoft.VisualBasic.DateAndTime.Second(DateTime `TimeValue`)|Second()||

## <a name="systemdatetime-method-instance-mapping"></a>System.DateTime メソッド (インスタンス) のマッピング

|System.DateTime メソッド (インスタンス)|正規関数|
|-----------------------------------------|------------------------|
|Boolean Equals(DateTime `value`)|= 演算子|
|Day|Day(`this`)|
|Hour|Hour(`this`)|
|Millisecond|Millisecond(`this`)|
|Minute|Minute(`this`)|
|月|Month(`this`)|
|Second|Second(`this`)|
|Year|Year(`this`)|

## <a name="systemdatetimeoffset-method-instance-mapping"></a>System.DateTimeOffset メソッド (インスタンス) のマッピング

示されているプロパティに対する `get` メソッドのマッピングを示します。

|System.DateTimeOffset メソッド (インスタンス)|正規関数|メモ|
|-----------------------------------------------|------------------------|-----------|
|Day|Day(`this`)|SQL Server 2005 ではサポートされません。|
|Hour|Hour(`this`)|SQL Server 2005 ではサポートされません。|
|Millisecond|Millisecond(`this`)|SQL Server 2005 ではサポートされません。|
|Minute|Minute(`this`)|SQL Server 2005 ではサポートされません。|
|月|Month(`this`)|SQL Server 2005 ではサポートされません。|
|Second|Second(`this`)|SQL Server 2005 ではサポートされません。|
|Year|Year(`this`)|SQL Server 2005 ではサポートされません。|

> [!NOTE]
> 比較した <xref:System.DateTimeOffset.Equals%2A> オブジェクトが等しい場合、`true` メソッドは <xref:System.DateTimeOffset> を返します。それ以外の場合は `false` を返します。 比較した <xref:System.DateTimeOffset.CompareTo%2A> オブジェクトが等しい、より大きい、またはより小さい場合、<xref:System.DateTimeOffset> メソッドはそれぞれ 0、1、または -1 を返します。

## <a name="systemdatetimeoffset-method-static-mapping"></a>System.DateTimeOffset メソッド (静的) のマッピング

示されているプロパティに対する `get` メソッドのマッピングを示します。

|System.DateTimeOffset メソッド (静的)|正規関数|メモ|
|---------------------------------------------|------------------------|-----------|
|System.DateTimeOffset.Now()|CurrentDateTimeOffset()|SQL Server 2005 ではサポートされません。|

## <a name="systemtimespan-method-instance-mapping"></a>System.TimeSpan メソッド (インスタンス) のマッピング

示されているプロパティに対する `get` メソッドのマッピングを示します。

|System.TimeSpan メソッド (インスタンス)|正規関数|メモ|
|-----------------------------------------|------------------------|-----------|
|時間|Hour(`this`)|SQL Server 2005 ではサポートされません。|
|Milliseconds|Millisecond(`this`)|SQL Server 2005 ではサポートされません。|
|分|Minute(`this`)|SQL Server 2005 ではサポートされません。|
|Seconds|Second(`this`)|SQL Server 2005 ではサポートされません。|

> [!NOTE]
> 比較した <xref:System.TimeSpan.Equals%2A> オブジェクトが等しい場合、`true` メソッドは <xref:System.TimeSpan> を返します。それ以外の場合は `false` を返します。 比較した <xref:System.TimeSpan.CompareTo%2A> オブジェクトが等しい、より大きい、またはより小さい場合、<xref:System.TimeSpan> メソッドはそれぞれ 0、1、または -1 を返します。

### <a name="datepart-function"></a>DatePart 関数

`DatePart` 関数は、`Interval` の値に応じて、複数の異なる正規関数のいずれかにマップされます。 サポートされている各 `Interval` 値に対応する正規関数のマッピングを次の表に示します。

|Interval 値|正規関数|
|--------------------|------------------------|
|DateInterval.Year|Year()|
|DateInterval.Month|Month()|
|DateInterval.Day|Day()|
|DateInterval.Hour|Hour()|
|DateInterval.Minute|Minute()|
|DateInterval.Second|Second()|

## <a name="mathematical-function-mapping"></a>数学関数のマッピング

|CLR メソッド|正規関数|
|----------------|------------------------|
|System.Decimal.Ceiling(Decimal `d`)|Ceiling(`d`)|
|System.Decimal.Floor(Decimal `d`)|Floor(`d`)|
|System.Decimal.Round(Decimal `d`)|Round(`d`)|
|System.Math.Ceiling(Decimal `d`)|Ceiling(`d`)|
|System.Math.Floor(Decimal `d`)|Floor(`d`)|
|System.Math.Round(Decimal `d`)|Round(`d`)|
|System.Math.Ceiling(Double `a`)|Ceiling(`a`)|
|System.Math.Floor(Double `a`)|Floor(`a`)|
|System.Math.Round(Double `a`)|Round(`a`)|
|System.Math.Round(Double value, Int16 digits)|Round(value, digits)|
|System.Math.Round(Double value, Int32 digits)|Round(value, digits)|
|System.Math.Round(Decimal value, Int16 digits)|Round(value, digits)|
|System.Math.Round(Decimal value, Int32, digits)|Round(value, digits)|
|System.Math.Abs(Int16 value)|Abs(value)|
|System.Math.Abs(Int32 value)|Abs(value)|
|System.Math.Abs(Int64 value)|Abs(value)|
|System.Math.Abs(Byte value)|Abs(value)|
|System.Math.Abs(Single value)|Abs(value)|
|System.Math.Abs(Double value)|Abs(value)|
|System.Math.Abs(Decimal value)|Abs(value)|
|System.Math.Truncate(Double value, Int16 digits)|Truncate(value, digits)|
|System.Math.Truncate(Double value, Int32 digits)|Truncate(value, digits)|
|System.Math.Truncate(Decimal value, Int16 digits)|Truncate(value, digits)|
|System.Math.Truncate(Decimal value, Int32 digits)|Truncate(value, digits)|
|System.Math.Power(Int32 value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Int32 value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Int32 value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Decimal exponent)|Power(value, exponent)|

## <a name="bitwise-operator-mapping"></a>ビット演算子のマッピング

|ビット演算子|非ブール型のオペランドの正規関数|ブール型のオペランドの正規関数|
|----------------------|--------------------------------------------------|---------------------------------------------|
|ビット演算子 AND|BitWiseAnd|op1 AND op2|
|ビット演算子 OR|BitWiseOr|op1 OR op2|
|ビット演算子 NOT|BitWiseNot|NOT(op)|
|ビット演算子 XOR|BitWiseXor|((op1 AND NOT(op2)) OR (NOT(op1) AND op2))|

## <a name="other-mapping"></a>その他のマッピング

|メソッド|正規関数|
|------------|------------------------|
|Guid.NewGuid()|NewGuid()|

## <a name="see-also"></a>関連項目

- [LINQ to Entities](linq-to-entities.md)
