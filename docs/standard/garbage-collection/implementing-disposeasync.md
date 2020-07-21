---
title: DisposeAsync メソッドの実装
description: ''
author: IEvangelist
ms.author: dapine
ms.date: 06/02/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
helpviewer_keywords:
- DisposeAsync method
- garbage collection, DisposeAsync method
ms.openlocfilehash: 31c4cc9136862551e02fae030e38ebd6c2916a38
ms.sourcegitcommit: 4ad2f8920251f3744240c3b42a443ffbe0a46577
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86100926"
---
# <a name="implement-a-disposeasync-method"></a>DisposeAsync メソッドの実装

<xref:System.IAsyncDisposable?displayProperty=nameWithType> インターフェイスが、C# 8.0 の一部として導入されました。 <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> メソッドは、[Dispose メソッドの実装](implementing-dispose.md)と同様、リソースのクリーンアップを実行する必要がある場合に実装します。 両者の重要な違いの 1 つは、この実装により、非同期のクリーンアップ操作が可能になることです。 <xref:System.IAsyncDisposable.DisposeAsync> は、非同期の破棄操作を表す <xref:System.Threading.Tasks.ValueTask> を返します。

通常は、<xref:System.IAsyncDisposable> インターフェイスを実装するときに、クラスは <xref:System.IDisposable> インターフェイスも実装します。 推奨される <xref:System.IAsyncDisposable> インターフェイスの実装パターンは、同期の破棄か非同期の破棄のために準備をすることです。 破棄パターンの実装に関するガイダンスのすべての説明は、非同期の実装に適用されます。 この記事では、読者が [Dispose メソッドの実装](implementing-dispose.md)方法について既に理解していることを前提としています。

## <a name="disposeasync-and-disposeasynccore"></a>DisposeAsync() および DisposeAsyncCore()

<xref:System.IAsyncDisposable> インターフェイスは、パラメーターなしの単一のメソッド <xref:System.IAsyncDisposable.DisposeAsync> を宣言します。 すべての非シールド クラスには、追加の `DisposeAsyncCore()` メソッドが必要です。このメソッドも <xref:System.Threading.Tasks.ValueTask> を返します。

- パラメーターを持たない `public` <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> の実装。
- 次のシグネチャを持つ `protected virtual ValueTask DisposeAsyncCore()` メソッド。

```csharp
protected virtual ValueTask DisposeAsyncCore()
{
}
```

`DisposeAsyncCore()` メソッドは `virtual` であるので、派生クラスはオーバーライドで追加のクリーンアップを定義できます。

### <a name="the-disposeasync-method"></a>DisposeAsync() メソッド

`public` のパラメーターなしの `DisposeAsync()` メソッドは、`await using` ステートメントで暗黙的に呼び出されます。その目的は、アンマネージド リソースを解放し、通常のクリーンアップを実行し、ファイナライザーが存在する場合、それを実行する必要がないことを示すことです。 管理されたオブジェクトに関連付けられているメモリを解放するのは、常に[ガベージ コレクター](index.md)のドメインです。 このため、次のような標準的な実装があります。

```csharp
public async ValueTask DisposeAsync()
{
    // Perform async cleanup.
    await DisposeAsyncCore();

    // Dispose of managed resources.
    Dispose(false);
    // Suppress finalization.
    GC.SuppressFinalize(this);
}
```

> [!NOTE]
> 非同期の破棄パターンでの、その破棄パターンとの主な違いの 1 つは、<xref:System.IAsyncDisposable.DisposeAsync> から `Dispose(bool)` オーバーロード メソッドへの呼び出しで、`false` が引数として渡されることです。 一方、<xref:System.IDisposable.Dispose?displayProperty=nameWithType> メソッドを実装する場合は、`true` が渡されます。 これにより、同期の破棄パターンとの機能の等価性が確保されるほか、ファイナライザーのコード パスが引き続き呼び出されるようにできます。 言い換えると、`DisposeAsyncCore()` メソッドでは管理対象リソースが非同期的に破棄されるため、同期的にも破棄される必要はありません。 したがって、`Dispose(true)` ではなく `Dispose(false)` を呼び出します。

## <a name="implement-the-async-dispose-pattern"></a>非同期の破棄パターンの実装

非シールド クラスは、継承される可能性があるため、潜在的な基底クラスと見なす必要があります。 潜在的な基底クラスに対して非同期の破棄パターンを実装する場合、`protected virtual ValueTask DisposeAsyncCore()` メソッドを指定する必要があります。 次に、<xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType> を使用する非同期の破棄パターンの実装例を示します。

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/disposeasync.cs":::

上の例では、<xref:System.Text.Json.Utf8JsonWriter> を使用しています。`System.Text.Json` の詳細については、[Newtonsoft.Json から System.Text.Json への移行](../serialization/system-text-json-migrate-from-newtonsoft-how-to.md)に関するページを参照してください。

## <a name="using-async-disposable"></a>非同期の破棄可能の使用

<xref:System.IAsyncDisposable> インターフェイスを実装するオブジェクトを適切に使用するには、[await](../../csharp/language-reference/operators/await.md) キーワードと [using](../../csharp/language-reference/keywords/using.md) キーワードを一緒に使用します。 次の例では、`ExampleAsyncDisposable` クラスがインスタンス化され、`await using` ステートメントでラップされています。

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/proper-await-using.cs":::

> [!IMPORTANT]
> 元のコンテキストやスケジューラでタスクの継続をマーシャリングする方法を構成するには、<xref:System.IAsyncDisposable> インターフェイスの <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)> 拡張メソッドを使用します。 `ConfigureAwait` の詳細については、「[ConfigureAwait に関する FAQ](https://devblogs.microsoft.com/dotnet/configureawait-faq/)」を参照してください。

`ConfigureAwait` を使用する必要がない場合、`await using` ステートメントは次のように簡略化できます。

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-non-configureawait.cs":::

さらに、[using 宣言](../../csharp/whats-new/csharp-8.md#using-declarations)の暗黙的なスコープを使用するように記述することもできます。

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-declaration.cs":::

## <a name="stacked-usings"></a>using の積み重ね

<xref:System.IAsyncDisposable> を実装する複数のオブジェクトを作成して使用する場合、`using` ステートメントを誤った条件で積み重ねると、<xref:System.IAsyncDisposable.DisposeAsync> を呼び出すことができなくなる可能性があります。 潜在的な問題を防ぐため、積み重ねを避け、次の例のパターンに従う必要があります。

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

## <a name="see-also"></a>関連項目

- <xref:System.IAsyncDisposable>
- <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)>
