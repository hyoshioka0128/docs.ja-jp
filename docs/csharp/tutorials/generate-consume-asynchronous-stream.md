---
title: 非同期ストリームの生成と使用
description: この上級チュートリアルでは、非同期ストリームを生成し、使用する方法について説明します。 非同期ストリームでは、非同期で生成される可能性があるデータのシーケンスを自然な方法で処理できます。
ms.date: 02/10/2019
ms.technology: csharp-async
ms.custom: mvc
ms.openlocfilehash: fd9fed3469d18c919102640df7bb501b116f5e0e
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420371"
---
# <a name="tutorial-generate-and-consume-async-streams-using-c-80-and-net-core-30"></a>チュートリアル: C#8.0 および .NET Core 3.0 を使用して非同期ストリームを生成および使用する

C# 8.0 では、データのストリーミング元をモデル化する**非同期ストリーム**が導入されました。 データ ストリームでは、多くの場合、要素を非同期で取得または生成します。 非同期ストリームは .NET Standard 2.1 で導入された新しいインターフェイスに依存します。 このインターフェイスは .NET Core 3.0 以降でサポートされています。 非同期でストリーミングするデータ ソースにとって自然なプログラミング モデルが与えられます。

このチュートリアルでは、次の作業を行う方法について説明します。

> [!div class="checklist"]
>
> - データ要素のシーケンスを非同期で生成するデータ ソースを作成します。
> - そのデータ ソースを非同期で使用します。
> - 非同期ストリームのキャンセルとキャプチャされたコンテキストをサポートします。
> - 新しいインターフェイスとデータ ソースが以前の同期データ シーケンスより優先される場合を認識します。

## <a name="prerequisites"></a>必須コンポーネント

お使いのコンピューターを、.NET Core が実行されるように設定する必要があります。C# 8.0 コンパイラも実行されるようにします。 C# 8 コンパイラは [Visual Studio 2019 バージョン 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) または [.NET Core 3.0 SDK](https://dotnet.microsoft.com/download) 以降で使用できます。

