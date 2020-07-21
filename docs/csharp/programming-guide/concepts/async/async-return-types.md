---
title: 非同期の戻り値の型 (C#)
ms.date: 04/14/2020
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
ms.openlocfilehash: c2584f1e285a7ab76eb43f9a211a8d2a51c2c55e
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83761877"
---
# <a name="async-return-types-c"></a>非同期の戻り値の型 (C#)

非同期メソッドには、次の戻り値の型があります。

- <xref:System.Threading.Tasks.Task%601>: 値を返す非同期メソッドの場合。
- <xref:System.Threading.Tasks.Task>: 操作を実行し、値を返さない非同期メソッドの場合。
- `void`: イベント ハンドラーの場合。
- C# 7.0 以降、アクセス可能な `GetAwaiter` を持つ任意の型です。 <xref:System.Runtime.CompilerServices.ICriticalNotifyCompletion?displayProperty=nameWithType> メソッドによって返されるオブジェクトは、`GetAwaiter` インターフェイスを実装する必要があります。
- C# 8.0 以降、"*非同期ストリーム*" を返す非同期メソッドの場合は <xref:System.Collections.Generic.IAsyncEnumerable%601>。

非同期メソッドの詳細については、「[Async および Await を使用した非同期プログラミング (C#)](./index.md)」を参照してください。  
  
## <a name="tasktresult-return-type"></a>Task\<TResult\> の戻り値の型  
オペランドが `TResult` の [return](../../../language-reference/keywords/return.md) (C#) ステートメントを含む非同期メソッドには、<xref:System.Threading.Tasks.Task%601> 戻り値の型が使用されます。  
  
次の例では、`GetLeisureHours` 非同期メソッドには整数を返す `return` ステートメントが含まれます。 そのため、メソッド宣言では、戻り値の型を `Task<int>` と指定する必要があります。  <xref:System.Threading.Tasks.Task.FromResult%2A> 非同期メソッドは、文字列を返す操作を表すプレースホルダーです。
  
:::code language="csharp" source="./snippets/async-return-types/async-returns1.cs" id="SnippetFirstExample":::

`GetLeisureHours` が `ShowTodaysInfo` メソッドの await 式の中から呼び出されると、await 式は `GetLeisureHours` メソッドから返されるタスクに格納されている整数値 (`leisureHours` の値) を取得します。 await 式の詳細については、「[await](../../../language-reference/operators/await.md)」を参照してください。  
  
次のコードが示すように、`GetLeisureHours` への呼び出しを `await` のアプリケーションから分離すると、`await` で `Task<T>` から結果を取得する方法をよりよく理解できます。 メソッドの宣言から予想されるように、直ちに待機しない `GetLeisureHours` メソッドの呼び出しは、`Task<int>` を返します。 タスクは、この例の `integerTask` 変数に割り当てられます。 `integerTask` は <xref:System.Threading.Tasks.Task%601> であるため、<xref:System.Threading.Tasks.Task%601.Result> 型の `TResult` プロパティが含まれています。 この場合、`TResult` は整数型を表します。 `await` が `integerTask` に適用されると、`integerTask` の <xref:System.Threading.Tasks.Task%601.Result%2A> プロパティの内容が await 式の評価となります。 この値は `ret` 変数に割り当てられます。  
  
> [!IMPORTANT]
> <xref:System.Threading.Tasks.Task%601.Result%2A> プロパティは Blocking プロパティです。 タスクが終了する前にアクセスしようとすると、現在アクティブなスレッドは、タスクが完了して値が使用可能になるまで、ブロックされます。 多くの場合、プロパティに直接アクセスする代わりに、`await` を使用して値にアクセスする必要があります。 <br/> 前の例では、アプリケーションが終了する前に `ShowTodaysInfo` メソッドが実行を終了できるように、<xref:System.Threading.Tasks.Task%601.Result%2A> プロパティの値を取得してメイン スレッドをブロックしました。  

:::code language="csharp" source="./snippets/async-return-types/async-returns1a.cs" id="SnippetSecondVersion":::

## <a name="task-return-type"></a>Task の戻り値の型  
`return` ステートメントを含まない非同期メソッド、またはオペランドを返さない `return` ステートメントを含む非同期メソッドは、通常は <xref:System.Threading.Tasks.Task> の戻り値の型を指定します。 こうしたメソッドは、同期的に実行するように作成されている場合に `void` を返します。 非同期メソッドに戻り値の型 <xref:System.Threading.Tasks.Task> を使用した場合、呼び出し元のメソッドは `await` 演算子を使って、呼び出された async のメソッドが終了するまで、呼び出し元の完了を中断します。  
  
次の例では、`WaitAndApologize` 非同期メソッドには `return` ステートメントが含まれていないため、メソッドは <xref:System.Threading.Tasks.Task> オブジェクトを返します。 `Task` を返すことで、`WaitAndApologize` を待機できるようになります。 <xref:System.Threading.Tasks.Task> 型には戻り値がないため、`Result` プロパティを含みません。  

:::code language="csharp" source="./snippets/async-return-types/async-returns2.cs" id="SnippetTaskReturn":::

`WaitAndApologize` を待機するには、void を返す同期メソッドを呼び出す場合と同様に、await 式でなく、await ステートメントを使用します。 この場合、await 演算子の適用によって値は生成されません。  
  
前の <xref:System.Threading.Tasks.Task%601> の例のように、次のコードに示すとおり、`WaitAndApologize` の呼び出しを await 演算子の適用から分離することができます。 ただし `Task` は `Result` プロパティを持たないこと、また await 演算子が `Task` に適用されるときに値は生成されないことに注意します。  
  
次のコードは、`WaitAndApologize` メソッドの呼び出しを、そのメソッドが返すタスクの待機から分離します。  

:::code language="csharp" source="./snippets/async-return-types/async-returns2a.cs" id="SnippetAwaitTask":::

## <a name="void-return-type"></a>Void の戻り値の型

`void` 戻り値の型は、`void` 戻り値の型が必要な非同期イベント ハンドラーで使用します。 値を返さないイベント ハンドラー以外のメソッドについては、<xref:System.Threading.Tasks.Task> を返す必要があります。これは、`void` を返す非同期メソッドを待機できないためです。 このようなメソッドの呼び出し元は、呼び出された非同期メソッドが完了するまで待機せずに、完了するまで続行する必要があります。 呼び出し元は、非同期メソッドによって生成される値や例外から独立している必要があります。  
  
void を返す非同期メソッドの呼び出し元は、メソッドからスローされる例外をキャッチすることはできません。そのようなハンドルされない例外によって、アプリケーションが失敗する可能性が高くなります。 <xref:System.Threading.Tasks.Task> または <xref:System.Threading.Tasks.Task%601> を返すメソッドから例外がスローされた場合、例外は返されたタスクに格納されます。 タスクを待機しているときは、例外が再スローされます。 したがって、例外を生成する場合がある非同期メソッドは <xref:System.Threading.Tasks.Task> または <xref:System.Threading.Tasks.Task%601> の戻り値の型を持つこと、またメソッドの呼び出しが待機することを確認します。  
  
非同期メソッドで例外をキャッチする方法の詳細については、「[try-catch](../../../language-reference/keywords/try-catch.md)」の記事の「[非同期メソッドの例外](../../../language-reference/keywords/try-catch.md#exceptions-in-async-methods)」を参照してください。  
  
次の例では、非同期イベント ハンドラーの動作を示します。 コード例では、非同期イベント ハンドラーが終了したとき、その非同期イベント ハンドラーからメイン スレッドに通知が送られる必要があります。 このため、メイン スレッドでは、非同期イベント ハンドラーの終了を待ってから、プログラムを終了することができます。

:::code language="csharp" source="./snippets/async-return-types/async-returns3.cs":::

## <a name="generalized-async-return-types-and-valuetasktresult"></a>一般化された非同期の戻り値の型と ValueTask\<TResult\>

C# 7.0 以降、非同期メソッドで、アクセス可能な `GetAwaiter` メソッドを持つ任意の型を返すことができます。

<xref:System.Threading.Tasks.Task> および <xref:System.Threading.Tasks.Task%601> は参照型であるため、特に厳密なループ処理で割り当てが発生すると、パフォーマンスが重要なパスのメモリ割り当てが、パフォーマンスに悪影響を及ぼすことがあります。 一般化された戻り値の型のサポートにより、参照型ではなく、軽量な値の型を返すことができ、追加のメモリ割り当てを回避することが可能です。

.NET には、一般化されたタスク戻り値の軽量な実装として、<xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType> 構造が用意されています。 <xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType> 型を使用するには、`System.Threading.Tasks.Extensions` NuGet パッケージをプロジェクトに追加する必要があります。 次の例では、<xref:System.Threading.Tasks.ValueTask%601> 構造を使用して、2 つのさいころを転がしたときの値を取得します。
  
:::code language="csharp" source="./snippets/async-return-types/async-valuetask.cs":::

## <a name="async-streams-with-iasyncenumerablet"></a>IAsyncEnumerable\<T\> を使用する非同期ストリーム

C# 8.0 以降は、非同期メソッドから <xref:System.Collections.Generic.IAsyncEnumerable%601> で表される*非同期ストリーム*が返される場合があります。 非同期ストリームを使用すると、非同期呼び出しが繰り返される要素がチャンクで生成されるときに、ストリームから読み取られた項目を列挙できます。 次の例は、非同期ストリームを生成する非同期メソッドを示しています。

:::code language="csharp" source="./snippets/async-return-types/AsyncStreams.cs" id="SnippetGenerateAsyncStream":::

前の例では、文字列から非同期に行を読み取ります。 各行が読み取られると、コードによって文字列内の各単語が列挙されます。 呼び出し元では、`await foreach` ステートメントを使用して各単語を列挙します。 このメソッドを使用すると、ソース文字列から次の行を非同期的に読み取る必要があるときに待機できます。

## <a name="see-also"></a>関連項目

- <xref:System.Threading.Tasks.Task.FromResult%2A>
- [チュートリアル: Async と Await を使用した Web へのアクセス (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md)
- [非同期プログラムにおける制御フロー (C#)](./control-flow-in-async-programs.md)
- [async](../../../language-reference/keywords/async.md)
- [await](../../../language-reference/operators/await.md)
