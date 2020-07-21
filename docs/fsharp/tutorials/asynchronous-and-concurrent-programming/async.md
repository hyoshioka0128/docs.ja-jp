---
title: 非同期プログラミング
description: F# では、コア機能プログラミングの概念から派生した言語レベルのプログラミング モデルに基づいて、非同期のクリーン サポートを提供する方法について説明します。
ms.date: 12/17/2018
ms.openlocfilehash: 0a7d400c9778e30d6b25798239f12b7b2b0e3d82
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021522"
---
# <a name="async-programming-in-f"></a>F の非同期プログラミング\#

非同期プログラミングは、さまざまな理由で最新のアプリケーションに不可欠なメカニズムです。 ほとんどの開発者が遭遇する主な使用例は次の 2 つがあります。

- 大量の同時着信要求に対応できるサーバー・プロセスを提示し、要求処理がそのプロセスの外部のシステムまたはサービスからの入力を待機する間、占有されるシステム・リソースを最小化する。
- バックグラウンド作業を同時に進行しながら、応答性の高い UI またはメイン スレッドを維持する

バックグラウンドでの作業には複数のスレッドの使用が伴うことがよくありますが、非同期とマルチスレッドの概念を別々に考慮することが重要です。 実際、それらは別々の懸念事項であり、一方は他方を意味するものではありません。 この記事では、個別の概念について詳しく説明します。

## <a name="asynchrony-defined"></a>非同期定義

非同期が複数のスレッドの使用率とは無関係であるという前の点は、もう少し説明する価値があります。 関連する場合もありますが、互いに厳密に独立している 3 つの概念があります。

- 同時実行;複数の計算が重複する期間で実行される場合。
- 並列処理;複数の計算または単一の計算の複数の部分がまったく同時に実行される場合。
- 非同期;1 つ以上の計算がメインプログラムフローとは別に実行できる場合。

3つとも直交概念ですが、特に一緒に使用する場合は簡単に収縮できます。 たとえば、複数の非同期計算を並列に実行する必要がある場合があります。 この関係は、並列性や非同期が互いを暗示することを意味するものではありません。

"非同期" という語の語源を考えると、次の 2 つの部分が含まれます。

- "a"、つまり"not"。
- 「同期」、つまり「同時に」を意味します。

これら 2 つの用語を組み合わせると、「非同期」とは「同時に」という意味ではないことがわかります。 これで完了です。 この定義には、同時実行または並列処理の意味はありません。 これは実際にも当てはまります。

実際には、F# の非同期計算は、メイン プログラム フローとは独立して実行するようにスケジュールされています。 この独立した実行は、同時実行や並列処理を意味するわけではなく、計算が常にバックグラウンドで行われるという意味でもありません。 実際、非同期計算は、計算の性質や計算が実行される環境に応じて、同期的に実行されることさえあります。

主な取り上げは、非同期計算はメインプログラムフローから独立していることです。 非同期計算の実行時期や方法に関する保証はほとんどありませんが、それらを調整してスケジュールする方法がいくつかあります。 この記事の残りの部分では、F# 非同期の主要な概念と、F# に組み込まれている型、関数、および式の使用方法について説明します。

## <a name="core-concepts"></a>主要な概念

F# では、非同期プログラミングは、次の 3 つの主要な概念を中心にしています。

- 構成`Async<'T>`可能な非同期計算を表す型。
- 非同期`Async`処理のスケジュール設定、非同期計算の作成、非同期結果の変換を行うモジュール関数。
- `async { }`[計算式](../../language-reference/computation-expressions.md)は、非同期計算を構築および制御するための便利な構文を提供します。

次の例では、これら 3 つの概念を確認できます。

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn "File %s has %d bytes" fileName bytes.Length
    }

[<EntryPoint>]
let main argv =
    printTotalFileBytes "path-to-file.txt"
    |> Async.RunSynchronously

    Console.Read() |> ignore
    0
```

この例では、`printTotalFileBytes`関数の型`string -> Async<unit>`は です。 関数を呼び出しても、実際には非同期計算は実行されません。 代わりに、非同期的`Async<unit>`に実行する作業の*仕様*として機能する を返します。 この関数`Async.AwaitTask`は、その本文を呼び出し、<xref:System.IO.File.ReadAllBytesAsync%2A>結果を適切な型に変換します。

もう 1 つの重要な`Async.RunSynchronously`行は、 への呼び出しです。 これは、F# 非同期計算を実際に実行する場合に呼び出す必要がある Async モジュールの開始関数の 1 つです。

これは、C# /Visual Basic のプログラミングスタイルと`async`の基本的な違いです。 F# では、非同期計算は**Cold タスク**と考えることができます。 実際に実行するには、明示的に開始する必要があります。 C# や Visual Basic よりも簡単に非同期作業を組み合わせたり、シーケンス処理したりできるため、この方法には利点があります。

## <a name="combine-asynchronous-computations"></a>非同期計算を組み合わせる

次に、計算を組み合わせて前の例に基づいて作成する例を示します。

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn "File %s has %d bytes" fileName bytes.Length
    }

[<EntryPoint>]
let main argv =
    argv
    |> Array.map printTotalFileBytes
    |> Async.Parallel
    |> Async.Ignore
    |> Async.RunSynchronously

    0
```

