---
title: 'F # 4.5 の新機能-F # ガイド'
description: 'F # 4.5 で利用可能な新機能の概要を説明します。'
ms.date: 11/27/2019
ms.openlocfilehash: 2c978c66a4bf231398508cbc1cbb8839228ea8e9
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202349"
---
# <a name="whats-new-in-f-45"></a>F # 4.5 の新機能

F # 4.5 では、F # 言語に複数の機能強化が加えられています。 これらの機能の多くは、F # で効率的なコードを記述できるようにするためにまとめられています。また、このコードが安全であることを保証します。 これにより、言語にいくつかの概念が追加され、これらのコンストラクトを使用するときに大量のコンパイラ分析が行われることになります。

## <a name="get-started"></a>作業開始

F # 4.5 は、すべての .NET Core ディストリビューションと Visual Studio ツールで使用できます。 詳細については、 [F # の概要に関する](../get-started/index.md)ページをご覧ください。

## <a name="span-and-byref-like-structs"></a>Span および byref に似た構造体

<xref:System.Span%601>.Net Core で導入された型を使用すると、厳密に型指定された方法でメモリ内のバッファーを表すことができます。 f # 4.5 で始まる f # で使用できるようになりました。 次の例は、 <xref:System.Span%601> 別のバッファー表現を使用して、で動作する関数を再利用する方法を示しています。

```fsharp
let safeSum (bytes: Span<byte>) =
    let mutable sum = 0
    for i in 0 .. bytes.Length - 1 do
        sum <- sum + int bytes.[i]
    sum

// managed memory
let arrayMemory = Array.zeroCreate<byte>(100)
let arraySpan = new Span<byte>(arrayMemory)

safeSum(arraySpan) |> printfn "res = %d"

// native memory
let nativeMemory = Marshal.AllocHGlobal(100);
let nativeSpan = new Span<byte>(nativeMemory.ToPointer(), 100)

safeSum(nativeSpan) |> printfn "res = %d"
Marshal.FreeHGlobal(nativeMemory)

// stack memory
let mem = NativePtr.stackalloc<byte>(100)
let mem2 = mem |> NativePtr.toVoidPtr
let stackSpan = Span<byte>(mem2, 100)

safeSum(stackSpan) |> printfn "res = %d"
```

これにとって重要な点は、Span とその他の[byref に似た構造体](../language-reference/structures.md#byreflike-structs)は、コンパイラによって実行される静的分析が非常に厳密であり、予期しない状態になる可能性がある方法でその使用を制限することです。 これは、F # 4.5 で導入されたパフォーマンス、表現力、および安全性の基本的なトレードオフです。

## <a name="revamped-byrefs"></a>Byref の改良

F # 4.5 より前では、F # の[byref](../language-reference/byrefs.md)は安全ではないため、多くのアプリケーションでは聞こえませんでした。 Byref に関する束縛の問題が F # 4.5 で対処されており、span と byref に似た構造体に対して実行される同じ静的分析も適用されました。

### <a name="inreft-and-outreft"></a>inref< ' t> および outref< '>

読み取り専用、書き込み専用、および読み取り/書き込みマネージポインターの概念を表すために、F # 4.5 では、 `inref<'T>` `outref<'T>` それぞれ読み取り専用ポインターと書き込み専用ポインターを表す型が導入されています。 それぞれに異なるセマンティクスがあります。 たとえば、に書き込むことはできません `inref<'T>` 。

```fsharp
let f (dt: inref<DateTime>) =
    dt <- DateTime.Now // ERROR - cannot write to an inref!
```

既定では、型の推定は、 `inref<'T>` 変更可能として既に宣言されていない限り、F # コードの不変の性質を持つとして、マネージポインターをとして推論します。 何かを書き込み可能にするには、その `mutable` アドレスを操作する関数またはメンバーに渡す前に、型をとして宣言する必要があります。 詳細については、「 [byref](../language-reference/byrefs.md)」を参照してください。

## <a name="readonly-structs"></a>Readonly 構造体

F # 4.5 以降では、次のようにを使用して構造体に注釈を付けることができ <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute> ます。

```fsharp
[<IsReadOnly; Struct>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

これにより、構造体で変更可能なメンバーを宣言し、アセンブリから使用するときに F # と C# が読み取り専用として扱うことができるメタデータを生成することはできません。 詳細については、「 [ReadOnly 構造体](../language-reference/structures.md#readonly-structs)」を参照してください。

## <a name="void-pointers"></a>Void ポインター

`voidptr`型は、次の関数のように F # 4.5 に追加されます。

* `NativePtr.ofVoidPtr`void ポインターをネイティブ int ポインターに変換するには
* `NativePtr.toVoidPtr`ネイティブの int ポインターを void ポインターに変換するには

これは、void ポインターを使用するネイティブコンポーネントと相互運用する場合に役立ちます。

## <a name="the-match-keyword"></a>`match!` キーワード

キーワードは、 `match!` コンピュテーション式の内部でパターンマッチングを強化します。

```fsharp
// Code that returns an asynchronous option
let checkBananaAsync (s: string) =
    async {
        if s = "banana" then
            return Some s
        else
            return None
    }

// Now you can use 'match!'
let funcWithString (s: string) =
    async {
        match! checkBananaAsync s with
        | Some bananaString -> printfn "It's banana!"
        | None -> printfn "%s" s
}
```

これにより、非同期などのコンピュテーション式でオプション (または他の型) を混在させることが多いコードを短縮できます。 詳細については、「 [match!](../language-reference/computation-expressions.md#match)」を参照してください。

## <a name="relaxed-upcasting-requirements-in-array-list-and-sequence-expressions"></a>配列、リスト、およびシーケンス式における緩やかなキャストの要件

配列、リスト、およびシーケンス式の内部で別の型から継承する可能性のある型を混在させるには、またはを使用して派生型をその親型にアップキャストする必要がありました `:>` `upcast` 。 これは、次に示すように、緩和されました。

```fsharp
let x0 : obj list  = [ "a" ] // ok pre-F# 4.5
let x1 : obj list  = [ "a"; "b" ] // ok pre-F# 4.5
let x2 : obj list  = [ yield "a" :> obj ] // ok pre-F# 4.5

let x3 : obj list  = [ yield "a" ] // Now ok for F# 4.5, and can replace x2
```

## <a name="indentation-relaxation-for-array-and-list-expressions"></a>配列とリスト式のインデント緩和

F # 4.5 より前では、メソッド呼び出しに引数として渡すときに、配列とリスト式を過度にインデントする必要がありました。 これは必要なくなりました。

```fsharp
module NoExcessiveIndenting =
    System.Console.WriteLine(format="{0}", arg = [|
        "hello"
    |])
    System.Console.WriteLine([|
        "hello"
    |])
```
