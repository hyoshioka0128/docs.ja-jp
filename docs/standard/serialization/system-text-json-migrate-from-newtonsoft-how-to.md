---
title: Newtonsoft.Json から System.Text.Json に移行する - .NET
author: tdykstra
ms.author: tdykstra
no-loc:
- System.Text.Json
- Newtonsoft.Json
ms.date: 01/10/2020
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: fe370b34d311816a815f3b2d419751ac7871f013
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "83703582"
---
# <a name="how-to-migrate-from-newtonsoftjson-to-systemtextjson"></a>Newtonsoft.Json から System.Text.Json に移行する方法

この記事では、[Newtonsoft.Json](https://www.newtonsoft.com/json) から <xref:System.Text.Json> に移行する方法を示します。

`System.Text.Json` 名前空間は、JavaScript Object Notation (JSON) との間でのシリアル化と逆シリアル化の機能を提供します。 `System.Text.Json` ライブラリは、[.NET Core 3.0](https://aka.ms/netcore3download) 共有フレームワークに含まれています。 その他のターゲット フレームワークの場合は、[System.Text.Json](https://www.nuget.org/packages/System.Text.Json) NuGet パッケージをインストールします。 このパッケージで以下がサポートされます。

* .NET Standard 2.0 以降のバージョン
* .NET Framework 4.7.2 以降のバージョン
* .NET Core 2.0、2.1、および 2.2

`System.Text.Json` は、主にパフォーマンス、セキュリティ、標準への準拠に焦点を当てています。 これには既定の動作について重要な違いがいくつかあり、`Newtonsoft.Json` との機能パリティを持つことがこの目的ではありません。 一部のシナリオでは、`System.Text.Json` に組み込み機能がなくても、推奨される回避策があります。 それ以外のシナリオでは、回避策は実用的ではありません。 お使いのアプリケーションで、欠如している機能を利用する必要がある場合は、ご自分のシナリオのサポートを追加できるかどうかを確認するために、[問題を申請](https://github.com/dotnet/runtime/issues/new)することを検討してください。

<!-- For information about which features might be added in future releases, see the [Roadmap](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md). [Restore this when the roadmap is updated.]-->

この記事のほとんどの内容は、<xref:System.Text.Json.JsonSerializer> API の使用方法に関するものですが、<xref:System.Text.Json.JsonDocument> (ドキュメント オブジェクト モデル: DOM を表します)、<xref:System.Text.Json.Utf8JsonReader>、<xref:System.Text.Json.Utf8JsonWriter> の型の使用方法に関するガイダンスも含まれています。

## <a name="table-of-differences-between-newtonsoftjson-and-systemtextjson"></a>Newtonsoft.Json と System.Text.Json の相違点の表

次の表は、`Newtonsoft.Json` の機能と、それと同等の `System.Text.Json` の機能を一覧にしたものです。 同等機能は次のカテゴリに分けられます。

* 組み込み機能によってサポートされています。 `System.Text.Json` で同様の動作を得るには、属性またはグローバル オプションの使用が必要になる場合があります。
* サポートされていませんが、回避策を適用できます。 回避策とは[カスタム コンバーター](system-text-json-converters-how-to.md)のことですが、これによって `Newtonsoft.Json` の機能との完全なパリティが得られるとは限りません。 これらの一部については、サンプル コードが例として提供されます。 `Newtonsoft.Json` のこれらの機能を利用する必要がある場合、移行するには、.NET オブジェクト モデルに対する変更やその他のコード変更が必要になります。
* サポートされていません。回避策は実用的でないか不可能です。 `Newtonsoft.Json` のこれらの機能を利用する必要がある場合、移行を可能にするには大幅な変更が必要です。

| Newtonsoft.Json の機能                               | System.Text.Json での同等機能 |
|-------------------------------------------------------|-----------------------------|
| 既定での大文字と小文字の区別のない逆シリアル化           | ✔️ [PropertyNameCaseInsensitive グローバル設定](#case-insensitive-deserialization) |
| キャメルケースのプロパティ名                             | ✔️ [PropertyNamingPolicy グローバル設定](system-text-json-how-to.md#use-camel-case-for-all-json-property-names) |
| 最小限の文字のエスケープ                            | ✔️ [厳密な文字エスケープ、構成可能](#minimal-character-escaping) |
| `NullValueHandling.Ignore` グローバル設定             | ✔️ [IgnoreNullValues グローバル オプション](system-text-json-how-to.md#exclude-all-null-value-properties) |
| コメントを許可する                                        | ✔️ [ReadCommentHandling グローバル設定](#comments) |
| 末尾のコンマを許可する                                 | ✔️ [AllowTrailingCommas グローバル設定](#trailing-commas) |
| カスタム コンバーターの登録                         | ✔️ [優先順位の順序が異なる](#converter-registration-precedence) |
| 既定では最大深度がない                           | ✔️ [既定の最大深度は 64、構成可能](#maximum-depth) |
| さまざまな型のサポート                    | ⚠️ [一部の型にはカスタム コンバーターが必要である](#types-without-built-in-support) |
| 文字列を数値として逆シリアル化する                        | ⚠️ [サポートされていない、回避策、サンプル](#quoted-numbers) |
| 文字列以外のキーを含む `Dictionary` を逆シリアル化する          | ⚠️ [サポートされていない、回避策、サンプル](#dictionary-with-non-string-key) |
| ポリモーフィックなシリアル化                             | ⚠️ [サポートされていない、回避策、サンプル](#polymorphic-serialization) |
| ポリモーフィックな逆シリアル化                           | ⚠️ [サポートされていない、回避策、サンプル](#polymorphic-deserialization) |
| 推論された型を `object` のプロパティに逆シリアル化する      | ⚠️ [サポートされていない、回避策、サンプル](#deserialization-of-object-properties) |
| JSON の `null` リテラルを null 非許容値の型に逆シリアル化する | ⚠️ [サポートされていない、回避策、サンプル](#deserialize-null-to-non-nullable-type) |
| 不変のクラスと構造体への逆シリアル化          | ⚠️ [サポートされていない、回避策、サンプル](#deserialize-to-immutable-classes-and-structs) |
| `[JsonConstructor]` 属性                         | ⚠️ [サポートされていない、回避策、サンプル](#specify-constructor-to-use) |
| `[JsonProperty]` 属性での `Required` の設定        | ⚠️ [サポートされていない、回避策、サンプル](#required-properties) |
| `[JsonProperty]` 属性での `NullValueHandling` の設定 | ⚠️ [サポートされていない、回避策、サンプル](#conditionally-ignore-a-property)  |
| `[JsonProperty]` 属性での `DefaultValueHandling` の設定 | ⚠️ [サポートされていない、回避策、サンプル](#conditionally-ignore-a-property)  |
| `DefaultValueHandling` グローバル設定                 | ⚠️ [サポートされていない、回避策、サンプル](#conditionally-ignore-a-property) |
| プロパティを除外するための `DefaultContractResolver`       | ⚠️ [サポートされていない、回避策、サンプル](#conditionally-ignore-a-property) |
| `DateTimeZoneHandling`、`DateFormatString` の設定   | ⚠️ [サポートされていない、回避策、サンプル](#specify-date-format) |
| コールバック                                             | ⚠️ [サポートされていない、回避策、サンプル](#callbacks) |
| パブリックおよび非パブリック フィールドのサポート              | ⚠️ [サポートされていない、回避策](#public-and-non-public-fields) |
| 内部およびプライベートのプロパティのセッターとゲッターのサポート | ⚠️ [サポートされていない、回避策](#internal-and-private-property-setters-and-getters) |
| `JsonConvert.PopulateObject` メソッド                   | ⚠️ [サポートされていない、回避策](#populate-existing-objects) |
| `ObjectCreationHandling` グローバル設定               | ⚠️ [サポートされていない、回避策](#reuse-rather-than-replace-properties) |
| セッターなしでコレクションに追加する                    | ⚠️ [サポートされていない、回避策](#add-to-collections-without-setters) |
| `PreserveReferencesHandling` グローバル設定           | ❌ [サポートされていない](#preserve-object-references-and-handle-loops) |
| `ReferenceLoopHandling` グローバル設定                | ❌ [サポートされていない](#preserve-object-references-and-handle-loops) |
| `System.Runtime.Serialization` 属性のサポート | ❌ [サポートされていない](#systemruntimeserialization-attributes) |
| `MissingMemberHandling` グローバル設定                | ❌ [サポートされていない](#missingmemberhandling) |
| 引用符なしのプロパティ名を許可する                   | ❌ [サポートされていない](#json-strings-property-names-and-string-values) |
| 文字列値を囲む単一引用符を許可する              | ❌ [サポートされていない](#json-strings-property-names-and-string-values) |
| 文字列のプロパティに対して文字列ではない JSON 値を許可する    | ❌ [サポートされていない](#non-string-values-for-string-properties) |

これは `Newtonsoft.Json` 機能の包括的なリストではありません。 この一覧には、[GitHub の問題](https://github.com/dotnet/runtime/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json)または [StackOverflow](https://stackoverflow.com/questions/tagged/system.text.json) の投稿でリクエストされたシナリオの多くが含まれています。 ここに一覧表示されたシナリオのうち、現在サンプル コードがないシナリオの 1 つに回避策を実装する場合、およびご自分の解決策を共有する場合は、このページの下部にある **[フィードバック]** セクションで **[このページ]** を選択してください。 これにより、問題がこのドキュメントの GitHub リポジトリに作成され、このページの **[フィードバック]** セクションにも記載されます。

## <a name="differences-in-default-jsonserializer-behavior-compared-to-newtonsoftjson"></a>Newtonsoft.Json と比較した既定の JsonSerializer の動作の相違点

既定では <xref:System.Text.Json> は厳格であり、確定的な動作を重視して、呼び出し元のために推測や解釈は行われません。 このライブラリは、パフォーマンスとセキュリティを確保するために意図的にこのように設計されています。 `Newtonsoft.Json` は既定で柔軟性を持っています。 設計上のこの基本的な違いが、既定の動作における次のような固有の相違点の多くで、その背景にあります。

### <a name="case-insensitive-deserialization"></a>大文字と小文字の区別のない逆シリアル化

逆シリアル化中、`Newtonsoft.Json` では、大文字と小文字の区別のないプロパティ名の照合が既定で行われます。 <xref:System.Text.Json> の既定では大文字と小文字が区別されます。完全一致が行われるため、これによってパフォーマンスが向上します。 大文字と小文字の区別のない照合の実行方法については、「[大文字と小文字を区別しないプロパティ照合](system-text-json-how-to.md#case-insensitive-property-matching)」を参照してください。

ASP.NET Core を使用して `System.Text.Json` を間接的に使用している場合、`Newtonsoft.Json` のような動作を得るために何かをする必要はありません。 ASP.NET Core では、`System.Text.Json` を使用するときに、[Camel 形式のプロパティ名](system-text-json-how-to.md#use-camel-case-for-all-json-property-names)および大文字と小文字を区別しない照合のための設定が指定されます。

### <a name="minimal-character-escaping"></a>最小限の文字のエスケープ

シリアル化中、`Newtonsoft.Json` では文字をエスケープしないままにすることが比較的許容されています。 つまり、`xxxx` が文字のコード ポイントである場合、その文字が `\uxxxx` には置き換えられません。 文字がエスケープされる場合、その文字の前に `\` が出力されます (たとえば、`"` は `\"` になります)。 <xref:System.Text.Json> の場合、既定でより多くの文字がエスケープされ、クロスサイト スクリプティング (XSS) や情報漏えいの攻撃に対する多層防御保護が実現します。そのために 6 文字のシーケンスが使用されます。 `System.Text.Json` では、既定で ASCII 以外の文字がすべてエスケープされるため、`Newtonsoft.Json` で `StringEscapeHandling.EscapeNonAscii` を使用している場合は、何もする必要はありません。 また、`System.Text.Json` では、既定で HTML に影響する文字もエスケープされます。 `System.Text.Json` の既定の動作をオーバーライドする方法については、「[文字エンコードをカスタマイズする](system-text-json-how-to.md#customize-character-encoding)」を参照してください。

### <a name="comments"></a>コメント

逆シリアル化中、`Newtonsoft.Json` では既定で JSON 内のコメントは無視されます。 <xref:System.Text.Json> の既定では、コメントに対して例外がスローされます。[RFC 8259](https://tools.ietf.org/html/rfc8259) 仕様にそれが含まれていないためです。 コメントを許可する方法については、「[コメントと末尾のコンマを許可する](system-text-json-how-to.md#allow-comments-and-trailing-commas)」を参照してください。

### <a name="trailing-commas"></a>末尾のコンマ

逆シリアル化中、`Newtonsoft.Json` では既定で末尾のコンマは無視されます。 また、複数の末尾のコンマ (たとえば、`[{"Color":"Red"},{"Color":"Green"},,]`) も無視されます。 <xref:System.Text.Json> の既定では、末尾のコンマに対して例外がスローされます。[RFC 8259](https://tools.ietf.org/html/rfc8259) 仕様でそれが許可されていないためです。 `System.Text.Json` で受け入れられるようにする方法については、「[コメントと末尾のコンマを許可する](system-text-json-how-to.md#allow-comments-and-trailing-commas)」を参照してください。 複数の末尾のコンマが許可されるようにする方法はありません。

### <a name="converter-registration-precedence"></a>コンバーターの登録の優先順位

`Newtonsoft.Json` でのカスタム コンバーターの登録の優先順位は次のとおりです。

* プロパティの属性
* 型の属性
* [Converters](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializerSettings_Converters.htm) コレクション

この順序は、`Converters` コレクション内のカスタム コンバーターが、型レベルの属性を適用して登録されたコンバーターによってオーバーライドされることを意味します。 これらの登録はどちらも、プロパティ レベルの属性によってオーバーライドされます。

<xref:System.Text.Json> でのカスタム コンバーターの登録の優先順位は異なります。

* プロパティの属性
* <xref:System.Text.Json.JsonSerializerOptions.Converters> コレクション
* 型の属性

ここでの違いは、`Converters` コレクション内のカスタム コンバーターによって型レベルの属性がオーバーライドされる点です。 この優先順位の背後にある意図は、実行時の変更によって設計時の選択がオーバーライドされるようにすることです。 優先順位を変更する方法はありません。

カスタム コンバーターの登録の詳細については、「[カスタム コンバーターを登録する](system-text-json-converters-how-to.md#register-a-custom-converter)」を参照してください。

### <a name="maximum-depth"></a>最大の深さ

`Newtonsoft.Json` の場合、既定では最大の深さの制限はありません。 <xref:System.Text.Json> の場合、64 という既定の制限があり、<xref:System.Text.Json.JsonSerializerOptions.MaxDepth?displayProperty=nameWithType> を設定して構成できます。

### <a name="json-strings-property-names-and-string-values"></a>JSON 文字列 (プロパティ名と文字列値)

逆シリアル化中、`Newtonsoft.Json` では、二重引用符か単一引用符で囲まれた、または引用符なしのプロパティ名が受け取入れられます。 文字列値は、二重引用符または単一引用符で囲まれたものが受け入れられます。 たとえば、`Newtonsoft.Json` では次の JSON が受け入れられます。

```json
{
  "name1": "value",
  'name2': "value",
  name3: 'value'
}
```

`System.Text.Json` では、二重引用符で囲まれたプロパティ名と文字列値のみが受け入れられます。この形式が [RFC 8259](https://tools.ietf.org/html/rfc8259) 仕様で要求されており、有効な JSON と見なされる唯一の形式であるためです。

値を単一引用符で囲むと、次のメッセージと共に [JsonException](xref:System.Text.Json.JsonException) が発生します。

```
''' is an invalid start of a value.
```

### <a name="non-string-values-for-string-properties"></a>文字列プロパティに対する文字列以外の値

`Newtonsoft.Json` では、文字列型のプロパティへの逆シリアル化の場合、数値やリテラル `true` と `false` など、文字列以外の値が受け入れられます。 `Newtonsoft.Json` で次のクラスへの逆シリアル化が正常に行われてる JSON の例を、以下に示します。

```json
{
  "String1": 1,
  "String2": true,
  "String3": false
}
```

```csharp
public class ExampleClass
{
    public string String1 { get; set; }
    public string String2 { get; set; }
    public string String3 { get; set; }
}
```

`System.Text.Json` では、文字列以外の値は文字列プロパティに逆シリアル化されません。 文字列フィールドに対して文字列以外の値を受け取ると、次のメッセージと共に [JsonException](xref:System.Text.Json.JsonException) が発生します。

```
The JSON value could not be converted to System.String.
```

## <a name="scenarios-using-jsonserializer-that-require-workarounds"></a>回避策を必要とする JsonSerializer を使用するシナリオ

次のシナリオは、組み込み機能ではサポートされていませんが、回避策を適用できます。 回避策とは[カスタム コンバーター](system-text-json-converters-how-to.md)のことですが、これによって `Newtonsoft.Json` の機能との完全なパリティが得られるとは限りません。 これらの一部については、サンプル コードが例として提供されます。 `Newtonsoft.Json` のこれらの機能を利用する必要がある場合、移行するには、.NET オブジェクト モデルに対する変更やその他のコード変更が必要になります。

### <a name="types-without-built-in-support"></a>組み込みサポートのない型

<xref:System.Text.Json> には、次の型に対する組み込みサポートはありません。

* <xref:System.Data.DataTable> および関連する型
* F# の型 ([判別共用体](../../fsharp/language-reference/discriminated-unions.md)、[レコード型](../../fsharp/language-reference/records.md)、[匿名レコード型](../../fsharp/language-reference/anonymous-records.md)など)。
* <xref:System.Dynamic.ExpandoObject>
* <xref:System.TimeZoneInfo>
* <xref:System.Numerics.BigInteger>
* <xref:System.TimeSpan>
* <xref:System.DBNull>
* <xref:System.Type>
* <xref:System.ValueTuple> およびそれに関連付けられているジェネリック型

カスタム コンバーターは、組み込みサポートのない型に対して実装できます。

### <a name="quoted-numbers"></a>引用符で囲まれた数値

`Newtonsoft.Json` では、JSON 文字列によって表された (引用符で囲まれた) 数値をシリアル化または逆シリアル化できます。 たとえば、`{"DegreesCelsius":23}` ではなく `{"DegreesCelsius":"23"}` を受け入れることができます。 <xref:System.Text.Json> でこの動作を有効にするには、次の例のようなカスタム コンバーターを実装します。 このコンバーターでは、`long` として定義されたプロパティが処理されます。

* JSON 文字列としてシリアル化されます。
* 逆シリアル化中に、JSON の数値と引用符で囲まれた数値が受け入れられます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/LongToStringConverter.cs)]

このカスタム コンバーターを登録するには、個々の `long` プロパティで[属性を使用](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property)するか、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーター を追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

### <a name="dictionary-with-non-string-key"></a>文字列以外のキーを含むディクショナリ

`Newtonsoft.Json` では、`Dictionary<TKey, TValue>` 型のコレクションがサポートされます。 <xref:System.Text.Json> では、ディクショナリ コレクションに対する組み込みサポートは `Dictionary<string, TValue>` に限定されています。 つまり、キーは文字列である必要があります。

キーとして整数やその他の型を含むディクショナリをサポートするには、[カスタム コンバーターを記述する方法](system-text-json-converters-how-to.md#support-dictionary-with-non-string-key)に関する記事の例にあるようなコンバーターを作成します。

### <a name="polymorphic-serialization"></a>ポリモーフィックなシリアル化

`Newtonsoft.Json` では、ポリモーフィックなシリアル化が自動的に行われます。 <xref:System.Text.Json> の制限付きのポリモーフィックなシリアル化機能については、「[派生クラスのプロパティのシリアル化](system-text-json-how-to.md#serialize-properties-of-derived-classes)」を参照してください。

そこで説明されている回避策は、派生クラスを含むことができるプロパティを、`object` 型として定義することです。 これが不可能な場合、別のオプションとして、[カスタム コンバーターを記述する方法](system-text-json-converters-how-to.md#support-polymorphic-deserialization)に関する記事の例にあるような、継承型階層全体に対する `Write` メソッドを使用してコンバーターを作成する方法があります。

### <a name="polymorphic-deserialization"></a>ポリモーフィックな逆シリアル化

`Newtonsoft.Json` には、シリアル化中に型名のメタデータを JSON に追加する `TypeNameHandling` 設定があります。 これは、逆シリアル化中にそのメタデータを使用して、ポリモーフィックな逆シリアル化を行います。 <xref:System.Text.Json> では限定された範囲の[ポリモーフィックなシリアル化](system-text-json-how-to.md#serialize-properties-of-derived-classes)を行うことができますが、ポリモーフィックな逆シリアル化を行うことはできません。

ポリモーフィックな逆シリアル化をサポートするには、[カスタム コンバーターを記述する方法](system-text-json-converters-how-to.md#support-polymorphic-deserialization)に関する記事の例にあるようなコンバーターを作成します。

### <a name="deserialization-of-object-properties"></a>オブジェクト プロパティの逆シリアル化

`Newtonsoft.Json` では、<xref:System.Object> への逆シリアル化中に以下が行われます。

* JSON ペイロード内のプリミティブ値 (`null` 以外) の型を推測し、格納されている `string`、`long`、`double`、`boolean`、または `DateTime` をボックス化されたオブジェクトとして返します。 "*プリミティブ値*" は、JSON の数値、文字列、`true`、`false`、`null` などの 1 つの JSON 値です。
* JSON ペイロード内の複合値の `JObject` または `JArray` を返します。 "*複合値*" は、中かっこ (`{}`) 内の JSON のキーと値のペアのコレクション、または角かっこ (`[]`) 内の値のリストです。 中かっこまたは角かっこ内のプロパティと値には、追加のプロパティまたは値を含めることができます。
* ペイロードに `null` JSON リテラルが含まれている場合は、null 参照を返します。

<xref:System.Text.Json> では、<xref:System.Object> への逆シリアル化中には常に、プリミティブと複合の両方の値に対してボックス化された `JsonElement` が格納されます。例えば、以下のようなものです。

* `object` プロパティ。
* `object` ディクショナリ値。
* `object` 配列値。
* ルート `object`。

ただし、`System.Text.Json` では `null` が `Newtonsoft.Json` と同じ方法で処理され、ペイロードに `null` JSON リテラルが含まれている場合は null 参照が返されます。

`object` プロパティに型の推定を実装するには、[カスタム コンバーターを記述する方法](system-text-json-converters-how-to.md#deserialize-inferred-types-to-object-properties)に関する記事の例にあるようなコンバーターを作成します。

### <a name="deserialize-null-to-non-nullable-type"></a>null を null 非許容型に逆シリアル化する

`Newtonsoft.Json` では、次のシナリオでは例外がスローされません。

* `NullValueHandling` が `Ignore` に設定されている。さらに
* 逆シリアル化中に、JSON の null 非許容値型に null 値が含まれている。

<xref:System.Text.Json> では、同じシナリオで例外がスローされます。 (対応する null 処理設定は <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType>です。)

ターゲット型を所有している場合、最適な回避策は、問題のプロパティを null 許容にすることです (たとえば、`int` を `int?` に変更します)。

もう 1 つの回避策として、`DateTimeOffset` 型に対する null 値を処理する次の例のように、型のコンバーターを作成する方法があります。

[!code-csharp[](snippets/system-text-json-how-to/csharp/DateTimeOffsetNullHandlingConverter.cs)]

このカスタム コンバーターを登録するには、[プロパティで属性を使用](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property)するか、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーター を追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

**注:** 上記のコンバーターでは、既定値を指定する POCO に対して `Newtonsoft.Json` が処理する場合とは**異なる方法で null 値が処理**されます。 たとえば、次のコードがターゲット オブジェクトを表しているとします。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithDefault)]

さらに、上記のコンバーターを使用して、次の JSON が逆シリアル化されるとします。

```json
{
  "Date": null,
  "TemperatureCelsius": 25,
  "Summary": null
}
```

逆シリアル化が行われた後、`Date` プロパティには 1/1/0001 (`default(DateTimeOffset)`) が設定されます。つまり、コンストラクターで設定された値が上書きされます。 同じ POCO と JSON を使用する場合、`Newtonsoft.Json` の逆シリアル化では `Date` プロパティに 1/1/2001 が設定されたままになります。

### <a name="deserialize-to-immutable-classes-and-structs"></a>不変のクラスと構造体への逆シリアル化

`Newtonsoft.Json` では、パラメーターを持つコンストラクターを使用できるため、不変のクラスと構造体に逆シリアル化できます。 <xref:System.Text.Json> では、パラメーターなしのパブリック コンストラクターのみがサポートされます。 回避策として、カスタム コンバーターでパラメーターを持つコンストラクターを呼び出すことができます。

複数のコンストラクター パラメーターを持つ不変の構造体を次に示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/ImmutablePoint.cs#ImmutablePoint)]

さらに、この構造体をシリアル化および逆シリアル化するコンバーターを示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/ImmutablePointConverter.cs)]

このカスタム コンバーターを登録するには、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーターを追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

オープン ジェネリック プロパティを処理する同様のコンバーターの例については、[キーと値のペアの組み込みコンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/JsonValueConverterKeyValuePair.cs)に関する記事を参照してください。

### <a name="specify-constructor-to-use"></a>使用するコンストラクターを指定する

`Newtonsoft.Json` の `[JsonConstructor]` 属性を使用すると、POCO への逆シリアル化時に呼び出すコンストラクターを指定できます。 <xref:System.Text.Json> では、パラメーターなしのコンストラクターのみがサポートされます。 回避策として、必要なコンストラクターをカスタム コンバーターで呼び出すことができます。 「[不変のクラスと構造体への逆シリアル化](#deserialize-to-immutable-classes-and-structs)」の例を参照してください。

### <a name="required-properties"></a>必須プロパティ

`Newtonsoft.Json` では、`[JsonProperty]` 属性に `Required` を設定して、プロパティが必須であることを指定します。 必須とマーク付けされたプロパティに対して JSON で値が取得されない場合、`Newtonsoft.Json` で例外がスローされます。

<xref:System.Text.Json> では、ターゲット型のいずれかのプロパティに対して値が取得されない場合でも、例外はスローされません。 たとえば、`WeatherForecast` クラスがあるとします。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

次の JSON はエラーなしで逆シリアル化されます。

```json
{
    "TemperatureCelsius": 25,
    "Summary": "Hot"
}
```

JSON に `Date` プロパティがない場合に逆シリアル化が失敗するようにするには、カスタム コンバーターを実装します。 次のサンプル コンバーター コードでは、逆シリアル化の完了後に `Date` プロパティが設定されていない場合は例外がスローされます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastRequiredPropertyConverter.cs)]

このカスタム コンバーターを登録するには、[POCO クラスで属性を使用](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type)するか、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーター を追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

このパターンに従う場合は、<xref:System.Text.Json.JsonSerializer.Serialize%2A> または <xref:System.Text.Json.JsonSerializer.Deserialize%2A> を再帰的に呼び出すときにオプション オブジェクトを渡さないでください。 オプション オブジェクトには、<xref:System.Text.Json.JsonSerializerOptions.Converters%2A> コレクションが含まれています。 それを `Serialize` または `Deserialize` に渡すと、カスタム コンバーターはそれ自体を呼び出し、無限ループが形成され、結果的にスタック オーバーフロー例外が発生します。 既定のオプションを使用できない場合は、必要な設定を使用してオプションの新しいインスタンスを作成します。 この方法では、新しい各インスタンスが個別にキャッシュされるため、速度が遅くなります。

上記のコンバーター コードは、簡略化された例です。 属性 ([[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) など) または別のオプション (カスタム エンコーダーなど) を処理する必要がある場合は、追加のロジックが必要になります。 また、例のコードでは、既定値がコンストラクター内で設定されているプロパティは処理されません。 さらに、この方法では次のシナリオの違いは識別されません。

* プロパティが JSON から欠落している。
* null 非許容型のプロパティが JSON に存在するが、値がその型の既定である (たとえば、`int` ではゼロ)。
* null 許容値型のプロパティが JSON に存在するが、値が null である。

### <a name="conditionally-ignore-a-property"></a>プロパティを条件付きで無視する

`Newtonsoft.Json` には、シリアル化または逆シリアル化時にプロパティを条件付きで無視する方法がいくつか用意されています。

* `DefaultContractResolver` を使用すると、任意の条件に基づいて含めたり除外したりするプロパティを選択できます。
* `JsonSerializerSettings` の `NullValueHandling` と `DefaultValueHandling` の設定を使用すると、null 値または既定値のすべてのプロパティを無視することを指定できます。
* `[JsonProperty]` 属性の `NullValueHandling` と `DefaultValueHandling` の設定を使用すると、null または既定値に設定されている場合に無視する個々のプロパティを指定できます。

<xref:System.Text.Json> には、シリアル化中にプロパティを除外するために次の方法が用意されています。

* プロパティで [[JsonIgnore]](system-text-json-how-to.md#exclude-individual-properties) 属性を使用すると、シリアル化中にそのプロパティが JSON から除外されます。
* [IgnoreNullValues](system-text-json-how-to.md#exclude-all-null-value-properties) グローバル オプションを使用すると、すべての null 値プロパティを除外できます。
* [IgnoreReadOnlyProperties](system-text-json-how-to.md#exclude-all-read-only-properties) グローバル オプションを使用すると、すべての読み取り専用プロパティを除外できます。

これらのオプションでは、以下を行うことは**できません**。

* 型に対して既定値を持つすべてのプロパティを無視する。
* 型に対して既定値を持つ、選択したプロパティを無視する。
* 選択したプロパティを、値が null である場合に無視する。
* 実行時に評価される任意の基準に基づいて、選択したプロパティを無視する。

この機能のために、カスタム コンバーターを記述できます。 この方法を紹介するサンプルの POCO とそれに対するカスタム コンバーターを、次に示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastRuntimeIgnoreConverter.cs)]

このコンバーターでは、`Summary` プロパティは、値が null、空の文字列、または "N/A" の場合、シリアル化から除外されます。

このカスタム コンバーターを登録するには、[クラスで属性を使用](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type)するか、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーター を追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

この方法では、次の場合に追加のロジックが必要になります。

* POCO に複合プロパティが含まれている。
* `[JsonIgnore]` などの属性や、カスタム エンコーダーなどのオプションを処理する必要がある。

### <a name="specify-date-format"></a>日付形式を指定する

`Newtonsoft.Json` には、`DateTime` および `DateTimeOffset` 型のプロパティをどのようにシリアル化および逆シリアル化するかを制御する方法がいくつか用意されています。

* `DateTimeZoneHandling` 設定を使用すると、すべての `DateTime` 値を UTC 日付としてシリアル化できます。
* `DateFormatString` 設定と `DateTime` コンバーターを使用すると、日付文字列の形式をカスタマイズできます。

<xref:System.Text.Json> では、サポートが組み込まれている形式は ISO 8601-1:2019 のみです。これが広く採用されていて明確であり、ラウンド トリップが正確に行われるためです。 他の形式を使用するには、カスタム コンバーターを作成します。 詳細については、「[System.Text.Json での DateTime と DateTimeOffset のサポート](../datetime/system-text-json-support.md)」を参照してください。

### <a name="callbacks"></a>コールバック

`Newtonsoft.Json` では、シリアル化または逆シリアル化プロセスの複数の時点でカスタム コードを実行できます。

* OnDeserializing (オブジェクトの逆シリアル化の開始時点)
* OnDeserialized (オブジェクトの逆シリアル化の完了時点)
* OnSerializing (オブジェクトのシリアル化の開始時点)
* OnSerialized (オブジェクトのシリアル化の完了時点)

<xref:System.Text.Json> では、カスタム コンバーターを記述することでコールバックをシミュレートできます。 次の例は、POCO のカスタム コンバーターを示しています。 このコンバーターには、`Newtonsoft.Json` のコールバックに対応する各時点でメッセージを表示するコードが含まれています。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastCallbacksConverter.cs)]

このカスタム コンバーターを登録するには、[クラスで属性を使用](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type)するか、<xref:System.Text.Json.JsonSerializerOptions.Converters> コレクションに[コンバーター を追加](system-text-json-converters-how-to.md#registration-sample---converters-collection)します。

上記のサンプルに従ったカスタム コンバーターを使用すると、次のようになります。

* `OnDeserializing` コードでは、新しい POCO インスタンスにアクセスできません。 逆シリアル化の開始時に新しい POCO インスタンスを操作するには、そのコードを POCO コンストラクターに挿入します。
* `Serialize` または `Deserialize` を再帰的に呼び出すときにオプション オブジェクトを渡さないでください。 オプション オブジェクトには、`Converters` コレクションが含まれています。 `Serialize` または `Deserialize` に渡すと、コンバーターが使用されることになり、無限ループが形成され、結果的にスタック オーバーフロー例外が発生します。

### <a name="public-and-non-public-fields"></a>パブリックおよび非パブリック フィールド

`Newtonsoft.Json` では、フィールドおよびプロパティをシリアル化および逆シリアル化できます。 <xref:System.Text.Json> は、パブリック プロパティでのみ機能します。 この機能は、カスタム コンバーターによって得られます。

### <a name="internal-and-private-property-setters-and-getters"></a>内部およびプライベート プロパティのセッターとゲッター

`Newtonsoft.Json` では、`JsonProperty` 属性を通じて、プライベートおよび内部プロパティのセッターとゲッターを使用できます。 <xref:System.Text.Json> ではパブリック セッターのみがサポートされます。 この機能は、カスタム コンバーターによって得られます。

### <a name="populate-existing-objects"></a>既存のオブジェクトの設定

`Newtonsoft.Json` の `JsonConvert.PopulateObject` メソッドでは、新しいインスタンスを作成するのではなく、クラスの既存のインスタンスに JSON ドキュメントが逆シリアル化されます。 <xref:System.Text.Json> では常に、既定のパラメーターなしのパブリック コンストラクターを使用して、ターゲット型の新しいインスタンスが作成されます。 カスタム コンバーターによって、既存のインスタンスに逆シリアル化できます。

### <a name="reuse-rather-than-replace-properties"></a>プロパティを置き換えるのではなく再利用する

`Newtonsoft.Json` の `ObjectCreationHandling` 設定を使用すると、逆シリアル化中に、プロパティ内のオブジェクトを置き換えるのではなく再利用することを指定できます。 <xref:System.Text.Json> では常に、プロパティ内のオブジェクトが置き換えられます。  この機能は、カスタム コンバーターによって得られます。

### <a name="add-to-collections-without-setters"></a>セッターなしでコレクションに追加する

逆シリアル化中、`Newtonsoft.Json` ではプロパティにセッターがない場合でも、オブジェクトがコレクションに追加されます。 <xref:System.Text.Json> では、セッターのないプロパティは無視されます。 この機能は、カスタム コンバーターによって得られます。

## <a name="scenarios-that-jsonserializer-currently-doesnt-support"></a>現在 JsonSerializer でサポートされていないシナリオ

次のシナリオでは、回避策は実用的でないか不可能です。 `Newtonsoft.Json` のこれらの機能を利用する必要がある場合、移行を可能にするには大幅な変更が必要です。

### <a name="preserve-object-references-and-handle-loops"></a>オブジェクト参照を保持してループを処理する

既定では、`Newtonsoft.Json` では値によってシリアル化します。 たとえば、オブジェクトに同じ `Person` オブジェクトへの参照を含む 2 つのプロパティが含まれている場合、その `Person` オブジェクトのプロパティの値は JSON 内で複製されます。

`Newtonsoft.Json` には、`JsonSerializerSettings` に、参照によってシリアル化できるようにする `PreserveReferencesHandling` 設定があります。

* 最初の `Person` オブジェクト用に作成された JSON に識別子メタデータが追加されます。
* 2番目の `Person` オブジェクト用に作成された JSON には、プロパティ値ではなく、その識別子への参照が含まれます。

`Newtonsoft.Json` には、例外をスローするのではなく循環参照を無視できるようにする `ReferenceLoopHandling` 設定もあります。

<xref:System.Text.Json> では値によるシリアル化のみがサポートされ、循環参照に対しては例外がスローされます。

### <a name="systemruntimeserialization-attributes"></a>System.Runtime.Serialization 属性

<xref:System.Text.Json> では、`DataMemberAttribute` や `IgnoreDataMemberAttribute` などの、`System.Runtime.Serialization` 名前空間の属性はサポートされません。

### <a name="octal-numbers"></a>8 進数

`Newtonsoft.Json` では、先頭にゼロを持つ数値は 8 進数として扱われます。 <xref:System.Text.Json> では先頭のゼロは許容されません。[RFC 8259](https://tools.ietf.org/html/rfc8259) 仕様で許可されていないためです。

### <a name="missingmemberhandling"></a>MissingMemberHandling

`Newtonsoft.Json` は、ターゲット型に存在しないプロパティが JSON に含まれている場合、逆シリアル化中に例外をスローするように構成できます。 <xref:System.Text.Json> では、[[JsonExtensionData] 属性](system-text-json-how-to.md#handle-overflow-json)を使用する場合を除き、JSON 内の余分なプロパティは無視されます。 欠落しているメンバー機能に対する回避策はありません。

### <a name="tracewriter"></a>TraceWriter

`Newtonsoft.Json` では、`TraceWriter` を使用してシリアル化または逆シリアル化によって生成されたログを表示し、デバッグできます。 <xref:System.Text.Json> では、ログ記録は行われません。

## <a name="jsondocument-and-jsonelement-compared-to-jtoken-like-jobject-jarray"></a>JToken (JObject、JArray など) と比較した JsonDocument と JsonElement

<xref:System.Text.Json.JsonDocument?displayProperty=fullName> には、既存の JSON ペイロードから**読み取り専用**のドキュメント オブジェクト モデル (DOM) を解析して作成する機能が用意されています。 DOM では、JSON ペイロード内のデータへのランダム アクセスが提供されます。 ペイロードを構成する JSON 要素には、<xref:System.Text.Json.JsonElement> 型を使用してアクセスできます。 `JsonElement` 型には、JSON テキストを一般的な .NET 型に変換するための API が用意されています。 `JsonDocument` では <xref:System.Text.Json.JsonDocument.RootElement> プロパティが公開されます。

### <a name="jsondocument-is-idisposable"></a>JsonDocument は IDisposable

`JsonDocument` では、データのメモリ内ビューがプールされたバッファー内に作成されます。 そのため、`Newtonsoft.Json` の `JObject` や `JArray` とは異なり、`JsonDocument` 型は `IDisposable` を実装し、Using ブロック内で使用される必要があります。

有効期間中全体の所有権を呼び出し元に移譲し、責任を破棄する場合は、API から `JsonDocument` のみを返します。 ほとんどのシナリオでは、これは必要ありません。 呼び出し元が JSON ドキュメント全体を操作する必要がある場合は、<xref:System.Text.Json.JsonDocument.RootElement%2A> (つまり <xref:System.Text.Json.JsonElement>) の <xref:System.Text.Json.JsonElement.Clone%2A> を返します。 呼び出し元が JSON ドキュメント内の特定の要素を操作する必要がある場合は、その <xref:System.Text.Json.JsonElement> の <xref:System.Text.Json.JsonElement.Clone%2A> を返します。 `Clone` を作成せずに直接 `RootElement` またはサブ要素を返した場合、呼び出し元は、返された `JsonElement` には、それを所有する `JsonDocument` が破棄されるとアクセスできなくなります。

`Clone` を作成する必要がある例を次に示します。

```csharp
public JsonElement LookAndLoad(JsonElement source)
{
    string json = File.ReadAllText(source.GetProperty("fileName").GetString());

    using (JsonDocument doc = JsonDocument.Parse(json))
    {
        return doc.RootElement.Clone();
    }
}
```

上記のコードでは、`fileName` プロパティを含む `JsonElement` が想定されています。 これにより、JSON ファイルが開き、`JsonDocument` が作成されます。 このメソッドでは、呼び出し元がドキュメント全体を操作することが想定されているため、`RootElement` の `Clone` が返されます。

`JsonElement` を受け取り、サブ要素を返す場合は、サブ要素の `Clone` を返す必要はありません。 呼び出し元は、渡された `JsonElement` が属している `JsonDocument` が破棄されないように維持する役割を負っています。 次に例を示します。

```csharp
public JsonElement ReturnFileName(JsonElement source)
{
   return source.GetProperty("fileName");
}
```

### <a name="jsondocument-is-read-only"></a>JsonDocument は読み取り専用

<xref:System.Text.Json> の DOM では、JSON 要素の追加、削除、変更を行うことはできません。 このように設計されている理由は、パフォーマンスを向上させ、一般的な JSON ペイロード サイズ (つまり、< 1 MB) を解析するための割り当てを減らすためです。 現在のシナリオで変更可能な DOM を使用している場合は、次のいずれかの回避策を実行できる可能性があります。

* `JsonDocument` を最初から作成する (つまり、既存の JSON ペイロードを `Parse` メソッドに渡さない場合) には、`Utf8JsonWriter` を使用して JSON テキストを記述し、そこからの出力を解析して新しい `JsonDocument` を作成します。
* 既存の `JsonDocument` を変更するには、それを使用して JSON テキストを記述し、記述中に変更を行い、そこからの出力を解析して新しい `JsonDocument` を作成します。
* 既存の JSON ドキュメントをマージする、つまり、`Newtonsoft.Json` の `JObject.Merge` または `JContainer.Merge` API と同等のことを行うには、[この GitHub の問題](https://github.com/dotnet/corefx/issues/42466#issuecomment-570475853)を参照してください。

### <a name="jsonelement-is-a-union-struct"></a>JsonElement は union 構造体

`JsonDocument` では、<xref:System.Text.Json.JsonElement> 型 (任意の JSON 要素を含む共用体の構造体型) のプロパティとして `RootElement` が公開されます。 `Newtonsoft.Json` では `JObject`、`JArray`、`JToken` などの専用の階層型が使用されます。 `JsonElement` に対して検索と列挙を行うことができます。また、`JsonElement` を使用して、JSON 要素を .NET 型に具体化することができます。

### <a name="how-to-search-a-jsondocument-and-jsonelement-for-sub-elements"></a>JsonDocument と JsonElement でのサブ要素の検索方法

`Newtonsoft.Json` の `JObject` または `JArray` を使用した JSON トークンの検索は、何らかのディクショナリ内での検索であるため、比較的高速になる傾向があります。 それに対し、`JsonElement` での検索にはプロパティの順次検索が必要になるため、比較的低速になります (たとえば、`TryGetProperty` を使用する場合)。 <xref:System.Text.Json> は、検索時間ではなく、初期解析時間を最小限に抑えるように設計されています。 そのため、`JsonDocument` オブジェクトで検索する場合は、次の方法を使用してパフォーマンスを最適化してください。

* 独自のインデックス作成やループを実行するのではなく、組み込みの列挙子 (<xref:System.Text.Json.JsonElement.EnumerateArray%2A> と <xref:System.Text.Json.JsonElement.EnumerateObject%2A>) を使用します。
* `RootElement` を使用して、`JsonDocument` 全体ですべてのプロパティの順次検索を行わないでください。 代わりに、JSON データの既知の構造に基づいて、入れ子になった JSON オブジェクトで検索します。 たとえば、`Student` オブジェクトで `Grade` プロパティを探している場合は、`Student` オブジェクトをループし、それぞれの `Grade` の値を取得するようにします。すべての `JsonElement` オブジェクトで `Grade` プロパティを検索することは避けてください。 後者を行うと、同じデータに対して不要なパスが行われます。

コード例については、「[JsonDocument を使用してデータにアクセスする](system-text-json-how-to.md#use-jsondocument-for-access-to-data)」を参照してください。

## <a name="utf8jsonreader-compared-to-jsontextreader"></a>JsonTextReader と比較した Utf8JsonReader

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> は、UTF-8 でエンコードされた JSON テキスト用の、ハイ パフォーマンス、低割り当て、順方向専用のリーダーです。[ReadOnlySpan\<byte>](xref:System.ReadOnlySpan%601) または [ReadOnlySequence\<byte>](xref:System.Buffers.ReadOnlySequence%601) から読み取られます。 `Utf8JsonReader` は低レベルの型であり、カスタム パーサーとデシリアライザーを構築するために使用できます。

以下のセクションでは、`Utf8JsonReader` を使用する場合の推奨されるプログラミング パターンについて説明します。

### <a name="utf8jsonreader-is-a-ref-struct"></a>Utf8JsonReader は ref 構造体

`Utf8JsonReader` 型は "*ref 構造体*" であるため、[特定の制限](../../csharp/language-reference/builtin-types/struct.md#ref-struct)があります。 たとえば、ref 構造体以外のクラスまたは構造体にフィールドとして格納することはできません。 ハイ パフォーマンスを実現するには、この型が `ref struct` である必要があります。これは、入力の [ReadOnlySpan\<byte>](xref:System.ReadOnlySpan%601) (これ自体が ref 構造体です) をキャッシュする必要があるためです。 さらに、この型は状態が保持されるため変更可能です。 そのため、これは、値ではなく **ref で渡してください**。 値で渡すと、構造体のコピーが生成され、呼び出し元が状態の変更を確認できません。 これは `Newtonsoft.Json` とは異なります。`Newtonsoft.Json` `JsonTextReader` がクラスであるためです。 ref 構造体の使用方法の詳細については、「[安全で効率的な C# コードを記述する](../../csharp/write-safe-efficient-code.md)」をご覧ください。

### <a name="read-utf-8-text"></a>UTF-8 テキストを読み取る

`Utf8JsonReader` を使用しているときに最大限のパフォーマンスを達成するには、UTF-16 文字列としてではなく、UTF-8 テキストとして既にエンコードされている JSON ペイロードを読み取ります。 コード例については、「[Utf8JsonReader を使用してデータをフィルター処理する](system-text-json-how-to.md#filter-data-using-utf8jsonreader)」を参照してください。

### <a name="read-with-a-stream-or-pipereader"></a>ストリームまたは PipeReader で読み取る

`Utf8JsonReader` では、UTF-8 でエンコードされた [ReadOnlySpan\<byte>](xref:System.ReadOnlySpan%601) または [ReadOnlySequence\<byte>](xref:System.Buffers.ReadOnlySequence%601) (これは <xref:System.IO.Pipelines.PipeReader> からの読み取りの結果です) からの読み取りがサポートされます。

同期読み取りの場合は、ストリームの末尾に到達するまで JSON ペイロードをバイト配列に読み込み、それをリーダーに渡すことができます。 (UTF-16 としてエンコードされた) 文字列からの読み取りの場合は、<xref:System.Text.Encoding.UTF8>.<xref:System.Text.Encoding.GetBytes%2A> を呼び出して、 最初にその文字列を UTF-8 でエンコードされたバイト配列にトランスコードします。 その後、それを `Utf8JsonReader` に渡します。

`Utf8JsonReader` では入力が JSON テキストと見なされるため、UTF-8 バイト オーダー マーク (BOM) は無効な JSON と見なされます。 呼び出し元は、それをフィルターで除外してからデータをリーダーに渡す必要があります。

コード例については、「[Utf8JsonReader を使用する](system-text-json-how-to.md#use-utf8jsonreader)」を参照してください。

### <a name="read-with-multi-segment-readonlysequence"></a>マルチセグメントの ReadOnlySequence で読み取る

JSON の入力が [ReadOnlySpan\<byte>](xref:System.ReadOnlySpan%601) の場合、各 JSON 要素には、読み取りループを実行するときにリーダーの `ValueSpan` プロパティからアクセスできます。 ただし、入力が [ReadOnlySequence\<byte>](xref:System.Buffers.ReadOnlySequence%601) (これは、<xref:System.IO.Pipelines.PipeReader> からの読み取りの結果です) である場合、一部の JSON 要素が `ReadOnlySequence<byte>` オブジェクトの複数のセグメントにまたがることがあります。 これらの要素には、連続メモリ ブロック内で <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> からアクセスすることはできません。 代わりに、マルチセグメントの `ReadOnlySequence<byte>` を入力として使用する場合は必ず、リーダーで <xref:System.Text.Json.Utf8JsonReader.HasValueSequence%2A> プロパティをポーリングして、現在の JSON 要素へのアクセス方法を確認します。 推奨されるパターンを次に示します。

```csharp
while (reader.Read())
{
    switch (reader.TokenType)
    {
        // ...
        ReadOnlySpan<byte> jsonElement = reader.HasValueSequence ?
            reader.ValueSequence.ToArray() :
            reader.ValueSpan;
        // ...
    }
}
```

### <a name="use-valuetextequals-for-property-name-lookups"></a>プロパティ名の検索に ValueTextEquals を使用する

プロパティ名の検索用に <xref:System.MemoryExtensions.SequenceEqual%2A> を呼び出してバイト単位の比較を実行する場合は、<xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> を使用しないでください。 代わりに <xref:System.Text.Json.Utf8JsonReader.ValueTextEquals%2A> を呼び出してください。このメソッドにより、JSON でエスケープされた文字がエスケープ解除されるためです。 以下は、"name" という名前のプロパティの検索方法を示す例です。

[!code-csharp[](snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs?name=SnippetDefineUtf8Var)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs?name=SnippetUseUtf8Var&highlight=11)]

### <a name="read-null-values-into-nullable-value-types"></a>null 許容値型に null 値を読み込む

`Newtonsoft.Json` には、<xref:System.Nullable%601> を返す API が用意されています。たとえば、`bool?` を返すことで `Null` `TokenType` を処理する `ReadAsBoolean` などがあります。 組み込みの `System.Text.Json` の API では、null 非許容値型のみが返されます。 たとえば、<xref:System.Text.Json.Utf8JsonReader.GetBoolean%2A?displayProperty=nameWithType> では `bool` が返されます。 JSON で `Null` が見つかると、例外がスローされます。 次の例は、null を処理する 2 つの方法を示しています。1 つは null 許容値型を返す方法で、もう 1 つは既定値を返す方法です。

```csharp
public bool? ReadAsNullableBoolean()
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return null;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

```csharp
public bool ReadAsBoolean(bool defaultValue)
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return defaultValue;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

### <a name="multi-targeting"></a>マルチターゲット

特定のターゲット フレームワークに対して `Newtonsoft.Json` の使用を継続する必要がある場合は、マルチターゲットにし、実装を 2 つにすることができます。 ただし、これは簡単ではなく、いくつかの `#ifdefs` とソースの複製が必要になります。 できるだけ多くのコードを共有する 1 つの方法として、`Utf8JsonReader` と `Newtonsoft.Json` `JsonTextReader` を囲む `ref struct` ラッパーを作成する方法があります。 このラッパーでは、動作の違いを隔離しつつ、公開されている表面部分は統合されます。 これにより、変更を主に型の構造に隔離すると共に、新しい型を参照によって渡すことができます。 これは、[Microsoft.Extensions.DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) ライブラリが従っているパターンです。

* [UnifiedJsonReader.JsonTextReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.JsonTextReader.cs)
* [UnifiedJsonReader.Utf8JsonReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.Utf8JsonReader.cs)

## <a name="utf8jsonwriter-compared-to-jsontextwriter"></a>JsonTextWriter と比較した Utf8JsonWriter

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> は、`String`、`Int32`、`DateTime` のような一般的な .NET 型から UTF-8 でエンコードされた JSON テキストを書き込むための、ハイパフォーマンスな方法です。 ライターは低レベルの型であり、カスタム シリアライザーを構築するために使用できます。

以下のセクションでは、`Utf8JsonWriter` を使用する場合の推奨されるプログラミング パターンについて説明します。

### <a name="write-with-utf-8-text"></a>UTF-8 テキストで書き込む

`Utf8JsonWriter` を使用しているときに最大限のパフォーマンスを達成するには、UTF-16 文字列としてではなく、UTF-8 テキストとして既にエンコードされている JSON ペイロードを書き込みます。 UTF-16 文字列リテラルを使用するのではなく、<xref:System.Text.Json.JsonEncodedText> を使用して、既知の文字列プロパティの名前と値をスタティックとしてキャッシュおよび事前エンコードし、ライターに渡します。 これは、UTF-8 バイト配列をキャッシュして使用するより高速です。

この方法は、カスタム エスケープ処理を行う必要がある場合にも機能します。 `System.Text.Json` では、文字列の記述中にエスケープ処理を無効にすることはできません。 ただし、独自のカスタム <xref:System.Text.Encodings.Web.JavaScriptEncoder> をオプションとしてライターに渡すことができます。または、`JavascriptEncoder` を使用する独自の `JsonEncodedText` を作成してエスケープ処理を行ってから、文字列の代わりに `JsonEncodedText` を書き込むこともできます。 詳細については、「[文字エンコードをカスタマイズする](system-text-json-how-to.md#customize-character-encoding)」を参照してください。

### <a name="write-raw-values"></a>生の値を書き込む

`Newtonsoft.Json` `WriteRawValue` メソッドでは、値が必要な生の JSON が書き込まれます。 <xref:System.Text.Json> には、それに直接相当するものはありませんが、有効な JSON のみが書き込まれるようにする回避策を次に示します。

```csharp
using JsonDocument doc = JsonDocument.Parse(string);
doc.WriteTo(writer);
```

### <a name="customize-character-escaping"></a>文字のエスケープ処理をカスタマイズする

`JsonTextWriter` の [StringEscapeHandling](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_StringEscapeHandling.htm) 設定には、すべての ASCII 以外の文字**または** HTML 文字をエスケープするオプションが用意されています。 既定では、`Utf8JsonWriter` ではすべての ASCII 以外**および** HTML 文字がエスケープされます。 このエスケープ処理は、多層防御セキュリティ上の理由で行われます。 別のエスケープ処理ポリシーを指定するには、<xref:System.Text.Encodings.Web.JavaScriptEncoder> を作成し、<xref:System.Text.Json.JsonWriterOptions.Encoder?displayProperty=nameWithType> を設定します。 詳細については、「[文字エンコードをカスタマイズする](system-text-json-how-to.md#customize-character-encoding)」を参照してください。

### <a name="customize-json-format"></a>JSON 形式をカスタマイズする

`JsonTextWriter` には次の設定が含まれていますが、`Utf8JsonWriter` には同等のものがありません。

* [Indentation](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_Indentation.htm) - インデントする文字数を指定します。 `Utf8JsonWriter` では常に 2 文字のインデントが行われます。
* [IndentChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_IndentChar.htm) - インデントに使用する文字を指定します。  `Utf8JsonWriter` では常に空白文字が使用されます。
* [QuoteChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteChar.htm) - 文字列値を囲むために使用する文字を指定します。  `Utf8JsonWriter` では常に二重引用符が使用されます。
* [QuoteName](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteName.htm) - プロパティ名を引用符で囲むかどうかを指定します。  `Utf8JsonWriter` では常に引用符で囲みます。

`Utf8JsonWriter` によって生成された JSON をこれらの方法でカスタマイズできる回避策はありません。

### <a name="write-null-values"></a>null 値を書き込む

`Utf8JsonWriter` を使用して null 値を書き込むには、以下を呼び出します。

* <xref:System.Text.Json.Utf8JsonWriter.WriteNull%2A>。null を値として指定し、キーと値のペアを書き込みます。
* <xref:System.Text.Json.Utf8JsonWriter.WriteNullValue%2A>。JSON 配列の要素として null を書き込みます。

文字列プロパティでは、文字列が null の場合、<xref:System.Text.Json.Utf8JsonWriter.WriteString%2A> と <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> は `WriteNull` と `WriteNullValue` に相当します。

### <a name="write-timespan-uri-or-char-values"></a>Timespan、Uri、または char の値を書き込む

`JsonTextWriter` には、[TimeSpan](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_18.htm)、[Uri](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_22.htm)、[char](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_3.htm) の値のための `WriteValue` メソッドがあります。 `Utf8JsonWriter` には同等のメソッドがありません。 代わりに、これらの値を文字列として書式設定し (たとえば `ToString()` を呼び出します)、<xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> を呼び出します。

### <a name="multi-targeting"></a>マルチターゲット

特定のターゲット フレームワークに対して `Newtonsoft.Json` の使用を継続する必要がある場合は、マルチターゲットにし、実装を 2 つにすることができます。 ただし、これは簡単ではなく、いくつかの `#ifdefs` とソースの複製が必要になります。 できるだけ多くのコードを共有する 1 つの方法として、`Utf8JsonWriter` と `Newtonsoft` `JsonTextWriter` を囲むラッパーを作成する方法があります。 このラッパーでは、動作の違いを隔離しつつ、公開されている表面部分は統合されます。 これにより、主に型の構造に変更を隔離できます。 [Microsoft.Extensions.DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) ライブラリは以下に従っています。

* [UnifiedJsonWriter.JsonTextWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.JsonTextWriter.cs)
* [UnifiedJsonWriter.Utf8JsonWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.Utf8JsonWriter.cs)

## <a name="additional-resources"></a>その他の技術情報

<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)[Restore this when the roadmap is updated.]-->
* [System.Text.Json の概要](system-text-json-overview.md)
* [System.Text.Json の使用方法](system-text-json-how-to.md)
* [カスタム コンバーターを記述する方法](system-text-json-converters-how-to.md)
* [System.Text.Json での DateTime と DateTimeOffset のサポート](../datetime/system-text-json-support.md)
* [System.Text.Json API リファレンス](xref:System.Text.Json)
* [System.Text.Json.Serialization API リファレンス](xref:System.Text.Json.Serialization)
