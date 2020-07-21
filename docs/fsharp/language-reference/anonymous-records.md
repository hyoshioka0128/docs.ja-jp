---
title: 匿名のレコード
description: データの操作に役立つ言語機能である匿名レコードの構築および使用方法について説明します。
ms.date: 06/12/2019
ms.openlocfilehash: 121f0f638dff2ae529b2488d8e3b1ad9c064cf90
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81738496"
---
# <a name="anonymous-records"></a>匿名のレコード

匿名レコードは、使用する前に宣言する必要のない名前付き値の単純な集計です。 これらの変数は、構造体または参照型として宣言できます。 これらは既定で参照型です。

## <a name="syntax"></a>構文

次の例は、匿名レコードの構文を示しています。 オプションで`[item]`区切られた項目。

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a>基本的な使用方法

匿名レコードは、インスタンス化の前に宣言する必要がない F# レコード型として考えるのが最適です。

たとえば、匿名レコードを生成する関数と対話する方法を次に示します。

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

次の例では、入力として匿名レコードを受`printCircleStats`け取る関数を使用して、前の例を展開します。

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

入力`printCircleStats`型と同じ "shape" を持たない匿名レコード型を使用して呼び出すと、コンパイルに失敗します。

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a>匿名レコードの構造化

匿名レコードは、省略可能`struct`なキーワードを使用して struct として定義することもできます。 次の例では、構造体の匿名レコードを生成して使用することで、上記のレコードを強化します。

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a>構造体の推論

構造体の匿名レコードでは、呼び出しサイトで`struct`キーワードを指定する必要がない「構造体の推論」も可能です。 この例では、 を呼び`struct`出すとき`printCircleStats`にキーワードをエリデします。

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

入力型が構造体の匿名`struct`レコードでない場合に指定する逆のパターンは、コンパイルに失敗します。

## <a name="embedding-anonymous-records-within-other-types"></a>他の型に匿名レコードを埋め込む

ケースがレコードである[判別共用体](discriminated-unions.md)を宣言すると便利です。 ただし、レコード内のデータが判別共用体と同じ型の場合は、すべての型を相互再帰として定義する必要があります。 匿名レコードを使用すると、この制限を回避できます。 次に、パターンが一致する型と関数の例を示します。

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named record for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a>式のコピーと更新

匿名レコードは[、コピー式と更新式](copy-and-update-record-expressions.md)を使用した構築をサポートします。 たとえば、既存のデータをコピーする匿名レコードの新しいインスタンスを作成する方法を次に示します。

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

ただし、名前付きレコードとは異なり、匿名レコードを使用すると、コピー式と更新式を使用してまったく異なるフォームを作成できます。 次の例では、前の例と同じ匿名レコードを取得し、新しい匿名レコードに拡張します。

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

名前付きレコードのインスタンスから匿名レコードを作成することもできます。

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

また、参照レコードと構造体匿名レコードとの間でデータをコピーすることもできます。

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a>匿名レコードのプロパティ

匿名レコードには、その使用方法を完全に理解するために不可欠な特性が多数あります。

### <a name="anonymous-records-are-nominal"></a>匿名レコードは名目上のレコードです

匿名レコードは[名義型 です](https://en.wikipedia.org/wiki/Nominal_type_system)。 これらは、事前宣言を必要としない名前付き[レコード](records.md)型 (名義型) として考えるのが最善です。

次の例を 2 つの匿名レコード宣言で考えてみます。

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

`x`と`y`の値は異なる型を持ち、互いに互換性がありません。 彼らは等しいものではなく、比較できません。 これを説明するために、名前付きレコードと同等の名前を考えてみましょう。

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

型の等価性または比較に関しては、名前付きレコードと同等の名前を付けると、匿名レコードについて本質的に違いはありません。

### <a name="anonymous-records-use-structural-equality-and-comparison"></a>匿名レコードは構造的な等価性と比較を使用する

レコードの種類と同様に、匿名レコードも構造的に同等であり、同等です。 これは、すべての構成型が等価と比較をサポートする場合にのみ当てはまります 。(レコードの種類と同様)。 等値または比較をサポートするには、2 つの匿名レコードが同じ "図形" を持つ必要があります。

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a>匿名レコードはシリアル化可能

名前付きレコードと同様に、匿名レコードをシリアル化できます。 ニュートン[ソフト.Json](https://www.nuget.org/packages/Newtonsoft.Json/)を使用した例を次に示します。

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn "Name: %s Age: %d" phillip.name phillip.age
```

匿名レコードは、シリアル化/逆シリアル化された型のドメインを事前に定義する必要なしに、ネットワーク経由で軽量データを送信する場合に便利です。

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a>匿名レコードは C# の匿名型と相互運用できる

[C# 匿名型](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)の使用を必要とする .NET API を使用できます。 C# 匿名型は、匿名レコードを使用して相互運用するのは簡単です。 次の例は、匿名レコードを使用して、匿名型を必要とする[LINQ](../../csharp/programming-guide/concepts/linq/index.md)オーバーロードを呼び出す方法を示しています。

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn "%s has first letter %c" ng.Name ng.FirstLetter
```

匿名型の渡しを使用する必要がある他の多数の API が .NET 全体で使用されています。 匿名レコードは、それらを操作するためのツールです。

## <a name="limitations"></a>制限事項

匿名レコードの使用にはいくつかの制限があります。 デザインに固有のものもありますが、変更が可能なものもあります。

### <a name="limitations-with-pattern-matching"></a>パターンマッチングの制限

匿名レコードは、名前付きレコードとは異なり、パターン マッチングをサポートしません。 次の 3 つの理由があります。

1. 名前付きレコードの種類とは異なり、パターンは匿名レコードのすべてのフィールドを考慮する必要があります。 これは、匿名レコードは構造サブタイプをサポートしていないためです。
2. (1) の場合、パターン一致式に追加のパターンを持つ機能はありません。
3. (3) の場合、匿名レコード パターンは"ドット" 表記の使用よりも詳細になります。

[限られたコンテキストでパターンマッチングを可能](https://github.com/fsharp/fslang-suggestions/issues/713)にするオープン言語の提案があります。

### <a name="limitations-with-mutability"></a>変異性に関する制限

現在、データを使用`mutable`して匿名レコードを定義することはできません。 変更可能なデータを許可する[オープン言語の提案](https://github.com/fsharp/fslang-suggestions/issues/732)があります。

### <a name="limitations-with-struct-anonymous-records"></a>構造体匿名レコードの制限

構造体匿名レコードを または`IsByRefLike``IsReadOnly`として宣言することはできません。 オープン言語の[提案](https://github.com/fsharp/fslang-suggestions/issues/712)`IsByRefLike`と`IsReadOnly`匿名のレコードがあります。
