---
title: stackalloc 式 - C# リファレンス
ms.date: 03/13/2020
f1_keywords:
- stackalloc_CSharpKeyword
helpviewer_keywords:
- stackalloc expression [C#]
ms.openlocfilehash: 2e99ce8b1e44dfa040c1acac799a3a55b375bd91
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2020
ms.locfileid: "79546602"
---
# <a name="stackalloc-expression-c-reference"></a>stackalloc 式 (C# リファレンス)

`stackalloc` 式を使用すると、スタックにメモリ ブロックを割り当てることができます。 メソッドの実行中に作成された、スタックに割り当てられたメモリ ブロックは、そのメソッドが戻るときに自動的に破棄されます。 `stackalloc` を使用して割り当てられたメモリを明示的に開放することはできません。 スタックに割り当てられたメモリ ブロックは、[ガベージ コレクション](../../../standard/garbage-collection/index.md)の対象外であり、[`fixed` ステートメント](../keywords/fixed-statement.md)を使用してピン留めする必要はありません。

`stackalloc` 式の結果を、次のいずれかの型の変数に割り当てることができます。

- C# 7.2 以降では <xref:System.Span%601?displayProperty=nameWithType> または <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>。次に例を示します。

  [!code-csharp[stackalloc span](snippets/StackallocOperator.cs#AssignToSpan)]

  スタックに割り当てられたメモリ ブロックを <xref:System.Span%601> 変数または <xref:System.ReadOnlySpan%601> 変数に割り当てるときに、[unsafe](../keywords/unsafe.md) コンテキストを使用する必要はありません。

  これらの型を操作するときに、次の例に示すように、[条件](conditional-operator.md)式または代入式の中で `stackalloc` 式を使用できます。

  [!code-csharp[stackalloc expression](snippets/StackallocOperator.cs#AsExpression)]

  C# 8.0 以降では、次の例のように、<xref:System.Span%601> または <xref:System.ReadOnlySpan%601> の変数が許可されるところでは、他の式の中で `stackalloc` 式を使用できます。

  [!code-csharp[stackalloc in nested expressions](snippets/StackallocOperator.cs#Nested)]

  > [!NOTE]
  > スタックに割り当てられたメモリを操作するときは、できるだけ <xref:System.Span%601> 型または <xref:System.ReadOnlySpan%601> 型を使用することをお勧めします。

- [ポインター型](../../programming-guide/unsafe-code-pointers/pointer-types.md)。次に例を示します。

  [!code-csharp[stackalloc pointer](snippets/StackallocOperator.cs#AssignToPointer)]

  前の例に示したように、ポインター型を操作するときは、`unsafe` コンテキストを使用する必要があります。

  ポインター型の場合、ローカル変数宣言でのみ `stackalloc` 式を使用し、変数を初期化できます。

スタックで使用可能なメモリ容量は制限されています。 スタックに割り当てたメモリが多すぎると、<xref:System.StackOverflowException> がスローされます。 これを回避するために、次の規則に従ってください。

- `stackalloc` を使って割り当てるメモリ容量を制限する:

  [!code-csharp[limit stackalloc](snippets/StackallocOperator.cs#LimitStackalloc)]

  スタックで使用可能なメモリ容量はコードが実行される環境によって異なるため、実際の制限値は控えめに定義する必要があります。

- ループ内での `stackalloc` の使用を避ける。 ループの外側でメモリ ブロックを割り当て、それをループ内で再利用してください。

新しく割り当てられたメモリの内容は未定義です。 これは、使用する前に初期化する必要があります。 たとえば、すべての項目を `T` 型の既定値に設定する <xref:System.Span%601.Clear%2A?displayProperty=nameWithType> メソッドを使用できます。

C# 7.3 以降、配列初期化子構文を使用して、新しく割り当てられたメモリの内容を定義できます。 これを実行するさまざまな方法を次の例に示します。

[!code-csharp[stackalloc initialization](snippets/StackallocOperator.cs#StackallocInit)]

式 `stackalloc T[E]` では、`T` は[アンマネージド型](../builtin-types/unmanaged-types.md)である必要があり、`E` は負でない [int](../builtin-types/integral-numeric-types.md) 値に評価される必要があります。

## <a name="security"></a>セキュリティ

`stackalloc` を使用すると、共通言語ランタイム (CLR) のバッファー オーバーラン検出機能が自動的に有効になります。 バッファー オーバーランが検出されると、悪意のあるコードが実行される可能性を最小限に抑えるために、プロセスはできる限り迅速に終了されます。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)に関するページの「[スタック割り当て](~/_csharplang/spec/unsafe-code.md#stack-allocation)」セクションと、[入れ子になった `stackalloc` の許可](~/_csharplang/proposals/csharp-8.0/nested-stackalloc.md)に関する機能提案メモをご覧ください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
- [ポインターに関連する演算子](pointer-related-operators.md)
- [ポインター型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [メモリおよびスパンに関連する型](../../../standard/memory-and-spans/index.md)
- [stackalloc の注意事項](https://vcsjones.dev/2020/02/24/stackalloc/)
