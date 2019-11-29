---
title: TimeOffset support in での DateTime と DateTimeOffset のサポート
description: System.string ライブラリでの DateTime 型と DateTimeOffset 型のサポートの概要について説明します。
ms.technology: dotnet-standard
author: layomia
ms.author: laakinri
ms.date: 07/22/2019
helpviewer_keywords:
- JSON, Serializer, Utf8
- JSON DateTime, JSON DateTimeOffset
- DateTime, DateTimeOffset
- JsonSerializer, Utf8JsonReader, Utf8JsonWriter, JsonElement, JsonDocument
- JSON Serializer, JSON Reader, JSON Writer
- Converter, JSON Converter, DateTime Converter
- ISO, ISO 8601, ISO 8601-1:2019
ms.openlocfilehash: 04e0e3c613b194ac85241d50d3bc5fd5dc0b6e54
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73977325"
---
# <a name="datetime-and-datetimeoffset-support-in-systemtextjson"></a>TimeOffset support in での DateTime と DateTimeOffset のサポート

System.string ライブラリは、ISO 8601:-2019 拡張プロファイルに従って、<xref:System.DateTime> と <xref:System.DateTimeOffset> の値を解析して書き込みます。
[コンバーター](xref:System.Text.Json.Serialization.JsonConverter%601)は、<xref:System.Text.Json.JsonSerializer>によるシリアル化と逆シリアル化のためのカスタムサポートを提供します。
<xref:System.Text.Json.Utf8JsonReader> と <xref:System.Text.Json.Utf8JsonWriter>を使用する場合は、カスタムサポートを実装することもできます。

## <a name="support-for-the-iso-8601-12019-format"></a>ISO 8601-1:2019 形式のサポート

<xref:System.Text.Json.JsonSerializer>、<xref:System.Text.Json.Utf8JsonReader>、<xref:System.Text.Json.Utf8JsonWriter>、および <xref:System.Text.Json.JsonElement> の種類では、ISO 8601-1:2019 形式の拡張プロファイルに従って、<xref:System.DateTime> と <xref:System.DateTimeOffset> のテキスト表現を解析して記述します。たとえば、2019-07-26T16:59:57-05:00 のようになります。

<xref:System.DateTime> と <xref:System.DateTimeOffset> のデータは <xref:System.Text.Json.JsonSerializer>でシリアル化できます。

[!code-csharp[example-serializing-with-jsonserializer](~/samples/snippets/standard/datetime/json/csharp/serializing-with-jsonserializer/Program.cs)]

また、<xref:System.Text.Json.JsonSerializer>で逆シリアル化することもできます。

[!code-csharp[example-deserializing-with-jsonserializer-valid](~/samples/snippets/standard/datetime/json/csharp/deserializing-with-jsonserializer-valid/Program.cs)]

既定のオプションでは、入力 <xref:System.DateTime> と <xref:System.DateTimeOffset> テキスト表現は、拡張 ISO 8601-1:2019 プロファイルに準拠している必要があります。
プロファイルに準拠していない表現を逆シリアル化しようとすると、<xref:System.Text.Json.JsonSerializer> によって <xref:System.Text.Json.JsonException>がスローされます。

[!code-csharp[example-deserializing-with-jsonserializer-error](~/samples/snippets/standard/datetime/json/csharp/deserializing-with-jsonserializer-error/Program.cs)]

<xref:System.Text.Json.JsonDocument> は、<xref:System.DateTime> や <xref:System.DateTimeOffset> 表現など、JSON ペイロードのコンテンツへの構造化されたアクセスを提供します。 次の例では、温度のコレクションを指定した場合に、月曜日の平均温度を計算できる方法を示しています。

[!code-csharp[example-computing-with-jsondocument-valid](~/samples/snippets/standard/datetime/json/csharp/computing-with-jsondocument-valid/Program.cs)]

準拠していない <xref:System.DateTime> 表現を持つペイロードで平均温度を計算しようとすると、<xref:System.Text.Json.JsonDocument> によって <xref:System.FormatException>がスローされます。

[!code-csharp[example-computing-with-jsondocument-error](~/samples/snippets/standard/datetime/json/csharp/computing-with-jsondocument-error/Program.cs)]