ご覧のとおり、この`main`関数にはさらに多くの呼び出しが行われます。 概念的には、次の処理を行います。

1. コマンド ライン引数を を`Async<unit>`使用して`Array.map`計算に変換します。
2. 実行時`Async<'T[]>`に計算を並列に`printTotalFileBytes`実行する を作成します。
3. 並列計算`Async<unit>`を実行し、その結果を無視する を作成します。
4. 最後の計算を明示的に実行`Async.RunSynchronously`し、最後の計算を完了するまでブロックします。

このプログラムを実行すると`printTotalFileBytes`、コマンド ライン引数ごとに並列実行されます。 非同期計算はプログラム フローとは独立して実行されるため、情報を出力して実行を終了する順序はありません。 計算は並列にスケジュールされますが、実行順序は保証されません。

## <a name="sequence-asynchronous-computations"></a>シーケンス非同期計算

既`Async<'T>`に実行されているタスクではなく、作業の仕様であるため、複雑な変換を簡単に実行できます。 次に、非同期計算のセットをシーケンスして、次の例を次に示します。

```fsharp
let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn "File %s has %d bytes" fileName bytes.Length
    }

[<EntryPoint>]
let main argv =
    argv
    |> Array.map printTotalFileBytes
    |> Async.Sequential
    |> Async.Ignore
    |> Async.RunSynchronously
    |> ignore
```

これは、並列`printTotalFileBytes`にスケジュールするのではなく、要素`argv`の順序で実行するようにスケジュールします。 次の項目は、最後の計算の実行が終了するまでスケジュールされないため、実行に重複がないように計算が順番に作成されます。

## <a name="important-async-module-functions"></a>重要な非同期モジュール関数

F# で非同期コードを記述する場合、通常は計算のスケジューリングを処理するフレームワークと対話します。 ただし、必ずしもそうであるとは限らないので、非同期作業をスケジュールするさまざまな開始関数を学習することをお勧めします。

F# 非同期計算は、既に実行されている作業の表現ではなく、作業の_仕様_であるため、開始関数を使用して明示的に開始する必要があります。 さまざまなコンテキストで役立つ非同期[開始関数](https://msdn.microsoft.com/library/ee370232.aspx)が多数あります。 次のセクションでは、一般的な開始関数について説明します。

### <a name="asyncstartchild"></a>非同期.スタートチャイルド

非同期計算内で子の計算を開始します。 これにより、複数の非同期計算を同時に実行できます。 子計算は、親の計算とキャンセル トークンを共有します。 親の計算がキャンセルされた場合、子計算も取り消されます。

署名:

```fsharp
computation: Async<'T> * timeout: ?int -> Async<Async<'T>>
```

使う状況:

- 複数の非同期計算を同時に実行する場合は、同時に 1 つずつ実行するのではなく、並列にスケジュールを設定する必要はありません。
- 子計算の有効期間を親計算の有効期間に結び付ける場合。

注意すべきこと:

- 複数の計算を並列`Async.StartChild`に実行する場合と同じではありません。 計算を並列にスケジュールする場合は、 を`Async.Parallel`使用します。
- 親計算をキャンセルすると、開始したすべての子計算のキャンセルがトリガーされます。

### <a name="asyncstartimmediate"></a>非同期.スタートイミディエイト

非同期計算を実行し、現在のオペレーティング システムのスレッドですぐに開始します。 これは、計算中に呼び出し元のスレッドで何かを更新する必要がある場合に役立ちます。 たとえば、非同期計算で UI を更新する必要がある場合 (進行状況バーの更新など`Async.StartImmediate`)、使用する必要があります。

署名:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

使う状況:

- 非同期計算の途中で呼び出し元スレッドで何かを更新する必要がある場合。

注意すべきこと:

- 非同期計算のコードは、スケジュールされたスレッドで実行されます。 これは、UI スレッドなど、何らかの形でスレッドが機密性の高い場合に問題になる可能性があります。 このような場合、`Async.StartImmediate`使用することは不適切である可能性が高い。

### <a name="asyncstartastask"></a>非同期.スタートタスタスク

