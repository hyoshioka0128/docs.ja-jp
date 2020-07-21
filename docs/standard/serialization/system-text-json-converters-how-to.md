---
title: JSON シリアル化のためのカスタム コンバーターを作成する方法 - .NET
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: abda23ea538c2c0da6ada4f359ce745602dca45d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84279764"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a>.NET で JSON シリアル化 (マーシャリング) のためのカスタム コンバーターを作成する方法

この記事では、<xref:System.Text.Json> 名前空間で提供される JSON シリアル化クラス用のカスタム コンバーターを作成する方法について説明します。 `System.Text.Json` の概要については、[.NET で JSON のシリアル化と逆シリアル化を行う方法](system-text-json-how-to.md)に関するページを参照してください。

"*コンバーター*" は、オブジェクトまたは値を JSON との間で双方向に変換するクラスです。 `System.Text.Json` 名前空間には、JavaScript のプリミティブに対応するほとんどのプリミティブ型に対して、組み込みのコンバーターがあります。 次の目的で、カスタム コンバーターを作成することができます。

* 組み込みコンバーターの既定の動作をオーバーライドするため。 たとえば、`DateTime` の値を、既定の ISO 8601-1:2019 形式ではなく、mm/dd/yyyy 形式で表すことができます。
* カスタム値型をサポートするため。 たとえば、`PhoneNumber` 構造体などです。

また、カスタム コンバーターを作成し、現在のリリースには含まれない機能で `System.Text.Json` をカスタマイズまたは拡張することもできます。 この記事ではこの後、次のシナリオについて説明します。

