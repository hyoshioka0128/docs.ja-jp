---
title: コンピュテーション式
description: 制御フローの構成体とバインディングを使用してシーケンス処理および結合できる、F# で計算を記述するための便利な構文を作成する方法について説明します。
ms.date: 11/04/2019
ms.openlocfilehash: 55406cc12d9e6e890fe69d712f79486d23b84452
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401083"
---
# <a name="computation-expressions"></a>コンピュテーション式

F# の計算式は、制御フローの構成体とバインディングを使用してシーケンス処理および結合できる計算を記述するための便利な構文を提供します。 計算式の種類に応じて、モナド、モノイド、モナド変圧器、および適用的なファンクタを表現する方法として考えることができます。 しかし、他の言語 (Haskell の*記述*など) とは異なり、それらは単一の抽象化に結び付けられておらず、便利で状況に応じて構文を実行するためにマクロやその他の形のメタプログラミングに依存しません。

## <a name="overview"></a>概要

計算には多くの形式があります。 最も一般的な計算形式はシングルスレッド実行であり、これは理解しやすく、変更が容易です。 ただし、すべての形式の計算がシングルスレッド実行ほど簡単ではありません。 次に例をいくつか示します。

- 非決定論的計算
- 非同期計算
- 効果のある計算
- 生成計算

より一般的には、*アプリケーションの特定の*部分で実行する必要がある状況依存の計算があります。 コンテキスト依存型コードの記述は、抽象化せずに特定のコンテキストの外部で計算を「リーク」し、そうすることを防ぐために簡単に行われるため、困難な場合があります。 これらの抽象化は、多くの場合、自分で記述するのが難しいので、F# には **、いわゆる計算式**を行うための一般的な方法があります。

計算式は、コンテキスト依存計算をエンコードするための統一された構文と抽象化モデルを提供します。

