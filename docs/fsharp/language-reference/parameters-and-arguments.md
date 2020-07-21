---
title: パラメーターと引数
description: パラメーターの定義と、関数、メソッド、およびプロパティへの引数の引き渡しに関する F# 言語のサポートについて説明します。
ms.date: 12/04/2019
ms.openlocfilehash: b234ef939128e7cf09d35f9580d4d5010d7dc639
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401053"
---
# <a name="parameters-and-arguments"></a>パラメーターと引数

このトピックでは、パラメーターを定義し、関数、メソッド、およびプロパティに引数を渡すための言語サポートについて説明します。 参照渡し方法、および可変個の引数を受け取るメソッドの定義方法と使用方法に関する情報が含まれています。

## <a name="parameters-and-arguments"></a>パラメーターと引数

*パラメーター*という用語は、指定される値の名前を記述するために使用されます。 引数という*用語*は、各パラメーターに指定された値に使用されます。

パラメーターは、タプルまたはカリー化された形式で指定することも、2 つの組み合わせで指定することもできます。 引数は、明示的なパラメーター名を使用して渡すことができます。 メソッドのパラメーターは、オプションとして指定でき、デフォルト値を指定できます。

## <a name="parameter-patterns"></a>パラメータパターン

関数やメソッドに渡されるパラメータは、一般に、スペースで区切られたパターンです。 つまり、原則として、「[一致式](match-expressions.md)」で説明されているパターンは、関数またはメンバーのパラメーター・リストで使用できます。

メソッドは、通常、引数を渡すタプル形式を使用します。 これにより、タプル形式が .NET メソッドでの引数の渡し方と一致するため、他の .NET 言語の観点からより明確な結果が得られます。

カリー化された形式は、バインディングを使用して作成された関数で`let`最もよく使用されます。

次の擬似コードは、組とカリー化された引数の例を示しています。

```fsharp
// Tuple form.
member this.SomeMethod(param1, param2) = ...
// Curried form.
let function1 param1 param2 = ...
```

組の中に一部の引数があり、一部の引数が組に含まれていない場合は、結合形式が可能です。

```fsharp
let function2 param1 (param2a, param2b) param3 = ...
```

パラメーター・リストでも他のパターンを使用できますが、パラメーター・パターンがすべての入力に一致しない場合は、実行時に不完全な一致が発生する可能性があります。 例外`MatchFailureException`は、引数の値がパラメーター・リストで指定されたパターンと一致しない場合に生成されます。 パラメーター パターンで不完全な一致が許可されると、コンパイラは警告を発行します。 パラメーター・リストには、他のパターンが少なくとも 1 つ使用され、ワイルドカード・パターンとして使用されます。 指定された引数を無視するだけの場合は、パラメーター リストでワイルドカード パターンを使用します。 次のコードは、引数リストでのワイルドカード パターンの使用を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3801.fs)]

ワイルドカード パターンは、次のコードのように、通常は文字列配列として指定されるコマンド ライン引数に関心がない場合に、プログラムへのメイン エントリ ポイントなどで渡される引数が必要ない場合に便利です。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3802.fs)]

引数で使用されるパターン、および判別共用体`as`とアクティブなパターンに関連付けられた識別子パターンは、他にもあります。 単一ケースの判別共用体パターンは、次のように使用できます。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3803.fs)]

出力は次のとおりです。

```console
Data begins at 0 and ends at 4 in string Et tu, Brute?
Et tu
```

アクティブパターンは、たとえば、次の例のように、引数を目的の形式に変換する場合に、パラメータとして役立ちます。

```fsharp
type Point = { x : float; y : float }

let (| Polar |) { x = x; y = y} =
    ( sqrt (x*x + y*y), System.Math.Atan (y/ x) )

let radius (Polar(r, _)) = r
let angle (Polar(_, theta)) = theta
```

次の`as`コード行に示すように、パターンを使用して、一致した値をローカル値として格納できます。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3805.fs)]

時折使用されるもう 1 つのパターンは、関数の本体として、暗黙的な引数に対してパターン一致を即座に実行するラムダ式を提供することによって、最後の引数を無名のままにする関数です。 この例は、次のコード行です。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3804.fs)]

このコードは、汎用リストを受け取り、`true`リストが空の場合、または`false`そうでない場合に返す関数を定義します。 このような手法を使用すると、コードの読み取りが困難になる可能性があります。

不完全な一致を伴うパターンが役立つ場合があります。例えば、プログラム内のリストに 3 つの要素しか含めならない場合は、パラメーター・リストで次のようなパターンを使用できます。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3806.fs)]

不完全な一致を持つパターンの使用は、迅速なプロトタイプ作成やその他の一時的な使用のために予約するのが最善です。 コンパイラは、このようなコードに対して警告を発行します。 このようなパターンは、すべての入力可能な一般的なケースをカバーできないため、コンポーネント API には適していません。

## <a name="named-arguments"></a>名前付き引数

メソッドの引数は、コンマ区切りの引数リスト内の位置によって指定することも、名前を指定してメソッドに明示的に渡し、その後に等号と渡す値を指定することもできます。 名前を指定して指定した場合は、宣言で使用されている順序とは異なる順序で表示できます。

名前付き引数を使用すると、メソッド パラメーターの並べ替えなど、API の特定の種類の変更に対して、コードをより読みやすく、適応性が高くなります。

名前付き引数はメソッド`let`に対してのみ使用できます。