* [推論された型をオブジェクトのプロパティに逆シリアル化する](#deserialize-inferred-types-to-object-properties)。
* [文字列以外のキーでディクショナリをサポートする](#support-dictionary-with-non-string-key)。
* [ポリモーフィックな逆シリアル化をサポートする](#support-polymorphic-deserialization)。
* [Stack\<T> のラウンドトリップをサポートする](#support-round-trip-for-stackt)。

## <a name="custom-converter-patterns"></a>カスタム コンバーターのパターン

カスタム コンバーターの作成には、基本パターンとファクトリ パターンという 2 つのパターンがあります。 ファクトリ パターンは、`Enum` 型またはオープン ジェネリックを処理するコンバーター用です。 基本パターンは、非ジェネリック型およびクローズ ジェネリック型用です。  たとえば、次のような型のコンバーターには、ファクトリ パターンが必要です。

* `Dictionary<TKey, TValue>`
* `Enum`
* `List<T>`

基本パターンで処理できる型の例としては、次のようなものがあります。

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* `DateTime`
* `Int32`

基本パターンでは、1 つの型を処理できるクラスが作成されます。 ファクトリ パターンによって作成されるクラスの場合は、実行時に必要な特定の型が決定されて、適切なコンバーターが動的に作成されます。

## <a name="sample-basic-converter"></a>基本コンバーターのサンプル

次のサンプルは、既存のデータ型に対する既定のシリアル化をオーバーライドするコンバーターです。 そのコンバーターでは、`DateTimeOffset` のプロパティに対して mm/dd/yyyy の形式が使用されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs)]

## <a name="sample-factory-pattern-converter"></a>ファクトリ パターン コンバーターのサンプル

次のコードでは、`Dictionary<Enum,TValue>` で動作するカスタム コンバーターを示します。 そのコードは、1 番目のジェネリック型パラメーターが `Enum` で、2 番目がオープンであるため、ファクトリ パターンに従います。 `CanConvert` メソッドでは、2 つのジェネリック パラメーターを持つ `Dictionary` に対してのみ `true` が返されます。最初のパラメーターは `Enum` 型です。 内部のコンバーターでは、実行時に `TValue` に対して提供される任意の型を処理するために、既存のコンバーターが取得されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

上記のコードは、後の「[文字列以外のキーでディクショナリをサポートする](#support-dictionary-with-non-string-key)」で示されているものと同じです。

## <a name="steps-to-follow-the-basic-pattern"></a>基本パターンに従うための手順

次の手順では、基本パターンに従ってコンバーターを作成する方法について説明します。

* <xref:System.Text.Json.Serialization.JsonConverter%601> から派生するクラスを作成します。`T` は、シリアル化および逆シリアル化される型です。
* 受信した JSON を逆シリアル化して `T` 型に変換するように、`Read` メソッドをオーバーライドします。 JSON を読み取るには、メソッドに渡される <xref:System.Text.Json.Utf8JsonReader> を使用します。
* 受信した `T` 型のオブジェクトをシリアル化するように、`Write` メソッドをオーバーライドします。 JSON を書き込むには、メソッドに渡される <xref:System.Text.Json.Utf8JsonWriter> を使用します。
* `CanConvert` メソッドは、必要な場合にのみオーバーライドします。 変換する型が `T` 型である場合、既定の実装では `true` が返されます。 したがって、`T` 型だけをサポートするコンバーターでは、このメソッドをオーバーライドする必要はありません。 このメソッドをオーバーライドする必要があるコンバーターの例については、後の「[ポリモーフィックな逆シリアル化をサポートする](#support-polymorphic-deserialization)」を参照してください。

カスタム コンバーターを作成するための参考の実装として、[組み込みコンバーターのソース コード](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/)を参照できます。

## <a name="steps-to-follow-the-factory-pattern"></a>ファクトリ パターンに従うための手順

次の手順では、ファクトリ パターンに従ってコンバーターを作成する方法について説明します。

* <xref:System.Text.Json.Serialization.JsonConverterFactory> から派生するクラスを作成します。
* 変換する型がコンバーターで処理できる型である場合は true を返すように、`CanConvert` メソッドをオーバーライドします。 たとえば、コンバーターが `List<T>` 用の場合は、`List<int>`、`List<string>`、`List<DateTime>` だけを処理できます。
* 実行時に提供される変換対象の型を処理するコンバーター クラスのインスタンスを返すように、`CreateConverter` メソッドをオーバーライドします。
* `CreateConverter` メソッドによってインスタンス化されるコンバーター クラスを作成します。

オブジェクトと文字列を双方向に変換するコードは、すべての型に対して同じではないため、オープン ジェネリックにはファクトリ パターンが必要です。 オープン ジェネリック型 (`List<T>` など) 用のコンバーターでは、背後にあるクローズ ジェネリック型 (`List<DateTime>` など) 用のコンバーターを作成する必要があります。 コンバーターで処理できる各クローズ ジェネリック型を処理するためのにコードを記述する必要があります。

`Enum` 型はオープン ジェネリック型に似ています。`Enum` 用のコンバーターでは、背後にある特定の `Enum` (`WeekdaysEnum` など) に対するコンバーターを作成する必要があります。

## <a name="error-handling"></a>エラー処理

エラー処理コードで例外をスローする必要がある場合は、メッセージを含まない <xref:System.Text.Json.JsonException> をスローすることを検討します。 この例外型では、エラーの原因となった JSON の部分へのパスを含むメッセージが自動的に作成されます。 たとえば、`throw new JsonException();` というステートメントでは、次の例のようなエラー メッセージが生成されます。

```
Unhandled exception. System.Text.Json.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

メッセージ (`throw new JsonException("Error occurred")` など) を指定した場合でも、例外の <xref:System.Text.Json.JsonException.Path> プロパティでパスが提供されます。

## <a name="register-a-custom-converter"></a>カスタム コンバーターを登録する

"*カスタム コンバーター*" を登録して、`Serialize` メソッドと `Deserialize` メソッドでそれが使用されるようにします。 次のいずれかの方法を使用します。

* コンバーター クラスのインスタンスを <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> コレクションに追加します。
* カスタム コンバーターを必要とするプロパティに、[[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) 属性を適用します。
* カスタム値型を表すクラスまたは構造体に、[[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) 属性を適用します。

## <a name="registration-sample---converters-collection"></a>登録の例 - Converters コレクション

<xref:System.ComponentModel.DateTimeOffsetConverter> を <xref:System.DateTimeOffset> 型のプロパティの既定値にする例を次に示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetSerialize)]

次の型のインスタンスをシリアル化するとします。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

カスタム コンバーターが使用されたことを示す JSON 出力の例を次に示します。

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

次のコードでは、同じ方法を使用し、カスタム `DateTimeOffset` コンバーターを使用して逆シリアル化します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-property"></a>登録の例 - [JsonConverter] プロパティ

次のコードでは、`Date` プロパティのカスタム コンバーターを選択します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithConverterAttribute)]

`WeatherForecastWithConverterAttribute` をシリアル化するコードでは、`JsonSerializeOptions.Converters` を使用する必要はありません。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetSerialize)]

逆シリアル化するコードでも、`Converters` を使用する必要はありません。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-type"></a>登録の例 - 型での [JsonConverter]

構造体を作成し、それに `[JsonConverter]` 属性を適用するコードを次に示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/Temperature.cs)]

上記の構造体のカスタム コンバーターは次のようになります。

[!code-csharp[](snippets/system-text-json-how-to/csharp/TemperatureConverter.cs)]

構造体の `[JsonConvert]` 属性では、`Temperature` 型のプロパティに対する既定値としてカスタム コンバーターが登録されます。 次の型の `TemperatureCelsius` プロパティでは、シリアル化または逆シリアル化のときに、コンバーターが自動的に使用されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithTemperatureStruct)]

## <a name="converter-registration-precedence"></a>コンバーターの登録の優先順位

シリアル化または逆シリアル化のとき、コンバーターは各 JSON 要素に対して次の順序 (優先度が高い順) で選択されます。

* `[JsonConverter]` がプロパティに適用されます。
* `Converters` コレクションにコンバーターが追加されます。
* `[JsonConverter]` がカスタム値型または POCO に適用されます。

1 つの型に対して複数のカスタム コンバーターが `Converters` コレクションに登録されている場合は、`CanConvert` に対して true を返す最初のコンバーターが使用されます。

適用可能なカスタム コンバーターが登録されていない場合にのみ、組み込みコンバーターが選択されます。

## <a name="converter-samples-for-common-scenarios"></a>一般的なシナリオでのコンバーターの例

以下のセクションでは、組み込み機能では処理されない一般的なシナリオに対処するコンバーターの例を示します。

* [推論された型をオブジェクトのプロパティに逆シリアル化する](#deserialize-inferred-types-to-object-properties)
* [文字列以外のキーでディクショナリをサポートする](#support-dictionary-with-non-string-key)
* [ポリモーフィックな逆シリアル化をサポートする](#support-polymorphic-deserialization)
* [Stack\<T> のラウンドトリップをサポートする](#support-round-trip-for-stackt)。

### <a name="deserialize-inferred-types-to-object-properties"></a>推論された型をオブジェクトのプロパティに逆シリアル化する

`object` 型のプロパティに逆シリアル化すると、`JsonElement` オブジェクトが作成されます。 その理由は、逆シリアライザーでは、作成する CLR 型がわからず、推測が試みられないためです。 たとえば、JSON プロパティが "true" である場合、逆シリアライザーでは値が `Boolean` であることは推定されません。また、要素が "01/01/2019" である場合、逆シリアライザーではそれが `DateTime` であることは推定されません。

型の推定は不正確になる可能性があります。 逆シリアライザーで、小数点を含まない JSON の数値が `long` と解析された場合、値がもともと `ulong` または `BigInteger` としてシリアル化されていたとすると、範囲外の問題が発生する可能性があります。 数値がもともと `decimal` としてシリアル化されていた場合、小数点を含む数値が `double` と解析されると、精度が失われる可能性があります。

次のコードでは、型の推定が必要なシナリオでの、`object` プロパティに対するカスタム コンバーターを示します。 次のような変換が行われます。

* `true` と `false` は `Boolean` に
* 小数点を含まない数値は `long` に
* 小数点を含む数値は `double` に
* 日付は `DateTime` に
* 文字列は `string` に
* それ以外はすべて `JsonElement` に

[!code-csharp[](snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs)]

次のコードではコンバーターが登録されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs?name=SnippetRegister)]

`object` プロパティを含む型の例を次に示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithObjectProperties)]

次の逆シリアル化を行う JSON の例には、`DateTime`、`long`、`string` として逆シリアル化される値が含まれています。

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

カスタム コンバーターを使用しないと、逆シリアル化によって各プロパティに `JsonElement` が挿入されます。

`System.Text.Json.Serialization` 名前空間の[単体テスト フォルダー](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/)には、`object` プロパティへの逆シリアル化を処理するカスタム コンバーターの例がさらにあります。

### <a name="support-dictionary-with-non-string-key"></a>文字列以外のキーでディクショナリをサポートする

ディクショナリ コレクションに対する組み込みのサポートは `Dictionary<string, TValue>` 用です。 つまり、キーは文字列である必要があります。 キーが整数または他の型であるディクショナリをサポートするには、カスタム コンバーターが必要です。

次のコードでは、`Dictionary<Enum,TValue>` で動作するカスタム コンバーターを示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

次のコードではコンバーターが登録されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs?name=SnippetRegister)]

このコンバーターでは、次の `Enum` を使用する次のクラスの `TemperatureRanges` プロパティをシリアル化および逆シリアル化できます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithEnumDictionary)]

シリアル化からの JSON 出力は、次の例のようになります。

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "Cold": 20,
    "Hot": 40
  }
}
```

`System.Text.Json.Serialization` 名前空間の[単体テスト フォルダー](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/)には、文字列以外のキーのディクショナリを処理するカスタム コンバーターの例がさらにあります。

### <a name="support-polymorphic-deserialization"></a>ポリモーフィックな逆シリアル化をサポートする

組み込み機能では、[ポリモーフィックなシリアル化](system-text-json-how-to.md#serialize-properties-of-derived-classes)は限られた範囲で提供されていますが、逆シリアル化はまったくサポートされていません。 逆シリアル化を行うには、カスタム コンバーターが必要です。

たとえば、抽象基底クラス `Person` と、派生クラス `Employee` および `Customer` があるとします。 ポリモーフィックな逆シリアル化とは、デザイン時に逆シリアル化ターゲットとして `Person` を指定すると、実行時に JSON 内の `Customer` オブジェクトと `Employee` オブジェクトが正しく逆シリアル化されることを意味します。 逆シリアル化の間に、JSON で必要な型を識別する手掛かりを見つける必要があります。 使用できる手掛かりの種類は、シナリオによって異なります。 たとえば、識別子プロパティを使用できる場合や、特定のプロパティの有無に依存しなければならない場合があります。 `System.Text.Json` の現在のリリースでは、ポリモーフィックな逆シリアル化のシナリオを処理する方法を指定する属性が提供されていないため、カスタム コンバーターが必要になります。

次のコードでは、基底クラス、2 つの派生クラス、およびそれらのカスタム コンバーターを示します。 コンバーターでは、識別子プロパティを使用して、ポリモーフィックな逆シリアル化を行います。 型の識別子はクラス定義には含まれていませんが、シリアル化の間に作成され、逆シリアル化の間に読み取られます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/Person.cs?name=SnippetPerson)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs)]

次のコードではコンバーターが登録されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs?name=SnippetRegister)]