スレッド プールで計算を実行します。 計算<xref:System.Threading.Tasks.Task%601>が終了すると(結果が生成されるか、例外をスローするか、またはキャンセルされるか)、対応する状態で完了するを返します。 キャンセル トークンが指定されていない場合は、既定のキャンセル トークンが使用されます。

署名:

```fsharp
computation: Async<'T> * taskCreationOptions: ?TaskCreationOptions * cancellationToken: ?CancellationToken -> Task<'T>
```

使う状況:

- 非同期計算の結果を表すことを期待する .NET <xref:System.Threading.Tasks.Task%601> API を呼び出す必要がある場合。

注意すべきこと:

- この呼び出しは`Task`追加のオブジェクトを割り当て、頻繁に使用する場合はオーバーヘッドを増加させます。

### <a name="asyncparallel"></a>非同期.パラレル

並列実行される非同期計算のシーケンスをスケジュールします。 並列処理の度合いは、`maxDegreesOfParallelism`パラメーターを指定することによって、必要に応じて調整/調整できます。

署名:

```fsharp
computations: seq<Async<'T>> * ?maxDegreesOfParallelism: int -> Async<'T[]>
```

使用するタイミング:

- 一連の計算を同時に実行する必要があり、その実行順序に依存しない場合。
- 並列にスケジュールされた計算の結果が完了するまで必要ない場合。

注意すべきこと:

- すべての計算が完了した後にのみ、結果の値の配列にアクセスできます。
- 計算は、スケジュールが設定されるたびに実行されます。 この動作は、実行順序に依存できないことを意味します。

### <a name="asyncsequential"></a>非同期.シーケンシャル

渡された順序で実行される非同期計算のシーケンスをスケジュールします。 最初の計算が実行され、次に次の計算が実行されます。 並列計算は実行されません。

署名:

```fsharp
computations: seq<Async<'T>> -> Async<'T[]>
```

使用するタイミング:

- 複数の計算を順番に実行する必要がある場合。

注意すべきこと:

- すべての計算が完了した後にのみ、結果の値の配列にアクセスできます。
- 計算はこの関数に渡された順序で実行されるため、結果が返されるまでの時間が増える可能性があります。

### <a name="asyncawaittask"></a>非同期.Awaitタスク

指定<xref:System.Threading.Tasks.Task%601>された計算が完了するのを待ち、結果を`Async<'T>`

署名:

```fsharp
task: Task<'T> -> Async<'T>
```

使う状況:

- F# の非同期計算内でを<xref:System.Threading.Tasks.Task%601>返す .NET API を使用している場合。

注意すべきこと:

- 例外はタスク並列ライブラリ<xref:System.AggregateException>の規則に従ってラップされ、この動作は、F# 非同期が一般的に例外を表面化する方法とは異なります。

### <a name="asynccatch"></a>非同期キャッチ

指定`Async<'T>`された を実行する非同期計算を作成します`Async<Choice<'T, exn>>`。 指定`Async<'T>`された値が正常に完了すると、結果`Choice1Of2`の値を a が返されます。 例外が完了する前にスローされた場合、a`Choice2of2`が返され、例外が発生します。 それ自体が多くの計算で構成されている非同期計算で使用され、それらの計算の 1 つが例外をスローする場合、包含計算は完全に停止されます。

署名:

```fsharp
computation: Async<'T> -> Async<Choice<'T, exn>>
```

使う状況:

- 例外で失敗する可能性がある非同期作業を実行していて、呼び出し元でその例外を処理する場合。

注意すべきこと:

- 結合された非同期計算または順序付き非同期計算を使用する場合、包含計算は、その「内部」計算の 1 つが例外をスローした場合に完全に停止します。

### <a name="asyncignore"></a>非同期.無視

指定された計算を実行し、その結果を無視する非同期計算を作成します。

署名:

```fsharp
computation: Async<'T> -> Async<unit>
```

使う状況:

- 非同期計算の結果が不要な場合。 これは、非同期ではないコードの`ignore`コードに似ています。

注意すべきこと:

- を使用`Async.Ignore`する必要がある場合`Async.Start`や、 を必要とする別の`Async<unit>`関数を使用する必要がある場合は、結果を破棄しても問題ありません。 型シグネチャに適合するだけの結果を破棄しないようにします。

### <a name="asyncrunsynchronously"></a>同期.実行同期的に

非同期計算を実行し、呼び出し元のスレッドで結果を待機します。 この呼び出しはブロックしています。

署名:

```fsharp
computation: Async<'T> * timeout: ?int * cancellationToken: ?CancellationToken -> 'T
```

使用するタイミング:

- 必要な場合は、アプリケーション内で 1 回だけ使用します 。
- パフォーマンスを気にしないで、他の一連の非同期操作を一度に実行する必要がある場合。

