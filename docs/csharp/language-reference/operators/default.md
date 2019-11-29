---
title: default 演算子 - C# リファレンス
ms.custom: seodec18
description: 型の既定値を生成するには、default 演算子を使います
ms.date: 08/01/2019
helpviewer_keywords:
- default keyword [C#]
ms.openlocfilehash: 6503e82a42f116a7ba8461ae060592377579f255
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039047"
---
# <a name="default-operator-c-reference"></a>default 演算子 (C# リファレンス)

`default` 演算子では、型の[既定値](../keywords/default-values-table.md)が生成されます。 `default` 演算子への引数では、型または型パラメーターの名前を指定する必要があります。

`default` 演算子の使い方を次の例に示します。

[!code-csharp-interactive[default of T](~/samples/csharp/language-reference/operators/DefaultOperator.cs#WithOperand)]

また、[`switch` ステートメント](../keywords/switch.md)内の既定の case ラベルとして、`default` キーワードを使うこともできます。

## <a name="default-literal"></a>default リテラル

C# 7.1 以降では、`default` リテラルを使って、コンパイラが式の型を推論できる場合に、型の既定値を生成できます。 `default` リテラル式では、`T` が推定型である式 `default(T)` と同じ値が生成されます。 `default` リテラルは、次のいずれの場合でも使用できます。

- 変数の代入または初期化。
- [省略可能なメソッド パラメーター](../../methods.md#optional-parameters-and-arguments)の既定値の宣言。
- メソッド呼び出しでの引数値の指定。
- [`return` ステートメント](../keywords/return.md)内、または[式のようなメンバー](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)内の式として。

`default` リテラルの使い方の例を次に示します。

[!code-csharp-interactive[default literal](~/samples/csharp/language-reference/operators/DefaultOperator.cs#DefaultLiteral)]

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の「[既定値の式](~/_csharplang/spec/expressions.md#default-value-expressions)」セクションをご覧ください。

`default` リテラルについて詳しくは、[機能提案メモ](~/_csharplang/proposals/csharp-7.1/target-typed-default.md)をご覧ください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
- [既定値の一覧表](../keywords/default-values-table.md)
- [.NET のジェネリック](../../../standard/generics/index.md)