コンバーターでは、次のように、同じコンバーターを使用してシリアル化することによって作成された JSON を逆シリアル化できます。

```json
[
  {
    "TypeDiscriminator": 1,
    "CreditLimit": 10000,
    "Name": "John"
  },
  {
    "TypeDiscriminator": 2,
    "OfficeNumber": "555-1234",
    "Name": "Nancy"
  }
]
```

前の例のコンバーターのコードでは、各プロパティの読み取りと書き込みを手動で行います。 別の方法として、`Deserialize` または `Serialize` を呼び出すことにより、一部の作業を行うことができます。 例としては、[こちらの StackOverflow の投稿](https://stackoverflow.com/a/59744873/12509023)を参照してください。

### <a name="support-round-trip-for-stackt"></a>Stack\<T> のラウンドトリップをサポートする

JSON 文字列を <xref:System.Collections.Generic.Stack%601> オブジェクトに逆シリアル化した後、そのオブジェクトをシリアル化した場合、スタックの内容は逆の順序になります。 この動作は、次の型とインターフェイス、およびそれらから派生するユーザー定義型に適用されます。

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

スタックの元の順序を維持するシリアル化と逆シリアル化をサポートするには、カスタム コンバーターが必要です。

次のコードでは、`Stack<T>` オブジェクトとの間でのラウンドトリップを可能にするカスタム コンバーターを示します。

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs)]