下位レベルの <xref:System.Text.Json.Utf8JsonWriter> は、データ <xref:System.DateTime> と <xref:System.DateTimeOffset> を書き込みます。

[!code-csharp[example-writing-with-utf8jsonwriter](~/samples/snippets/standard/datetime/json/csharp/writing-with-utf8jsonwriter/Program.cs)]

<xref:System.Text.Json.Utf8JsonReader> は、<xref:System.DateTime> と <xref:System.DateTimeOffset> データを解析します。

[!code-csharp[example-reading-with-utf8jsonreader-valid](~/samples/snippets/standard/datetime/json/csharp/reading-with-utf8jsonreader-valid/Program.cs)]

<xref:System.Text.Json.Utf8JsonReader> に準拠していない形式を読み取ろうとすると、<xref:System.FormatException>がスローされます。

[!code-csharp[example-reading-with-utf8jsonreader-error](~/samples/snippets/standard/datetime/json/csharp/reading-with-utf8jsonreader-error/Program.cs)]

## <a name="custom-support-for-xrefsystemdatetime-and-xrefsystemdatetimeoffset"></a><xref:System.DateTime> および <xref:System.DateTimeOffset> のカスタムサポート

### <a name="when-using-xrefsystemtextjsonjsonserializer"></a><xref:System.Text.Json.JsonSerializer> を使用する場合

シリアライザーでカスタムの解析または書式設定を実行する場合は、[カスタムコンバーター](xref:System.Text.Json.Serialization.JsonConverter%601)を実装できます。
いくつかの例を次に示します。

#### <a name="using-datetimeoffsetparse-and-datetimeoffsettostring"></a>`DateTime(Offset).Parse` と `DateTime(Offset).ToString` の使用

入力 <xref:System.DateTime> の形式や <xref:System.DateTimeOffset> テキスト表現を特定できない場合は、コンバーターの読み取りロジックで `DateTime(Offset).Parse` メソッドを使用できます。 これにより、を使用できるようになります。さまざまな <xref:System.DateTime> および <xref:System.DateTimeOffset> テキスト形式を解析するための広範なサポート (ISO 8601 以外の文字列や iso 8601 形式の拡張 ISO 8601-1:2019 プロファイルに準拠していない)。 この方法では、シリアライザーのネイティブ実装よりもパフォーマンスが大幅に低下します。

シリアル化の場合は、コンバーター書き込みロジックで `DateTime(Offset).ToString` メソッドを使用できます。 これにより、[標準の日付と時刻の形式](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings)、および[カスタムの日付と時刻](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings)の形式を使用して、<xref:System.DateTime> と <xref:System.DateTimeOffset> の値を書き込むことができます。
これは、シリアライザーのネイティブ実装を使用する場合よりも、パフォーマンスが大幅に低下します。

[!code-csharp[example-showing-datetime-parse](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example1/Program.cs)]

> [!NOTE]
> <xref:System.Text.Json.Serialization.JsonConverter%601>を実装し、`T` を <xref:System.DateTime>場合、`typeToConvert` パラメーターは常に `typeof(DateTime)`になります。
パラメーターは、ポリモーフィックなケースを処理する場合や、ジェネリックを使用してパフォーマンスの高い方法で `typeof(T)` を取得する場合に便利です。

#### <a name="using-xrefsystembufferstextutf8parser-and-xrefsystembufferstextutf8formatter"></a><xref:System.Buffers.Text.Utf8Parser> と <xref:System.Buffers.Text.Utf8Formatter> の使用

入力 <xref:System.DateTime> または <xref:System.DateTimeOffset> テキスト表現が "R"、"l"、"O"、"G" のいずれかの[標準の日時書式指定文字列](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings)に準拠している場合、またはこれらの形式のいずれかに従って記述する場合は、コンバーターロジックで utf-8 ベースの高速な解析および書式指定メソッドを使用できます。 これは `DateTime(Offset).Parse` と `DateTime(Offset).ToString`を使用するよりもはるかに高速です。

次の例は、 ["R" 標準形式](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-rfc1123-r-r-format-specifier)に従って <xref:System.DateTime> 値をシリアル化および逆シリアル化するカスタムコンバーターを示しています。