すべての計算式は *、ビルダー*型によって裏付けられます。 ビルダーの型は、計算式で使用できる操作を定義します。 カスタム[計算式の作成方法を示す「新しいタイプの計算式](computation-expressions.md#creating-a-new-type-of-computation-expression)の作成」を参照してください。

### <a name="syntax-overview"></a>構文の概要

すべての計算式の形式は次のとおりです。

```fsharp
builder-expr { cexper }
```

ここで`builder-expr`、計算式を定義するビルダー型の名前であり`cexper`、計算式の式本体です。 たとえば、`async`計算式コードは次のようになります。

```fsharp
let fetchAndDownload url =
    async {
        let! data = downloadData url

        let processedData = processData data

        return processedData
    }
```

前の例に示すように、計算式内で使用できる特別な追加構文があります。 計算式では、次の式フォームが可能です。

```fsharp
expr { let! ... }
expr { do! ... }
expr { yield ... }
expr { yield! ... }
expr { return ... }
expr { return! ... }
expr { match! ... }
```

これらのキーワード、およびその他の標準 F# キーワードは、バッキング ビルダーの型で定義されている場合にのみ、計算式で使用できます。 唯一の例外は、`match!`それ自体が結果にパターンマッチ`let!`を続けて使用するための構文砂糖です。

ビルダー型は、計算式のフラグメントを結合する方法を制御する特別なメソッドを定義するオブジェクトです。つまり、そのメソッドは、計算式の動作を制御します。 ビルダー クラスを記述するもう 1 つの方法は、ループやバインドなど、多くの F# 構造体の操作をカスタマイズできるということです。

### `let!`

キーワード`let!`は、別の計算式の呼び出しの結果を名前にバインドします。

```fsharp
let doThingsAsync url =
    async {
        let! data = getDataAsync url
        ...
    }
```

を使用`let`して計算式に呼び出しをバインドすると、計算式の結果は得られない。 代わりに、*未実現*呼び出しの値をその計算式にバインドします。 結果`let!`にバインドするために使用します。

`let!`は、ビルダー型`Bind(x, f)`のメンバーによって定義されます。

### `do!`

キーワード`do!`は、-like 型 (ビルダーの`unit`メンバーによって定義される) を`Zero`返す計算式を呼び出す場合に使用します。

```fsharp
let doThingsAsync data url =
    async {
        do! submitData data url
        ...
    }
```

[非同期ワークフロー](asynchronous-workflows.md)の場合、このタイプは`Async<unit>`です。 その他の計算式の場合、型は`CExpType<unit>`.

`do!`は、ビルダー型`Bind(x, f)`のメンバーによって定義されます。 `f` `unit`

### `yield`

キーワード`yield`は、計算式から値を返し、それをとして使用するためのキーワードです<xref:System.Collections.Generic.IEnumerable%601>。

```fsharp
let squares =
    seq {
        for i in 1..10 do
            yield i * i
    }

for sq in squares do
    printfn "%d" sq
```

ほとんどの場合、呼び出し元によって省略できます。 省略`yield`する最も一般的な方法は`->`、演算子を使用します。

```fsharp
let squares =
    seq {
        for i in 1..10 -> i * i
    }

for sq in squares do
    printfn "%d" sq
```

多くの異なる値を生成する可能性があるより複雑な式、およびおそらく条件付きで、キーワードを省略するだけで、次のことができます。

```fsharp
let weekdays includeWeekend =
    seq {
        "Monday"
        "Tuesday"
        "Wednesday"
        "Thursday"
        "Friday"
        if includeWeekend then
            "Saturday"
            "Sunday"
    }
```

[C#](../../csharp/language-reference/keywords/yield.md)の yield キーワードと同様に、計算式の各要素は、反復処理のたびに返されます。

`yield`は、ビルダー型`Yield(x)``x`のメンバーによって定義されます。

### `yield!`

キーワード`yield!`は、計算式から値のコレクションをフラット化するためのものです。

```fsharp
let squares =
    seq {
        for i in 1..3 -> i * i
    }

let cubes =
    seq {
        for i in 1..3 -> i * i * i
    }

let squaresAndCubes =
    seq {
        yield! squares
        yield! cubes
    }

printfn "%A" squaresAndCubes // Prints - 1; 4; 9; 1; 8; 27
```

評価されると、 によって`yield!`呼び出される計算式の項目が 1 つずつ戻され、結果が平坦化されます。

`yield!`は、値の`YieldFrom(x)`コレクション`x`であるビルダー型のメンバーによって定義されます。

と`yield`は`yield!`異なり、 明示的に指定する必要があります。 その動作は、計算式では暗黙的ではありません。

### `return`

この`return`キーワードは、計算式に対応する型の値をラップします。 を使用する`yield`計算式以外に、計算式を「完了」するために使用されます。

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        let! data = fetch url
        return data
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return`は、`x`ビルダー型`Return(x)`のメンバーによって定義されます。

### `return!`

キーワード`return!`は、計算式の値を認識し、その結果、計算式に対応する型をラップします。

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        return! fetch url
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return!`は、別の`ReturnFrom(x)`計算式である`x`ビルダー型のメンバーによって定義されます。

### `match!`

この`match!`キーワードを使用すると、別の計算式とパターン一致の呼び出しをインライン化できます。

```fsharp
let doThingsAsync url =
    async {
        match! callService url with
        | Some data -> ...
        | None -> ...
    }
```

で`match!`計算式を呼び出すと、呼び出しの結果が`let!`. これは、結果がオプションである計算式を呼び出すときによく使用[されます](options.md)。

## <a name="built-in-computation-expressions"></a>組み込みの計算式

F# コア ライブラリは、[シーケンス式](sequences.md)、[非同期ワークフロー](asynchronous-workflows.md)、および[クエリ式](query-expressions.md)という 3 つの組み込みの計算式を定義します。

## <a name="creating-a-new-type-of-computation-expression"></a>新しい型の計算式の作成

独自の計算式の特性を定義するには、ビルダー クラスを作成し、クラスに特定の特殊なメソッドを定義します。 ビルダー クラスは、次の表に示すようにメソッドをオプションで定義できます。

次の表は、ワークフロー ビルダー クラスで使用できるメソッドを示しています。

|**Method**|**一般的な署名**|**説明**|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|計算式`let!`で`do!`呼び出されます。|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|計算式を関数としてラップします。|
|`Return`|`'T -> M<'T>`|計算式`return`で呼び出されます。|
|`ReturnFrom`|`M<'T> -> M<'T>`|計算式`return!`で呼び出されます。|
|`Run`|`M<'T> -> M<'T>` または<br /><br />`M<'T> -> 'T`|計算式を実行します。|
|`Combine`|`M<'T> * M<'T> -> M<'T>` または<br /><br />`M<unit> * M<'T> -> M<'T>`|計算式のシーケンス処理に対して呼び出されます。|
|`For`|`seq<'T> * ('T -> M<'U>) -> M<'U>` または<br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|計算式`for...do`の式に対して呼び出されます。|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|計算式`try...finally`の式に対して呼び出されます。|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|計算式`try...with`の式に対して呼び出されます。|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'T :> IDisposable`|計算式`use`のバインディングに対して呼び出されます。|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|計算式`while...do`の式に対して呼び出されます。|
|`Yield`|`'T -> M<'T>`|計算式`yield`の式に対して呼び出されます。|
|`YieldFrom`|`M<'T> -> M<'T>`|計算式`yield!`の式に対して呼び出されます。|
|`Zero`|`unit -> M<'T>`|計算式の`else`式の`if...then`空の分岐に対して呼び出されます。|
|`Quote`|`Quotations.Expr<'T> -> Quotations.Expr<'T>`|計算式が引用符としてメンバーに`Run`渡されることを示します。 これは、計算のすべてのインスタンスを引用に変換します。|

ビルダー クラスのメソッドの多くは、コンストラクト`M<'T>`を使用して返します。 `Async<'T>` `Seq<'T>` これらのメソッドのシグネチャを使用すると、それらを結合して入れ子にして、ある構成要素から返されるワークフロー オブジェクトを次の構成要素に渡すことができます。 コンパイラは、計算式を解析するときに、前の表のメソッドと計算式のコードを使用して、その式を一連の入れ子になった関数呼び出しに変換します。

ネストされた式は次の形式です。

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

上記のコードでは、計算式ビルダー `Run` `Delay`クラスで定義されていない場合は、呼び出しと省略されます。 ここで示す`{| cexpr |}`計算式の本体は、次の表に示す変換によって、ビルダー クラスのメソッドを含む呼び出しに変換されます。 計算式`{| cexpr |}`は、F# 式であり、`expr``cexpr`計算式であるこれらの変換に従って再帰的に定義されます。

|式|翻訳|
|----------|-----------|
|<code>{ let binding in cexpr }</code>|<code>let binding in {&#124; cexpr &#124;}</code>|
|<code>{ let! pattern = expr in cexpr }</code>|<code>builder.Bind(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ do! expr in cexpr }</code>|<code>builder.Bind(expr, (fun () -> {&#124; cexpr &#124;}))</code>|
|<code>{ yield expr }</code>|`builder.Yield(expr)`|
|<code>{ yield! expr }</code>|`builder.YieldFrom(expr)`|
|<code>{ return expr }</code>|`builder.Return(expr)`|
|<code>{ return! expr }</code>|`builder.ReturnFrom(expr)`|
|<code>{ use pattern = expr in cexpr }</code>|<code>builder.Using(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ use! value = expr in cexpr }</code>|<code>builder.Bind(expr, (fun value -> builder.Using(value, (fun value -> { cexpr }))))</code>|
|<code>{ if expr then cexpr0 &#124;}</code>|<code>if expr then { cexpr0 } else builder.Zero()</code>|
|<code>{ if expr then cexpr0 else cexpr1 &#124;}</code>|<code>if expr then { cexpr0 } else { cexpr1 }</code>|
|<code>{ match expr with &#124; pattern_i -> cexpr_i }</code>|<code>match expr with &#124; pattern_i -> { cexpr_i }</code>|
|<code>{ for pattern in expr do cexpr }</code>|<code>builder.For(enumeration, (fun pattern -> { cexpr }))</code>|
|<code>{ for identifier = expr1 to expr2 do cexpr }</code>|<code>builder.For(enumeration, (fun identifier -> { cexpr }))</code>|
|<code>{ while expr do cexpr }</code>|<code>builder.While(fun () -> expr, builder.Delay({ cexpr }))</code>|
|<code>{ try cexpr with &#124; pattern_i -> expr_i }</code>|<code>builder.TryWith(builder.Delay({ cexpr }), (fun value -> match value with &#124; pattern_i -> expr_i &#124; exn -> reraise exn)))</code>|
|<code>{ try cexpr finally expr }</code>|<code>builder.TryFinally(builder.Delay( { cexpr }), (fun () -> expr))</code>|
|<code>{ cexpr1; cexpr2 }</code>|<code>builder.Combine({ cexpr1 }, { cexpr2 })</code>|
|<code>{ other-expr; cexpr }</code>|<code>expr; { cexpr }</code>|
|<code>{ other-expr }</code>|`expr; builder.Zero()`|

前の表では、`other-expr`表にリストされていない式について説明します。 ビルダー クラスは、すべてのメソッドを実装する必要はありませんし、前の表に示されているすべての変換をサポートします。 実装されていないコンストラクトは、その型の計算式では使用できません。 たとえば、計算式で`use`キーワードをサポートしたくない場合は、ビルダークラス`Use`の定義を省略できます。

次のコード例は、計算を一度に 1 ステップずつ評価できる一連のステップとしてカプセル化する計算式を示しています。 判別共用体型 は`OkOrException`、これまで評価された式のエラー状態をエンコードします。 このコードは、いくつかのビルダー メソッドの定型的な実装など、計算式で使用できるいくつかの一般的なパターンを示しています。

```fsharp
// Computations that can be run step by step
type Eventually<'T> =
    | Done of 'T
    | NotYetDone of (unit -> Eventually<'T>)

module Eventually =
    // The bind for the computations. Append 'func' to the
    // computation.
    let rec bind func expr =
        match expr with
        | Done value -> func value
        | NotYetDone work -> NotYetDone (fun () -> bind func (work()))

    // Return the final value wrapped in the Eventually type.
    let result value = Done value

    type OkOrException<'T> =
        | Ok of 'T
        | Exception of System.Exception

    // The catch for the computations. Stitch try/with throughout
    // the computation, and return the overall result as an OkOrException.
    let rec catch expr =
        match expr with
        | Done value -> result (Ok value)
        | NotYetDone work ->
            NotYetDone (fun () ->
                let res = try Ok(work()) with | exn -> Exception exn
                match res with
                | Ok cont -> catch cont // note, a tailcall
                | Exception exn -> result (Exception exn))

    // The delay operator.
    let delay func = NotYetDone (fun () -> func())

    // The stepping action for the computations.
    let step expr =
        match expr with
        | Done _ -> expr
        | NotYetDone func -> func ()

    // The rest of the operations are boilerplate.
    // The tryFinally operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryFinally expr compensation =
        catch (expr)
        |> bind (fun res ->
            compensation();
            match res with
            | Ok value -> result value
            | Exception exn -> raise exn)

    // The tryWith operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryWith exn handler =
        catch exn
        |> bind (function Ok value -> result value | Exception exn -> handler exn)

    // The whileLoop operator.
    // This is boilerplate in terms of "result" and "bind".
    let rec whileLoop pred body =
        if pred() then body |> bind (fun _ -> whileLoop pred body)
        else result ()

    // The sequential composition operator.
    // This is boilerplate in terms of "result" and "bind".
    let combine expr1 expr2 =
        expr1 |> bind (fun () -> expr2)

    // The using operator.
    let using (resource: #System.IDisposable) func =
        tryFinally (func resource) (fun () -> resource.Dispose())

    // The forLoop operator.
    // This is boilerplate in terms of "catch", "result", and "bind".
    let forLoop (collection:seq<_>) func =
        let ie = collection.GetEnumerator()
        tryFinally
            (whileLoop
                (fun () -> ie.MoveNext())
                (delay (fun () -> let value = ie.Current in func value)))
            (fun () -> ie.Dispose())

// The builder class.
type EventuallyBuilder() =
    member x.Bind(comp, func) = Eventually.bind func comp
    member x.Return(value) = Eventually.result value
    member x.ReturnFrom(value) = value
    member x.Combine(expr1, expr2) = Eventually.combine expr1 expr2
    member x.Delay(func) = Eventually.delay func
    member x.Zero() = Eventually.result ()
    member x.TryWith(expr, handler) = Eventually.tryWith expr handler
    member x.TryFinally(expr, compensation) = Eventually.tryFinally expr compensation
    member x.For(coll:seq<_>, func) = Eventually.forLoop coll func
    member x.Using(resource, expr) = Eventually.using resource expr

let eventually = new EventuallyBuilder()

let comp = eventually {
    for x in 1..2 do
        printfn " x = %d" x
    return 3 + 4 }

// Try the remaining lines in F# interactive to see how this
// computation expression works in practice.
let step x = Eventually.step x

// returns "NotYetDone <closure>"
comp |> step

// prints "x = 1"
// returns "NotYetDone <closure>"
comp |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "Done 7"
comp |> step |> step |> step |> step
```

計算式には基になる型があり、式が返されます。 基になる型は、計算結果または実行できる遅延計算を表す場合もあれば、何らかの種類のコレクションを反復処理する方法を提供する場合があります。 前の例では、基になる型は **"最終的" でした**。 シーケンス式の場合、基になる型は<xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>です。 クエリ式の場合、基になる型は<xref:System.Linq.IQueryable?displayProperty=nameWithType>です。 非同期ワークフローの場合、基になる型は[`Async`](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7)です。 オブジェクト`Async`は、結果を計算するために実行される作業を表します。 たとえば、計算を実行[`Async.RunSynchronously`](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b)して結果を返す呼び出しを行うとします。

## <a name="custom-operations"></a>カスタム操作

計算式にカスタム演算を定義し、カスタム演算を計算式の演算子として使用できます。 たとえば、クエリ式にクエリ演算子を含めることができます。 カスタム操作を定義する場合は、計算式で Yield メソッドと For メソッドを定義する必要があります。 カスタム操作を定義するには、計算式のビルダー クラスに配置し、 を適用します[`CustomOperationAttribute`](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19)。 この属性は、引数として文字列を受け取ります。 この名前は、計算式の中かっこの先頭にスコープが付けられます。 したがって、このブロックでは、カスタム操作と同じ名前の識別子を使用しないでください。 たとえば、クエリ式などの識別子を`all``last`使用しないようにします。

### <a name="extending-existing-builders-with-new-custom-operations"></a>新しいカスタム操作で既存のビルダーを拡張する

既にビルダー クラスがある場合は、そのカスタム操作をこのビルダー クラスの外部から拡張できます。 拡張機能はモジュールで宣言する必要があります。 名前空間には、同じファイルと、型が定義されている同じ名前空間宣言グループ内以外の拡張メンバーを含めることはできません。

既存の`Microsoft.FSharp.Linq.QueryBuilder`クラスの拡張を次の例に示します。

```fsharp
type Microsoft.FSharp.Linq.QueryBuilder with

    [<CustomOperation("existsNot")>]
    member _.ExistsNot (source: QuerySource<'T, 'Q>, predicate) =
        Enumerable.Any (source.Source, Func<_,_>(predicate)) |> not
```

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [非同期ワークフロー](asynchronous-workflows.md)
- [シーケンス](https://msdn.microsoft.com/library/6b773b6b-9c9a-4af8-bd9e-d96585c166db)
- [クエリ式](query-expressions.md)
