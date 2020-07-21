---
title: Byrefs
description: 低レベルプログラミングに使用される f# で byref 型と byref 型について説明します。
ms.date: 11/04/2019
ms.openlocfilehash: 527f465ee87fe153a2deae1306b6730531dc4123
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187048"
---
# <a name="byrefs"></a>Byrefs

F# には、低レベルプログラミングの領域を扱う主な機能が 2 つ用意されています。

* `byref`/マネージ`outref`ポインターである型。 `inref` / これらのプログラムには使用法に制限があるため、実行時に無効なプログラムをコンパイルすることはできません。
* 類似`byref`のセマンティクスとコンパイル時の制限を持つ[構造体](structures.md)である -like 構造体 。 `byref<'T>` その一例<xref:System.Span%601>が です。

## <a name="syntax"></a>構文

```fsharp
// Byref types as parameters
let f (x: byref<'T>) = ()
let g (x: inref<'T>) = ()
let h (x: outref<'T>) = ()

// Calling a function with a byref parameter
let mutable x = 3
f &x

// Declaring a byref-like struct
open System.Runtime.CompilerServices

[<Struct; IsByRefLike>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

## <a name="byref-inref-and-outref"></a>バイレフ、インレフ、およびアウトレフ

の 3 つの`byref`形式があります。

* `inref<'T>`基になる値を読み取るためのマネージ ポインター。
* `outref<'T>`の基になる値に書き込むマネージ ポインター。
* `byref<'T>`の読み取りと書き込みのマネージ ポインター。

が`byref<'T>`期待されるところで`inref<'T>`渡すことができます。 同様に、`byref<'T>`が必要な場所`outref<'T>`に a を渡すことができます。

## <a name="using-byrefs"></a>参照の使用

を`inref<'T>`使用するには、 を使用してポインター値を取得`&`する必要があります。

```fsharp
open System

let f (dt: inref<DateTime>) =
    printfn "Now: %s" (dt.ToString())

let usage =
    let dt = DateTime.Now
    f &dt // Pass a pointer to 'dt'
```

または を使用してポインターに書き込むには、 へのポインターを取得する値を`mutable`作成する必要もあります。 `byref<'T>` `outref<'T>`

```fsharp
open System

let f (dt: byref<DateTime>) =
    printfn "Now: %s" (dt.ToString())
    dt <- DateTime.Now

// Make 'dt' mutable
let mutable dt = DateTime.Now

// Now you can pass the pointer to 'dt'
f &dt
```

ポインタを読む代わりに書くだけの場合は、`outref<'T>``byref<'T>`の代わりに を使用することを検討してください。

### <a name="inref-semantics"></a>インレフセマンティクス

次のコードについて考えてみましょう。

```fsharp
let f (x: inref<SomeStruct>) = x.SomeField
```

意味的には、これは次の意味を意味します。

* ポインターのホルダーは`x`、値の読み取りにのみ使用できます。
* 内`struct``SomeStruct`にネストされたフィールドに取得されたポインタには、 `inref<_>`type が与えられます。

次のことも当てはまります。

* 他のスレッドまたはエイリアスに対する`x`書き込みアクセス権が与えないことを意味するわけではありません。
* あるというのは、`SomeStruct`不変の`x`意味はありません`inref`。

ただし、不**変の**F# 値型の`this`場合、ポインターは`inref`.

これらの規則はすべて、`inref`ポインタの所有者が、指しているメモリの直接の内容を変更しないことを意味します。

### <a name="outref-semantics"></a>アウトレフセマンティクス

の目的`outref<'T>`は、ポインタの書き込みのみを指示することです。 予期せず、`outref<'T>`その名前にもかかわらず、基になる値を読み取ることができます。 これは互換性を目的としています。 意味的には`outref<'T>`、 と`byref<'T>`同じではありません。

### <a name="interop-with-c"></a>C との相互運用性\#

C# では`in ref`、`out ref`および キーワードをサポート`ref`し、さらに、リターンもサポートします。 次の表は、F# が C# の出力を解釈する方法を示しています。

|C# コンストラクト|F# の推論|
|------------|---------|
|`ref`戻り値|`outref<'T>`|
|`ref readonly`戻り値|`inref<'T>`|
|`in ref` パラメーター|`inref<'T>`|
|`out ref` パラメーター|`outref<'T>`|

次の表は、F# の出力を示しています。

|F# コンストラクト|放出されたコンストラクト|
|------------|-----------------|
|`inref<'T>` 引数|`[In]`引数の属性|
|`inref<'T>`返す|`modreq`値の属性|
|`inref<'T>`抽象的なスロットまたは実装で|`modreq`引数または戻り値の場合|
|`outref<'T>` 引数|`[Out]`引数の属性|

### <a name="type-inference-and-overloading-rules"></a>型の推論とオーバーロードの規則

型`inref<'T>`は、次の場合に F# コンパイラによって推論されます。

