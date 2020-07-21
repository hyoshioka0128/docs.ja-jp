---
title: IDisposable を実装するオブジェクトの使用
description: .NET で IDisposable インターフェイスを実装するオブジェクトを使用する方法について学習します。 アンマネージ リソースを使用する型は、リソースを再利用できるように IDisposable を実装します。
ms.date: 05/13/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- try/finally block
- garbage collection, encapsulating resources
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
ms.openlocfilehash: 7d5d4080f22aab6870a230d495b4a4b9ebcb3b96
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599855"
---
# <a name="using-objects-that-implement-idisposable"></a>IDisposable を実装するオブジェクトの使用

共通言語ランタイムのガベージ コレクターは、アンマネージド オブジェクトによって使用されているメモリを解放しますが、アンマネージ リソースを使用する型は、これらのアンマネージ リソースで必要なリソースが再利用されるように <xref:System.IDisposable> インターフェイスを実装しています。 <xref:System.IDisposable> を実装するオブジェクトを使い終わったら、オブジェクトの <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> の実装を呼び出す必要があります。 2 つの方法のいずれかでこれを行うことができます。

- C# の `using` ステートメント (Visual Basic の `Using`)。
- `try/finally` ブロックを実装し、`finally` で <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> を呼び出します。

## <a name="the-using-statement"></a>using ステートメント

C# の [`using` ステートメント](../../csharp/language-reference/keywords/using-statement.md)および Visual Basic の [`Using` ステートメント](../../visual-basic/language-reference/statements/using-statement.md)を使用すると、オブジェクトのクリーンアップ時に記述する必要のあるコードが簡略化されます。 `using` ステートメントは、1 つ以上のリソースを取得し、指定されたステートメントを実行し、オブジェクトを自動的に破棄します。 ただし、`using` ステートメントは、オブジェクトが構築されるメソッドのスコープ内で使用されるオブジェクトに対してのみ有効です。

次の例では、`using` ステートメントを使用して <xref:System.IO.StreamReader?displayProperty=nameWithType> オブジェクトを作成し解放します。

[!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
[!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]

<xref:System.IO.StreamReader> クラスは <xref:System.IDisposable> インターフェイスを実装し、これはアンマネージ リソースを使用することを示していますが、例では <xref:System.IO.StreamReader.Dispose%2A?displayProperty=nameWithType> メソッドを明示的に呼び出していません。 C# または Visual Basic コンパイラが `using` ステートメントを見つけると、明示的に `try/finally` ブロックを含む次のコードと同等の中間言語 (IL) を生成します。

[!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
[!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]

また、C# の `using` ステートメントでは、単一のステートメントで複数のリソースを取得できます。そのようなステートメントは、内部的には複数の `using` ステートメントを入れ子にした場合と同等です。 次の例では、2 つの異なるファイルの内容を読み取るために、<xref:System.IO.StreamReader> の 2 つのオブジェクトをインスタンス化します。

[!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]

## <a name="tryfinally-block"></a>Try/Finally ブロック

`using` ステートメントで `try/finally` ブロックをラップする代わりに、`try/finally` ブロックを直接実装することもできます。 これは、個人のコーディング スタイルであることも、次のいずれかの理由からそうすることもあります。

- `catch` ブロックでスローされた例外を処理する `try` ブロックを含めるため。 それ以外の場合、`using` ステートメント内でスローされた例外は処理されません。

- 宣言されたブロックに対してスコープがローカルでない <xref:System.IDisposable> を実装するオブジェクトをインスタンス化するため。

次の例は前の例に似ていますが、`try/catch/finally` ブロックを使用して、<xref:System.IO.StreamReader> オブジェクトのインスタンス化、使用、破棄を実行し、<xref:System.IO.StreamReader> コンストラクターと <xref:System.IO.StreamReader.ReadToEnd%2A> メソッドによってスローされた例外を処理しています。 `finally` メソッドを呼び出す前に <xref:System.IDisposable> を実装するオブジェクトが `null` でないことを <xref:System.IDisposable.Dispose%2A> ブロックのコードがチェックします。 これを行わない場合、実行時に <xref:System.NullReferenceException> 例外が発生する可能性があります。

[!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
[!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]

この基本パターンを利用できるのは、プログラミング言語で `using` ステートメントがサポートされていないが、<xref:System.IDisposable.Dispose%2A> メソッドを直接呼び出すことはできるため、`try/finally` ブロックの実装を選択した場合、または実装する必要がある場合です。

## <a name="idisposable-instance-members"></a>IDisposable インスタンス メンバー

クラスがインスタンス メンバーとして <xref:System.IDisposable> の実装 (フィールドまたはプロパティ) を保持している場合、クラスも <xref:System.IDisposable> を実装する必要があります。 詳細については、[カスケード破棄の実装に関する記事](implementing-dispose.md#cascade-dispose-calls)を参照してください。

## <a name="see-also"></a>関連項目

- [アンマネージ リソースのクリーンアップ](unmanaged.md)
- [using ステートメント (C# リファレンス)](../../csharp/language-reference/keywords/using-statement.md)
- [Using ステートメント (Visual Basic)](../../visual-basic/language-reference/statements/using-statement.md)