[!code-csharp[example-showing-utf8-parser-and-formatter](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example2/Program.cs)]

> [!NOTE]
> "R" 標準形式の長さは常に29文字です。

#### <a name="using-datetimeoffsetparse-as-a-fallback-to-the-serializers-native-parsing"></a>シリアライザーのネイティブ解析へのフォールバックとしての `DateTime(Offset).Parse` の使用

入力 <xref:System.DateTime> または <xref:System.DateTimeOffset> データが拡張 ISO 8601-1:2019 プロファイルに準拠していると予想される場合は、シリアライザーのネイティブ解析ロジックを使用できます。 また、場合によっては、フォールバックメカニズムを実装することもできます。
この例では、<xref:System.Text.Json.Utf8JsonReader.TryGetDateTime(System.DateTime@)>を使用して <xref:System.DateTime> テキスト表現の解析に失敗した後、コンバーターが <xref:System.DateTime.Parse(System.String)>を使用してデータを正常に解析することを示しています。

[!code-csharp[example-showing-datetime-parse-as-fallback](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example3/Program.cs)]

### <a name="when-writing-with-xrefsystemtextjsonutf8jsonwriter"></a><xref:System.Text.Json.Utf8JsonWriter> を使用して書き込む場合

カスタム <xref:System.DateTime> を作成する場合、または <xref:System.Text.Json.Utf8JsonWriter>でテキスト表現を <xref:System.DateTimeOffset> する場合は、カスタム表現を <xref:System.String>、`ReadOnlySpan<Byte>`、`ReadOnlySpan<Char>`、または <xref:System.Text.Json.JsonEncodedText>に書式設定し、それを対応する[Utf8JsonWriter](https://docs.microsoft.com/dotnet/api/system.text.json.utf8jsonwriter.writestringvalue?view=netcore-3.0)または[WriteString](https://docs.microsoft.com/dotnet/api/system.text.json.utf8jsonwriter.writestring?view=netcore-3.0)メソッドに渡すことができます。

次の例では、<xref:System.DateTime.ToString(System.String,System.IFormatProvider)>でカスタムの <xref:System.DateTime> 形式を作成し、<xref:System.Text.Json.Utf8JsonWriter.WriteStringValue(System.String)> メソッドを使用して記述する方法を示します。

[!code-csharp[example-custom-writing-with-utf8jsonwriter](~/samples/snippets/standard/datetime/json/csharp/custom-writing-with-utf8jsonwriter/Program.cs)]

### <a name="when-reading-with-xrefsystemtextjsonutf8jsonreader"></a><xref:System.Text.Json.Utf8JsonReader> を使用した読み取り時

カスタム <xref:System.DateTime> を読み取る場合や、<xref:System.Text.Json.Utf8JsonReader>でテキスト表現を <xref:System.DateTimeOffset> する場合は、<xref:System.Text.Json.Utf8JsonReader.GetString>を使用して現在の JSON トークンの値を <xref:System.String> として取得し、その値をカスタムロジックを使用して解析することができます。

次の例では、<xref:System.Text.Json.Utf8JsonReader.GetString>を使用してカスタム <xref:System.DateTimeOffset> テキスト表現を取得し、<xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)>を使用して解析する方法を示します。

[!code-csharp[example-custom-reading-with-utf8jsonreader](~/samples/snippets/standard/datetime/json/csharp/custom-reading-with-utf8jsonreader/Program.cs)]

## <a name="the-extended-iso-8601-12019-profile-in-systemtextjson"></a>System.string の拡張された ISO 8601-1:2019 プロファイル

### <a name="date-and-time-components"></a>日付と時刻のコンポーネント

<xref:System.Text.Json> で実装されている拡張 ISO 8601-1:2019 プロファイルは、日付と時刻の表現に対して次のコンポーネントを定義します。 これらのコンポーネントは、<xref:System.DateTime> と <xref:System.DateTimeOffset> 表現を解析および書式設定するときにサポートされるさまざまな粒度レベルを定義するために使用されます。

