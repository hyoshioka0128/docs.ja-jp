---
title: ローカル関数 - C# プログラミング ガイド
ms.date: 06/14/2017
helpviewer_keywords:
- local functions [C#]
ms.openlocfilehash: 200fbd097b7c71a1cd392d62622955528a80fd66
ms.sourcegitcommit: 73aa9653547a1cd70ee6586221f79cc29b588ebd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82102945"
---
# <a name="local-functions-c-programming-guide"></a>ローカル関数 (C# プログラミング ガイド)

C# 7.0 以降、C# では*ローカル関数*がサポートされています。 ローカル関数は、別のメンバーの入れ子になっているタイプのプライベート メソッドです。 親メンバーからのみ呼び出すことができます。 ローカル関数は次の要素で宣言し、呼び出すことができます。

- メソッド (特に反復子メソッドと非同期メソッド)
- コンストラクター
- プロパティ アクセサー
- イベント アクセサー
- 匿名メソッド
- ラムダ式
- ファイナライザー
- その他のローカル関数

ただし、ローカル関数は、式形式のメンバーの内部では宣言できません。

> [!NOTE]
> 場合によっては、ラムダ式を使用して、ローカル関数でもサポートされている機能を実装できます。 比較については、「[ローカル関数とラムダ式の比較](#local-functions-vs-lambda-expressions)」を参照してください。

ローカル関数を使用すると、コードの意図が明確になります。 コードを見た人は、メソッドが親メソッドによってのみ呼び出し可能であることがわかります。 また、チーム プロジェクトの場合は、別の開発者がクラスや構造体の別の場所から誤ってメソッドを直接呼び出すことができなくなります。

## <a name="local-function-syntax"></a>ローカル関数の構文

ローカル関数は、親メンバーの内側に、入れ子になったメソッドとして定義されます。 その定義の構文は次のとおりです。

```csharp
<modifiers: async | unsafe> <return-type> <method-name> <parameter-list>
```

ローカル関数では、[async](../../language-reference/keywords/async.md) および [unsafe](../../language-reference/keywords/unsafe.md) 修飾子を使用できます。

メソッドのパラメーターを含め、親メンバーに定義されたすべてのローカル変数は、ローカル関数からアクセス可能です。

メソッド定義とは異なり、ローカル関数の定義にメンバー アクセス修飾子を含めることはできません。 すべてのローカル関数はプライベートであるため、`private` キーワードなどのアクセス修飾子が含まれていると、コンパイラ エラー CS0106 "修飾子 'private' がこの項目に対して有効ではありません" が生成されます。

> [!NOTE]
> C# 8.0 より前では、ローカル関数に `static` 修飾子を含めることはできません。 `static` キーワードが含まれていると、コンパイラ エラー CS0106 "修飾子 'static' がこの項目に対して有効ではありません" が生成されます。

さらに、ローカル関数またはローカル関数のパラメーターと型パラメーターには属性を適用できません。

次の例は、`GetText` というメソッドに対してプライベートな `AppendPathSeparator` というローカル関数を定義しています。

[!code-csharp[LocalFunctionExample](~/samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]  

## <a name="local-functions-and-exceptions"></a>ローカル関数と例外

ローカル関数の便利な機能の 1 つは、例外を直ちに検出できることです。 メソッド反復子の場合、例外は返されたシーケンスを列挙する時点でしか検出されず、反復子を取得した時点では検出されません。 非同期メソッドの場合、非同期メソッドでスローされた例外は、タスクの戻りを待機中に検出されます。

次の例は、指定した範囲にある奇数を列挙する `OddSequence` メソッドを定義しています。 100 より大きい数値を `OddSequence` 列挙子メソッドに渡しているため、メソッドは <xref:System.ArgumentOutOfRangeException> をスローします。 この例の出力が示すように、例外は列挙子を取得したときではなく、数値を反復処理した時点でのみ検出されます。

[!code-csharp[LocalFunctionIterator1](~/samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)]

これに対して、次の例に示すようにローカル関数から列挙子を返すことによって、列挙子を取得する前の検証を実行する時点で例外をスローできます。

[!code-csharp[LocalFunctionIterator2](~/samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]

ローカル関数は、非同期操作の外部で例外を処理するために同様の方法で使用できます。 通常、非同期メソッドでスローされた例外では <xref:System.AggregateException> の内部例外を確認する必要があります。 ローカル関数を使用すると、コードを迅速に失敗させ (Fail Fast)、例外のスローと検出の両方を同時に行うことができます。

次の例は、`GetMultipleAsync` という非同期メソッドを使用して、指定した秒数だけ一時停止した後、その秒数のランダムな倍数である値を返します。 遅延の最大値は 5 秒です。値が 5 より大きい場合は <xref:System.ArgumentOutOfRangeException> が発生します。 次の例に示すように、`GetMultipleAsync` メソッドに渡された値が 6 の場合にスローされる例外は、`GetMultipleAsync` メソッドの実行開始後、<xref:System.AggregateException> にラップされます。

[!code-csharp[LocalFunctionAsync](~/samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)]

メソッド反復子と同様、非同期メソッドを呼び出す前に検証を実行するように、この例のコードをリファクターすることができます。 次の例の出力に示されているように、<xref:System.ArgumentOutOfRangeException> は <xref:System.AggregateException> にラップされていません。

[!code-csharp[LocalFunctionAsync](~/samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)]

## <a name="local-functions-vs-lambda-expressions"></a>ローカル関数とラムダ式の比較

一見したところ、ローカル関数と[ラムダ式](../statements-expressions-operators/lambda-expressions.md)は、非常に似ています。 多くの場合、ラムダ式とローカル関数の使用のどちらを選択するかは、スタイルと個人的な好みの問題です。 ただし、どちらか一方を使用できる場合、認識しておくべき実質的な違いがあります。

階乗アルゴリズムのローカル関数とラムダ式の実装の違いについて見てみましょう。 まずは、ローカル関数を使用するバージョンです。

[!code-csharp[LocalFunctionFactorial](../../../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "Recursive factorial using local function")]

ラムダ式を使用するバージョンの実装と比較します。

[!code-csharp[26_LambdaFactorial](../../../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "Recursive factorial using lambda expressions")]

ローカル関数には名前があります。 ラムダ式は匿名メソッドであり、`Func` または `Action` 型である変数に割り当てられます。 ローカル関数を宣言する場合、引数の型と戻り値の型は関数宣言の一部となります。 引数の型と戻り値の型は、ラムダ式の本体の一部ではなく、ラムダ式の変数型宣言の一部となります。 これら 2 つの違いにより、コードがわかりやすくなる場合があります。

ローカル関数には、ラムダ式とは異なる確実な代入のルールがあります。 ローカル関数宣言は、スコープ内にある任意のコードの場所から参照できます。 ラムダ式はデリゲート変数に割り当てないと、アクセスできません (ラムダ式を参照するデリゲートを通じて呼び出すこともできません)。 ラムダ式を使用したバージョンでは、ラムダ式 `nthFactorial` を定義する前に、宣言と初期化を行う必要があることに注意してください。 その手順を踏まないと、`nthFactorial` の割り当て前に参照することによるコンパイル時エラーが発生します。 これらの違いは、再帰的なアルゴリズムの作成はローカル関数を使用する方が簡単であることを意味します。 自身を呼び出すローカル関数を宣言して定義することができます。 ラムダ式は宣言して、既定値を割り当てないと、同じラムダ式を参照する本体に再割り当てできません。

確実な代入ルールは、ローカル関数またはラムダ式でキャプチャされる変数にも影響します。 ローカル関数とラムダ式の両方のルールでは、ローカル関数またはラムダ式がデリゲートに変換された時点で、キャプチャされた変数が確実に代入されることが要求されます。 違いは、ラムダ式が宣言時にデリゲートに変換されることです。 ローカル関数は、デリゲートとして使用される場合にのみ、デリゲートに変換されます。 ローカル関数を宣言し、メソッドのように呼び出して参照のみを行う場合は、デリゲートに変換されません。 このルールでは、外側のスコープ内の便利な場所でローカル関数を宣言できます。 親メソッドの末尾 (すべての return ステートメントの後) にローカル関数を宣言するのが一般的です。

3 つ目は、コンパイラは静的分析を実行できることです。これにより、ローカル関数で外側のスコープ内のキャプチャされた変数を確実に割り当てることができます。 次の例について考えます。

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

コンパイラは、呼び出し時に `LocalFunction` が `y` を確実に割り当てるかどうかを確認できます。 `return` ステートメントの前に `LocalFunction` が呼び出されるため、`y` は `return` ステートメントで確実に割り当てられます。

分析例を使用する分析では、4 つ目の違いを確認できます。 ローカル関数では、その使用に応じて、ラムダ式では常に必要なヒープの割り当てを回避できます。 ローカル関数がデリゲートに変換されておらず、ローカル関数でキャプチャされたいずれの変数も、デリゲートに変換された他のラムダやローカル関数でキャプチャされていない場合、コンパイラはヒープの割り当てを回避できます。

次の非同期の例について考えます。

[!code-csharp[TaskLambdaExample](../../../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "Task returning method with lambda expression")]

このラムダ式のクロージャに含まれるのは、`address`、`index`、および `name` 変数です。 ローカル関数の場合、クロージャを実装するオブジェクトが `struct` になる場合があります。 その構造体型はローカル関数に参照によって渡されます。 この実装の違いにより、割り当てが少なくなります。

ラムダ式に必要なインスタンス化では、余分なメモリの割り当てが必要となり、タイム クリティカルなコード パスに影響を与えるパフォーマンス因子となる可能性があります。 ローカル関数では、このオーバーヘッドは発生しません。 上記の例では、ローカル関数のバージョンは、ラムダ式のバージョンよりも割り当てが 2 つ少なくなっています。

> [!NOTE]
> このメソッドのローカル関数と同等のものも、同じクロージャのクラスを使用します。 ローカル関数のクロージャが `class` として実装される場合でも、実装の詳細が `struct` である場合でも同様です。 ローカル関数は `struct` を使用する場合がありますが、ラムダは常に `class` を使用します。

[!code-csharp[TaskLocalFunctionExample](../../../../samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

この例では説明しませんが、最後の 1 つの利点は値のシーケンスを生成するために `yield return` 構文を使用して、ローカル関数を反復子として実装できることです。 ラムダ式では `yield return` ステートメントは許可されません。

ローカル関数はラムダ式より冗長に思えるかもしれませんが、実際にはさまざまな目的に役立ち、用途もさまざまです。 ローカル関数は、別のメソッドのコンテキストからのみ呼び出される関数を記述する場合に、より効率が高くなります。

## <a name="see-also"></a>関連項目

- [メソッド](methods.md)
