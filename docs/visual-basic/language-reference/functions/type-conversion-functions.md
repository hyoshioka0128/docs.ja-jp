---
title: CString
ms.date: 10/24/2018
f1_keywords:
- vb.CUShort
- vb.csng
- vb.CDate
- CByte
- CSng
- vb.CDec
- CBool
- CStr
- vb.CULng
- CDec
- CVErr
- CDbl
- CShort
- vb.CObj
- vb.CVErr
- CULng
- vb.cdbl
- vb.cbool
- CObj
- CDate
- CLng
- vb.cstr
- vb.cbyte
- vb.clng
- vb.CChar
- CUShort
- vb.CUInt
- vb.cint
- vb.CShort
- CInt
- CUInt
- CChar
helpviewer_keywords:
- CDate function
- CByte function
- Integer data type [Visual Basic], converting
- string conversion [Visual Basic], conversion functions
- fractions
- data types [Visual Basic], converting
- text, converting
- CDec function
- Char data type [Visual Basic], converting
- type conversion [Visual Basic], functions for
- Single data type [Visual Basic], converting
- numbers [Visual Basic], rounding
- rounding numbers [Visual Basic], type conversion
- CUShort function
- Long data type [Visual Basic], converting
- return values [Visual Basic], data types
- single-precision numbers [Visual Basic], converting
- data type conversion [Visual Basic], functions for
- CStr function
- times [Visual Basic], converting
- CSng function
- conversions [Visual Basic], type conversion functions
- CBool function
- CDbl function
- CUInt function
- Currency data type [Visual Basic], conversion functions
- numbers [Visual Basic], converting
- Double data type [Visual Basic], converting
- CLng function
- CSByte function
- double-precision numbers
- Decimal data type [Visual Basic], converting
- Boolean data type [Visual Basic], converting
- integers [Visual Basic], type conversion functions
- dates [Visual Basic], converting
- CULng function
- CInt function
- Date data type [Visual Basic], converting
- Byte data type [Visual Basic], converting
- String data type [Visual Basic], converting
- CChar function
- banker's rounding
- Short data type [Visual Basic], converting
- rounding numbers [Visual Basic], banker's rounding
- type conversion [Visual Basic], Visual Basic vs. .NET Framework
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
ms.openlocfilehash: 5c0cfae01da02222d0827e81ec1ed35ce353ead1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415376"
---
# <a name="type-conversion-functions-visual-basic"></a>データ型変換関数 (Visual Basic)

これらの関数は、インラインでコンパイルされます。つまり、変換コードは、式を評価するコードに含まれます。 変換を実行するためのプロシージャの呼び出しがないことがありますが、これにより、パフォーマンスが向上します。 各関数では、式を特定のデータ型に強制的に変換します。

## <a name="syntax"></a>構文

```vb
CBool(expression)
CByte(expression)
CChar(expression)
CDate(expression)
CDbl(expression)
CDec(expression)
CInt(expression)
CLng(expression)
CObj(expression)
CSByte(expression)
CShort(expression)
CSng(expression)
CStr(expression)
CUInt(expression)
CULng(expression)
CUShort(expression)
```

## <a name="part"></a>パーツ

`expression`  
必須です。 ソース データ型の任意の式。

## <a name="return-value-data-type"></a>戻り値のデータ型

次の表に示すように、関数名によって、それが返す値のデータ型が決まります。