| コンポーネント       | 形式                      | 説明                                                                     |
|-----------------|-----------------------------|---------------------------------------------------------------------------------|
| Year            | "yyyy"                      | 0001-9999                                                                       |
| 月           | "MM"                        | 01-12                                                                           |
| Day             | "dd"                        | 01-28、01-29、01-30、01-31 (月/年)                                  |
| Hour            | "HH"                        | 00-23                                                                           |
| Minute          | "mm"                        | 00-59                                                                           |
| Second          | "ss"                        | 00-59                                                                           |
| 2番目の分数 | "FFFFFFF"                   | 最低1桁、最大16桁                                      |
| 時間のオフセット     | "K"                         | "Z" または "(' + '/'-') HH ': ' mm '                                                |
| 部分的な時間    | "HH ': ' mm ': ' ss [FFFFFFF]"     | UTC オフセット情報なしの時間                                             |
| 完全な日付       | "yyyy'-'mm'-'dd't'hh-' MM'-' dd"            | カレンダーの日付                                                                   |
| フルタイム       | "Partial time'K"           | 現地時刻と UTC の時差を使用した日の UTC または現地時刻 |
| 日付/時刻       | "' 完全な日付 ' ' ' ' ' ' ' は完全な時刻 '" になります。 | カレンダーの日付と時刻。例: 2019-07-26T16:59:57-05:00                   |

### <a name="support-for-parsing"></a>解析のサポート

解析のために次の粒度のレベルが定義されています。

1. ' 完全な日付 '
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' dd"

2. "' Full date ' ' ' Hour ' ': ' ' Minute '"
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' + ': ' MM '

3. "' 完全な日付 ' t ' ' Partial time '"
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss ' ([並べ替え可能な (" s ") 書式指定子](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-sortable-s-format-specifier))
    2. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFF

4. "' Full date ' ' ' Time Time ' ': ' ' Minute ' ' Time offset '"
    1. "yyyy'-'mm'-'dd't'hh-" MM'-' Dd' T' HH ': ' mmZ "
    2. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' Hh ': ' mm (' + '/'-') HH ': ' mm '

5. ' 日時 '
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ssZ '
    2. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFFZ "
    3. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' mm ': ' ss (' + '/'-') HH ': ' mm '
    4. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFF (' + '/'-') HH ': ' mm "

秒の小数部がある場合は、少なくとも1つの数字が必要です。`2019-07-26T00:00:00.` は許可されていません。
最大16桁の小数部を使用できますが、最初の7だけが解析されます。 それを超えるものはゼロと見なされます。
たとえば、`2019-07-26T00:00:00.1234567890` は `2019-07-26T00:00:00.1234567`であるかのように解析されます。
これは、この解決に限定される <xref:System.DateTime> の実装との互換性を維持するためのものです。

うるう秒はサポートされていません。

### <a name="support-for-formatting"></a>書式設定のサポート

次の粒度レベルは、書式設定のために定義されています。

1. "' 完全な日付 ' t ' ' Partial time '"
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss ' ([並べ替え可能な (" s ") 書式指定子](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-sortable-s-format-specifier))

        秒の小数部を含まない <xref:System.DateTime> の書式を設定し、オフセット情報を使用しないようにします。

    2. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFF

        秒の小数部のオフセット情報を含まない <xref:System.DateTime> の書式を設定するために使用します。

2. ' 日時 '
    1. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ssZ '

        秒の小数部を除いて、UTC オフセットを使用して <xref:System.DateTime> を書式設定するために使用します。

    2. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFFZ "

        秒の小数部と UTC オフセットを使用して <xref:System.DateTime> の書式を設定するために使用します。

    3. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' mm ': ' ss (' + '/'-') HH ': ' mm '

        秒の小数部を除いて、ローカルオフセットを使用して、<xref:System.DateTime> または <xref:System.DateTimeOffset> を書式設定するために使用します。

    4. "yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss '. 'FFFFFFF (' + '/'-') HH ': ' mm "

        秒の小数部とローカルオフセットを使用して、<xref:System.DateTime> または <xref:System.DateTimeOffset> の書式を設定するために使用します。

存在する場合は、最大7桁の小数部が書き込まれます。 これは、この解決に限定される <xref:System.DateTime> の実装と一致します。
