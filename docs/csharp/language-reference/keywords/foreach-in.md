---
title: C# foreach ステートメント
ms.date: 06/03/2020
f1_keywords:
- foreach
- foreach_CSharpKeyword
helpviewer_keywords:
- foreach keyword [C#]
- foreach statement [C#]
- in keyword [C#]
ms.assetid: 5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec
ms.openlocfilehash: 1645a246c9feee2a92c0d4e4bbeda47f0afde7d9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401889"
---
# <a name="foreach-in-c-reference"></a>foreach、in (C# リファレンス)

`foreach` ステートメントは、<xref:System.Collections.IEnumerable?displayProperty=nameWithType> または <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> インターフェイスを実装している型のインスタンス内の要素ごとに、ステートメントまたはステートメントのブロックを実行します。 `foreach` ステートメントはこのような型にのみ限定されるものではなく、次の条件を満たす任意の型のインスタンスに適用できます。

- 戻り値の型がクラス、構造体、インターフェイス型のいずれかである、パラメーターなしのパブリック メソッド `GetEnumerator` を持っている。
- `GetEnumerator` メソッドの戻り値の型が、パブリック プロパティ `Current` と、戻り値の型が <xref:System.Boolean> であるパラメーターなしのパブリック メソッド `MoveNext` を持っている。

使用時のほとんどは、各要素が `T` 型であるとして、`foreach` が `IEnumerable<T>` 式を反復処理します。 ただし、要素には、`Current` プロパティの型からの暗黙的または明示的な変換を含む任意の型を指定できます。 `Current` プロパティが `SomeType` を返した場合、要素の型は次のようになります。

- `SomeType` の基底クラス。
- `SomeType` によって実装されるインターフェイス。

さらに、`SomeType` が `class` または `interface` であり、`sealed` でない場合は、要素の型には次のものが含まれる可能性があります。

- `SomeType` から派生した任意の型。
- 任意のインターフェイス。 すべてのインターフェイスは `SomeType` から派生したクラス、またはそれを実装しているクラスによって実装される可能性があるため、あらゆるインターフェイスが許可されます。

前の規則に一致する任意の型を使用して、反復変数を宣言できます。 `SomeType` から反復変数の型への変換に明示的なキャストが必要な場合、変換に失敗すると、その操作によって <xref:System.InvalidCastException> がスローされる可能性があります。

C# 7.3 以降、列挙子の `Current` プロパティが、[参照戻り値](ref.md#reference-return-values) (`ref T``T` はコレクション要素の種類です) を返す場合、`ref` または `ref readonly` 修飾子を使用して繰り返し変数を宣言することができます。

C# 8.0 以降では、コレクション型で `await` インターフェイスが実装されている場合、`foreach` 演算子が <xref:System.Collections.Generic.IAsyncEnumerable%601> ステートメントに適用される場合があります。 次の要素が非同期で取得されている限り、ループの各反復は中断される可能性があります。 既定では、ストリーム要素はキャプチャされたコンテキストで処理されます。 コンテキストのキャプチャを無効にする場合は、<xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait%2A?displayProperty=nameWithType> 拡張メソッドを使用します。 同期コンテキストについて、および現在のコンテキストのキャプチャについての詳細は、「[タスク ベースの非同期パターンの利用](../../../standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)」を参照してください。

`foreach` ステートメント ブロック内の任意の位置で、[break](break.md) ステートメントを使ってループから抜けることができます。または、[continue](continue.md) ステートメントを使って、ループ内の次の繰り返しにスキップできます。 また、[goto](goto.md)、[return](return.md)、[throw](throw.md) ステートメントのいずれかを使って `foreach` ループを終了することもできます。

`foreach` ステートメントを `null` に適用した場合、<xref:System.NullReferenceException> がスローされます。 `foreach` ステートメントのソース コレクションが空の場合、`foreach` ループの本体は実行されず、スキップされます。

## <a name="examples"></a>使用例

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

次の例では、<xref:System.Collections.Generic.IEnumerable%601> インターフェイスを実装する <xref:System.Collections.Generic.List%601> 型のインスタンスを使用して、`foreach` ステートメントの使用方法を示します。

:::code language="csharp" source="snippets/IterationKeywordsExamples.cs" id="1" interactive="try-dotnet-method" :::

次の例では、何のインターフェイスも実装していない <xref:System.Span%601?displayProperty=nameWithType> 型のインスタンスを使用して、`foreach` ステートメントを使用します。

:::code language="csharp" source="snippets/IterationKeywordsExamples.cs" id="2" :::

次の例では、stackalloc 配列内の各項目の値を設定するために、`ref` 繰り返し変数を使用します。 `ref readonly` バージョンは、すべての値を出力するコレクションを反復処理します。 `readonly` 宣言では、暗黙のローカル変数宣言を使用します。 暗黙の変数宣言は、`ref` または `ref readonly` 宣言で使用でき、変数の宣言を明示的に型指定できます。

:::code language="csharp" source="snippets/IterationKeywordsExamples.cs" id="RefSpan" :::

次の例では、`await foreach` を使用して、各要素を非同期に生成するコレクションを反復処理します。

:::code language="csharp" source="snippets/IterationKeywordsExamples.cs" id="AwaitForeach"  :::

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](/dotnet/csharp/language-reference/language-specification/introduction)」の [foreach ステートメント](~/_csharplang/spec/statements.md#the-foreach-statement)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [配列での foreach の使用](../../programming-guide/arrays/using-foreach-with-arrays.md)
- [for ステートメント](for.md)