|関数名|戻り値のデータ型|`expression` 引数の範囲|
|-------------------|----------------------|-------------------------------------|
|`CBool`|[Boolean データ型](../data-types/boolean-data-type.md)|任意の有効な `Char` または `String` または数値式。|
|`CByte`|[Byte データ型](../data-types/byte-data-type.md)|<xref:System.Byte.MinValue?displayProperty=nameWithType> (0) から <xref:System.Byte.MaxValue?displayProperty=nameWithType> (255) (符号なし)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CByte` 関数による浮動小数点からバイトへの変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CChar`|[Char データ型](../data-types/char-data-type.md)|任意の有効な `Char` または `String` 式。`String` の最初の文字のみが変換されます。値には 0 から 65535 (符号なし) を指定できます。|
|`CDate`|[Date データ型](../data-types/date-data-type.md)|日付と時刻の任意の有効な表現。|
|`CDbl`|[Double 型](../data-types/double-data-type.md)|負の値の場合は -1.79769313486231570E+308 から -4.94065645841246544E-324 for negative values。正の値の場合は 4.94065645841246544E-324 から 1.79769313486231570E+308。|
|`CDec`|[Decimal データ型](../data-types/decimal-data-type.md)|ゼロスケールの数値 (つまり、小数点以下を含まない数値) の場合は +/-79,228,162,514,264,337,593,543,950,335。 小数点以下 28 桁の数値の場合の範囲は +/-7.9228162514264337593543950335 です。 0 以外の最小値は 0.0000000000000000000000000001 (+/-1E-28) です。|
|`CInt`|[Integer データ型](../data-types/integer-data-type.md)|<xref:System.Int32.MinValue?displayProperty=nameWithType> (-2147483648) から <xref:System.Int32.MaxValue?displayProperty=nameWithType> (2147483647)。小数部は丸められます。<sup>1</sup> <br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CInt` 関数による浮動小数点から整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。 |
|`CLng`|[Long データ型](../data-types/long-data-type.md)|<xref:System.Int64.MinValue?displayProperty=nameWithType> (-9,223,372,036,854,775,808) から <xref:System.Int64.MaxValue?displayProperty=nameWithType> (9,223,372,036,854,775,807)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CLng` 関数による浮動小数点から 64 ビット整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CObj`|[Object 型](../data-types/object-data-type.md)|任意の有効な式。|
|`CSByte`|[SByte データ型](../data-types/sbyte-data-type.md)|<xref:System.SByte.MinValue?displayProperty=nameWithType> (-128) から <xref:System.SByte.MaxValue?displayProperty=nameWithType> (127)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CSByte` 関数による浮動小数点から符号付きバイトへの変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CShort`|[Short データ型](../data-types/short-data-type.md)|<xref:System.Int16.MinValue?displayProperty=nameWithType> (-32,768) から <xref:System.Int16.MaxValue?displayProperty=nameWithType> (32,767)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CShort` 関数による浮動小数点から 16 ビット整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CSng`|[Single データ型](../data-types/single-data-type.md)|負の値の場合は、-3.402823E+38 から -1.401298E-45。正の値の場合は、1.401298E-45 から 3.402823E+38。|
|`CStr`|[String データ型](../data-types/string-data-type.md)|`CStr` の戻り値は、`expression` 引数によって異なります。 「[CStr 関数の戻り値](return-values-for-the-cstr-function.md)」を参照してください。|
|`CUInt`|[UInteger データ型](../data-types/uinteger-data-type.md)|<xref:System.UInt32.MinValue?displayProperty=nameWithType> (0) から <xref:System.UInt32.MaxValue?displayProperty=nameWithType> (4,294,967,295)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CUInt` 関数による浮動小数点から符号なし整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CULng`|[ULong データ型](../data-types/ulong-data-type.md)|<xref:System.UInt64.MinValue?displayProperty=nameWithType> (0) から <xref:System.UInt64.MaxValue?displayProperty=nameWithType> (18,446,744,073,709,551,615)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CULng` 関数による浮動小数点から符号なし長整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|
|`CUShort`|[UShort データ型](../data-types/ushort-data-type.md)|<xref:System.UInt16.MinValue?displayProperty=nameWithType> (0) から <xref:System.UInt16.MaxValue?displayProperty=nameWithType> (65,535) (符号なし)。小数部は丸められます。<sup>1</sup><br/><br/>Visual Basic 15.8 以降、Visual Basic では、`CUShort` 関数による浮動小数点から符号なし 16 ビット整数への変換のパフォーマンスが最適化されます。詳細については、「[解説](#remarks)」セクションを参照してください。 例については、「[CInt の例](#cint-example)」セクションを参照してください。|

<sup>1</sup> 小数部は、*銀行型丸め*と呼ばれる特殊な種類の丸めの対象となる場合があります。 詳細については、「解説」を参照してください。

## <a name="remarks"></a>Remarks

原則として、<xref:System.Convert> クラスで、または個々の型の構造体またはクラスで、`ToString()` などの .NET Framework メソッドに優先して、Visual Basic の型変換関数を使用する必要があります。 Visual Basic 関数は、Visual Basic コードとの最適な相互作用のために設計されており、さらにそれらによって、ソースコードが短くなり、読みやすくなります。 また、.NET Framework 変換メソッドでは、常に Visual Basic 関数と同じ結果が生成されるとは限りません。たとえば、`Boolean` を `Integer` に変換する場合などです。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」を参照してください。

Visual Basic 15.8 以降、次のメソッドによって返される <xref:System.Single> または <xref:System.Double> 値を、整数変換関数 (`CByte`、`CShort`、`CInt`、`CLng`、`CSByte`、`CUShort`、`CUInt`、`CULng`) のいずれかに渡す場合に、浮動小数点から整数への変換のパフォーマンスが最適化されます。

- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Single)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Single)?displayProperty=nameWithType>
- <xref:System.Math.Ceiling(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Floor(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Round(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Truncate(System.Double)?displayProperty=nameWithType>

この最適化によって、大量の整数変換を行うコードで、実行が最大 2 倍速くなります。 次の例では、それらの最適化された浮動小数点から整数への変換を示しています。

```vb
Dim s As Single = 173.7619
Dim d As Double = s

Dim i1 As Integer = CInt(Fix(s))               ' Result: 173
Dim b1 As Byte = CByte(Int(d))                 ' Result: 173
Dim s1 AS Short = CShort(Math.Truncate(s))     ' Result: 173
Dim i2 As Integer = CInt(Math.Ceiling(d))      ' Result: 174
Dim i3 As Integer = CInt(Math.Round(s))        ' Result: 174
```

## <a name="behavior"></a>動作

- **強制型変換。** 一般に、データ型変換関数を使用すると、操作の結果を、既定のデータ型ではなく、特定のデータ型に強制的に変換することができます。 たとえば、単精度、倍精度、または整数の算術演算が通常行われるところで、`CDec` を使用して、10 進数の算術演算を強制的に実行します。

- **変換の失敗。** 関数に渡された `expression` が、変換先のデータ型の範囲外である場合、<xref:System.OverflowException> が発生します。

- **小数部。** 非整数値を整数型に変換する場合、整数変換関数 (`CByte`、`CInt`、`CLng`、`CSByte`、`CShort`、`CUInt`、`CULng`、および `CUShort`) で、小数部を削除し、値を最も近い整数に丸めます。

     小数部がちょうど 0.5 の場合、整数変換関数では、最も近い偶数の整数に丸められます。 たとえば、0.5 は 0 に丸められ、1.5 と 2.5 は両方とも 2 に丸められます。 これは、*銀行型丸め*と呼ばれることもあり、その目的は、そのような多数の数値を加算するときに累積する可能性があるバイアスを補正することです。

     `CInt` と `CLng` は、<xref:Microsoft.VisualBasic.Conversion.Int%2A> 関数や <xref:Microsoft.VisualBasic.Conversion.Fix%2A> 関数とは異なり、数値の小数部を丸めるのではなく、切り捨てます。 さらに、`Fix` と `Int` は常に、渡された同じデータ型の値を返します。

- **日付/時刻の変換。** <xref:Microsoft.VisualBasic.Information.IsDate%2A> 関数を使用して、値を日付と時刻に変換できるかどうかを判断します。 `CDate` は、日付リテラルと時刻リテラルを認識しますが、数値は認識しません。 Visual Basic 6.0 の `Date` 値を Visual Basic 2005 以降のバージョンの `Date` 値に変換するには、<xref:System.DateTime.FromOADate%2A?displayProperty=nameWithType> メソッドを使用できます。

- **ニュートラル日付/時刻値。** [Date データ型](../data-types/date-data-type.md)には、常に日付と時刻の両方の情報が格納されます。 型変換の目的で、Visual Basic では、1/1/0001 (1 年の 1 月 1 日) を日付の*ニュートラル値*、00:00:00 (午前 0 時) を時刻のニュートラル値と見なします。 `Date` 値を文字列に変換する場合、`CStr` では、結果の文字列にニュートラル値が含まれません。 たとえば、`#January 1, 0001 9:30:00#` を文字列に変換した場合、結果は "9:30:00 AM" になります。日付情報は含まれません。 ただし、日付情報は元の `Date` 値には引き続き存在しているため、<xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> 関数などの関数を使用して回復できます。

- **カルチャの感度。** 文字列に関連する型変換関数では、アプリケーションの現在のカルチャ設定に基づいて変換が実行されます。 たとえば、`CDate` では、システムのロケール設定に従って日付形式が認識されます。 ロケールの正しい順序で日、月、年を指定する必要があります。そうしないと、日付が正しく解釈されない場合があります。 "Wednesday" など、曜日の文字列が含まれている場合、長い日付形式は認識されません。

     ロケールによって指定された形式以外の形式で、値の文字列表現の変換を行う必要がある場合は、Visual Basic 型変換関数を使用できません。 これを行うには、その値の型の `ToString(IFormatProvider)` および `Parse(String, IFormatProvider)` メソッドを使用します。 たとえば、文字列を `Double` に変換する場合は <xref:System.Double.Parse%2A?displayProperty=nameWithType> を使用し、`Double` 型の値を文字列に変換する場合は <xref:System.Double.ToString%2A?displayProperty=nameWithType> を使用します。

## <a name="ctype-function"></a>CType Function

[CType 関数](ctype-function.md)は、2 つ目の引数 `typename` を受け取り、`expression` を `typename` に強制的に変換します。ここで `typename` は、それに対して有効な変換が存在する任意のデータ型、構造体、クラス、またはインターフェイスなどです。

`CType` と他の型変換キーワードとの比較については、「[DirectCast 演算子](../operators/directcast-operator.md)」と「[TryCast 演算子](../operators/trycast-operator.md)」を参照してください。

## <a name="cbool-example"></a>CBool の例

次の例では、`CBool` 関数を使用して、式を `Boolean` 値に変換しています。 式が 0 以外の値に評価される場合、`CBool` では `True` が返されます。それ以外の場合は `False` が返されます。

[!code-vb[VbVbalrFunctions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#1)]

## <a name="cbyte-example"></a>CByte の例

次の例では、`CByte` 関数を使用して、式を `Byte` に変換しています。

[!code-vb[VbVbalrFunctions#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#2)]

## <a name="cchar-example"></a>CChar の例

次の例では、`CChar` 関数を使用して、`String` 式の最初の文字を `Char` 型に変換しています。

[!code-vb[VbVbalrFunctions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#3)]

`CChar` の入力引数は、`Char` または `String` データ型である必要があります。 `CChar` を使用して数値を文字に変換することはできません。これは `CChar` では数値データ型を受け入れないためです。 次の例では、コード ポイント (文字コード) を表す数値を取得し、それを対応する文字に変換しています。 <xref:Microsoft.VisualBasic.Interaction.InputBox%2A> 関数を使用して、数字の文字列を取得し、`CInt` を使用して、文字列を `Integer` 型に変換し、`ChrW` を使用して、数値を `Char` 型に変換しています。

[!code-vb[VbVbalrFunctions#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#4)]

## <a name="cdate-example"></a>CDate の例

次の例では、`CDate` 関数を使用して、文字列を `Date` 値に変換しています。 一般に、日付と時刻を文字列としてハードコーディングする (この例に示すように) ことは推奨されません。 代わりに、#Feb 12、1969#、#4:45:23 PM# などの日付リテラルと時刻リテラルを使用します。

[!code-vb[VbVbalrFunctions#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#5)]

## <a name="cdbl-example"></a>CDbl の例

[!code-vb[VbVbalrFunctions#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#6)]

## <a name="cdec-example"></a>CDec の例

次の例では、`CDec` 関数を使用して、数値を `Decimal` に変換しています。

[!code-vb[VbVbalrFunctions#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#7)]

## <a name="cint-example"></a>CInt の例

次の例では、`CInt` 関数を使用して、値を `Integer` に変換しています。

[!code-vb[VbVbalrFunctions#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#8)]

## <a name="clng-example"></a>CLng の例

次の例では、`CLng` 関数を使用して、値を `Long` に変換しています。

[!code-vb[VbVbalrFunctions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#9)]

## <a name="cobj-example"></a>CObj の例

次の例では、`CObj` 関数を使用して、数値を `Object` に変換しています。 `Object` 変数自体には、それに代入される `Double` 値を指す 4 バイトのポインターのみが格納されます。

[!code-vb[VbVbalrFunctions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#10)]

## <a name="csbyte-example"></a>CSByte の例

次の例では、`CSByte` 関数を使用して、数値を `SByte` に変換しています。

[!code-vb[VbVbalrFunctions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#11)]

## <a name="cshort-example"></a>CShort の例

次の例では、`CShort` 関数を使用して、数値を `Short` に変換しています。

[!code-vb[VbVbalrFunctions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#12)]

## <a name="csng-example"></a>CSng の例

次の例では、`CSng` 関数を使用して、値を `Single` に変換しています。

[!code-vb[VbVbalrFunctions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#13)]

## <a name="cstr-example"></a>CStr の例

次の例では、`CStr` 関数を使用して、数値を `String` に変換しています。

[!code-vb[VbVbalrFunctions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#14)]

次の例では、`CStr` 関数を使用して、 `Date` 値を `String` 値に変換しています。

[!code-vb[VbVbalrFunctions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#15)]

`CStr` では常に、現在のロケールの標準の短い形式 ("6/15/2003 4:35:47 PM" など) で `Date` 値がレンダリングされます。 ただし `CStr` では、日付の 1/1/0001 と時刻の 00:00:00 の*ニュートラル値*が含まれません。

`CStr` によって返される値の詳細については、「[CStr 関数の戻り値](return-values-for-the-cstr-function.md)」を参照してください。

## <a name="cuint-example"></a>CUInt の例

次の例では、`CUInt` 関数を使用して、数値を `UInteger` に変換しています。

[!code-vb[VbVbalrFunctions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#16)]

## <a name="culng-example"></a>CULng の例

次の例では、`CULng` 関数を使用して、数値を `ULong` に変換しています。

[!code-vb[VbVbalrFunctions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#17)]

## <a name="cushort-example"></a>CUShort の例

次の例では、`CUShort` 関数を使用して、数値を `UShort` に変換しています。

[!code-vb[VbVbalrFunctions#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#18)]

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- <xref:Microsoft.VisualBasic.Conversion.Int%2A>
- <xref:Microsoft.VisualBasic.Conversion.Fix%2A>
- <xref:Microsoft.VisualBasic.Strings.Format%2A>
- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:Microsoft.VisualBasic.Conversion.Oct%2A>
- <xref:Microsoft.VisualBasic.Conversion.Str%2A>
- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [変換関数](conversion-functions.md)
- [Visual Basic における型変換](../../programming-guide/language-features/data-types/type-conversions.md)