名前付き引数の使用方法を次のコード例に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3807.fs)]

クラス コンストラクターの呼び出しでは、名前付き引数と同様の構文を使用して、クラスのプロパティの値を設定できます。 この構文の例を次に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

詳細については、「コンストラクター [(F#)」](https://msdn.microsoft.com/library/2cd0ed07-d214-4125-8317-4f288af99f05)を参照してください。

## <a name="optional-parameters"></a>省略可能なパラメーター

パラメーター名の前に疑問符を使用して、メソッドのオプション・パラメーターを指定できます。 オプション のパラメーターは F# オプション型として解釈されるため、 と`match``Some``None`を指定して式を使用して、オプション型をクエリする通常の方法でクエリを実行できます。 オプションのパラメーターは、バインディングを使用`let`して作成された関数ではなく、メンバーに対してのみ許可されます。

または などの`?arg=None``?arg=Some(3)`パラメーター名によって既存のオプション値をメソッドに渡すことができます`?arg=arg`。 これは、別のメソッドに省略可能な引数を渡すメソッドを構築する場合に役立ちます。

オプション引数の既定値を設定`defaultArg`する関数 を使用することもできます。 この`defaultArg`関数は、オプションのパラメータを最初の引数として、デフォルト値を 2 番目の引数として受け取ります。

次の例は、省略可能なパラメーターの使用方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3808.fs)]

出力は次のとおりです。

```console
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
Baud Rate: 300 Duplex: Half Parity: true
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
```

C# と Visual Basic 相互運用機能の目的で、F# の属性`[<Optional; DefaultParameterValue<(...)>]`を使用して、呼び出し元に引数を省略可能と見なすことができます。 これは、引数を C# での オプションとして定義する`MyMethod(int i = 3)`のと同じです。

```fsharp
open System
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue("Hello world")>] message) =
        printfn "%s" message
```

新しいオブジェクトをデフォルトのパラメータ値として指定することもできます。 たとえば、メンバーは`Foo`代わりに入力としてオプション`CancellationToken`を持つことができます。

```fsharp
open System.Threading
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue(CancellationToken())>] ct: CancellationToken) =
        printfn "%A" ct
```

引数として指定する値は`DefaultParameterValue`、パラメーターの型と一致する必要があります。 たとえば、次の項目は許可されません。

```fsharp
type C =
    static member Wrong([<Optional; DefaultParameterValue("string")>] i:int) = ()
```

この場合、コンパイラは警告を生成し、両方の属性を完全に無視します。 コンパイラが誤った型`null`、すなわちを推測するので、デフォルト値は型注釈付きである必要があることに注意してください。 `[<Optional; DefaultParameterValue(null:obj)>] o:obj`

## <a name="passing-by-reference"></a>参照渡し

参照によって F# 値を渡すと、マネージ ポインター型である[byrefs](byrefs.md)が使用されます。 使用するタイプのガイダンスは次のとおりです。

- ポインタ`inref<'T>`を読み取るだけで済む場合に使用します。
- ポインタ`outref<'T>`に書き込むだけで済む場合に使用します。
- ポインター`byref<'T>`の読み取りと書き込みの両方が必要な場合に使用します。

```fsharp
let example1 (x: inref<int>) = printfn "It's %d" x

let example2 (x: outref<int>) = x <- x + 1

let example3 (x: byref<int>) =
    printfn "It'd %d" x
    x <- x + 1

let test () =
    // No need to make it mutable, since it's read-only
    let x = 1
    example1 &x

    // Needs to be mutable, since we write to it
    let mutable y = 2
    example2 &y
    example3 &y // Now 'y' is 3
```

パラメーターがポインターであり、値が変更可能であるため、値に対する変更は関数の実行後も保持されます。

戻り値としてタプルを使用して、.NET ライブラリ`out`メソッドにパラメーターを格納できます。 または、パラメータを`out``byref`パラメータとして扱うことができます。 両方の方法を次のコード例に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3810.fs)]

## <a name="parameter-arrays"></a>パラメーター配列

場合によっては、異種型の任意の数のパラメータを受け取る関数を定義する必要があります。 使用できるすべての型を考慮するために、オーバーロードされた可能性のあるメソッドをすべて作成することは現実的ではありません。 .NET の実装では、パラメーター配列機能を使用して、このようなメソッドをサポートしています。 シグネチャのパラメータ配列を受け取るメソッドは、任意の数のパラメータを指定できます。 パラメータは配列に格納されます。 配列要素の型によって、関数に渡すことができるパラメーターの型が決まります。 要素型として`System.Object`パラメーター配列を定義する場合、クライアント コードは任意の型の値を渡すことができます。

F# では、パラメーター配列はメソッドでのみ定義できます。 スタンドアロン関数やモジュールで定義されている関数では使用できません。

パラメーター配列は、 属性を使用`ParamArray`して定義します。 属性`ParamArray`は最後のパラメーターにのみ適用できます。

次のコードは、パラメーター配列を受け取る .NET メソッドの呼び出しと、パラメーター配列を受け取るメソッドを持つ F# の型の定義の両方を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-2/snippet3811.fs)]

プロジェクトで実行する場合、前のコードの出力は次のようになります。

```console
a 1 10 Hello world 1 True
"a"
1
10.0
"Hello world"
1u
true
```

## <a name="see-also"></a>関連項目

- [メンバー](./members/index.md)
