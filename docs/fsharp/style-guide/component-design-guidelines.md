---
title: F# コンポーネント デザインのガイドライン
description: '他の呼び出し元による使用を目的とした F # コンポーネントを作成するためのガイドラインについて説明します。'
ms.date: 05/14/2018
ms.openlocfilehash: 590bda0660d54ea73c590d31e694f3d499e0fd9f
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209137"
---
# <a name="f-component-design-guidelines"></a>F# コンポーネント デザインのガイドライン

このドキュメントは、f # コンポーネントの設計ガイドライン、v14、Microsoft Research、および最初に F # Software Foundation によって curated および保守されたバージョンに基づいて、F # プログラミングのコンポーネント設計ガイドラインのセットです。

このドキュメントでは、F # プログラミングに精通していることを前提としています。 F # コミュニティに感謝し、このガイドのさまざまなバージョンに関する投稿や役立つフィードバックをお寄せください。

## <a name="overview"></a>概要

このドキュメントでは、F # コンポーネントの設計とコーディングに関連するいくつかの問題について説明します。 コンポーネントは、次のいずれかを意味します。

* プロジェクト内の外部コンシューマーを持つ F # プロジェクト内のレイヤー。
* アセンブリ境界を越えて F # コードによる使用を目的としたライブラリ。
* アセンブリ境界を越えて .NET 言語による使用を目的としたライブラリ。
* [NuGet](https://nuget.org)などのパッケージリポジトリを使用した配布を目的としたライブラリ。

この記事で説明する手法は、[優れた F # コードの5つの原則](index.md#five-principles-of-good-f-code)に従っているため、必要に応じて機能とオブジェクトの両方のプログラミングを利用します。

どの方法論にもかかわらず、コンポーネントおよびライブラリデザイナーは、開発者が最も簡単に使用できる API を開発する際に、いくつかの実用的で prosaic の問題に直面しています。 [.Net ライブラリの設計ガイドライン](../../standard/design-guidelines/index.md)の Conscientious アプリケーションでは、使用してもよい api の一貫性のあるセットを作成することを目指しています。

## <a name="general-guidelines"></a>一般的なガイドライン

ライブラリの対象読者に関係なく、F # ライブラリに適用される汎用ガイドラインがいくつかあります。

### <a name="learn-the-net-library-design-guidelines"></a>.NET ライブラリのデザインガイドラインについて説明します。

実行する F # のコードの種類に関係なく、 [.Net ライブラリのデザインガイドライン](../../standard/design-guidelines/index.md)に関する実用的な知識があることが重要です。 その他のほとんどの F # と .NET プログラマーは、これらのガイドラインについて理解し、.NET コードに準拠していることを期待しています。

.NET ライブラリの設計ガイドラインでは、名前付け、クラスとインターフェイスの設計、メンバーのデザイン (プロパティ、メソッド、イベントなど) などの一般的なガイダンスを提供し、さまざまな設計ガイダンスについて、最初に参考にします。

### <a name="add-xml-documentation-comments-to-your-code"></a>XML ドキュメントコメントをコードに追加する

パブリック Api に関する XML ドキュメントでは、これらの型とメンバーを使用するときに、ユーザーが優れた Intellisense と Quickinfo を取得し、ライブラリのドキュメントファイルのビルドを有効にすることができます。 Xmldoc コメント内の追加のマークアップに使用できるさまざまな xml タグに関する[Xml ドキュメント](../language-reference/xml-documentation.md)を参照してください。

```fsharp
/// A class for representing (x,y) coordinates
type Point =

    /// Computes the distance between this point and another
    member DistanceTo: otherPoint:Point -> float
```

短い形式の XML コメント ( `/// comment` )、または標準の xml コメント () のいずれかを使用でき `///<summary>comment</summary>` ます。

### <a name="consider-using-explicit-signature-files-fsi-for-stable-library-and-component-apis"></a>安定したライブラリおよびコンポーネント Api に明示的な署名ファイル (fsi.exe) を使用することを検討してください。

F # ライブラリで明示的なシグネチャファイルを使用すると、パブリック API の簡潔な概要が提供されます。これにより、ライブラリの完全なパブリックサーフェスを確実に把握し、パブリックドキュメントと内部実装の詳細を明確に分離することができます。 シグネチャファイルは、実装ファイルと署名ファイルの両方で変更を行う必要があるため、パブリック API の変更に摩擦を追加します。 そのため、通常、署名ファイルは API が solidified になったときにのみ導入され、大幅に変更されることが予想されなくなります。

### <a name="always-follow-best-practices-for-using-strings-in-net"></a>.NET で文字列を使用する場合は常にベストプラクティスに従う

.NET のガイダンス[で文字列を使用するためのベストプラクティス](../../standard/base-types/best-practices-strings.md)に従ってください。 特に、文字列の変換と比較には、常に*カルチャの意図*を明示的に指定します (該当する場合)。

## <a name="guidelines-for-f-facing-libraries"></a>F # に接続されるライブラリのガイドライン

このセクションでは、パブリックな F # 向けライブラリの開発に関する推奨事項を示します。つまり、F # 開発者が使用することを意図したパブリック Api を公開するライブラリです。 特に F # には、ライブラリ設計に関するさまざまな推奨事項が適用されています。 以下の特定の推奨事項がない場合は、「.NET ライブラリの設計ガイドライン」がフォールバックガイダンスです。

### <a name="naming-conventions"></a>名前付け規則

#### <a name="use-net-naming-and-capitalization-conventions"></a>.NET の名前付け規則と大文字小文字の表記規則を使用する

次の表は、.NET の名前付け規則と大文字小文字の表記規則に従っています。 F # コンストラクトも含まれています。

| 構成体 | ケース | パーツ | 例 | Notes |
|-----------|------|------|----------|-------|
| 具象型 | パスカルケース | 名詞/形容詞 | List、Double、Complex | 具象型は、構造体、クラス、列挙体、デリゲート、レコード、および共用体です。 OCaml では、型名は従来は小文字ですが、F # では型の .NET 名前付けスキームが採用されています。
| DLL           | パスカルケース |                 | Fabrikam. Core .dll |  |
| 共用体タグ     | パスカルケース | [名詞] | Some、Add、Success | パブリック Api でプレフィックスを使用しないでください。 必要に応じて、内部でプレフィックスを使用します。たとえば、`type Teams = TAlpha | TBeta | TDelta.` |
| Event          | パスカルケース | 動詞 | ValueChanged/ValueChanging |  |
| 例外     | パスカルケース |      | WebException | 名前は "Exception" で終わる必要があります。 |
| フィールド          | パスカルケース | [名詞] | CurrentName  | |
| インターフェイス型 |  パスカルケース | 名詞/形容詞 | IDisposable | 名前は "I" で始まる必要があります。 |
| Method |  パスカルケース |  動詞 | ToString | |
| 名前空間 | パスカルケース | | Fsharp.core | 一般 `<Organization>.<Technology>[.<Subnamespace>]` に、テクノロジが組織に依存していない場合は、組織を削除します。 |
| パラメーター | キャメルケース | [名詞] |  typeName、transform、range | |
| let 値 (内部) | キャメルケースまたはパスワードの大文字と小文字の区別 | 名詞/動詞 |  getValue、myTable |
| let 値 (外部) | キャメルケースまたはパスワードの大文字と小文字の区別 | 名詞/動詞  | List. map, Dates. 今日 | 従来の機能デザインパターンに従うと、多くの場合、let バインド値がパブリックになります。 ただし、通常は、他の .NET 言語から識別子を使用できる場合は、文字を使用します。 |
| プロパティ  | パスカルケース  | 名詞/形容詞  | IsEndOfFile、BackColor  | 通常、ブール型プロパティではを使用し、IsNotEndOfFile ではなく IsEndOfFile のように肯定を使用できます。

#### <a name="avoid-abbreviations"></a>省略形を避ける

.NET ガイドラインでは、省略形を使用しないようにしています (たとえば、"ではなく" を使用し `OnButtonClick` `OnBtnClick` ます)。 "非同期" などの一般的な省略形 `Async` は許容されます。 このガイドラインは、関数型プログラミングでは無視されることがあります。たとえば、は `List.iter` "反復処理" の省略形を使用します。 このため、省略形を使用すると、F # から F # へのプログラミングにおいてより高い次数が許容されるようになりますが、一般に、パブリックコンポーネントの設計では回避できます。

#### <a name="avoid-casing-name-collisions"></a>名前の大文字と小文字の競合を避ける

.NET のガイドラインでは、一部のクライアント言語 (Visual Basic など) で大文字と小文字が区別されないため、名前の競合を明確に区別するために大文字と小文字を区別することはできません。

#### <a name="use-acronyms-where-appropriate"></a>必要に応じて頭字語を使用する

XML などの頭字語は省略形ではなく、.NET ライブラリでは Xml (xml) で広く使用されています。 よく知られている、広く認識されている頭字語だけを使用する必要があります。

#### <a name="use-pascalcase-for-generic-parameter-names"></a>汎用パラメーター名には、文字を使用する

パブリック Api のジェネリックパラメーター名には、(F # に対応するライブラリの場合を含む) を使用してください。 特に、、、などの名前を `T` `U` `T1` `T2` 任意のジェネリックパラメーターに使用し、特定の名前が意味する場合は、F # に接続されたライブラリでは `Key` 、、 `Value` `Arg` (たとえば、ではなく) のような名前を使用し `TKey` ます。

#### <a name="use-either-pascalcase-or-camelcase-for-public-functions-and-values-in-f-modules"></a>F # モジュールのパブリック関数と値には、キャメルケースを使用します。

キャメルケースは、非修飾 (など) で使用するように設計されたパブリック関数、 `invalidArg` および "標準コレクション関数" (たとえば、List. map) に使用されます。 どちらの場合も、関数名は言語のキーワードとよく似ています。

### <a name="object-type-and-module-design"></a>オブジェクト、型、およびモジュールのデザイン

#### <a name="use-namespaces-or-modules-to-contain-your-types-and-modules"></a>名前空間またはモジュールを使用して、型とモジュールを含める

コンポーネント内の各 F # ファイルは、名前空間宣言またはモジュール宣言で始まる必要があります。

```fsharp
namespace Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
     ...

module CommonOperations =
    ...
```

or

```fsharp
module Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
    ...

module CommonOperations =
    ...
```

モジュールと名前空間を使用して最上位レベルでコードを整理する場合の違いは次のとおりです。

* 名前空間は複数のファイルにまたがることができます。
* 内部モジュール内にある場合を除き、名前空間に F # 関数を含めることはできません
* 特定のモジュールのコードは、1つのファイル内に含まれている必要があります。
* トップレベルモジュールには、内部モジュールを必要とせずに F # 関数を含めることができます。

最上位レベルの名前空間またはモジュールのいずれかを選択すると、コードのコンパイルされた形式に影響します。したがって、API が F # コード外で最終的に使用される場合は、他の .NET 言語からのビューに影響します。

#### <a name="use-methods-and-properties-for-operations-intrinsic-to-object-types"></a>オブジェクトの種類に固有の操作に対してメソッドとプロパティを使用する

オブジェクトを使用する場合は、使用できる機能がその型のメソッドとプロパティとして実装されていることを確認することをお勧めします。

```fsharp
type HardwareDevice() =

    member this.ID = ...

    member this.SupportedProtocols = ...

type HashTable<'Key,'Value>(comparer: IEqualityComparer<'Key>) =

    member this.Add(key, value) = ...

    member this.ContainsKey(key) = ...

    member this.ContainsValue(value) = ...
```

特定のメンバーの機能の多くは、必ずしもそのメンバーに実装する必要はありませんが、その機能の利用可能な部分はにする必要があります。

#### <a name="use-classes-to-encapsulate-mutable-state"></a>クラスを使用して変更可能な状態をカプセル化する

F # では、その状態が、クロージャ、シーケンス式、非同期計算などの別の言語構成体によってまだカプセル化されていない場合にのみ、この操作を行う必要があります。

```fsharp
type Counter() =
    // let-bound values are private in classes.
    let mutable count = 0

    member this.Next() =
        count <- count + 1
        count
```

#### <a name="use-interfaces-to-group-related-operations"></a>インターフェイスを使用して関連する操作をグループ化する

インターフェイス型を使用して、一連の操作を表します。 これは、関数の組や関数のレコードなど、他のオプションにも適しています。

```fsharp
type Serializer =
    abstract Serialize<'T>: preserveRefEq: bool -> value: 'T -> string
    abstract Deserialize<'T>: preserveRefEq: bool -> pickle: string -> 'T
```

次のように設定します。

```fsharp
type Serializer<'T> = {
    Serialize: bool -> 'T -> string
    Deserialize: bool -> string -> 'T
}
```

インターフェイスは .NET のファーストクラスの概念であり、通常どのような機能を提供するかを実現するために使用できます。 また、プログラムに存在する型をエンコードするために使用することもできます。関数のレコードは使用できません。

#### <a name="use-a-module-to-group-functions-that-act-on-collections"></a>モジュールを使用して、コレクションに対して機能する関数をグループ化する

コレクション型を定義する場合は、 `CollectionType.map` `CollectionType.iter` 新しいコレクション型に対してやなどの標準的な操作のセットを提供することを検討してください。

```fsharp
module CollectionType =
    let map f c =
        ...
    let iter f c =
        ...
```

このようなモジュールを含める場合は、Fsharp.core で見つかった関数の標準的な名前付け規則に従います。

#### <a name="use-a-module-to-group-functions-for-common-canonical-functions-especially-in-math-and-dsl-libraries"></a>モジュールを使用して、一般的な正規関数の関数をグループ化します。数学および DSL ライブラリでは特にそうです。

たとえば、 `Microsoft.FSharp.Core.Operators` は、 `abs` `sin` fsharp.core によって提供されるトップレベル関数 (やなど) の自動オープンコレクションです。

同様に、統計ライブラリには関数と関数を含むモジュールが含まれている場合があり `erf` `erfc` ます。このモジュールは、明示的に、または自動的に開くように設計されています。

#### <a name="consider-using-requirequalifiedaccess-and-carefully-apply-autoopen-attributes"></a>RequireQualifiedAccess を使用して、AutoOpen 属性を慎重に適用することを検討してください。

モジュールに属性を追加すると、モジュールが `[<RequireQualifiedAccess>]` 開かれていないこと、およびモジュールの要素への参照に明示的な修飾アクセスが必要であることが示されます。 たとえば、モジュールに `Microsoft.FSharp.Collections.List` はこの属性があります。

これは、モジュールの関数と値の名前が、他のモジュールの名前と競合する可能性がある場合に便利です。 修飾されたアクセスを必要とすると、ライブラリの長期的な保守性と発展性を大幅に向上させることができます。

`[<AutoOpen>]`モジュールに属性を追加すると、含まれている名前空間を開いたときにモジュールが開かれることを意味します。 アセンブリ `[<AutoOpen>]` を参照するときに自動的に開くモジュールを示すために、属性をアセンブリに適用することもできます。

たとえば、統計ライブラリ**MathsHeaven**には、を `module MathsHeaven.Statistics.Operators` 含む関数とが含まれている場合があります。 `erf` `erfc` このモジュールをとしてマークするのは妥当です `[<AutoOpen>]` 。 また、 `open MathsHeaven.Statistics` このモジュールを開き、名前 `erf` とスコープをにすることもでき `erfc` ます。 のもう1つの優れた使用 `[<AutoOpen>]` 方法は、拡張メソッドを含むモジュールです。

`[<AutoOpen>]`潜在顧客を汚染され名前空間に使用すると、属性を慎重に使用する必要があります。 特定のドメイン内の特定のライブラリについては、を慎重 `[<AutoOpen>]` に使用することで、使いやすさを向上させることができます。

#### <a name="consider-defining-operator-members-on-classes-where-using-well-known-operators-is-appropriate"></a>よく知られている演算子を使用する場合は、クラスに演算子メンバーを定義することを検討してください。

ベクターなどの数学的構造をモデル化するために、クラスが使用されることがあります。 モデル化されているドメインに既知の演算子がある場合は、そのドメインをクラスに組み込まれているメンバーとして定義すると便利です。

```fsharp
type Vector(x: float) =

    member v.X = x

    static member (*) (vector: Vector, scalar: float) = Vector(vector.X * scalar)

    static member (+) (vector1: Vector, vector2: Vector) = Vector(vector1.X + vector2.X)

let v = Vector(5.0)

let u = v * 10.0
```

このガイダンスは、これらの型の .NET の一般的なガイダンスに対応しています。 ただし、F # コーディングではさらに重要になることがあります。これにより、これらの型を、# sumBy などのメンバー制約を持つ F # 関数およびメソッドと組み合わせて使用できるようになります。

#### <a name="consider-using-compiledname-to-provide-a-net-friendly-name-for-other-net-language-consumers"></a>CompiledName を使用してを提供することを検討してください。他の .NET 言語コンシューマーの NET フレンドリ名

場合によっては、F # コンシューマーの1つのスタイル (たとえば、小文字の静的メンバー) に名前を付けて、アセンブリにコンパイルされるときに、名前に異なるスタイルを使用することができます。 属性を使用して、 `[<CompiledName>]` F # 以外のコードでアセンブリを使用するための別のスタイルを指定できます。

```fsharp
type Vector(x:float, y:float) =

    member v.X = x
    member v.Y = y

    [<CompiledName("Create")>]
    static member create x y = Vector (x, y)

let v = Vector.create 5.0 3.0
```

を使用 `[<CompiledName>]` すると、アセンブリの F # 以外のコンシューマーに .net の名前付け規則を使用できます。

#### <a name="use-method-overloading-for-member-functions-if-doing-so-provides-a-simpler-api"></a>より単純な API を提供する場合は、メンバー関数に対してメソッドのオーバーロードを使用する

メソッドのオーバーロードは、同様の機能を実行する必要があるが、異なるオプションや引数を使用して API を簡素化するための強力なツールです。

```fsharp
type Logger() =

    member this.Log(message) =
        ...
    member this.Log(message, retryPolicy) =
        ...
```

F # では、引数の型ではなく、引数の数に対してオーバーロードする方が一般的です。

#### <a name="hide-the-representations-of-record-and-union-types-if-the-design-of-these-types-is-likely-to-evolve"></a>これらの型の設計が進化する可能性が高い場合に、レコードと共用体型の表現を非表示にする

オブジェクトの具象表現が明らかにならないようにします。 たとえば、値の具象表現 <xref:System.DateTime> は、.net ライブラリデザインの外部のパブリック API では公開されません。 実行時に共通言語ランタイムは、実行全体で使用されるコミット済みの実装を認識します。 ただし、コンパイルされたコード自体は、具象表現の依存関係を取得しません。

#### <a name="avoid-the-use-of-implementation-inheritance-for-extensibility"></a>拡張機能の実装継承の使用を回避する

F # では、実装の継承はほとんど使用されません。 また、多くの場合、継承階層は複雑で、新しい要件が発生したときに変更するのは困難です。 互換性のために F # には継承の実装が存在しますが、問題の解決策として最適なソリューションであることがありますが、インターフェイスの実装など、ポリモーフィズムを設計する際には、F # プログラムで代替手法を検討する必要があります。

### <a name="function-and-member-signatures"></a>関数とメンバーのシグネチャ

#### <a name="use-tuples-for-return-values-when-returning-a-small-number-of-multiple-unrelated-values"></a>複数の関連性のない値の数が少ない場合に、戻り値に組を使用する

戻り値の型で組を使用する場合の適切な例を次に示します。

```fsharp
val divrem: BigInteger -> BigInteger -> BigInteger * BigInteger
```

多くのコンポーネントを含む戻り値の型、またはコンポーネントが1つの特定可能なエンティティに関連する場合は、タプルではなく名前付きの型を使用することを検討してください。

#### <a name="use-asynct-for-async-programming-at-f-api-boundaries"></a>`Async<T>`F # API の境界で非同期プログラミングに使用する

という名前の同期操作があり、それによってが返される場合、 `Operation` 非同期操作は、を返す場合は、それが返される場合 `T` はという名前にする必要があり `AsyncOperation` `Async<T>` `OperationAsync` `Task<T>` ます。 Begin/End メソッドを公開する一般的に使用される .NET 型については、を使用して、 `Async.FromBeginEnd` その .Net api に F # の非同期プログラミングモデルを提供するための拡張メソッドをファサードとして記述することを検討してください。

```fsharp
type SomeType =
    member this.Compute(x:int): int =
        ...
    member this.AsyncCompute(x:int): Async<int> =
        ...

type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        ...
```

### <a name="exceptions"></a>例外

例外、結果、およびオプションの適切な使用方法については、「[エラー管理](conventions.md#error-management)」を参照してください。

### <a name="extension-members"></a>拡張メンバー

#### <a name="carefully-apply-f-extension-members-in-f-to-f-components"></a>F # から f # のコンポーネントに F # 拡張メンバーを慎重に適用する

F # 拡張メンバーは、一般に使用されているほとんどのモードの型に関連付けられている組み込み操作を終了する操作にのみ使用する必要があります。 一般的な用途の1つは、さまざまな .NET 型に対して F # に慣用的なする Api を提供することです。

```fsharp
type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        Async.FromBeginEnd(this.BeginReceive, this.EndReceive)

type System.Collections.Generic.IDictionary<'Key,'Value> with
    member this.TryGet key =
        let ok, v = this.TryGetValue key
        if ok then Some v else None
```

### <a name="union-types"></a>共用体型

#### <a name="use-discriminated-unions-instead-of-class-hierarchies-for-tree-structured-data"></a>ツリー構造データのクラス階層の代わりに判別共用体を使用する

ツリーのような構造体は再帰的に定義されます。 これは継承には不便ですが、判別共用体を使用すると洗練されています。

```fsharp
type BST<'T> =
    | Empty
    | Node of 'T * BST<'T> * BST<'T>
```

また、判別共用体を使用してツリーのようなデータを表すことで、パターンマッチングで exhaustiveness を活用することもできます。

#### <a name="use-requirequalifiedaccess-on-union-types-whose-case-names-are-not-sufficiently-unique"></a>`[<RequireQualifiedAccess>]`ケース名が十分に一意でない共用体型で使用する

判別共用体のケースなど、さまざまな項目に対して、同じ名前が最適な名前であるドメインが存在する場合があります。 を使用すると `[<RequireQualifiedAccess>]` 、ステートメントの順序に依存するシャドウが原因で混乱エラーが発生しないようにするために、ケース名を明確にすることができます。 `open`

#### <a name="hide-the-representations-of-discriminated-unions-for-binary-compatible-apis-if-the-design-of-these-types-is-likely-to-evolve"></a>これらの型の設計が進化する可能性がある場合は、バイナリ互換の Api の判別共用体の表現を非表示にします

共用体の型は、簡潔なプログラミングモデルの F # パターンマッチングフォームに依存しています。 前述のように、これらの型の設計が進化する可能性がある場合は、具象データ表現が明らかにならないようにする必要があります。

たとえば、判別共用体の表現は、プライベートまたは内部の宣言を使用して、または署名ファイルを使用して非表示にすることができます。

```fsharp
type Union =
    private
    | CaseA of int
    | CaseB of string
```

判別共用体をむやみに明らかにすると、ユーザーコードを壊さずにライブラリのバージョンを作成することが困難になる場合があります。 代わりに、1つまたは複数のアクティブパターンを明らかにして、型の値に対するパターンマッチングを許可することを検討してください。

アクティブパターンを使用すると、f # のコンシューマーにパターンマッチングを提供する代わりに、F # 共用体型を直接公開しないようにすることができます。

### <a name="inline-functions-and-member-constraints"></a>インライン関数とメンバー制約

#### <a name="define-generic-numeric-algorithms-using-inline-functions-with-implied-member-constraints-and-statically-resolved-generic-types"></a>暗黙的なメンバー制約と静的に解決されるジェネリック型を持つインライン関数を使用して、汎用数値アルゴリズムを定義します。

算術メンバー制約と F # 比較制約は、F # プログラミングの標準です。 次に例を示します。

```fsharp
let inline highestCommonFactor a b =
    let rec loop a b =
        if a = LanguagePrimitives.GenericZero<_> then b
        elif a < b then loop a (b - a)
        else loop (a - b) b
    loop a b
```

この関数の型は次のとおりです。

```fsharp
val inline highestCommonFactor : ^T -> ^T -> ^T
                when ^T : (static member Zero : ^T)
                and ^T : (static member ( - ) : ^T * ^T -> ^T)
                and ^T : equality
                and ^T : comparison
```

これは、数学的ライブラリのパブリック API に適した関数です。

#### <a name="avoid-using-member-constraints-to-simulate-type-classes-and-duck-typing"></a>型クラスとアヒル型のシミュレーションにメンバー制約を使用しない

F # メンバー制約を使用して "アヒル入力" をシミュレートすることができます。 ただし、このを使用するメンバーは、F #-F # ライブラリの設計では一般的に使用されません。 これは、不明または非標準の暗黙的な制約に基づくライブラリデザインが、ユーザーコードが柔軟性を持たなくなり、1つの特定のフレームワークパターンに関連付けられる可能性があるためです。

また、このような方法でメンバー制約を多用すると、コンパイル時間が非常に長くなる可能性があります。

### <a name="operator-definitions"></a>演算子の定義

#### <a name="avoid-defining-custom-symbolic-operators"></a>カスタムのシンボリック演算子を定義しない

カスタム演算子は、状況によっては不可欠であり、大規模な数値表記の実装コード内でデバイスを使用すると非常に便利です。 ライブラリの新しいユーザーには、多くの場合、名前付き関数を使用する方が簡単です。 さらに、カスタムのシンボリック演算子をドキュメント化するのは難しい場合があります。また、ユーザーは、IDE や検索エンジンの既存の制限事項により、演算子のヘルプを検索するのが難しくなります。

そのため、機能を名前付きの関数やメンバーとして公開することをお勧めします。また、この機能のための演算子を公開するのは、数値表記の利点がドキュメントとそれを持つ認知コストを上回る場合に限られます。

### <a name="units-of-measure"></a>測定単位

#### <a name="carefully-use-units-of-measure-for-added-type-safety-in-f-code"></a>F # コードでタイプセーフを追加するために、測定単位を慎重に使用する

測定単位の追加の入力情報は、他の .NET 言語で表示すると消去されます。 .NET のコンポーネント、ツール、およびリフレクションでは、種類が san 単位であることに注意してください。 たとえば、C# のコンシューマーはで `float` はなくを参照し `float<kg>` ます。

### <a name="type-abbreviations"></a>型略称

#### <a name="carefully-use-type-abbreviations-to-simplify-f-code"></a>F # コードを簡略化するために型略称を慎重に使用する

.NET のコンポーネント、ツール、およびリフレクションでは、型の省略名は表示されません。 また、型の省略形を頻繁に使用することで、ドメインを実際のより複雑にすることもできます。これにより、コンシューマーを混乱させる可能性があります。

#### <a name="avoid-type-abbreviations-for-public-types-whose-members-and-properties-should-be-intrinsically-different-to-those-available-on-the-type-being-abbreviated"></a>メンバーとプロパティは、省略されている型で使用できるものと本質的に異なる必要があるパブリック型の型略称を避けてください。

この場合、省略されている型は、定義されている実際の型の表現に関してあまり多くを意味します。 代わりに、クラス型または単一ケースの判別共用体の省略形をラップすることを検討してください (または、パフォーマンスが重要な場合は、構造体型を使用して省略形をラップすることを検討してください)。

たとえば、次のように、F # マップの特殊なケースとしてマルチマップを定義することをお勧めします。

```fsharp
type MultiMap<'Key,'Value> = Map<'Key,'Value list>
```

ただし、この型の論理ドット表記演算は、マップ上の操作と同じではありません。たとえば、lookup 操作では適切です。[key] 例外を発生させるのではなく、キーがディクショナリに含まれていない場合は、空のリストを返します。

## <a name="guidelines-for-libraries-for-use-from-other-net-languages"></a>他の .NET 言語から使用するためのライブラリのガイドライン

他の .NET 言語で使用するためのライブラリを設計する場合は、 [.Net ライブラリのデザインガイドライン](../../standard/design-guidelines/index.md)に従うことが重要です。 このドキュメントでは、これらのライブラリには、制限なしで F # のコンストラクトを使用する F # 向けのライブラリではなく、バニラ .NET ライブラリというラベルが付けられています。 バニラ .NET ライブラリの設計は、パブリック API で F # 固有の構造を使用することを最小限にすることで、使い慣れた Api と慣用的な Api を他の .NET Framework と一貫性のあるものにすることを意味します。 これらの規則については、次のセクションで説明します。

### <a name="namespace-and-type-design-for-libraries-for-use-from-other-net-languages"></a>名前空間と型のデザイン (他の .NET 言語から使用するライブラリ用)

#### <a name="apply-the-net-naming-conventions-to-the-public-api-of-your-components"></a>コンポーネントのパブリック API に .NET の名前付け規則を適用する

省略名と .NET の大文字と小文字のガイドラインを使用することに特に注意してください。

```fsharp
type pCoord = ...
    member this.theta = ...

type PolarCoordinate = ...
    member this.Theta = ...
```

#### <a name="use-namespaces-types-and-members-as-the-primary-organizational-structure-for-your-components"></a>コンポーネントの主要な組織構造として名前空間、型、およびメンバーを使用する

パブリック機能を含むすべてのファイルは、宣言で始まる必要があり `namespace` ます。また、名前空間の公開されているエンティティは型だけです。 F # モジュールは使用しないでください。

非パブリックモジュールを使用して、実装コード、ユーティリティの種類、およびユーティリティ関数を保持します。

オーバーロードや、F # モジュール内で使用できないその他の .NET API デザインの概念を使用するように API を将来進化させることができるため、モジュールよりも静的な型を使用することをお勧めします。

たとえば、次のパブリック API の代わりに使用します。

```fsharp
module Fabrikam

module Utilities =
    let Name = "Bob"
    let Add2 x y = x + y
    let Add3 x y z = x + y + z
```

代わりに、次の点を考慮してください。

```fsharp
namespace Fabrikam

[<AbstractClass; Sealed>]
type Utilities =
    static member Name = "Bob"
    static member Add(x,y) = x + y
    static member Add(x,y,z) = x + y + z
```

#### <a name="use-f-record-types-in-vanilla-net-apis-if-the-design-of-the-types-wont-evolve"></a>型の設計が進化しない場合は、バニラ .NET Api で F # のレコード型を使用する

F # のレコード型は、単純な .NET クラスにコンパイルされます。 これらは、Api のいくつかの単純な安定した型に適しています。 `[<NoEquality>]` `[<NoComparison>]` インターフェイスの自動生成を抑制するには、属性と属性を使用することを検討してください。 また、バニラ .NET Api では、パブリックフィールドを公開するため、変更可能なレコードフィールドを使用しないようにします。 クラスが将来の API の進化に対してより柔軟なオプションを提供するかどうかを常に検討してください。

たとえば、次の F # コードでは、パブリック API を C# コンシューマーに公開しています。

F#: 

```fsharp
[<NoEquality; NoComparison>]
type MyRecord =
    { FirstThing: int
        SecondThing: string }
```

C#:

```csharp
public sealed class MyRecord
{
    public MyRecord(int firstThing, string secondThing);
    public int FirstThing { get; }
    public string SecondThing { get; }
}
```

#### <a name="hide-the-representation-of-f-union-types-in-vanilla-net-apis"></a>バニラ .NET Api で F # 共用体型の表現を非表示にする

F # から F # へのコーディングでも、f # の共用体型は、コンポーネントの境界を越えて使用されることはよくありません。 これらは、コンポーネントおよびライブラリ内で内部的に使用される場合に、優れた実装デバイスです。

バニラ .NET API を設計するときは、プライベート宣言または署名ファイルを使用して、共用体型の表現を非表示にすることを検討してください。

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True
```

また、共用体表現をメンバーで内部的に使用する型を拡張して、必要なを提供することもできます。NET に接続する API。

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True

    /// A public member for use from C#
    member x.Evaluate =
        match x with
        | And(a,b) -> a.Evaluate && b.Evaluate
        | Not a -> not a.Evaluate
        | True -> true

    /// A public member for use from C#
    static member CreateAnd(a,b) = And(a,b)
```

#### <a name="design-gui-and-other-components-using-the-design-patterns-of-the-framework"></a>フレームワークの設計パターンを使用した GUI とその他のコンポーネントの設計

.NET 内には、WinForms、WPF、ASP.NET など、さまざまなフレームワークが用意されています。 これらのフレームワークで使用するコンポーネントを設計する場合は、それぞれの名前付けと設計規則を使用する必要があります。 たとえば、WPF プログラミングでは、設計するクラスの WPF デザインパターンを採用します。 ユーザーインターフェイスプログラミングのモデルの場合は、イベントや、にあるような通知ベースのコレクションなどのデザインパターンを使用し <xref:System.Collections.ObjectModel> ます。

### <a name="object-and-member-design-for-libraries-for-use-from-other-net-languages"></a>オブジェクトとメンバーのデザイン (他の .NET 言語から使用するためのライブラリ用)

#### <a name="use-the-clievent-attribute-to-expose-net-events"></a>CLIEvent 属性を使用して .NET イベントを公開する

`DelegateEvent`オブジェクトと (既定では型を使用するのではなく) を受け取る特定の .net デリゲート型を使用してを構築し `EventArgs` `Event` `FSharpHandler` ます。これにより、イベントが他の .net 言語になじみのある方法で公開されるようになります。

```fsharp
type MyBadType() =
    let myEv = new Event<int>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish

type MyEventArgs(x: int) =
    inherit System.EventArgs()
    member this.X = x

    /// A type in a component designed for use from other .NET languages
type MyGoodType() =
    let myEv = new DelegateEvent<EventHandler<MyEventArgs>>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish
```

#### <a name="expose-asynchronous-operations-as-methods-that-return-net-tasks"></a>.NET タスクを返すメソッドとしての非同期操作の公開

タスクは、アクティブな非同期計算を表すために .NET で使用されます。 タスクは `Async<T>` 、"既に実行中" のタスクを表し、並列合成を実行する方法でまとめて構成することも、キャンセルシグナルやその他のコンテキストパラメーターの伝達を非表示にすることもできないため、F # のオブジェクトよりも一般的にはありません。

ただし、このような場合でも、タスクを返すメソッドは、.NET での非同期プログラミングの標準的な表現です。

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =

    let compute (x: int): Async<int> = async { ... }

    member this.ComputeAsync(x) = compute x |> Async.StartAsTask
```

また、明示的なキャンセルトークンを使用することもよくあります。

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =
    let compute(x: int): Async<int> = async { ... }
    member this.ComputeAsTask(x, cancellationToken) = Async.StartAsTask(compute x, cancellationToken)
```

#### <a name="use-net-delegate-types-instead-of-f-function-types"></a>F # 関数型の代わりに .NET デリゲート型を使用する

ここで "F # の関数型" は、のような型 `int -> int` を意味します。

次のようになります。

```fsharp
member this.Transform(f: int->int) =
    ...
```

これを行うには、次の手順を実行します。

```fsharp
member this.Transform(f: Func<int,int>) =
    ...
```

F # の関数型は、 `class FSharpFunc<T,U>` 他の .net 言語と同様に表示され、デリゲート型を理解する言語の機能やツールには適していません。 .NET Framework 3.5 以上を対象とする高階メソッドを作成する場合、 `System.Func` `System.Action` .net 開発者が低摩擦方式でこれらの api を使用できるようにするために、とデリゲートは発行する適切な api です。 (.NET Framework 2.0 を対象とする場合、システム定義のデリゲート型の方が制限されます。などの定義済みデリゲート型を使用する `System.Converter<T,U>` か、特定のデリゲート型を定義することを検討してください。)

フリップ側では、.NET デリゲートは F # 向けのライブラリに対しては自然なものではありません (F # に接続されたライブラリについては、次のセクションを参照してください)。 そのため、バニラ .NET ライブラリの高階メソッドを開発する際には、一般的な実装方法として、F # の関数型を使用してすべての実装を作成し、その後、実際の F # 実装の上にあるシンファサードとしてデリゲートを使用してパブリック API を作成します。

#### <a name="use-the-trygetvalue-pattern-instead-of-returning-f-option-values-and-prefer-method-overloading-to-taking-f-option-values-as-arguments"></a>F # のオプション値を返すのではなく、TryGetValue パターンを使用し、引数として F # オプションの値を取得するためにメソッドのオーバーロードを優先します。

Api での F # オプション型の一般的な使用パターンは、標準の .NET 設計手法を使用して、バニラ .NET Api での実装がより適切です。 F # オプションの値を返す代わりに、bool の戻り値の型と out パラメーターを "TryGetValue" パターンのように使用することを検討してください。 F # オプションの値をパラメーターとして使用するのではなく、メソッドのオーバーロードまたは省略可能な引数を使用することを検討してください。

```fsharp
member this.ReturnOption() = Some 3

member this.ReturnBoolAndOut(outVal: byref<int>) =
    outVal <- 3
    true

member this.ParamOption(x: int, y: int option) =
    match y with
    | Some y2 -> x + y2
    | None -> x

member this.ParamOverload(x: int) = x

member this.ParamOverload(x: int, y: int) = x + y
```

#### <a name="use-the-net-collection-interface-types-ienumerablet-and-idictionarykeyvalue-for-parameters-and-return-values"></a>.NET コレクションインターフェイスの型 IEnumerable \< T \> と IDictionary \< キー、 \> パラメーターと戻り値の値を使用します。

.NET 配列 `T[]` 、F # 型、などの具象コレクション型やなどの `list<T>` `Map<Key,Value>` `Set<T>` .net 具象コレクション型は使用しないようにして `Dictionary<Key,Value>` ください。 .NET ライブラリの設計ガイドラインでは、などのさまざまなコレクション型を使用するタイミングに関するアドバイスがあり `IEnumerable<T>` ます。 一部の `T[]` 状況では、パフォーマンス grounds で配列 () を使用することができます。 特に `seq<T>` 、はの F # エイリアスであるため、 `IEnumerable<T>` seq は通常はバニラ .net API に適した型です。

F # リストの代わりに、次のようになります。

```fsharp
member this.PrintNames(names: string list) =
    ...
```

F # のシーケンスを使用します。

```fsharp
member this.PrintNames(names: seq<string>) =
    ...
```

#### <a name="use-the-unit-type-as-the-only-input-type-of-a-method-to-define-a-zero-argument-method-or-as-the-only-return-type-to-define-a-void-returning-method"></a>ゼロ引数メソッドを定義するメソッドの唯一の入力型として、または void を返すメソッドを定義する唯一の戻り値の型として、単位の種類を使用します。

ユニットの種類の他の用途は避けてください。 次のような方法があります。

```fsharp
✔ member this.NoArguments() = 3

✔ member this.ReturnVoid(x: int) = ()
```

これは問題です。

```fsharp
member this.WrongUnit( x: unit, z: int) = ((), ())
```

#### <a name="check-for-null-values-on-vanilla-net-api-boundaries"></a>バニラ .NET API の境界で null 値を確認する

F # の実装コードでは、変更できないデザインパターンと F # 型の null リテラルの使用に関する制限があるため、null 値が少なくなる傾向があります。 その他の .NET 言語では、多くの場合、値として null が使用されます。 このため、バニラ .NET API を公開する F # コードは、API の境界で null のパラメーターをチェックし、これらの値が F # の実装コードに深く流れないようにする必要があります。 `isNull`パターンに対する関数またはパターンマッチングを `null` 使用できます。

```fsharp
let checkNonNull argName (arg: obj) =
    match arg with
    | null -> nullArg argName
    | _ -> ()

let checkNonNull` argName (arg: obj) =
    if isNull arg then nullArg argName
    else ()
```

#### <a name="avoid-using-tuples-as-return-values"></a>戻り値としてタプルを使用しない

代わりに、集計データを保持する名前付きの型を返すか、out パラメーターを使用して複数の値を返すことをお勧めします。 タプルと構造体の組は .NET に存在しますが (構造体の組に対する C# 言語のサポートを含む)、ほとんどの場合、.NET 開発者にとって理想的で期待される API を提供しません。

#### <a name="avoid-the-use-of-currying-of-parameters"></a>パラメーターのカリー化を使用しないようにする

代わりに、.NET の呼び出し規約を使用して `Method(arg1,arg2,…,argN)` ください。

```fsharp
member this.TupledArguments(str, num) = String.replicate num str
```

ヒント: 任意の .NET 言語で使用するためのライブラリを設計する場合、実際には、いくつかの試験的な C# および Visual Basic プログラミングを行って、これらの言語からライブラリが正しく動作するようにするための代替手段はありません。 .NET リフレクターや Visual Studio オブジェクトブラウザーなどのツールを使用して、ライブラリとそのドキュメントが開発者に期待どおりに表示されるようにすることもできます。

## <a name="appendix"></a>付録

### <a name="end-to-end-example-of-designing-f-code-for-use-by-other-net-languages"></a>他の .NET 言語で使用する F # コードを設計するためのエンドツーエンドの例

次のクラスについて考えてみます。

```fsharp
open System

type Point1(angle,radius) =
    new() = Point1(angle=0.0, radius=0.0)
    member x.Angle = angle
    member x.Radius = radius
    member x.Stretch(l) = Point1(angle=x.Angle, radius=x.Radius * l)
    member x.Warp(f) = Point1(angle=f(x.Angle), radius=x.Radius)
    static member Circle(n) =
        [ for i in 1..n -> Point1(angle=2.0*Math.PI/float(n), radius=1.0) ]
```

このクラスの推定 F # 型は次のとおりです。

```fsharp
type Point1 =
    new : unit -> Point1
    new : angle:double * radius:double -> Point1
    static member Circle : n:int -> Point1 list
    member Stretch : l:double -> Point1
    member Warp : f:(double -> double) -> Point1
    member Angle : double
    member Radius : double
```

この F # の型が、プログラマに別の .NET 言語を使用してどのように表示されるかを見てみましょう。 たとえば、C# のおおよその "シグニチャ" は次のようになります。

```csharp
// C# signature for the unadjusted Point1 class
public class Point1
{
    public Point1();

    public Point1(double angle, double radius);

    public static Microsoft.FSharp.Collections.List<Point1> Circle(int count);

    public Point1 Stretch(double factor);

    public Point1 Warp(Microsoft.FSharp.Core.FastFunc<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

ここでは、F # がコンストラクトを表す方法について注意する必要がある重要な点がいくつかあります。 次に例を示します。

* 引数名などのメタデータは保持されています。

* 2つの引数を受け取る F # メソッドは、2つの引数を受け取る C# メソッドになります。

* 関数とリストは、F # ライブラリ内の対応する型への参照になります。

次のコードは、このコードを調整してこれらの処理を考慮する方法を示しています。

```fsharp
namespace SuperDuperFSharpLibrary.Types

type RadialPoint(angle:double, radius:double) =

    /// Return a point at the origin
    new() = RadialPoint(angle=0.0, radius=0.0)

    /// The angle to the point, from the x-axis
    member x.Angle = angle

    /// The distance to the point, from the origin
    member x.Radius = radius

    /// Return a new point, with radius multiplied by the given factor
    member x.Stretch(factor) =
        RadialPoint(angle=angle, radius=radius * factor)

    /// Return a new point, with angle transformed by the function
    member x.Warp(transform:Func<_,_>) =
        RadialPoint(angle=transform.Invoke angle, radius=radius)

    /// Return a sequence of points describing an approximate circle using
    /// the given count of points
    static member Circle(count) =
        seq { for i in 1..count ->
                RadialPoint(angle=2.0*Math.PI/float(count), radius=1.0) }
```

コードの推論された F # の型は次のとおりです。

```fsharp
type RadialPoint =
    new : unit -> RadialPoint
    new : angle:double * radius:double -> RadialPoint
    static member Circle : count:int -> seq<RadialPoint>
    member Stretch : factor:double -> RadialPoint
    member Warp : transform:System.Func<double,double> -> RadialPoint
    member Angle : double
    member Radius : double
```

C# のシグネチャは、次のようになりました。

```csharp
public class RadialPoint
{
    public RadialPoint();

    public RadialPoint(double angle, double radius);

    public static System.Collections.Generic.IEnumerable<RadialPoint> Circle(int count);

    public RadialPoint Stretch(double factor);

    public RadialPoint Warp(System.Func<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

バニラ .NET ライブラリの一部として使用するために、この型を準備するために行われた修正は次のとおりです。

* いくつかの名前が調整されました。、、 `Point1` `n` `l` 、およびは `f` `RadialPoint` 、それぞれ、、、 `count` `factor` および `transform` です。

* を使用する `seq<RadialPoint>` `RadialPoint list` シーケンス構造を使用して、を使用してリストの構築を変更することで、ではなく戻り値の型を使用していま `[ ... ]` `IEnumerable<RadialPoint>` した。

* F # 関数型ではなく、.NET デリゲート型を使用して `System.Func` います。

これにより、C# コードでの使用がはるかに簡単になります。