1. 属性を持つ .NET パラメータまたは`IsReadOnly`戻り値の型。
2. 変更`this`可能なフィールドを持たない構造体型のポインター。
3. 別`inref<_>`のポインターから派生したメモリ位置のアドレス。

の暗黙のアドレスを`inref`取る場合、型の引数を持つオーバーロードは`SomeType`、 type の引数を持つオーバーロード`inref<SomeType>`より優先されます。 次に例を示します。

```fsharp
type C() =
    static member M(x: System.DateTime) = x.AddDays(1.0)
    static member M(x: inref<System.DateTime>) = x.AddDays(2.0)
    static member M2(x: System.DateTime, y: int) = x.AddDays(1.0)
    static member M2(x: inref<System.DateTime>, y: int) = x.AddDays(2.0)

let res = System.DateTime.Now
let v =  C.M(res)
let v2 =  C.M2(res, 4)
```

どちらの場合も、オーバーロードを取るのではなく`System.DateTime`、オーバーロードを取る代わりに、`inref<System.DateTime>`取るオーバーロードが解決されます。

## <a name="byref-like-structs"></a>バイレフのような構造体

`byref`/`inref`トリオ/に`outref`加えて、-like セマンティクスに従うことができる独自の構造体を`byref`定義できます。 これは<xref:System.Runtime.CompilerServices.IsByRefLikeAttribute>属性で行われます。

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike`は を`Struct`意味しません。 両方とも型に存在する必要があります。

F#`byref`の "-like" 構造体は、スタックにバインドされた値型です。 マネージ ヒープには割り当てが行きまとい。 `byref`-like 構造体は、有効期間と非キャプチャに関する強力なチェックのセットで実施される、高性能プログラミングに役立ちます。 ルールは次のとおりです。

* 関数パラメーター、メソッドパラメーター、ローカル変数、メソッドの戻り値として使用できます。
* クラスの静的メンバーまたはインスタンス メンバー、または通常の構造体にはできません。
* これらの関数は、どのクロージャ構造`async`(メソッドまたはラムダ式) でもキャプチャできません。
* ジェネリック パラメーターとして使用することはできません。

この最後のポイントは、F# パイプライン スタイルのプログラミングでは`|>`重要です。 この制限は、インラインであり`|>`、その本体のインライン化されていないジェネリック関数を呼び出さないため、将来的には緩和される可能性があります。

これらの規則は使用を強く制限しますが、安全な方法で高性能コンピューティングの約束を果たすために行います。

## <a name="byref-returns"></a>バイレフが戻る

F# 関数またはメンバーからの Byref 戻り値を生成して使用できます。 戻り値`byref`を使用する場合、値は暗黙的に逆参照されます。 次に例を示します。

```fsharp
let squareAndPrint (data : byref<int>) =
    let squared = data*data    // data is implicitly dereferenced
    printfn "%d" squared
```

値 byref を返すためには、値を含む変数は現在のスコープよりも長く存在する必要があります。
また、byref を返すために`&value`は、使用します (値は現在のスコープよりも長く存在する変数です)。

```fsharp
let mutable sum = 0
let safeSum (bytes: Span<byte>) =
    for i in 0 .. bytes.Length - 1 do
        sum <- sum + int bytes.[i]
    &sum  // sum lives longer than the scope of this function.
```

複数の連鎖呼び出しを通じて参照を渡すなど、暗黙的な逆`&x`参照を`x`回避するには、(値は場所) を使用します。

また、直接戻り . `byref` 次の (非常に命令的な) プログラムを検討してください。

```fsharp
type C() =
    let mutable nums = [| 1; 3; 7; 15; 31; 63; 127; 255; 511; 1023 |]

    override _.ToString() = String.Join(' ', nums)

    member _.FindLargestSmallerThan(target: int) =
        let mutable ctr = nums.Length - 1

        while ctr > 0 && nums.[ctr] >= target do ctr <- ctr - 1

        if ctr > 0 then &nums.[ctr] else &nums.[0]

[<EntryPoint>]
let main argv =
    let c = C()
    printfn "Original sequence: %s" (c.ToString())

    let v = &c.FindLargestSmallerThan 16

    v <- v*2 // Directly assign to the byref return

    printfn "New sequence:      %s" (c.ToString())

    0 // return an integer exit code
```

出力結果は次のとおりです。

```console
Original sequence: 1 3 7 15 31 63 127 255 511 1023
New sequence:      1 3 7 30 31 63 127 255 511 1023
```

## <a name="scoping-for-byrefs"></a>バイ参照のスコープ指定

バインド`let`された値は、その参照が定義されているスコープを超えることはできません。 たとえば、次の項目は許可されません。

```fsharp
let test2 () =
    let x = 12
    &x // Error: 'x' exceeds its defined scope!

let test () =
    let x =
        let y = 1
        &y // Error: `y` exceeds its defined scope!
    ()
```

これにより、最適化を使用してコンパイルするかどうかによって、異なる結果が得られるのを防ぐことができます。