注意すべきこと:

- 呼`Async.RunSynchronously`び出しは、実行が完了するまで呼び出しスレッドをブロックします。

### <a name="asyncstart"></a>非同期.開始

を返`unit`すスレッド プールで非同期計算を開始します。 結果を待ちません。 で`Async.Start`開始された入れ子になった計算は、それを呼び出した親の計算とは無関係に開始されます。 その有効期間は、親の計算に関連付けられてはいません。 親の計算がキャンセルされた場合、子の計算は取り消されません。

署名:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

次の場合にのみ使用します。

- 非同期計算では、結果が得られないか、処理が必要です。
- 非同期計算がいつ完了したのか知る必要はありません。
- 非同期計算が実行されるスレッドは気にしません。
- タスクの結果として生じる例外を認識したり報告したりする必要はありません。

注意すべきこと:

- で開始された計算によって発生した例外`Async.Start`は、呼び出し元に伝達されません。 呼び出し履歴は完全に巻き戻されます。
- 呼び出し`printfn``Async.Start`など、すべての作業は、プログラムの実行のメイン スレッドで発生する影響を発生しません。

## <a name="interoperate-with-net"></a>NET との相互運用

[非同期/await](../../../standard/async.md)スタイルの非同期プログラミングを使用する .NET ライブラリまたは C# コードベースを使用している可能性があります。 C# と大部分の .NET ライブラリでは<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.Task>と の型を使用するのではなく`Async<'T>`、コアの抽象化として使用するため、非同期処理にはこれら 2 つのアプローチの境界を越える必要があります。

### <a name="how-to-work-with-net-async-and-taskt"></a>NET 非同期と .NET の使用方法`Task<T>`

NET 非同期ライブラリとコードベースを使用<xref:System.Threading.Tasks.Task%601>する (つまり、戻り値を持つ非同期計算) は簡単で、F# でサポートが組み込まれています。

この関数を`Async.AwaitTask`使用して、.NET 非同期計算を待機できます。

```fsharp
let getValueFromLibrary param =
    async {
        let! value = DotNetLibrary.GetValueAsync param |> Async.AwaitTask
        return value
    }
```

この関数を`Async.StartAsTask`使用して、非同期計算を .NET 呼び出し元に渡すことができます。

```fsharp
let computationForCaller param =
    async {
        let! result = getAsyncResult param
        return result
    } |> Async.StartAsTask
```

### <a name="how-to-work-with-net-async-and-task"></a>NET 非同期と .NET の使用方法`Task`

を使用<xref:System.Threading.Tasks.Task>する API (つまり、値を返さない .NET 非同期計算) を使用するには、 を`Async<'T>`に変換する関数を追加する必要がある場合<xref:System.Threading.Tasks.Task>があります。

```fsharp
module Async =
    // Async<unit> -> Task
    let startTaskFromAsyncUnit (comp: Async<unit>) =
        Async.StartAsTask comp :> Task
```

as 入力を`Async.AwaitTask`受け入れる<xref:System.Threading.Tasks.Task>ものが既にあります。 これと以前に定義`startTaskFromAsyncUnit`した関数を使用すると、F#<xref:System.Threading.Tasks.Task>非同期計算から型を開始し、待機できます。

## <a name="relationship-to-multi-threading"></a>マルチスレッドとの関係

この記事ではスレッド処理について説明していますが、注意が必要な 2 つの点があります。

1. 現在のスレッドで明示的に開始しない限り、非同期計算とスレッドの間には関係性がありません。
1. F# の非同期プログラミングは、マルチスレッドの抽象化ではありません。

たとえば、計算は、実際には、作業の性質に応じて、その呼び出し元のスレッドで実行されます。 計算は、スレッド間で「ジャンプ」し、スレッドを少しの時間借りて、"待機中" の期間 (ネットワーク呼び出しが転送中の場合など) の間に有益な作業を行う可能性があります。

F# には、現在のスレッドで非同期計算を開始する機能がいくつか用意されていますが (明示的に現在のスレッドでは使用できません)、非同期は通常、特定のスレッド化戦略に関連付けらされていません。

## <a name="see-also"></a>関連項目

- [F# 非同期プログラミング モデル](https://www.microsoft.com/research/publication/the-f-asynchronous-programming-model)
- [Jet.com の F# 非同期ガイド](https://medium.com/jettech/f-async-guide-eb3c8a2d180a)
- [F# の楽しさと利益の非同期プログラミング ガイド](https://fsharpforfunandprofit.com/posts/concurrency-async-and-parallel/)
- [C# と F# の非同期: C の非同期の問題#](http://tomasp.net/blog/csharp-async-gotchas.aspx/)