[GitHub アクセス トークン](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/#creating-a-token)を作成して、GitHub GraphQL エンドポイントにアクセスできるようにする必要があります。 GitHub アクセス トークンに対して次のアクセス許可を選択します。

- repo:status
- public_repo

アクセス トークンを安全な場所に保存して、GitHub API エンドポイントへのアクセス権を得るために使用できるようにします。

> [!WARNING]
> 自分の個人用アクセス トークンをセキュリティで保護します。 個人用アクセス トークンを使用するソフトウェアでは、ユーザーのアクセス権を使用して GitHub API 呼び出しが行われる可能性があります。

このチュートリアルでは、.NET と、C# と Visual Studio または .NET Core CLI のいずれかに精通していることを前提としています。

## <a name="run-the-starter-application"></a>初期アプリケーションを実行する

このチュートリアルで使用される初期アプリケーションのコードは、[csharp/tutorials/AsyncStreams](https://github.com/dotnet/docs/tree/master/docs/csharp/tutorials/snippets/generate-consume-asynchronous-streams/start) フォルダー内の [dotnet/docs](https://github.com/dotnet/docs) リポジトリから取得できます。

初期アプリケーションは、[GitHub GraphQL](https://developer.github.com/v4/) インターフェイスを使用して、[dotnet/docs](https://github.com/dotnet/docs) リポジトリに書き込まれた最近の問題を取得するコンソール アプリケーションです。 まず、初期アプリの `Main` メソッドについて次のコードを参照します。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/start/Program.cs" id="SnippetStarterAppMain" :::

`GitHubKey` 環境変数を自分の個人用アクセス トークンに設定するか、`GenEnvVariable` への呼び出しの最後の引数を自分の個人用アクセス トークンで置き換えることができます。 ソースを他人と共有する場合、自分のアクセス コードをソース コードに置かないでください。 共有ソース リポジトリにアクセス コードをアップロードしないでください。

GitHub クライアントの作成後に、`Main` 内のコードによって進行状況レポート オブジェクトとキャンセル トークンが作成されます。 これらのオブジェクトが作成されると、`Main` によって `runPagedQueryAsync` が呼び出されて、作成された直近 250 件の問題が取得されます。 そのタスクが完了すると、結果が表示されます。

初期アプリケーションを実行するときに、このアプリケーションの実行方法についていくつかの重要な観察を行うことができます。  GitHub から返される各ページについてレポートされる進行状況を確認します。 問題の新しい各ページが GitHub から返される前に、注目すべき一時停止を観察できます。 最後に、問題は GitHub から 10 ページすべてが取得された後にのみ表示されます。

## <a name="examine-the-implementation"></a>実装を調べる

実装では、前のセクションで説明した動作を観察した理由が明らかになります。 `runPagedQueryAsync` のコードを調べます:

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/start/Program.cs" id="SnippetRunPagedQuery" :::

上記のコードのページング アルゴリズムと非同期構造体に注目してみましょう。 (GitHub GraphQL API について詳しくは、[GitHub GraphQL のドキュメント](https://developer.github.com/v4/guides/)をご覧ください。)`runPagedQueryAsync` メソッドでは、問題が新しい順に列挙されます。 1 ページあたり 25 件の問題を要求し、応答の `pageInfo` 構造体を調べて前のページに進みます。 次の GraphQL の標準的なページングでは、複数ページの応答がサポートされます。 応答には、前のページを要求するために使用される `hasPreviousPages` 値と `startCursor` 値を含む `pageInfo` オブジェクトが含まれています。 問題は `nodes` 配列内にあります。 `runPagedQueryAsync` メソッドでは、すべてのページからのすべての結果を格納する配列にこれらのノードが追加されます。

結果のページを取得し、復元した後、`runPagedQueryAsync` によって進行状況がレポートされ、キャンセルがチェックされます。 キャンセルが要求されている場合は、`runPagedQueryAsync` によって <xref:System.OperationCanceledException> がスローされます。

このコードには、改善できる要素がいくつかあります。 最も重要なものとして、`runPagedQueryAsync` では返されるすべての問題に記憶域を割り当てる必要があります。 未解決の問題をすべて取得するには、取得したすべての問題を格納するためにはるかに多くのメモリが必要になるので、このサンプルは 250 件の問題で停止します。 進行状況レポートとキャンセルをサポートするためのプロトコルが原因で、アルゴリズムを初読で理解することが難しくなります。 関連する型や API の数が増えます。 <xref:System.Threading.CancellationTokenSource> とそれに関連付けられた <xref:System.Threading.CancellationToken> を通じた通信をトレースして、キャンセルが要求されている場所と、付与されている場所を理解する必要があります。

## <a name="async-streams-provide-a-better-way"></a>非同期ストリームではより優れた方法が提供される

非同期ストリームおよび関連付けられている言語サポートは、これらすべての問題に対処します。 シーケンスを生成するコードでは、`yield return` を使用して、`async` 修飾子で宣言されたメソッド内で要素を返せるようになりました。 `foreach` ループを使用してシーケンスを使用する場合と同様に、`await foreach` ループを使用して非同期ストリームを使用することができます。

これらの新しい言語機能は、.NET Standard 2.1 に追加され、.NET Core 3.0 で実装された 3 つの新しいインターフェイスに依存します。

- <xref:System.Collections.Generic.IAsyncEnumerable%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.IAsyncEnumerator%601?displayProperty=nameWithType>
- <xref:System.IAsyncDisposable?displayProperty=nameWithType>

この 3 つのインターフェイスは、ほとんどの C# 開発者にとって見慣れたものです。 これらは、同期版と同じように動作します。

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.IEnumerator%601?displayProperty=nameWithType>
- <xref:System.IDisposable?displayProperty=nameWithType>

見慣れない可能性のある 1 つの型は <xref:System.Threading.Tasks.ValueTask?displayProperty=nameWithType> です。 `ValueTask` 構造体では、<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> クラスと同様の API が提供されます。 パフォーマンス上の理由から、これらのインターフェイスでは `ValueTask` が使用されます。

## <a name="convert-to-async-streams"></a>非同期ストリームに変換する

次に、`runPagedQueryAsync` メソッドを変換して非同期ストリームを生成します。 まず、`IAsyncEnumerable<JToken>` を返すように `runPagedQueryAsync` のシグネチャを変更し、次のコードに示すように、パラメーター リストからキャンセル トークンと進行状況オブジェクトを削除します。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetUpdateSignature" :::

次のコードに示すように、初期コードではページが取得されると各ページが処理されます。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/start/Program.cs" id="SnippetProcessPage" :::

この 3 行を次のコードに置き換えます。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetYieldReturnPage" :::

このメソッドの前の方にある `finalResults` の宣言と、変更したループに続く `return` ステートメントを削除することもできます。

非同期ストリームを生成するための変更が完了しました。 完了したメソッドは次のコードのようになります。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetGenerateAsyncStream" :::

次に、コレクションを使用するコードを変更して、非同期ストリームを使用するようにします。 `Main` 内で、問題のコレクションを処理する次のコードを探します。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/start/Program.cs" id="SnippetEnumerateOldStyle" :::

このコードを次の `await foreach` ループに置き換えます。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetEnumerateAsyncStream" :::

新しいインターフェイス <xref:System.Collections.Generic.IAsyncEnumerator%601> は <xref:System.IAsyncDisposable> から派生します。 つまり、前のループは、ループの完了時、ストリームを非同期で破棄します。 ループは次のコードのようになります。

```csharp
int num = 0;
var enumerator = runPagedQueryAsync(client, PagedIssueQuery, "docs").GetEnumeratorAsync();
try
{
    while (await enumerator.MoveNextAsync())
    {
        var issue = enumerator.Current;
        Console.WriteLine(issue);
        Console.WriteLine($"Received {++num} issues in total");
    }
} finally
{
    if (enumerator != null)
        await enumerator.DisposeAsync();
}
```

既定では、ストリーム要素はキャプチャされたコンテキストで処理されます。 コンテキストのキャプチャを無効にする場合は、<xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait%2A?displayProperty=nameWithType> 拡張メソッドを使用します。 同期コンテキストについて、および現在のコンテキストのキャプチャについての詳細は、「[タスク ベースの非同期パターンの利用](../../standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)」を参照してください。

非同期ストリームでは、他の `async` メソッドと同じプロトコルを利用してキャンセルできます。 キャンセルをサポートするよう、非同期反復子メソッドのシグネチャを次のように変更します。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetGenerateWithCancellation" :::

<xref:System.Runtime.CompilerServices.EnumeratorCancellationAttribute?dipslayProperty=nameWithType> 属性によってコンパイラは <xref:System.Collections.Generic.IAsyncEnumerator%601> のコードを生成します。このコードは、`GetAsyncEnumerator` に渡されたトークンを非同期反復子の本文にその引数として表示します。 `runQueryAsync` の中では、トークンの状態を調べたり、要求されたら、後続の処理をキャンセルしたりできます。

キャンセル トークンを非同期ストリームに渡すには、別の拡張メソッド <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.WithCancellation%2A> を使用します。 問題を列挙するループを次のように変更します。

:::code language="csharp" source="snippets/generate-consume-asynchronous-streams/finished/Program.cs" id="SnippetEnumerateWithCancellation" :::

完了したチュートリアルのコードは、[csharp/tutorials/AsyncStreams](https://github.com/dotnet/docs/tree/master/docs/csharp/tutorials/snippets/generate-consume-asynchronous-streams/finished) フォルダー内の [dotnet/docs](https://github.com/dotnet/docs) リポジトリから取得できます。

## <a name="run-the-finished-application"></a>完成したアプリケーションを実行する

アプリケーションをもう一度実行します。 その動作を初期アプリケーションの動作と比較します。 結果の最初のページは、使用可能になるとすぐに列挙されます。 新しい各ページが要求され、取得されるときに観測可能な一時停止があり、次のページの結果がすぐに列挙されます。 `try` / `catch` ブロックではキャンセルを処理する必要はありません。呼び出し元がコレクションの列挙を停止できます。 各ページがダウンロードされるときに非同期ストリームによって結果が生成されるので、進行状況が明確にレポートされます。 返される各問題の状態は、`await foreach` ループにシームレスに含まれます。 進行状況を追跡するためにコールバック オブジェクトは必要ありません。

コードを調べることで、メモリの改善を確認できます。 すべての結果が列挙される前にそれらを格納するコレクションを割り当てる必要がなくなります。 呼び出し元では、結果を使用する方法、および記憶域のコレクションが必要かどうかを判断できます。

初期アプリケーションと完成したアプリケーションの両方を実行し、実装間の違いを自分で確認できます。 完了後に、このチュートリアルの開始時に作成した GitHub アクセス トークンを削除することができます。 攻撃者は、そのトークンへのアクセス権を獲得すると、ユーザーの資格情報を使用して GitHub API にアクセスできます。
