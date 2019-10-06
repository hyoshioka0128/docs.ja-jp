---
title: null 許容値型の使用 - C# プログラミング ガイド
ms.custom: seodec18
description: C# の null 許容値型を使用する方法について説明します。
ms.date: 09/26/2019
helpviewer_keywords:
- nullable types [C#], about nullable types
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
ms.openlocfilehash: 65fc3b0ca94f9a41c9375e96000449b52cb7db26
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396161"
---
# <a name="using-nullable-value-types-c-programming-guide"></a>null 許容値型の使用 (C# プログラミング ガイド)

null 許容値型は、基になる値型 `T` のすべての値と、追加の [null](../../language-reference/keywords/null.md) 値を表す型です。 詳細については、「[null 許容値型](index.md)」のトピックを参照してください。

> [!NOTE]
> C# 8.0 で、Null 許容参照型機能が導入されました。 詳細については、「[null 許容参照型](../../nullable-references.md)」を参照してください。 null 許容値型は、C# 2 から使用できます。

`Nullable<T>` または `T?` の代替可能な形式のいずれかで null 許容値型を参照できます。 `T` は値の型である必要があります。

## <a name="declaration-and-assignment"></a>宣言と代入

値の型は、対応する null 許容値型に暗黙的に変換できるので、基になる値型の場合と同様に null 許容型に値を代入します。 `null` 値を代入することもできます。 次に例を示します。

[!code-csharp[declare and assign](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#1)]

## <a name="examination-of-a-nullable-type-value"></a>Null 許容型の値の検査

null 許容値型のインスタンスが null かどうかを調べて、基になる型の値を取得するには、次の読み取り専用プロパティを使用します。

- <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> は、Null 許容型のインスタンスに、基になる型の値が含まれるかどうかを示します。

- <xref:System.Nullable%601.HasValue%2A> が `true` の場合、<xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> は基になる型の値を取得します。 <xref:System.Nullable%601.HasValue%2A> が `false` の場合、<xref:System.Nullable%601.Value%2A> プロパティは <xref:System.InvalidOperationException> をスローします。

次の例のコードでは、`HasValue` プロパティを使用して、値を表示する前に変数に値が格納されているかどうかをテストします。

[!code-csharp-interactive[use HasValue](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#2)]

次の例に示すように、`HasValue` プロパティを使用する代わりに、null 許容値型の変数を `null` と比較することもできます。

[!code-csharp-interactive[use comparison with null](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#3)]

C# 7.0 以降では、[パターン マッチング](../../pattern-matching.md)を使用して null 許容値型の値を調べて取得することができます。

[!code-csharp-interactive[use pattern matching](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#4)]

## <a name="conversion-from-a-nullable-value-type-to-an-underlying-type"></a>null 許容値型から基になる型への変換

null 許容値型の値を非 null 許容型に代入する必要がある場合は、[null 合体演算子 `??`](../../language-reference/operators/null-coalescing-operator.md) を使用して、null 許容値型の値が null の場合に代入される値を指定します (<xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> メソッドを使用してこの操作を行うこともできます)。

[!code-csharp-interactive[?? operator](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#5)]

null 許容値型の値が `null` の場合に使用される値を、基になる値型の既定値にする場合は、<xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> メソッドを使用します。

null 許容値型を非 null 許容型に明示的にキャストすることができます。 次に例を示します。

[!code-csharp[explicit cast](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#6)]

実行時に null 許容値型の値が `null` の場合は、明示的なキャストによって <xref:System.InvalidOperationException> がスローされます。

Null 非許容値型は、対応する Null 許容型に暗黙的に変換されます。

## <a name="operators"></a>演算子

値型向けに存在している定義済みの単項演算子、2 項演算子およびすべてのユーザー定義演算子は、対応する null 許容型でも使用できます。 これらの演算子では、1 つまたは両方のオペランドが `null` の場合は `null` が生成され、null 以外の場合は、含まれている値に基づいて結果が算出されます。 次に例を示します。

[!code-csharp[operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#7)]

> [!NOTE]
> `bool?` 型の場合、定義済みの `&` および `|` 演算子は、このセクションで説明されている規則に従わないことに注意してください。オペランドの 1 つが `null` の場合も、演算子の評価の結果は null 以外である可能性があります。 詳細については、「[Boolean logical operators (ブール論理演算子)](../../language-reference/operators/boolean-logical-operators.md)」記事の「[Nullable Boolean logical operators (null 許容論理演算子)](../../language-reference/operators/boolean-logical-operators.md#nullable-boolean-logical-operators)」セクションを参照してください。
  
関係演算子 (`<`、`>`、`<=`、`>=`) では、1 つまたは両方のオペランドが `null` の場合、結果は `false` になります。 ある比較 (たとえば、`<=`) から返される結果が `false` であっても、逆の比較 (`>`) から返される結果が `true` であるとは限りません。 次の例は、10 が

- `null` 以上ではなく、
- `null` 未満でもないことを示します。

[!code-csharp-interactive[relational and equality operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#8)]

上記の例は、どちらも null である 2 つの null 許容値型を等価比較すると、結果が `true` と評価されることを示しています。

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)に関するページの「[リフトされた演算子](~/_csharplang/spec/expressions.md#lifted-operators)」セクションを参照してください。

## <a name="boxing-and-unboxing"></a>ボックス化とボックス化解除

Null 許容値型は、次の規則に従って[ボックス化](../types/boxing-and-unboxing.md)されます。

- <xref:System.Nullable%601.HasValue%2A> が `false` を返した場合は、null 参照が生成されます。
- <xref:System.Nullable%601.HasValue%2A> が `true` を返した場合は、<xref:System.Nullable%601> のインスタンスではなく、基になる値型 `T` の値がボックス化されます。

次の例に示すように、ボックス化された値型を、対応する Null 許容型にボックス化解除できます。

[!code-csharp-interactive[boxing and unboxing](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#9)]

## <a name="see-also"></a>関連項目

- [null 許容値型](index.md)
- [What Exactly Does 'Lifted' mean? ('Lifted' の正確な意味)](https://blogs.msdn.microsoft.com/ericlippert/2007/06/27/what-exactly-does-lifted-mean/)
