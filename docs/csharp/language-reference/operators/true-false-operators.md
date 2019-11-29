---
title: true 演算子と false 演算子 - C# リファレンス
ms.custom: seodec18
ms.date: 12/10/2018
helpviewer_keywords:
- false operator [C#]
- true operator [C#]
ms.assetid: 81a888fd-011e-4589-b242-6c261fea505e
ms.openlocfilehash: 780c63e5a8f3f0d82559565b3319fe54507e3d21
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73036125"
---
# <a name="true-and-false-operators-c-reference"></a>true 演算子と false 演算子 (C# リファレンス)

`true` 演算子は、オペランドが確実に true であることを示す[ブール](../keywords/bool.md)値 `true` を返します。 `false` 演算子は、オペランドが確実に false であることを示す `bool` 値 `true` を返します。 `true` および `false` 演算子が互いに補完することは保証されていません。 つまり、`true` と `false` 演算子の両方が同じオペランドに対して `bool` 値 `false` を返す場合があります。 ある型でこの 2 つの演算子の 1 つを定義する場合は、もう 1 つの演算子も定義する必要があります。

> [!TIP]
> 3 値ロジックをサポートする必要がある場合は、`bool?` 型を使用します。たとえば、3 値ブール型をサポートするデータベースを操作する場合などです。 C# には、`bool?` オペランドを使用して 3 値ロジックをサポートする `&` および `|` 演算子があります。 詳細については、「[Boolean logical operators (ブール論理演算子)](boolean-logical-operators.md)」記事の「[Nullable Boolean logical operators (null 許容論理演算子)](boolean-logical-operators.md#nullable-boolean-logical-operators)」セクションを参照してください。

## <a name="boolean-expressions"></a>ブール式

`true` 演算子が定義された型は、[if](../keywords/if-else.md)、[do](../keywords/do.md)、[while](../keywords/while.md)、および [for](../keywords/for.md) ステートメントと、[条件演算子 `?:`](conditional-operator.md) の制御条件式の結果の型にすることができます。 詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の[ブール型の式](~/_csharplang/spec/expressions.md#boolean-expressions)に関するセクションを参照してください。

## <a name="user-defined-conditional-logical-operators"></a>ユーザー定義の条件付き論理演算子

`true` と `false` 演算子が定義された型によって、[論理 OR 演算子](boolean-logical-operators.md#logical-or-operator-) `|` または[論理 AND 演算子](boolean-logical-operators.md#logical-and-operator-) `&` が特定の方法で[オーバーロード](operator-overloading.md)される場合、[条件付き論理 OR 演算子](boolean-logical-operators.md#conditional-logical-or-operator-) `||` または [条件付き論理 AND 演算子](boolean-logical-operators.md#conditional-logical-and-operator-) `&&` を、それぞれ、その型のオペランドに対して評価することができます。 詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の[ユーザー定義型条件論理演算子](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators)に関するセクションを参照してください。

## <a name="example"></a>例

次の例では、`true` と `false` 演算子の両方を定義する型を示します。 この型により、論理 AND 演算子 `&` もオーバーロードされ、演算子 `&&` もその型のオペランドで評価できるようになります。

[!code-csharp[true and false operators example](~/samples/csharp/language-reference/operators/TrueFalseOperators.cs)]

`&&` 演算子のショートサーキット動作に注意してください。 `GetFuelLaunchStatus` メソッドから `LaunchStatus.Red` が返されると、`&&` 演算子の右側のオペランドは評価されません。 これは、`LaunchStatus.Red` が確実に false であるためです。 したがって、論理 AND の結果は右側のオペランドの値に依存しません。 この例の出力は次のとおりです。

```console
Getting fuel launch status...
Wait!
```

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
- [true リテラル](../keywords/true-literal.md)
- [false リテラル](../keywords/false-literal.md)
