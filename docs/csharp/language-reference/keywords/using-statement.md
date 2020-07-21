---
title: using ステートメント - C# リファレンス
ms.date: 05/29/2020
helpviewer_keywords:
- using statement [C#]
ms.assetid: afc355e6-f0b9-4240-94dd-0d93f17d9fc3
ms.openlocfilehash: b889d2fcbdf854dbe8948744810f9b74e9f0dac2
ms.sourcegitcommit: 5280b2aef60a1ed99002dba44e4b9e7f6c830604
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84307047"
---
# <a name="using-statement-c-reference"></a>using ステートメント (C# リファレンス)

<xref:System.IDisposable> オブジェクトの正しい使用を保証する簡易構文を提供します。 C# 8.0 以降は、`using` ステートメントによって <xref:System.IAsyncDisposable> オブジェクトが適切に使用されるようになります。

## <a name="example"></a>例

`using` ステートメントを使用する方法の例を次に示します。

:::code language="csharp" source="snippets/usings.cs" id="SnippetFirstExample":::

C# 8.0 以降では、中かっこを必要としない `using` ステートメントに次の代替構文を使用できます。

:::code language="csharp" source="snippets/usings.cs" id="SnippetModernUsing":::

## <a name="remarks"></a>Remarks

<xref:System.IO.File> と <xref:System.Drawing.Font> は、アンマネージド リソース (この場合はファイル ハンドルとデバイス コンテキスト) にアクセスするマネージド型の例です。 アンマネージ リソースや、それをカプセル化するクラス ライブラリ型は他にもたくさんあります。 このようなすべての型は、<xref:System.IDisposable> インターフェイスまたは <xref:System.IAsyncDisposable> インターフェイスを実装する必要があります。

`IDisposable` オブジェクトの有効期間が 1 つのメソッドに限定されているとき、それを `using` ステートメントで宣言し、インスタンス化してください。 `using` ステートメントは、オブジェクトで正しく <xref:System.IDisposable.Dispose%2A> メソッドを呼び出します。(前述のようにこのステートメントを使用する場合) <xref:System.IDisposable.Dispose%2A> が呼び出されるとすぐに、オブジェクト自体がスコープの外側に出されます。 オブジェクトは、`using` ブロック内では読み取り専用です。変更したり再割り当てしたりすることはできません。 オブジェクトに `IDisposable` ではなく `IAsyncDisposable` が実装されている場合、`using` ステートメントからは <xref:System.IAsyncDisposable.DisposeAsync%2A> が呼び出され、返される <xref:System.Threading.Tasks.ValueTask> の `awaits` を行います。 <xref:System.IAsyncDisposable> の詳細については、「[DisposeAsync メソッドの実装](../../../standard/garbage-collection/implementing-disposeasync.md)」を参照してください。

`using` ステートメントにより、`using` ブロック内で例外が発生した場合でも必ず <xref:System.IDisposable.Dispose%2A> (または <xref:System.IAsyncDisposable.DisposeAsync%2A>) が呼び出されます。 オブジェクトを `try` ブロックに配置し、`finally` ブロック内で <xref:System.IDisposable.Dispose%2A> (または <xref:System.IAsyncDisposable.DisposeAsync%2A>) を呼び出しても、同じ結果が得られます。実際には、コンパイラによって `using` ステートメントがこのように変換されます。 前のコード例は、コンパイル時に次のコードに展開されます (オブジェクトのスコープ制限を定義する中かっこが加えられていることに注意してください)。

:::code language="csharp" source="snippets/usings.cs" id="SnippetTryFinallyExample":::

新しい `using` ステートメントの構文は似たコードに変換されます。 変数が宣言されている場所で `try` ブロックが開きます。 `finally` ブロックは、囲んでいるブロックの終わり、通常はメソッドの最後に追加されます。

`try`-`finally` ステートメントの詳細については、「[try-finally](try-finally.md)」の記事を参照してください。

次の例のように、1 つの `using` ステートメントで型の複数のインスタンスを宣言できます。 1 つのステートメントで複数の変数を宣言する場合、暗黙的に型指定された変数 (`var`) を使用できないことに注意してください。

:::code language="csharp" source="snippets/usings.cs" id="SnippetDeclareMultipleVariables":::

次の例に示すように、C# 8 で導入された新しい構文を使用して、同じ型の複数の宣言を組み合わせることができます。

:::code language="csharp" source="snippets/usings.cs" id="SnippetModernMultipleVariables":::

リソース オブジェクトをインスタンス化してから、変数を `using` ステートメントに渡すことはできますが、これはベスト プラクティスではありません。 この場合、アンマネージド リソースへのアクセスがなくなっている可能性が高いのにもかかわらず、制御が `using` ブロックを離れた後もオブジェクトはスコープ内に残ります。 つまり、完全に初期化されることはなくなります。 `using` ブロックの外側でオブジェクトを使用しようとすると、例外がスローされる可能性があります。 このため、オブジェクトを `using` ステートメントでインスタンス化して、そのスコープを `using` ブロックに制限することをお勧めします。

:::code language="csharp" source="snippets/usings.cs" id="SnippetDeclareBeforeUsing":::

`IDisposable` オブジェクトの破棄に関する詳細については、「[IDisposable を実装するオブジェクトの使用](../../../standard/garbage-collection/using-objects.md)」を参照してください。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](/dotnet/csharp/language-reference/language-specification/introduction)に関するページの [using ステートメント](~/_csharplang/spec/statements.md#the-using-statement)に関するセクションを参照してください。 言語仕様は、C# の構文と使用法に関する信頼性のある情報源です。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [using ディレクティブ](using-directive.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
- [IDisposable を実装するオブジェクトの使用](../../../standard/garbage-collection/using-objects.md)
- [IDisposable インターフェイス](xref:System.IDisposable)
- [C# 8.0 の using ステートメント](~/_csharplang/proposals/csharp-8.0/using.md)