次のコードではコンバーターが登録されます。

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs?name=SnippetRegister)]

## <a name="other-custom-converter-samples"></a>他のカスタム コンバーターのサンプル

[Newtonsoft.Json から System.Text.Json への移行](system-text-json-migrate-from-newtonsoft-how-to.md)に関する記事には、カスタム コンバーターの他のサンプルが含まれています。

`System.Text.Json.Serialization` のソース コードの[単体テスト フォルダー](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/)には、次のような他のカスタム コンバーターのサンプルが含まれています。

* [逆シリアル化時に null を 0 に変換する Int32 コンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)
* [逆シリアル化時に文字列値と数値の両方に対応できる Int32 コンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)
* [Enum コンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)
* [外部データを受け入れる List\<T> コンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)
* [コンマ区切りの数値リストを処理する Long[] コンバーター](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)

既存の組み込みコンバーターの動作を変更するコンバーターを作成する必要がある場合は、[既存のコンバーターのソース コード](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)を入手し、それを基にしてカスタマイズを始めることができ ます。

## <a name="additional-resources"></a>その他の技術情報

* [組み込みコンバーターのソース コード](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)
* [System.Text.Json での DateTime と DateTimeOffset のサポート](../datetime/system-text-json-support.md)
* [System.Text.Json の概要](system-text-json-overview.md)
* [System.Text.Json の使用方法](system-text-json-how-to.md)
* [Newtonsoft.Json から移行する方法](system-text-json-migrate-from-newtonsoft-how-to.md)
* [System.Text.Json API リファレンス](xref:System.Text.Json)
* [System.Text.Json.Serialization API リファレンス](xref:System.Text.Json.Serialization)
<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
